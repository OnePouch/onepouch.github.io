---
title: leetCode Day15
date: 2022-11-14 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Move Zeroes

題目:

    給一個數字陣列,把所有的0移動到陣列最後,不要使用複製原陣列的方法



解法:

    跑迴圈,如果字數為0,計算0出現幾次,如果不為0,和前面出現的第一個0換位子


<details> <summary>code</summary>
<pre><code>
func moveZeroes(nums []int)  {
    var tmp int
    zeroCount := 0
    for i:=0; i<len(nums); i++ {
        if nums[i] == 0 {
            zeroCount++
        } else {
            tmp = nums[i]
            nums[i] = 0
            nums[i-zeroCount] = tmp
        }
    }
}
</code></pre>
</details>


# Symmetric Tree

題目:

    給一個二分樹,判斷樹是不是對稱的



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
func isSymmetric(root *TreeNode) bool {
    return match(root.Left, root.Right)
}

func match(left *TreeNode, right *TreeNode) bool {
    if left == nil || right == nil {
        return left == right
    }
    
    if left.Val != right.Val {
        return false
    }
    
    return match(left.Left, right.Right) && match(left.Right, right.Left)
}
</code></pre>
</details>
