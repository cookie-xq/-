# 剑指 Offer 06. 从尾到头打印链表
练习链接：https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/
## 题目描述：
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。  

* 示例 1：  
输入：head = [1,3,2]  
输出：[2,3,1]  
 
限制：  
0 <= 链表长度 <= 10000  

## 代码
```javascript
var reversePrint = function(head) {
    let arr = []
    while(head){
        arr.unshift(head.val)
        head = head.next
    }
    return arr
};
```
考虑到 unshift() 效率不太好，可以先 push 然后 reverse()