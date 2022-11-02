---
title: leetCode Day3
date: 2022-11-02 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Valid Palindrome

題目:

    有一個字串把所有字母轉成小寫,並忽略其他符號,只留字母和數字,由前往後讀和由後往前讀都相同,返回true,不相同返回false



解法:

    先把字串改成小寫,跑迴圈從前面跟後面的值去做比對,如果值不是字母或數字就跳過這個值,最後都相同返回true,不相同返回false


<details> <summary>code</summary>
<pre><code>
func isPalindrome(s string) bool {
    x, y := 0, len(s) - 1
    str := strings.ToLower(s)
    
    for x < y {
        if !isValid(str[x]) {
            x++
            continue
        }
        if !isValid(str[y]) {
            y--
            continue
        }
        if str[x] != str[y] {
            return false
        }
        x++
        y--
    }
    
    return true
}

func isValid(a byte) bool {
    if (a >= 'a' && a <= 'z') || (a >= 'A' && a <= 'Z') || (a >= '0' && a <= '9') {
        return true
    }
    return false
}
</code></pre>
</details>


# Invert Binary Tree

題目:

    有一個二分樹,返回反轉的樹



解法:

    


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
func invertTree(root *TreeNode) *TreeNode {
    node := new(TreeNode)
    
    if root == nil {
        return root
    }
    
    node.Val = root.Val
    
    if root.Right != nil {
        node.Left = invertTree(root.Right)
    } else {
        node.Left = nil
    }
    
    if root.Left != nil {
        node.Right = invertTree(root.Left)
    } else {
        node.Right = nil
    }
    
    return node
}
</code></pre>
</details>