---
title: leetCode Day24
date: 2022-11-24 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Evaluate Reverse Polish Notation

題目:

    計算反向波蘭表示法中算數表達式的值。



解法:

    使用queue將數字存入queue中,然後遇到運算符號時,將queue中最後兩個數字取出,並算出結果,再丟回queue中,最後queue[0]為答案


<details> <summary>code</summary>
<pre><code>
func evalRPN(tokens []string) int {
    var result int
    var queue []int
    
    for _, value := range tokens {
        switch value {
            case "+":
                length := len(queue)
                result = queue[length - 2] + queue[length - 1]
                queue = queue[:len(queue)-2]
                queue = append(queue, result)
            case "-":
                length := len(queue)
                result = queue[length - 2] - queue[length - 1]
                queue = queue[:len(queue)-2]
                queue = append(queue, result)
            case "*":
                length := len(queue)
                result = queue[length - 2] * queue[length - 1]
                queue = queue[:len(queue)-2]
                queue = append(queue, result)
            case "/":
                length := len(queue)
                result = queue[length - 2] / queue[length - 1]
                queue = queue[:len(queue)-2]
                queue = append(queue, result)
            default:
                num, _ := strconv.Atoi(value)
                queue = append(queue, num)
        }
    }
    
    return queue[0]
}
</code></pre>
</details>


# Course Schedule

題目:

    有總共numCourses個課程,有一個陣列,裡面給你一個先決條件,其中prerequisites[i] = [ai, bi]表示如果你想修ai這門課,並須先修課程bi,判斷課程是否能被修完



解法:

    將矩陣轉換成圖形,如果圖形為一個環的話,代表課程沒有辦法修完,如果圖形有終點代表,課程能被修完


<details> <summary>code</summary>
<pre><code>
func canFinish(numCourses int, prerequisites [][]int) bool {
    visited := make([]int, numCourses)
    next := make([][]int, numCourses)
    
    for _, value := range prerequisites {
        next[value[0]] = append(next[value[0]], value[1])
    }
    
    for key := range next {
        if dfs(key, visited, next) == false {
            return false
        }
    }
    
    return true
}

func dfs(key int, visited []int, next [][]int) bool {
    if visited[key] == 1 {
        return true
    }
    if visited[key] == 2 {
        return false
    }
    visited[key] = 2
    for _, value := range next[key] {
        if dfs(value, visited, next) == false {
            return false
        }
    }
    visited[key] = 1

    return true
}
</code></pre>
</details>