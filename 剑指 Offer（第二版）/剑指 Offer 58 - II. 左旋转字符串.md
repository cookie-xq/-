# 剑指 Offer 58 - II. 左旋转字符串
练习链接：https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/

## 题目描述
字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。  

* 示例 1：
输入: s = "abcdefg", k = 2  
输出: "cdefgab"  

* 示例 2：
输入: s = "lrloseumgh", k = 6  
输出: "umghlrlose"  

限制：  
1 <= k < s.length <= 10000  

## 代码
```javascript
//1.我的代码
var reverseLeftWords = function(s, n) {
    s = s.split('')
    let spin = []
    for(let i = 0; i<n;i++){
        spin.push(s.shift(s[0]))
    }
    return s.concat(spin).join('')
};
//2.奇思妙想
//作者：eric-404
//链接：https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/solution/ru-guo-zhao-nu-peng-you-ye-neng-zhe-yao-b4mao/
var reverseLeftWords = function(s, n) {
    var data = `${s.slice(n)}${s.slice(0,n)}`
    return data
};
//3.不申请额外空间，只在本串上操作
//作者：carlsun-2
//链接：https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/solution/dai-ma-sui-xiang-lu-dai-ni-gao-ding-zuo-vs2oc/
var reverseLeftWords = function (s, n) {
    const reverse = (str, left, right) => {
        let strArr = str.split("");
        for (; left < right; left++, right--) {
            [strArr[left], strArr[right]] = [strArr[right], strArr[left]];
        }
        return strArr.join("");
    }
    s = reverse(s, 0, n - 1);
    s = reverse(s, n, s.length - 1);
    return reverse(s, 0, s.length - 1);
};
```