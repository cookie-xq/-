# 剑指 Offer 30. 包含min函数的栈
练习链接：https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/
## 题目描述：
定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。  

示例:  
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();   --> 返回 0.
minStack.min();   --> 返回 -2.
```

提示：  
各函数的调用总次数不超过 20000 次  

## 🧠 解题思路
根据题意，我们需要在常量级的时间内找到最小值  
这说明，我们绝不能在需要最小值的时候，再做排序，查找等操作来获取  
所以，我们可以创建两个栈，一个栈是主栈 stack，另一个是辅助栈 minStack，用于存放对应主栈不同时期的最小值。

## 🍭 示例代码
```javascript
var MinStack = function() {
    this.x_stack = [];
    this.min_stack = [Infinity];
};

MinStack.prototype.push = function(x) {
    this.x_stack.push(x);
    this.min_stack.push(Math.min(this.min_stack[this.min_stack.length - 1], x));
};

MinStack.prototype.pop = function() {
    this.x_stack.pop();
    this.min_stack.pop();
};

MinStack.prototype.top = function() {
    return this.x_stack[this.x_stack.length - 1];
};

MinStack.prototype.min = function() {
    return this.min_stack[this.min_stack.length - 1];
};
```
作者：demigodliu  
链接：https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/solution/fu-zhu-zhan-bao-han-minhan-shu-de-zhan-b-fx7t/