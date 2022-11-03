---
title: leetCode Day4
date: 2022-11-03 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Valid Anagram

題目:

    給兩個字串,如果這兩個字串裡面的字母從新組合都相同返回true,不同返回false



解法:

    判斷兩個數的長度,如果不一樣,回傳false,將第一個字串的所有字母存入hash表出現次數,遍歷第二個字串,如果出現字數次數為0,回傳false,字母出現次數--


<details> <summary>code</summary>
<pre><code>
func isAnagram(s string, t string) bool {    
    if len(s) != len(t) {
        return false
    }
    
    tmp := make(map[rune]int)
    
    for _, value := range s {
        tmp[value]++
    }
    
    for _, value := range t {
        if tmp[value] == 0 {
            return false
        }
        tmp[value]--
    }
    
    return true
}
</code></pre>
</details>


# Binary Search

題目:

    有一個數字陣列,找出目標值是否在陣列內,不在回傳-1,在的話回傳key, 空間複雜度O(log n)



解法:

    使用二分法看中間值跟目標值比大小,目標值大的話,最小值為中間值+1,目標值小的話,最大值為中間值-1,直到找出值,或是跑完陣列


<details> <summary>code</summary>
<pre><code>
func search(nums []int, target int) int {
    min, max, mid := 0, len(nums) - 1, 0
    
    for min <= max {
        mid = (min + max) / 2
        if nums[mid] > target {
            max = mid - 1
        } else if nums[mid] < target {
            min = mid + 1
        } else {
            return mid
        }
    }
    
    return -1
}
</code></pre>
</details>