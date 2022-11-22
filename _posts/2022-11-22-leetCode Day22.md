---
title: leetCode Day22
date: 2022-11-22 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Longest Substring Without Repeating Characters

題目:

    給一個字串,找出最長的子字串,子字串不能有重複的字



解法:

    定義一個陣列用來儲存字母在哪個位置出現過,字串跑迴圈,如果該字母沒有在陣列中出現,把字母存入陣列中,長度為max(之前的長度,跑到第幾個位置-前面最大的重複長度+1),如果字母有出現在陣列中,重複長度為max(重複長度,該字母上次出現的位置+1)


<details> <summary>code</summary>
<pre><code>
func lengthOfLongestSubstring(s string) int {
    var res int
    var j int
    arr := make(map[rune]int)
    
    for key, value := range s {
        if _, ok := arr[value]; ok {
            j = max(j, arr[value] + 1)
        }
        arr[value] = key
        res = max(res, key - j + 1)
    }
    
    return res
}

func max(a int, b int) int {
    if a > b {
        return a
    }
    
    return b
}
</code></pre>
</details>


# 3Sum

題目:

    有一個非排序數字陣列,求其中三個數的總和為0,三個數的位置皆不同,將符合的數組成矩陣返回



解法:

    先進行排序,遞回陣列,如果該值在上一次出現過,就跳過,設定後兩數的點為,該點+1(j)和最後一點(k),如果j<k就持續執行,算出三個座標的總和(s),s如果大於0,表示後兩數和過大,k--,s如果小於0,表示後兩數和過小,j++,如果s等於0,將三點的值丟入結果矩陣中,如果j和j+1的值相同的話,j++,如果k和k-1的值想同的話,k--


<details> <summary>code</summary>
<pre><code>
func threeSum(nums []int) [][]int {
    var result [][]int
    var jdx int
    var kdx int
    var s int
    
    sort.Ints(nums)
    
    for idx := 0; idx < len(nums); idx++ {
        if idx > 0 && nums[idx] == nums[idx - 1] {
            continue
        }
        
        jdx = idx + 1
        kdx = len(nums) - 1
        for jdx < kdx {
            s = nums[idx] + nums[jdx] + nums[kdx]
            if s == 0 {
                
                result = append(result, []int{nums[idx], nums[jdx], nums[kdx]})
                
                for jdx < kdx && nums[jdx] == nums[jdx + 1] {
                    jdx++
                }
                for jdx < kdx && nums[kdx] == nums[kdx - 1] {
                    kdx--
                }
                jdx++
                kdx--
            } else if s > 0 {
                kdx--
            } else {
                jdx++
            }
        }
    }
    
    return result
}
</code></pre>
</details>