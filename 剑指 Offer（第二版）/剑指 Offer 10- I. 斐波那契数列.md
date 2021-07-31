# 剑指 Offer 10- I. 斐波那契数列  
练习链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/  
## 题目描述 
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

**答案需要取模 1e9+7（1000000007）**，如计算初始结果为：1000000008，请返回 1。

* 示例 1：  
输入：n = 2  
输出：1  

* 示例 2：  
输入：n = 5  
输出：5  
 

提示：  
0 <= n <= 100

我第一反应递归，但果不其然失败了...超出了时间限制

每日一练的解析不错，代码也非常精简，贴在下面：  
## 🧠 解题思路  
这道题其实最传统的做法就是使用递归，但是我们知道，**若递归深度过大，就会导致栈溢出。**

为了解决该问题，我们可以使用动态规划，将每次前两数之和存起来，便于下次直接使用，这样子，我们就把一个栈溢出的问题，变为了单纯的数学加法，大大减少了内存的压力。  

## 🍭 示例代码  
```javascript
var fib = function(n) {
    let n1 = 0, n2 = 1, sum;
    for(let i = 0; i < n; i++){
        sum = (n1 + n2) % 1000000007;
        n1 = n2;
        n2 = sum;
    }
    return n1;
};
```

作者：demigodliu  
链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/solution/dong-tai-gui-hua-fei-bo-na-qi-shu-lie-by-fpca/  