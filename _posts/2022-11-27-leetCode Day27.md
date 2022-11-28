---
title: leetCode Day27
date: 2022-11-27 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Validate Binary Search Tree

題目:

    驗證是否為二分搜尋樹



解法:

    設定最大值為無限大,最小值為負無限大,每個節點的值會在最大和最小值中間,左節點時最大值要換成父節點的值,右節點時最小時要換成父節點的值,都有符合的話就為二分搜尋樹


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
func isValidBST(root *TreeNode) bool {
    max := math.MaxInt64
    min := math.MinInt64
    
    return check(root.Left, root.Val, min) && check(root.Right, max, root.Val)
}

func check(root *TreeNode, max int, min int) bool {
    if root == nil {
        return true
    }
    
    if root.Val < max && root.Val > min {
        return check(root.Left, root.Val, min) && check(root.Right, max, root.Val)
    } else {
        return false
    }
    
    return true
}
</code></pre>
</details>


# Number of Islands

題目:

    有一個矩陣是由1,0組成,1代表陸地,0代表海洋,求有幾座島嶼,1相鄰為同一座島嶼



解法:

    使用深度搜尋法,將跑過的陸地設為0,當跑到新的陸地時,結果+1


<details> <summary>code</summary>
<pre><code>
func numIslands(grid [][]byte) int {
    var result int
    m := len(grid)
    n := len(grid[0])
    
    for x := 0; x < m; x++ {
        for y := 0; y < n; y++ {
            if grid[x][y] == '1' {
                result += 1
                dfs(&grid, x, y, m, n)
            }
        }
    }
    
    return result
}

func dfs(grid *[][]byte, x int, y int, m int, n int) {
    if x < 0 || x >= m || y < 0 || y >= n || (*grid)[x][y] == '0' {
        return
    }
    (*grid)[x][y] = '0'
    dfs(grid, x + 1, y, m, n)
    dfs(grid, x - 1, y, m, n)
    dfs(grid, x, y + 1, m, n)
    dfs(grid, x, y - 1, m, n)
}
</code></pre>
</details>