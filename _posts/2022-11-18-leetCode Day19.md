---
title: leetCode Day19
date: 2022-11-18 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Maximum Subarray

題目:

    有一個數字陣列,找出此陣列中的子陣列總和最大的值



解法:

    跑迴圈,如果前面的總和為負數時,總和為0,從新計算總和,如果總和比最大值還大時,替換最大值


<details> <summary>code</summary>
<pre><code>
func maxSubArray(nums []int) int {
    sum := nums[0];
    max := nums[0];
    
    for i:=1; i<len(nums); i++ {
        if sum < 0 {
            sum = 0
        }
        sum += nums[i]
        
        if (sum > max) {
            max = sum
        }
    }
    
    return max
}
</code></pre>
</details>
