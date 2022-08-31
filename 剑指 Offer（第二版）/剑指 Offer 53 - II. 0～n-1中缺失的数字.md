# 剑指 Offer 53 - II. 0～n-1中缺失的数字
练习链接：https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/

**代码**  
```javascript
const missingNumber = function (nums) {
    if (nums[nums.length - 1] === nums.length - 1) {
        return nums.length
    }
    let left = 0, right = nums.length - 1;
    while (left <= right) {
        const mid = Math.floor((left + right) / 2)
        if (nums[mid] == mid) {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return left
};
```