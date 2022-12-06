---
title: leetCode Day35
date: 2022-12-06 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# String to Integer (atoi)

題目:

    將字串轉換成數字



解法:

    先判斷字串長度為0的話返回0,然後將前面的空白去除,在判斷當前是否為正或負,接下來進入數字判斷,如果數字比最大值除以10還大或是數字等於最大值並且當前數字大於7的話,返回最大值或最小值,如果沒有返回數字


<details> <summary>code</summary>
<pre><code>
func myAtoi(s string) int {
    idx := 0
    sign := 1
    total := 0

    if len(s) == 0 {
        return 0
    }

    for len(s) > idx && s[idx] == ' ' {
        idx++
    }

    if len(s) > idx && (s[idx] == '-' || s[idx] == '+') {
        if s[idx] == '-' {
            sign = -1
        }
        idx++
    }

    for len(s) > idx {
        digit := s[idx] - '0'
        if digit < 0 || digit > 9 {
            break
        }

        if math.MaxInt32 / 10 < total || math.MaxInt32 / 10 == total && math.MaxInt32 % 10 < digit {
            if sign == 1 {
                return math.MaxInt32
            }
            return math.MinInt32
        }

        total = 10 * total + int(digit)
        idx++
    }

    return sign * total
}
</code></pre>
</details>

