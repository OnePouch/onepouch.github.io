---
title: leetCode Day44
date: 2022-12-16 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Daily Temperatures

題目:

    有一個數字陣列,代表了每天的溫度,返回隔k天之後氣溫比較高該天高的陣列,如果沒有比較高的溫度,天數為0



解法:

    用stack把之前的idx存起來,在跟現在的比大小,就可以找出k天


<details> <summary>code</summary>
<pre><code>
func dailyTemperatures(temperatures []int) []int {
    ans := make([]int, len(temperatures))
    stack := make([]int, len(temperatures))
    top := -1

    for i := 0; i < len(temperatures); i++ {
        for top > -1 && temperatures[i] > temperatures[stack[top]] {
            idx := stack[top]
            ans[idx] = i - idx
            top--
        }
        top++
        stack[top] = i
    }

    return ans
}
</code></pre>
</details>