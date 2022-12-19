---
title: leetCode Day45
date: 2022-12-18 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# House Robber

題目:

    一個數字陣列,值代表多少金額,有個小偷偷錢,如果偷相鄰的兩個會觸發警報,求小偷最多能偷多少錢



解法:

    當前最大為前一個或是當前值+前第二個誰大,返回陣列最後的值,為最大值


<details> <summary>code</summary>
<pre><code>
func rob(nums []int) int {
    if len(nums) == 1 {
        return nums[0]
    }
    dp := make([]int, len(nums))
    dp[0] = nums[0]
    dp[1] = max(dp[0], nums[1])

    for i := 2; i < len(nums); i++ {
        dp[i] = max(dp[i - 1], nums[i] + dp[i - 2])
    }

    return dp[len(nums) - 1]
}

func max(a int, b int) int {
    if a > b{
        return a
    }
    return b
}
</code></pre>
</details>


# Gas Station

題目:

    有一個環形加油站,有每個站的加油數量和到下一個站所需的油量,如果能走完一圈返回從哪個點開始走,如果都不能返回-1



解法:

    當前總和小於0的話,左邊總和為上個左邊總和+當前總和,當前總和為0,idx為當前+1,最後如果左邊總和+總和小於0,返回-1,大於等於0,返回idx


<details> <summary>code</summary>
<pre><code>
func canCompleteCircuit(gas []int, cost []int) int {
    var sum int
    var total int
    var idx int

    for i := 0; i < len(gas); i++ {
        sum += gas[i] - cost[i]
        if sum < 0 {
            idx = i + 1
            total += sum
            sum = 0
        }
    }

    if total + sum >= 0 {
        return idx
    }
    return -1
}
</code></pre>
</details>