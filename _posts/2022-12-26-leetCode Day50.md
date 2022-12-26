---
title: leetCode Day50
date: 2022-12-26 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Find the Duplicate Number

題目:

    有一個數字陣列,有n + 1的數字,數字的值為1~n,求陣列中重複的數字



解法:

    建立一個陣列,用數字為key,值為bool,數字出現過設定為true,如果數字為true,代表重複出現


<details> <summary>code</summary>
<pre><code>
func findDuplicate(nums []int) int {
    exist := make([]bool, len(nums))

    for _, value := range nums {
        if exist[value] {
            return value
        }
        exist[value] = true
    }

    return 0
}
</code></pre>
</details>