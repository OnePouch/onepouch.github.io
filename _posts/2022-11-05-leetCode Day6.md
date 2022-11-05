---
title: leetCode Day6
date: 2022-11-05 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Lowest Common Ancestor of a Binary Search Tree

題目:

    給一個二搜尋樹，給兩個此樹的不相同節點，找出最低共同祖先的節點



解法:

    


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val   int
 *     Left  *TreeNode
 *     Right *TreeNode
 * }
 */

func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
    maxValue := Max(p.Val, q.Val)
    minValue := Min(p.Val, q.Val)
    
    for root != nil {
        if root.Val > maxValue {
            root = root.Left
        } else if root.Val < minValue {
            root = root.Right
        } else {
            return root
        }
    }
    
	return nil
}

func Max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func Min(a, b int) int {
    if a > b {
        return b
    }
    return a
}
</code></pre>
</details>


# Balanced Binary Tree

題目:

    給一個二分數, 判斷他的高度是否平衡



解法:

    計算每一層樹的層級的差距,超過1的話,就是不平衡的


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
func isBalanced(root *TreeNode) bool {
    level := CalLevel(root)
    
    if level == -1 {
        return false
    }
    return true
}

func CalLevel(root *TreeNode) int {
    if root == nil {
        return 0
    }
    leftLevel := CalLevel(root.Left)
    rightLevel := CalLevel(root.Right)
    
    if leftLevel == -1 || rightLevel == -1 {
        return -1
    }
    
    levelDiff := leftLevel - rightLevel
    if levelDiff < -1 || levelDiff > 1 {
        return -1
    }

    if leftLevel >= rightLevel {
        return leftLevel + 1
    } else {
        return rightLevel + 1
    }
}
</code></pre>
</details>


# Linked List Cycle

題目:

    給一個鏈表,判斷這張表是否重複



解法:

    定義fast為下兩個值,slow為下一個的值,循環直到如果fast的下一個或下兩個為空,結果為非重複,如果fast=slow的話,表示重複


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func hasCycle(head *ListNode) bool {
    if head == nil {
        return false
    }
    
    fast, slow := head, head
    
    for fast.Next != nil && fast.Next.Next != nil {
        fast = fast.Next.Next
        slow = slow.Next
        
        if fast == slow {
            return true
        }
    }
    
    return false
}
</code></pre>
</details>