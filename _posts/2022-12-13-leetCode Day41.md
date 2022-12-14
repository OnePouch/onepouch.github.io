---
title: leetCode Day41
date: 2022-12-13 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Find All Anagrams in a String

題目:

    有兩個字串,s和p,找出s字串中和p字串相似的子字串,並返回子字串開始的idx陣列



解法:

    先找出p字串中字母的出現次數為P,再將s陣列從頭掃過一次,P將字母--,如果該字母為0的話將,idx刪除,如果i大於等於p的長度,需把前面的字母加回來,如果P長度為0的話,表示為相似字串,將idx-p長度+1存入結果中


<details> <summary>code</summary>
<pre><code>
func findAnagrams(s string, p string) []int {
    var result []int
    P := make(map[byte]int)

    if len(p) > len(s) {
        return result
    }

    for i := 0; i < len(p); i++ {
        P[p[i]]++
    }

    for i := 0; i < len(s); i++ {
        P[s[i]]--
        if P[s[i]] == 0 {
            delete(P, s[i])
        }
        if i >= len(p) {
            P[s[i - len(p)]]++
            if P[s[i - len(p)]] == 0 {
                delete(P, s[i - len(p)])
            }
        }
        if len(P) == 0 {
            result = append(result, i - len(p) + 1)
        }
    }

    return result
}
</code></pre>
</details>