---
title: leetCode Day46
date: 2022-12-19 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Next Permutation

題目:

    有一個數字陣列,找出下一個比較大的最小數,如果都沒有的話,返回最小數



解法:

    從後往前看,如果為順序遞增的話,返回排序陣列,如果中間有一數較小,找出該數位置,再由後往前找出最小大於該數的位置,由於後往前一定為遞增,所以從後往前遇到的第一個比較大的數一定是最小的,兩個位置交換,在將i後面的數字排序


<details> <summary>code</summary>
<pre><code>
func nextPermutation(nums []int)  {
    i := len(nums) - 1
    for i >= 1 && nums[i] <= nums[i - 1] {
        i--
    }
    if i == 0 {
        sort.Ints(nums)
        return
    }
    i--
    j := len(nums) - 1
    for j > i && nums[i] >= nums[j] {
        j--
    }
    nums[i], nums[j] = nums[j], nums[i]
    sort.Ints(nums[i + 1:])

    return
}
</code></pre>
</details>


# Valid Sudoku

題目:

    9*9數獨,判斷行列不能重複,3*3小數獨也不能重複,返回true,有重複返回false



解法:

    如果行列和小數獨都沒有重複,此數獨一定成立


<details> <summary>code</summary>
<pre><code>
func isValidSudoku(board [][]byte) bool {
    for i := 0; i < 9; i++ {
        rowCheck, colCheck, boxCheck := make([]bool, 9), make([]bool, 9), make([]bool, 9)
        for j := 0; j < 9; j++ {
            if board[i][j] != '.' {
                idx := board[i][j] - '1'

                if rowCheck[idx] {
                    return false
                }

                rowCheck[idx] = true
            }

            if board[j][i] != '.' {
                idx := board[j][i] - '1'

                if colCheck[idx] {
                    return false
                }

                colCheck[idx] = true
            }

            x, y := i / 3 * 3 + j / 3, i % 3 * 3 + j % 3
            if board[x][y] != '.' {
                idx := board[x][y] - '1'

                if boxCheck[idx] {
                    return false
                }

                boxCheck[idx] = true
            }
        }
    }

    return true
}
</code></pre>
</details>


# Group Anagrams

題目:

    有一個字串陣列,把相似的字串組在一起,返回字串矩陣



解法:

    將字串排序當作矩陣的key,把key相同的字串組合在同一個key中


<details> <summary>code</summary>
<pre><code>
func groupAnagrams(strs []string) [][]string {
    var result [][]string
    solution := make(map[string][]string)

    for _, str := range strs {
        tmp := []byte(str)
        sort.Slice(tmp, func(i, j int) bool {
            return tmp[i] > tmp[j]
        })
        key := string(tmp)
        solution[key] = append(solution[key], str)
    }

    for _, value := range solution {
        result = append(result, value)
    }

    return result
}
</code></pre>
</details>