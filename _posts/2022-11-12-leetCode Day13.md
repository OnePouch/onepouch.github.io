---
title: leetCode Day13
date: 2022-11-12 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Counting Bits

題目:

    給一個正整數,返回從0至n的二進制,1出現的數量



解法:

    n出現1的數字為n向右移動一格,就會是n/2無條件捨去,然後再被右移移除的那個數是1還是0,就會是n%2,每層的算法就會是f[n / 2] + n % 2


<details> <summary>code</summary>
<pre><code>
func countBits(n int) []int {
    var result []int
    var num int
    
    result = append(result, 0)
    
    for i:=1; i<=n; i++ {
        num = result[i/2] + i % 2
        result = append(result, num)
    }
    
    return result
}
</code></pre>
</details>


# Same Tree

題目:

    給兩個二分樹,判斷這兩個是否相等



解法:

    遞歸,如果p等於nil,q等於nil,返回true,如果p等於nil,q不等於nil,或是p不等於nil,q等於nil,返回false,如果p.Val不等於q.Val,返回false,每層都帶各自的左右節點,最後判斷,左右是否皆為true


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
func isSameTree(p *TreeNode, q *TreeNode) bool {
    if p == nil && q == nil {
        return true
    }

    if (p == nil && q != nil) || (p != nil && q == nil) {
        return false
    }
    
    if p.Val != q.Val {
        return false
    }
    
    return isSameTree(p.Left, q.Left) && isSameTree(p.Right, q.Right)
}
</code></pre>
</details>


# Number of 1 Bits

題目:

    給一個數字轉成二進制,會有幾個1



解法:

    迴圈 num % 2, num / 2,如果num % 2為1的話,代表有1出現,一直跑到num為0,計算每層num%2的總和


<details> <summary>code</summary>
<pre><code>
func hammingWeight(num uint32) int {
    var result int
    
    for num != 0 {
        result += int(num % 2)
        num = num / 2
    }

    return result
}
</code></pre>
</details>