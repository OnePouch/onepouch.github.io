---
title: leetCode Day30
date: 2022-11-30 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Permutations

題目:

    有一個數字陣列,回傳所有的組合



解法:

    


<details> <summary>code</summary>
<pre><code>
func permute(nums []int) [][]int {
    var cur []int
    var result [][]int
    visited := make(map[int]int)
    
    search(nums, &visited, &cur, &result)
    
    return result
}

func search(nums []int, visited *map[int]int, cur *[]int, result *[][]int) {
    if len(nums) == len(*cur) {
        cpycur := make([]int, len(*cur))
        copy(cpycur, *cur)
        *result = append(*result, cpycur)
    }
    
    for i := 0; i < len(nums); i++ {
        if value, ok := (*visited)[i]; ok && value == 1 {
            continue
        }
        (*visited)[i] = 1
        *cur = append(*cur, nums[i])
        search(nums, visited, cur, result)
        (*visited)[i] = 0
        *cur = (*cur)[:len(*cur) - 1]
    }
}
</code></pre>
</details>


# Merge Intervals

題目:

    有一組數字矩陣,將有重複的部分合併



解法:

    如果當前的結束數字大於等於下一個陣列的開始數字,結束數字為大的值,遞迴


<details> <summary>code</summary>
<pre><code>
func merge(intervals [][]int) [][]int {
    if len(intervals) == 1 {
        return intervals
    }
    
    var result [][]int
    sort.Slice(intervals, func(i, j int) bool {
        return intervals[i][0] < intervals[j][0]
    })
    cur := intervals[0]
    
    for i := 1; i < len(intervals); i++ {
        if cur[1] >= intervals[i][0] {
            cur[1] = max(cur[1], intervals[i][1])
        } else {
            result = append(result, cur)
            cur = intervals[i]
        }
        
        if i == len(intervals) - 1 {
            result = append(result, cur)
        }
    }
    
    return result
}

func max(a int, b int) int {
    if a > b {
        return a
    }
    return b
}
</code></pre>
</details>