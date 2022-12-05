---
title: leetCode Day34
date: 2022-12-05 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Partition Equal Subset Sum

題目:

    有一個數字陣列,將陣列分成兩個,兩陣列總和相同,返回true



解法:

    先判斷陣列長度為1的話返回false,算出陣列總和,因為需要分成兩個和相同的陣列,所以和一定為偶數,如果為基數返回false,使用動態規劃,找出和除2是否存在於數列組合中


<details> <summary>code</summary>
<pre><code>
func canPartition(nums []int) bool {
    if len(nums) == 1 {
        return false
    }
    var sum int
    
    for _, value := range nums {
        sum += value
    }
    
    if sum % 2 == 1 {
        return false
    }
    sum /= 2
    
    dp := make([]bool, sum + 1)
    dp[0] = true
    
    var tmpSum int
    for _, value := range nums {
        tmpSum += value
        for i := sum; i >= 0; i-- {
            if i >= value {
                dp[i] = dp[i] || dp[i-value]
            }
        }
    }
    
    return dp[sum]
}
</code></pre>
</details>