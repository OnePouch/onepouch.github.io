---
title: leetCode Day17
date: 2022-11-16 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Convert Sorted Array to Binary Search Tree

題目:

    給一個順序排列的數字陣列,將它轉換成高平衡的二收尋樹



解法:

    找出陣列中間值,樹的左節點為中間值往左的陣列,樹的右節點為中間值往右的陣列,迴圈直到陣列跑完


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
func sortedArrayToBST(nums []int) *TreeNode {
    return sort(nums, 0, len(nums)-1)
}

func sort(nums []int, start int, end int) *TreeNode {
    if (start > end) {
        return nil
    }
    
    mid := (start + end) / 2
    
    node := &TreeNode{
        Val: nums[mid],
        Left: sort(nums, start, mid - 1),
        Right: sort(nums, mid + 1, end),
    }
    
    return node
}
</code></pre>
</details>


# Reverse Bits

題目:

    給一個數字,將轉成二進制並反轉,回傳結果



解法:

    預設結果為0,迴圈,結果左移,如果輸入為奇數,結果+1,輸入右移,跑32次迴圈,可得答案


<details> <summary>code</summary>
<pre><code>
func reverseBits(num uint32) uint32 {
    var result uint32
    
    for i:=0; i<32; i++ {
        result <<= 1
        if num % 2 == 1 {
            result += 1
        }
        num >>= 1
    }
    
    return result
}
</code></pre>
</details>
