# 剑指 Offer 35. 复杂链表的复制
练习链接：https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/

## 题目描述
请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

* 示例1：  
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]  
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]  

* 示例2：  
输入：head = [[1,1],[2,1]]  
输出：[[1,1],[2,1]]  

* 示例3：  
输入：head = [[3,null],[3,0],[3,null]]  
输出：[[3,null],[3,0],[3,null]]  

* 示例4：  
输入：head = []  
输出：[]  
解释：给定的链表为空（空指针），因此返回 null。  

提示：  
-10000 <= Node.val <= 10000  
Node.random 为空（null）或指向链表中的节点。  
节点数目不超过 1000 。  
## 方法一：回溯 + 哈希表
**思路及算法**  
本题要求我们对一个特殊的链表进行深拷贝。如果是普通链表，我们可以直接按照遍历的顺序创建链表节点。而本题中因为随机指针的存在，当我们拷贝节点时，「当前节点的随机指针指向的节点」可能还没创建，因此我们需要变换思路。一个可行方案是，我们利用回溯的方式，让每个节点的拷贝操作相互独立。对于当前节点，我们首先要进行拷贝，然后我们进行「当前节点的后继节点」和「当前节点的随机指针指向的节点」拷贝，拷贝完成后将创建的新节点的指针返回，即可完成当前节点的两指针的赋值。  

具体地，我们用哈希表记录每一个节点对应新节点的创建情况。遍历该链表的过程中，我们检查「当前节点的后继节点」和「当前节点的随机指针指向的节点」的创建情况。如果这两个节点中的任何一个节点的新节点没有被创建，我们都立刻**递归**地进行创建。当我们拷贝完成，回溯到当前层时，我们即可完成当前节点的指针赋值。注意一个节点可能被多个其他节点指向，因此我们可能递归地多次尝试拷贝某个节点，为了防止重复拷贝，我们需要首先检查当前节点是否被拷贝过，如果已经拷贝过，我们可以直接从哈希表中取出拷贝后的节点的指针并返回即可。  

在实际代码中，我们需要特别判断给定节点为空节点的情况。  

**代码**  
```javascript
var copyRandomList = function(head, cachedNode = new Map()) {
    if (head === null) {
        return null;
    }
    if (!cachedNode.has(head)) {
        cachedNode.set(head, {val: head.val})
        Object.assign(cachedNode.get(head), 
        {next: copyRandomList(head.next, cachedNode), 
        random: copyRandomList(head.random, cachedNode)})
    }
    return cachedNode.get(head);
}
```
**复杂度分析**  
时间复杂度：O(n)，其中 n 是链表的长度。对于每个节点，我们至多访问其「后继节点」和「随机指针指向的节点」各一次，均摊每个点至多被访问两次。  
空间复杂度：O(n)，其中 n 是链表的长度。为哈希表的空间开销。  

## 方法二：迭代 + 节点拆分
注意到方法一需要使用哈希表记录每一个节点对应新节点的创建情况，而我们可以使用一个小技巧来省去哈希表的空间。  

```javascript
var copyRandomList = function(head) {
    if (head === null) {
        return null;
    }
    for (let node = head; node !== null; node = node.next.next) {
        const nodeNew = new Node(node.val, node.next, null);
        node.next = nodeNew;
    }
    for (let node = head; node !== null; node = node.next.next) {
        const nodeNew = node.next;
        nodeNew.random = (node.random !== null) ? node.random.next : null;
    }
    const headNew = head.next;
    for (let node = head; node !== null; node = node.next) {
        const nodeNew = node.next;
        node.next = node.next.next;
        nodeNew.next = (nodeNew.next !== null) ? nodeNew.next.next : null;
    }
    return headNew;
};
```
**复杂度分析**  
时间复杂度：O(n)，其中 n 是链表的长度。我们只需要遍历该链表三次。  
读者们也可以自行尝试在计算拷贝节点的随机指针的同时计算其后继指针，这样只需要遍历两次。  
空间复杂度：O(1)。注意返回值不计入空间复杂度。  

作者：LeetCode-Solution  
链接：https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/solution/fu-za-lian-biao-de-fu-zhi-by-leetcode-so-9ik5/  