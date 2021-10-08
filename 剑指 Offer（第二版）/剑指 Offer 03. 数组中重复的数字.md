# 剑指 Offer 03. 数组中重复的数字
练习链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/

## 题目描述
找出数组中重复的数字。  

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。  

* 示例 1：  
输入：  
[2, 3, 1, 0, 2, 5, 3]  
输出：2 或 3   

限制：  
2 <= n <= 100000  

## 解题思路
* 直接扫描例如暴力双循环或者用indexOf(),时间都过长也不优雅，暂不考虑

* 常规思路就是把输入的数组排序，然后从排序的数组中找到重复的数字只需要从头到尾扫描排序后的数组即可。排序一个长度为n的数组需要 O(nlogn) 的时间复杂度  
```javascript
var findRepeatNumber = function(nums){
    nums.sort()
    for(let i = 0; i < nums.length - 1; i++){
       if(nums[i] == nums[i + 1]) return nums[i]
    }
}
```

* 第二种思路就是利用哈希表来解决。从头到尾扫描数组中的数字，每扫描一个数字，就用 O(1) 的时间去判断哈希表里是否包含该数字，如果哈希表里已经存在该数字，就找到一个重复的数字，如果哈希表里面没有这个数字，就把它加入哈希表。这个思路的时间复杂度为 O(n),空间复杂度为 O(n)  
```javascript
//1. Map()实现哈希
var findRepeatNumber = function(nums) {
    let map = new Map()
    for(let i of nums){
        if(map.has(i)) return i
        map.set(i, 1)
    }
}
//2. 自实现哈希
var findRepeatNumber = function(nums) {
    let obj = {}
    let cur
    for(let i = 0; i < nums.length; i++){
        cur = nums[i]
        if(obj[cur] == true){
            return cur
        }else{
            obj[cur] = true
        }
    }
}
//作者：WongDaWEEEE
//链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/solution/3chong-fang-fa-chao-99-ha-xi-zi-dian-pai-56uw/
```

* 我们现在把数组的索引利用起来；从头到尾扫描这个数组中的数字，当扫描到下标为 i 的数字时，首先比较这个数字（用 m 表示）是不是等于 i,如果是则接着扫描下一个数字；如果不是，则拿它和第 m 个数字进行比较，如果它和第 m 个数字相等，就找到了一个重复的数字（该数字在下标为 i 和 m 的位置都出现了）；如果它和第 m 个数字不相等，就把第 i 个数字和第 m 个数字交换，把 m 放到属于它的位置。接下来再重复这个比较、交换的过程，直到我们发现一个重复的数字  
```javascript
var findRepeatNumber = function(nums) {
  if (nums == null || nums.length < 0) {
    return -1;
  }
  // 题目的条件是数组 nums 里的所有数字都在 0～n-1 的范围内
  for (let i = 0, length = nums.length; i < length; i++) {
    if (nums[i] < 0 || nums[i] > length - 1) {
      return -1;
    }
  }
  // 思路就是把数字放到对应的索引上  比方说数字3放到索引3的位置
  for (let i = 0; i < nums.length; i++) {
    // 如果当前数字跟对应的索引不相同则交换
    while (nums[i] != i) {
      if (nums[i] == nums[nums[i]]) {
        return nums[i];
      }
      // 这里还不能用简化的方式   一用简化的方式就报超时问题
      // [nums[i], nums[nums[i]]] = [nums[nums[i]], nums[i]];
      let temp = nums[i];
      nums[i] = nums[temp];
      nums[temp] = temp;
    }
  }
  return -1;
};

var findRepeatNumber = function(nums){
    let cur
    for(let i = 0; i < nums.length; i++){
        while (nums[i] != i) {
            cur = nums[i]
            if (nums[i] == nums[cur]) {
                return nums[i];
            }else{
                nums[i] = nums[cur];
                nums[cur] = cur;
            }
        }
    }
}
//作者：WongDaWEEEE
//链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/solution/3chong-fang-fa-chao-99-ha-xi-zi-dian-pai-56uw/
```

解题思路来自：  
作者：angela-x  
链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/solution/jian-zhi-offer-shu-zhong-guan-fang-ti-ji-9i1o/  