---
title: leetCode Day15
date: 2022-11-14 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Missing Number

題目:

    給一組數字陣列,由0至n,找出消失的數字



解法:

    算出0至n的總和,跑迴圈總和減去數字,最後的數字,就為答案


<details> <summary>code</summary>
<pre><code>
func missingNumber(nums []int) int {
    sum := (len(nums) + 1) * len(nums) / 2
    for _, value := range nums {
        sum -= value
    }
    
    return sum
}
</code></pre>
</details>


# Palindrome Number

題目:

    給一個整數,判斷整數是否為回文



解法:

    判斷整數是否為負數,負數返回false,將整數取10的餘數,在除10,將整數翻轉,判斷反轉後的整數是否和原整數相同


<details> <summary>code</summary>
<pre><code>
func isPalindrome(x int) bool {
    if x < 0 {
        return false
    }
    
    o, r := x, 0
    for x > 0 {
        r = 10 * r + x % 10
        x /= 10
    }
    
    return r == o
}
</code></pre>
</details>
