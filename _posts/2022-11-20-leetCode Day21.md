---
title: leetCode Day21
date: 2022-11-21 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# 01 Matrix

題目:

    有一個由0,1組成的矩陣,算出各點到0的最短距離,兩個點之間的距離為1



解法:

    找出原矩陣值為0的點,將該點存入p矩陣中,並設定矩陣res,如果原矩陣點的值不為0,設定為最大值,為0的話設定為0,之後,如果p矩陣不為空的話,將p矩陣的點取出,跑相鄰的四的點,如果點的值為最大值,表示該點之前尚未走到過,該點為現在點的值+1,直到矩陣p跑完為空


<details> <summary>code</summary>
<pre><code>
func updateMatrix(mat [][]int) [][]int {
    dis := [][]int{{1, 0}, {0, 1}, {-1, 0}, {0, -1}}
    var result [][]int
    var q [][]int
    x, y := len(mat), len(mat[0])
    
    for i := 0; i < x ; i++ {
        result = append(result, make([]int, y))
        for j := 0; j < y; j++ {
            if mat[i][j] == 0 {
                q = append(q, []int{i, j})
                result[i][j] = 0
            } else {
                result[i][j] = x + y
            }
        }
    }
    
    for len(q) > 0 {
        p := q[0]
        q = q[1:]
        for _, value := range dis {
            m := p[0] + value[0]
            n := p[1] + value[1]
            if m >= 0 && m < x && n >= 0 && n < y && result[m][n] == x + y {
                result[m][n] = result[p[0]][p[1]] + 1
                q = append(q, []int{m, n})
            }
        }
    }
    
    return result
}
</code></pre>
</details>


# K Closest Points to Origin

題目:

    一個矩陣有多個點,找出距離原點最短的K個點



解法:

    使用快速收尋


<details> <summary>code</summary>
<pre><code>
func kClosest(points [][]int, k int) [][]int {
    sort.Slice(points, func(i, j int) bool {
        return points[i][0] * points[i][0] + points[i][1] * points[i][1] <
        points[j][0] * points[j][0] + points[j][1] * points[j][1]
    })
    
    return points[:k]
}
</code></pre>
</details>