# 剑指 Offer 11. 旋转数组的最小数字
练习链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/

## 题目描述
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

* 示例 1：  
输入：[3,4,5,1,2]  
输出：1  

* 示例 2：  
输入：[2,2,2,0,1]  
输出：0  

## 🧠 解题思路
根据题意，我们第一时间就能通过暴破来解决，用一个变量记录一下当前遍历过程中遇到的最小值是多少，然后遍历结束后，返回最小值即可。

但是，这样的暴破，不优雅！

为什么这么说呢，因为我们知道数组是被旋转了的，所以，在遍历过程中，只要有数字，小于了 numbers[0]，那么该数字一定是最小值，你品，你细品。

诶，所以说，就算是暴破，也要有值得被夸赞的亮点。

---

好了，闲言少叙，暴破不是我们的目标，我们的目标是尽量的降低算法的复杂度，所以我们这里采用二分法。

首先，创建两个指针 leftleft, rightright 分别指向 numbersnumbers 首尾数字，然后计算出两指针之间的中间索引值 middlemiddle，然后我们会遇到以下三种情况：  

middlemiddle > rightright ：代表最小值一定在 middlemiddle 右侧，所以 leftleft 移到 middle + 1middle+1 的位置。  
middlemiddle < rightright ：代表最小值一定在 middlemiddle 左侧或者就是 middlemiddle，所以 rightright 移到 middlemiddle 的位置。  
middlemiddle 既不大于 leftleft 指针的值，也不小于 rightright 指针的值，代表着 middlemiddle 可能等于 leftleft 指针的值，或者 rightright 指针的值，我们这时候只能让 rightright 指针递减，来一个一个找最小值了。

## 🍭 示例代码
```javascript
// 二分法
var minArray = function(numbers) {
    let left = 0, right = numbers.length - 1;
    while(left < right){
        let middle = left + ~~((right - left) / 2); //~~ 取整 ~是二进制的按位取反
        if(numbers[middle] > numbers[right]) left = middle + 1;
        else if(numbers[middle] < numbers[right]) right = middle;
        else right--;
    }
    return numbers[left];
};

// 暴破【不推荐】
function minArray(numbers) {
    for(let i = 0; i < numbers.length; i++){
        if(numbers[i] < numbers[0]){
            return numbers[i];
        }
    }
    return numbers[0];
}
```
作者：demigodliu  
链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/solution/er-fen-sou-suo-xuan-zhuan-shu-zu-de-zui-si7my/

```javascript
//我的暴破方法（用了相邻两数比较）
var minArray = function(numbers) {
    for(let i = 0; i < numbers.length; i++){
        if(numbers[i] > numbers[i+1]){
            return numbers[i+1]
        }
    }
    return numbers[0]
};
```