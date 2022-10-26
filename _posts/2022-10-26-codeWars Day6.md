---
title: codeWars Day6
date: 2022-10-26 00:00:00 +0800
categories: [codeWars]
tags: [Tang]     # TAG names should always be lowercase
---

# Highest Scoring Word

題目:

    有一個字串,每個文字由空白做分別,計算出文字的最大分數,如果分數相同的話,找出比較早出現的那個,分數計算:a = 1, b = 2, c = 3



解法:

    將字串切割,並將每個字母用int - 96換成分數,就能找出最早最大出現的字母


<details> <summary>code</summary>
<pre><code>
package kata

import "strings"

func High(s string) string {
  var maxSocres int
  var socres int
  var result string
  
  for _, value := range strings.Split(s, " ") {
    socres = 0
    for _, value1 := range value {
      socres += int(value1) - 96
    }
    
    if socres > maxSocres {
      maxSocres = socres
      result = value
    }
    
  }
  
  return result
}
</code></pre>
</details>

# Simple Fun #79: Delete a Digit

題目:

    給一個數字,找出刪除一個位數的最大值


解法: 

    千位數和百位數做比較,如果百位數大於千位數,就刪除千位數,以此類推,如果到個位數都還沒刪除,就刪除個位數


<details> <summary>code</summary>
<pre><code>
package kata

import "strconv"

func DeleteDigit(n int) int {
  var result int
  s := strconv.Itoa(n)
  for i := range s {
    if i == len(s) - 1 || s[i] < s[i + 1] {
      result, _ = strconv.Atoi(s[:i] + s[i+1:])
      break
    }
  }

  return result
}
</code></pre>
</details>