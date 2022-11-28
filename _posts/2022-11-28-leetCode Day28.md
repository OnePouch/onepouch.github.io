---
title: leetCode Day28
date: 2022-11-28 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Rotting Oranges

題目:

    有一個矩陣,2代表壞掉的橘子,1代表新鮮的橘子,0代表沒有橘子,過一天,壞掉的橘子會朝相鄰的新鮮橘子讓他壞掉,求最短多久會只剩下壞橘子,如果還有新鮮的橘子回傳-1



解法:

    先把一開始壞掉的橘子找出來,再找出壞掉橘子旁邊是否為新鮮的橘子,如果為新鮮的橘子,將橘子設定為壞掉的,然後將座標存入queue中,最為下一層的壞橘子,值到queue為空


<details> <summary>code</summary>
<pre><code>
func orangesRotting(grid [][]int) int {
    var result int
    var queue [][]int
    var fresh int
    
    m := len(grid)
    n := len(grid[0])
    
    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            if grid[i][j] == 2 {
                queue = append(queue, []int{i, j})
            }
            
            if grid[i][j] == 1 {
                fresh++
            }
        }
    }
    
    for len(queue) > 0 && fresh > 0 {
        result++
        size := len(queue)
        
        for i :=0; i < size; i++ {
            cur := queue[i]
            if bfs(grid, cur[0] + 1, cur[1], m, n) {
                fresh--
                grid[cur[0] + 1][cur[1]] = 2
                queue = append(queue, []int{cur[0] + 1, cur[1]})
            }
            if bfs(grid, cur[0] - 1, cur[1], m, n) {
                fresh--
                grid[cur[0] - 1][cur[1]] = 2
                queue = append(queue, []int{cur[0] - 1, cur[1]})
            }
            if bfs(grid, cur[0], cur[1] + 1, m, n) {
                fresh--
                grid[cur[0]][cur[1] + 1] = 2
                queue = append(queue, []int{cur[0], cur[1] + 1})
            }
            if bfs(grid, cur[0], cur[1] - 1, m, n) {
                fresh--
                grid[cur[0]][cur[1] - 1] = 2
                queue = append(queue, []int{cur[0], cur[1] - 1})
            }
        }
        queue = queue[size:]
    }
    
    if fresh > 0 {
        return -1
    }
    
    return result;
}

func bfs(grid [][]int, x int, y int, m int, n int) bool {
    if x >= 0 && x < m && y >= 0 && y < n && grid[x][y] == 1 {
        return true
    }
    return false
}
</code></pre>
</details>