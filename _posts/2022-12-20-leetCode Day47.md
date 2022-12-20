---
title: leetCode Day47
date: 2022-12-20 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Maximum Product Subarray

題目:

    有一個數字陣列,求子陣列中,乘積最大



解法:

    使用動態規劃,定義乘積最大和最小,如果值為正,乘積最大為max(dpMax[i-1]*nums[i],nums[i]),乘積最小為min(dpMin[i-1]*nums[i],nums[i]),如果值為負數,乘積最大為max(dpMin[i-1]*nums[i],nums[i]),乘積最小為min(dpMax[i-1]*nums[i],nums[i])


<details> <summary>code</summary>
<pre><code>
func maxProduct(nums []int) int {
    dpMax := make([]int, len(nums))
    dpMin := make([]int, len(nums))
    dpMax[0] = nums[0]
    dpMin[0] = nums[0]
    maximum := nums[0]

    for i := 1; i < len(nums); i++ {
        if nums[i] > 0 {
            dpMax[i] = max(dpMax[i - 1] * nums[i], nums[i])
            dpMin[i] = min(dpMin[i - 1] * nums[i], nums[i])
        } else {
            dpMax[i] = max(dpMin[i - 1] * nums[i], nums[i])
            dpMin[i] = min(dpMax[i - 1] * nums[i], nums[i])
        }
        if maximum < dpMax[i] {
            maximum = dpMax[i]
        }
    }

    return maximum
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func min(a, b int) int {
    if a > b {
        return b
    }
    return a
}
</code></pre>
</details>


# Design Add and Search Words Data Structure

題目:

    製作一個可以新增字串,並可以查詢字串存不存在的資料結構,如果查詢字串中有.代表可以是任意字母



解法:

    先算出字串長度,新增進該字串長度的矩陣中,查詢時如果,該字串長度沒有值,返回false,如果有就查看字串是否一致


<details> <summary>code</summary>
<pre><code>
type WordDictionary struct {
    Data [][]string
}


func Constructor() WordDictionary {
    var data [][]string
    for i := 0; i <= 25; i++ {
        data = append(data, make([]string, 0))
    }
    return WordDictionary{Data: data}
}


func (this *WordDictionary) AddWord(word string)  {
    strlen := len(word)
    this.Data[strlen] = append(this.Data[strlen], word)
    fmt.Println(len(this.Data[strlen]))
}


func (this *WordDictionary) Search(word string) bool {
    strlen := len(word)
    if len(this.Data[strlen]) == 0 {
        return false
    }

    for _, value := range this.Data[strlen] {
        flag := true
        for i := 0; i < strlen; i++ {
            if word[i] == '.' {
                continue
            }
            if word[i] != value[i] {
                flag = false
                break
            }
        }
        if flag {
            return true
        }
    }

    return false
}


/**
 * Your WordDictionary object will be instantiated and called as such:
 * obj := Constructor();
 * obj.AddWord(word);
 * param_2 := obj.Search(word);
 */
</code></pre>
</details>