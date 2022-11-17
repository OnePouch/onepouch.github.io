---
title: leetCode Day18
date: 2022-11-17 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Subtree of Another Tree

題目:

    給兩個二分樹,其中一個為另一個的子樹,返回true,不是返回false



解法:

    每個節點都判斷是否和子樹相同,如果所有節點都不想同,返回false,如果有一個節點相同返回true


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
func isSubtree(root *TreeNode, subRoot *TreeNode) bool {
    if root == nil {
        return false;
    }
    
    if isSame(root, subRoot) {
        return true;
    }
    
    return isSubtree(root.Left, subRoot) || isSubtree(root.Right, subRoot)
}

func isSame(root *TreeNode, subRoot *TreeNode) bool {
    if root == nil || subRoot == nil {
        return root == subRoot
    }
    
    if root.Val != subRoot.Val {
        return false
    }
    
    return isSame(root.Left, subRoot.Left) && isSame(root.Right, subRoot.Right)
}
</code></pre>
</details>


# Squares of a Sorted Array

題目:

    一個順序排列的數字陣列,陣列中的值平方在順序排序



解法:

    因為陣列是有序的,所以平方的最大數,不是第一位,就是最後一位,因次我們從頭和尾一起找哪個數平方較大,直到陣列跑完可得答案


<details> <summary>code</summary>
<pre><code>
func sortedSquares(nums []int) []int {
    arrLen := len(nums)
    s, e := 0, arrLen - 1
    result := make([]int, arrLen)
    
    for i:=arrLen - 1; i >= 0; i-- {
        if int(math.Abs(float64(nums[s]))) > nums[e] {
            result[i] = nums[s] * nums[s]
            s++
        } else {
            result[i] = nums[e] * nums[e]
            e--
        }
    }
    
    return result
}
</code></pre>
</details>
