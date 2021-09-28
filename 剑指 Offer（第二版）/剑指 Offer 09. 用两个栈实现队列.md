# 剑指 Offer 09. 用两个栈实现队列
练习链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/
## 题目描述：
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )  

* 示例 1：  
输入：  
["CQueue","appendTail","deleteHead","deleteHead"]  
[[],[3],[],[]]  
输出：[null,null,3,-1]  

* 示例 2：  
输入：  
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]  
[[],[],[5],[2],[],[]]  
输出：[null,-1,null,null,5,2]  

提示：  
1 <= values <= 10000  
最多会对 appendTail、deleteHead 进行 10000 次调用
## 🧠 解题思路：
一个入队栈，一个出队栈。  
首先我们知道，队列是先入先出，栈是后入先出，所以知道了这两个东西的特性，我们很容易就能根据题意使用两个栈来模拟队列。  
首先，两个栈分工不同，一个为入队栈，一个为出队栈，各自负责入队和出队。  
入队操作，直接压入入队栈即可，出队操作需要优先检查出队栈是否有数据，若无，需要从入队栈倒入后再操作。  
## 🍭 示例代码：  
```javascript
var CQueue = function() {
    this.stackA = [];
    this.stackB = [];
};

CQueue.prototype.appendTail = function(value) {
    this.stackA.push(value);
};

CQueue.prototype.deleteHead = function() {
    if(this.stackB.length){
        return this.stackB.pop();
    }else{
        while(this.stackA.length){
            this.stackB.push(this.stackA.pop());
        }
        if(!this.stackB.length){
            return -1;
        }else{
            return this.stackB.pop();
        }
    }
};
```
作者：demigodliu  
链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/solution/tu-jie-guan-fang-tui-jian-ti-jie-yong-li-yjbf/