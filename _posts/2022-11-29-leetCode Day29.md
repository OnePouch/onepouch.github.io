---
title: leetCode Day29
date: 2022-11-29 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Search in Rotated Sorted Array

題目:

    有一個旋轉排序的數字陣列,找出target是否存在陣列中



解法:

    使用二分法找到中間值,如果中間值,如果中間值比左邊的值還大的話,代表左邊是排序的,判斷target是否在左邊到中間之間,如果是的話右邊為中間-1,如果不是左邊為中間+1,如果中間值比左邊的值還要小的話,因為中間至右邊為排序的,判斷target是否在中間和右邊之間,如果是的話,左邊為中間+1,如果不是右邊為中間-1


<details> <summary>code</summary>
<pre><code>
func search(nums []int, target int) int {
    left := 0
    right := len(nums) - 1
    
    for left <= right {
        mid := (left + right) / 2
        if nums[mid] == target {
            return mid
        }

        if nums[mid] > nums[left] {
            if nums[mid] > target && target >= nums[left] {
                right = mid - 1
            } else {
                left = mid + 1
            }
        } else {
            if target > nums[mid] && nums[right] >= target {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
        
    }
    
    return -1
}
</code></pre>
</details>


# Combination Sum

題目:

    有一組數字陣列,裡面有不同的數字,求所有數字組合為target的數字組合,同一個數字可以使用無線多次



解法:

    使用深度搜尋法,取得所有的組合


<details> <summary>code</summary>
<pre><code>
func combinationSum(candidates []int, target int) [][]int {
    var result [][]int
    var cur []int
    
    search(candidates, 0, target, &cur, &result)
    return result
}

func search(candidates []int, idx int, target int, cur *[]int, result *[][]int) {
    if target == 0 {
        cpycur := make([]int, len(*cur))
        copy(cpycur, *cur)
        *result = append(*result, cpycur)
    }
    
    for i := idx; i < len(candidates); i++ {
        if candidates[i] > target {
            continue
        }
        *cur = append(*cur, candidates[i])
        search(candidates, i, target - candidates[i], cur, result)
        *cur = (*cur)[:len(*cur)-1]
    }
}
</code></pre>
</details>