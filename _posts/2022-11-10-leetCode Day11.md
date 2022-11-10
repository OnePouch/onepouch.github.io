---
title: leetCode Day11
date: 2022-11-10 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Contains Duplicate

題目:

    給一個數字陣列,如果任何一個數字出現最少兩次,返回成功,否則返回失敗



解法:

    設定一個空陣列arr,將nums的值出現的次數,存入arr中,如果大於等於2,返回成功,否則返回失敗


<details> <summary>code</summary>
<pre><code>
func containsDuplicate(nums []int) bool {
    arr := make(map[int]int)
    
    for _, value := range nums {
        arr[value]++
        if arr[value] == 2 {
            return true
        }
    }
    
    return false
}
</code></pre>
</details>


# Roman to Integer

題目:

    羅馬字母轉成數字



解法:

    如果前一位比後一位小的話,變負的總和相加


<details> <summary>code</summary>
<pre><code>
func romanToInt(s string) int {
    match := map[string]int {
        "I" : 1,
        "V" : 5,
        "X" : 10,
        "L" : 50,
        "C" : 100,
        "D" : 500,
        "M" : 1000,
    }
    var sum int
    
    for i:=0; i<len(s); i++ {
        if i != len(s) - 1 {
            if match[s[i:i+1]] < match[s[i+1:i+2]] {
               sum -= match[s[i:i+1]]
            } else {
                sum += match[s[i:i+1]]
            }
        } else {
            sum += match[s[i:i+1]]
        }
        
    }
    
    return sum
}
</code></pre>
</details>