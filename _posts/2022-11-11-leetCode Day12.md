---
title: leetCode Day12
date: 2022-11-11 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Backspace String Compare

題目:

    給兩個字串,如果兩個陣列相等回傳true,'#'為消除前一個字串



解法:

    


<details> <summary>code</summary>
<pre><code>
func backspaceCompare(s string, t string) bool {
    x := len(s) - 1
    y := len(t) - 1
    
    count := 0
    for true {
        for x >= 0 && (s[x] == 35 || count > 0) {
            if s[x] != 35 {
                count--
            } else {
                count++
            }
            x--
        }
        count = 0
        for y >=0 && (t[y] == 35 || count > 0) {
            if t[y] != 35 {
                count--
            } else {
                count++
            }
            y--
        }
        
        if x >= 0 && y >= 0 && s[x] == t[y] {
            x--
            y--
        } else {
            break
        }
    }

    return x == -1 && y == -1
}
</code></pre>
</details>