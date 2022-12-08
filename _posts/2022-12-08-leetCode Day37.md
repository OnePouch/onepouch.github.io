---
title: leetCode Day37
date: 2022-12-08 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Subsets

題目:

    有一個數字陣列,裡面的數字都不重複,組合成數字所有排列組合的矩陣



解法:

    使用遞歸,將每個組合找出來並存入結果裡面,最後返回結果


<details> <summary>code</summary>
<pre><code>
func subsets(nums []int) [][]int {
    var result [][]int

    result = append(result, []int{})

    return set(nums, 0, []int{}, result)
}

func set(nums []int, j int, cur []int, result [][]int) [][]int {
    for i := j; i < len(nums); i++ {
        cur = append(cur, nums[i])
        copyCur := make([]int, len(cur))
        copy(copyCur, cur)
        result = append(result, copyCur)
        result = set(nums, i + 1, cur, result)
        cur = cur[:len(cur) - 1]
    }

    return result
}
</code></pre>
</details>


# Binary Tree Right Side View

題目:

    有一個二分樹,把每一層最右邊的樹組成陣列



解法:

    如果節點為空跳過,判斷結果的長度和樹的層級相同的話,將節點的值存入結果中,優先執行右節點,在執行左節點,確保第一次進入下一層的值為最右的節點


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func rightSideView(root *TreeNode) []int {
    var result []int
    return search(root, result, 0)
}

func search(root *TreeNode, result []int, level int) []int {
    if root == nil {
        return result
    }

    if level == len(result) {
        result = append(result, root.Val)
    }
    
    result = search(root.Right, result, level + 1)
    result = search(root.Left, result, level + 1)

    return result
}
</code></pre>
</details>


# Longest Palindromic Substring

題目:

    有一個字串,求最大的回文字串



解法:

    以每個字串為基準,看是否有奇數回文或偶數回文,奇數回文為基準點左右是否相同,偶數回文為基準點和基準點右邊是否相同,如果相同左邊減一右邊加一,直到不相同為止,即可求出最大回文字串


<details> <summary>code</summary>
<pre><code>
func longestPalindrome(s string) string {
    var result string
    var tmp string

    for i := 0; i < len(s); i++ {
        tmp = even(s, i)
        if len(tmp) > len(result) {
            result = tmp
        }
        tmp = odd(s, i)
        if len(tmp) > len(result) {
            result = tmp
        }
    }

    return result
}

func even(s string, i int) string {
    var ans string
    left := i
    right := i + 1

    for left >= 0 && right < len(s) {
        if s[left] != s[right] {
            break
        }
        ans = s[left:right + 1]
        left--
        right++
    }

    return ans
}

func odd(s string, i int) string {
    var ans string
    ans = s[i:i + 1]
    left := i - 1
    right := i + 1

    for left >= 0 && right < len(s) {
        if s[left] != s[right] {
            break
        }
        ans = s[left:right + 1]
        left--
        right++
    }

    return ans
}
</code></pre>
</details>