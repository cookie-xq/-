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

## 题解：  
思路：一个入队栈，一个出队栈  
代码：  
```javascript
var CQueue = function() {
    this.stackA = [];// 入队栈
    this.stackB = [];// 出队栈
};

/** 
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
    this.stackA.push(value);
};

/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
    if(this.stackB.length){
        return this.stackB.pop()
    }else{
        while(this.stackA.length){
            this.stackB.push(this.stackA.pop())
        }
        if(!this.stackB.length){
            return -1
        }else{
            return this.stackB.pop()
        }
    }
}
```