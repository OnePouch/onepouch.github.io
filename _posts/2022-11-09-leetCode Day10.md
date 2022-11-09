---
title: leetCode Day10
date: 2022-11-09 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Middle of the Linked List

題目:

    給一個連結串,找出中間的節點,如果中間節點有兩個的話,返回第二個節點



解法:

    使用龜兔賽跑方式,fast走兩步,slow走一步,當fast走到終點時,slow剛好走到中間,返回slow


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func middleNode(head *ListNode) *ListNode {
    fast, slow := head, head;
    
    for fast != nil && fast.Next != nil {
        fast = fast.Next.Next
        slow = slow.Next
    }
    
    return slow
}
</code></pre>
</details>


# Maximum Depth of Binary Tree

題目:

    求二分數的最大深度



解法:

    每個節點的深度為左邊和右邊取最大值+1,如果左節點為空回傳0,右節點為空回傳0,每層跑完就能找到根節點的最大深度


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
func maxDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }
    
    left := maxDepth(root.Left)
    right := maxDepth(root.Right)
    
    return max(left, right) + 1
}

func max(a int, b int) int {
    if (a > b) {
        return a
    }
    return b
}
</code></pre>
</details>