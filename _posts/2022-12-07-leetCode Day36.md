---
title: leetCode Day36
date: 2022-12-07 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Spiral Matrix

題目:

    給一個數字矩陣,以螺旋的方式返回矩陣內所有元素



解法:

    先找出x和y的初始點和終點,再寫四個方法分別為由左至右,由上至下,由右至左,由下至上,迴圈直到矩陣內沒有數字,則返回結果


<details> <summary>code</summary>
<pre><code>
func spiralOrder(matrix [][]int) []int {
    var result []int
    y := len(matrix) - 1
    x := len(matrix[0]) - 1

    return oneOrder(matrix, 0, 0, x, y, result)
}

func oneOrder(matrix [][]int, i int, j int, x int, y int, result []int) []int {
    if i > x {
        return result
    }

    for k := i; k <= x; k++ {
        result = append(result, matrix[j][k])
    }

    return twoOrder(matrix, i, j + 1, x, y, result)
}

func twoOrder(matrix [][]int, i int, j int, x int, y int, result []int) []int {
    if j > y {
        return result
    }

    for k := j; k <= y; k++ {
        result = append(result, matrix[k][x])
    }

    return threeOrder(matrix, i, j, x - 1, y, result)
}

func threeOrder(matrix [][]int, i int, j int, x int, y int, result []int) []int {
    if i > x {
        return result
    }

    for k := x; k >= i; k-- {
        result = append(result, matrix[y][k])
    }

    return fourOrder(matrix, i, j, x, y - 1, result)
}

func fourOrder(matrix [][]int, i int, j int, x int, y int, result []int) []int {
    if j > y {
        return result
    }

    for k := y; k >= j; k-- {
        result = append(result, matrix[k][i])
    }

    return oneOrder(matrix, i + 1, j, x, y, result)
}
</code></pre>
</details>

