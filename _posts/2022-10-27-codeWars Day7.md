---
title: codeWars Day7
date: 2022-10-27 00:00:00 +0800
categories: [codeWars]
tags: [Tang]     # TAG names should always be lowercase
---

# How Much?

題目:

    我有n至m元, 買了9輛c元的車,剩下1元, 買了7艘b元的船,剩下2元, 求所有可能的組合



解法:

    迴圈跑n~m的金額, 找出同時符合汽車和船的金額


<details> <summary>code</summary>
<pre><code>
package kata

import "fmt"

func HowMuch(m int, n int) [][3]string {
  var result [][3]string
  if m > n {
    m, n = n, m
  }
  
  for i := m; i <= n; i++ {
    if i % 9 == 1 && i % 7 == 2 {
      result = append(result, [3]string{
        fmt.Sprintf("M: %d", i),
        fmt.Sprintf("B: %d", i / 7),
        fmt.Sprintf("C: %d", i / 9)})
    }
  }
  
  return result
}

</code></pre>
</details>

# Persistent Bugger.

題目:

    一個正整數num,將他每位數字相乘,值到算出的數字變成個位數,求計算了幾次


解法: 

    先判斷num是否大於10,如果大於10,去計算每位數字相乘


<details> <summary>code</summary>
<pre><code>
package kata

import "strconv"

func Persistence(n int) int {
	var count int
  
  for n > 9 {
    n, count = Multiply(n, count)
  }
  
  return count
}

func Multiply(n int, c int) (int, int) {
  sum := 1
  s := strconv.Itoa(n)
  for i := range s {
    num, _ := strconv.Atoi(s[i:i+1])
    sum *= num
  }
  c++
  return sum, c
}
</code></pre>
</details>