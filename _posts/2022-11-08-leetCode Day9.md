---
title: leetCode Day9
date: 2022-11-08 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Add Binary

題目:

    給兩個由0和1組成的字串,求這兩字串二進制相加為多少



解法:

    兩字串算出長度,長度-1就會為個位數,兩字串個位數相加為總和,總和%2為字串結果,總和/2代表進位,持續執行,直到跑完兩字串


<details> <summary>code</summary>
<pre><code>
func addBinary(a string, b string) string {
    var result string
    var carry int
    var sum int
    x := len(a) - 1
    y := len(b) - 1
    
    for x >= 0 || y >= 0 {
        sum = carry
        if x >= 0 {
            sum += int(a[x] - '0')
            x--
        }
        if y >= 0 {
            sum += int(b[y] - '0')
            y--
        }
        result = strconv.Itoa(sum % 2) + result
        carry = sum / 2
    }
    
    if carry == 1 {
        result = strconv.Itoa(1) + result
    }
    
    return result
}
</code></pre>
</details>


# Diameter of Binary Tree

題目:

    給一個二分樹,求樹的最大長度,路徑不一定會經過樹根



解法:

    算出個節點左右的深度,距離為左右深度相加,就能找出最大深度


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
func diameterOfBinaryTree(root *TreeNode) int {
    var maxDiameter int
    depth(root, &maxDiameter)
    
    return maxDiameter
}

func depth(root *TreeNode, maxDiameter *int) int {
    if root == nil {
        return 0
    }
    
    left := depth(root.Left, maxDiameter)
    right := depth(root.Right, maxDiameter)
    
    *maxDiameter = max(*maxDiameter, left + right)
    
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


#  

題目:

    



解法:

    


<details> <summary>code</summary>
<pre><code>

</code></pre>
</details>