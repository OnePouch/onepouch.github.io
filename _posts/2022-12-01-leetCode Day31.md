---
title: leetCode Day31
date: 2022-12-01 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Lowest Common Ancestor of a Binary Tree

題目:

    有一個二分樹,給兩個節點,找出最小的共同節點



解法:

    判斷節點是否為空或是p或是q,如果是的話返回該節點,將根節點的左節點和右節點都判斷p和q是否為根節點,如果一個為空,共同的節點就為另一個節點,如果都不為空,就為該節點


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
 func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
     if root == nil || root == p || root == q {
         return root
     }
     
     left := lowestCommonAncestor(root.Left, p, q)
     right := lowestCommonAncestor(root.Right, p, q)
     
     if left == nil {
         return right
     }
     
     if right == nil {
         return left
     }
     
     return root
 }
</code></pre>
</details>
