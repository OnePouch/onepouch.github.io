---
title: codeWars Day9
date: 2022-10-29 00:00:00 +0800
categories: [codeWars]
tags: [Tang]     # TAG names should always be lowercase
---

# CamelCase Method

題目:

    字串由空白作間隔,把字串第一個字遍大寫,並連起來



解法:

    字串切割,第一個字轉大寫


<details> <summary>code</summary>
<pre><code>
package kata

import "strings"

func CamelCase(s string) string {
  var result string

  for _, value := range strings.Split(s, " ") {
    for key1 := range value {
      value1 := value[key1:key1 + 1]
      if key1 == 0 {
        value1 = strings.ToUpper(value[key1:key1 + 1])
      }
      result += value1
    }
  }
  
  return result
}
</code></pre>
</details>