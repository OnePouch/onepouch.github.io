---
title: leetCode Day48
date: 2022-12-23 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Pacific Atlantic Water Flow

題目:

    有一個數字矩陣代表了水的高度,上方和左方為太平洋,右方和下方為大西洋,水會往低處流,求哪幾個節點同時流往太平洋和大西洋



解法:

    如果使用每個節點往四周跑dfs的話,有很多點需要重複執行,導致timeout,所以定義兩個布林矩陣,為能到達太平洋或大西洋,從邊界開始往四周跑,最後看每個點是否通過太平洋和大西洋


<details> <summary>code</summary>
<pre><code>
func pacificAtlantic(heights [][]int) [][]int {
    var result [][]int
    var p [][]bool
    var a [][]bool
    m := len(heights)
    n := len(heights[0])

    for i := 0; i < m; i++ {
        p = append(p, make([]bool, n))
        a = append(a, make([]bool, n))
    }

    for i := 0; i < n; i++ {
        dfs(heights, 0, i, 0, &p)
        dfs(heights, m - 1, i, 0, &a)
    }

    for i := 0; i < m; i++ {
        dfs(heights, i, 0, 0, &p)
        dfs(heights, i, n - 1, 0, &a)
    }

    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            if p[i][j] && a[i][j] {
                result = append(result, []int{i, j})
            }
        }
    }

    return result
}

func dfs(heights [][]int, x int, y int, val int, pass *[][]bool) {
    if x < 0 || y < 0 || x >= len(heights) || y >= len(heights[0]) {
        return
    }

    if (*pass)[x][y] || heights[x][y] < val {
        return
    }

    (*pass)[x][y] = true
    dfs(heights, x + 1, y, heights[x][y], pass)
    dfs(heights, x, y + 1, heights[x][y], pass)
    dfs(heights, x - 1, y, heights[x][y], pass)
    dfs(heights, x, y - 1, heights[x][y], pass)
}
</code></pre>
</details>