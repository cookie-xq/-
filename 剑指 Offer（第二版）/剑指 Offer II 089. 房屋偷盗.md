# 剑指 Offer II 089. 房屋偷盗
练习链接：https://leetcode-cn.com/problems/Gu0c2T/
## 题目描述
一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响小偷偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。  
给定一个代表每个房屋存放金额的非负整数数组 nums ，请计算 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。

* 示例 1：  
输入：nums = [1,2,3,1]  
输出：4  
解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。

* 示例 2：  
输入：nums = [2,7,9,3,1]  
输出：12  
解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。
 
提示：  
1 <= nums.length <= 100  
0 <= nums[i] <= 400

## 🍭 示例代码
```
// 1. 记忆化搜索
var rob = function(nums) {
    const n = nums.length
    const memo = new Array(n).fill(-1)

    const dfs = (i) => {
        if (i >= n) return 0
        if (memo[i] != -1) return memo[i]

        const left = dfs(i + 1)
        const right = dfs(i + 2)

        memo[i] = Math.max(left, right + nums[i])
        return memo[i]
    }

    return dfs(0)
};

// 2. 记忆化搜索(二)
var rob = function(nums) {
    const n = nums.length
    const memo = new Array(n).fill(-1)

    const dfs = (i) => {
        if (i == 0) return nums[0]
        if (i == 1) return Math.max(nums[0], nums[1])

        if (memo[i] != -1) return memo[i]

        const left = dfs(i - 1)
        const right = dfs(i - 2)

        memo[i] = Math.max(left, right + nums[i])
        return memo[i]
    }

// 3. 动态规划
var rob2 = function(nums) {
    const n = nums.length
    if (n == 1) return nums[0]

    const dp = new Array(n).fill(-1)
    dp[0] = nums[0]
    dp[1] = Math.max(nums[0], nums[1])

    for (let i = 2; i < n; i++) {
        dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i])
    }

    return dp[n - 1]
}

// 4. 动态规划 + 状态压缩
var rob4 = function(nums) {
    const n = nums.length
    if (n == 1) return nums[0]

    let prevMax = 0
    let currMax = 0

    for (const num of nums) {
        const tmpMax = Math.max(currMax, prevMax + num)
        prevMax = currMax
        currMax = tmpMax
    }

    return currMax
}
//作者：tangweiqun
//链接：https://leetcode-cn.com/problems/Gu0c2T/solution/jian-dan-yi-dong-javac-pythonjs-da-jia-j-kc58/
```