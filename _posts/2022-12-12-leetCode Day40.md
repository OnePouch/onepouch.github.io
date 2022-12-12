---
title: leetCode Day40
date: 2022-12-12 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Letter Combinations of a Phone Number

題目:

  給一串數字,求電話上面的字母的組合  



解法:

    先將數字代表的字串陣列定義出來,然後將每個數字帶入找出所有字串的組合


<details> <summary>code</summary>
<pre><code>
var M = map[byte]string {
    '2': "abc",
    '3': "def",
    '4': "ghi",
    '5': "jkl",
    '6': "mno",
    '7': "pqrs",
    '8': "tuv",
    '9': "wxyz",
}

func letterCombinations(digits string) []string {
    var result []string

    if len(digits) == 0 {
        return result
    }
    helper(digits, 0, "", &result)

    return result
}

func helper(digits string, x int, s string, result *[]string) {
    if x == len(digits) {
        *result = append(*result, s)
        return
    }

    for _, value := range M[digits[x]] {
        helper(digits, x + 1, s + string(value), result)
    }
    return
}
</code></pre>
</details>


# Word Search

題目:

    有一個字串矩陣,每個值代表一個字母,有一個字串,如果矩陣內相鄰的字母能組合出字串,返回true,另外矩陣內每個值只能使用一次



解法:

    先定義一個矩陣,存放是否使用過,然後找出矩陣內字母和字串相同文字,再找相鄰的四個字母是否為字串的下一個字母,另外需判斷矩陣的字母是否之前有被使用過


<details> <summary>code</summary>
<pre><code>
func exist(board [][]byte, word string) bool {
    var visited [][]bool
    var tmp []bool
    m := len(board)
    n := len(board[0])

    for i := 0; i < n; i++ {
        tmp = append(tmp, false)
    }

    for i := 0; i < m; i++ {
        copyTmp := make([]bool, len(tmp))
        copy(copyTmp, tmp)
        visited = append(visited, copyTmp)
    }

    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            if dfs(board, word, 0, i, j, m, n, visited) {
                return true
            }
        }
    }

    return false
}

func dfs(board [][]byte, word string, cur int, x int, y int, m int, n int, visited [][]bool) bool {
    if len(word) == cur {
        return true
    }
    if x < 0 || y < 0 || x >= m || y == n || board[x][y] != word[cur] || visited[x][y] {
        return false
    }
    visited[x][y] = true
    if dfs(board, word, cur + 1, x - 1, y, m, n, visited) || dfs(board, word, cur + 1, x + 1, y, m, n, visited) || dfs(board, word, cur + 1, x, y - 1, m, n, visited) || dfs(board, word, cur + 1, x, y + 1, m, n, visited) {
        return true
    }
    visited[x][y] = false
    return false        
}
</code></pre>
</details>