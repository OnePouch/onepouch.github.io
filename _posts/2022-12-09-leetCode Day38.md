---
title: leetCode Day38
date: 2022-12-09 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Unique Paths

題目:

    有一個矩陣原點在0,0,有寬m長n,終點為m-1,n-1,只能向右或向下走,求走到終點有幾種方法



解法:

    設定原點和往下到底和往右到底為1,任意點為左邊加上面的值,即可求得終點


<details> <summary>code</summary>
<pre><code>
func uniquePaths(m int, n int) int {
    var dp [][]int
    dp = append(dp, []int{1})
    for i := 1; i < m; i++ {
        dp = append(dp, []int{1})
    }

    for j := 1; j < n; j++ {
        dp[0] = append(dp[0], 1)
    }
    
    for i:= 1; i < m; i++ {
        for j := 1; j < n; j++ {
            dp[i] = append(dp[i], dp[i - 1][j] + dp[i][j - 1])
        }
    }

    return dp[m - 1][n - 1]
}
</code></pre>
</details>


# Construct Binary Tree from Preorder and Inorder Traversal

題目:

    有兩個數字陣列preorder和inorder,其中preorder代表二分樹的前序遍歷,inorder代表二分樹的中序遍歷,求二分樹為何



解法:

    因為前序遍歷為中左右,所以preorder[0]代表了root的值,然後中序遍歷為左中右,所以我們找到preorder[0]在inorder的index,此index前代表了在樹的左邊,index後代表在樹的右邊,遞迴方法就可以建出此樹,如果preorder或inorder為空的話,返回空


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
func buildTree(preorder []int, inorder []int) *TreeNode {
    if len(preorder) == 0 || len(inorder) == 0 {
        return nil
    }

    rootVal := preorder[0]
    result := &TreeNode{Val: rootVal}
    rootIdx := 0
    for rootIdx < len(inorder) {
        if inorder[rootIdx] == rootVal {
            break
        }
        rootIdx++
    }
    result.Left = buildTree(preorder[1:], inorder[:rootIdx])
    result.Right = buildTree(preorder[rootIdx + 1:], inorder[rootIdx + 1:])

    return result
}
</code></pre>
</details>