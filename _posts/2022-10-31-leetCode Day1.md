---
title: leetCode Day1
date: 2022-10-31 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Two Sum

題目:

    給一組數字陣列和一個數字target,找出陣列中兩數相加等於target的位置



解法:

    建立一個hash表, 跑陣列將陣列的key和value互換存入hash表, 如果target - value有在hash表存在,代表找到結果為key和hash表中target - value的值


<details> <summary>code</summary>
<pre><code>
func twoSum(nums []int, target int) []int {
    tmp := make(map[int]int)

    for key, value := range nums {
        index, ok := tmp[target - value]
        if ok {
            return []int{key, index}
        }
        tmp[value] = key
    }
    
    return nil
}
</code></pre>
</details>


# Valid Parentheses

題目:

    給一個字串只有(){}[]六個字元, 判斷這個字串是否合法? 1. 左括號一定有相應了右括號 2. 左右的括號必須是順序的 3.每一個右括號都要有一個相應的左括號



解法:

    先判斷字串大小如果為奇數,返回false,跑迴圈,如果為左括號,將對應的右括號存入tmp中,如果為右括號,將tmp中最後存入的值拿出,判斷是否為相同的右括號,如果不同,返回false,如果相同,把tmp最後的值丟出,最後判斷tmp是否為空,如果為空,返回true,如果不為空,回傳false


<details> <summary>code</summary>
<pre><code>
func isValid(s string) bool {
    if len(s) % 2 == 1 {
        return false
    }
    
    tmp := []rune{}
    match := map[rune]rune {
        '(': ')',
        '[': ']',
        '{': '}',
    }
    
    for _, value := range s {
        closed, ok := match[value];
        if ok {
            tmp = append(tmp, closed)
            continue
        }
        
        l := len(tmp) - 1
        if l < 0 || value != tmp[l] {
            return false
        }
        
        tmp = tmp[:l]
    }
    
    return len(tmp) == 0
}
</code></pre>
</details>