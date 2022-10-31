---
title: codeWars Day8
date: 2022-10-28 00:00:00 +0800
categories: [codeWars]
tags: [Tang]     # TAG names should always be lowercase
---

# Tortoise racing

題目:

    A會先跑G的距離,A的時速v1,B的時速v2,如果v1>v2, 表示追不到,回傳-1, 求B會在幾個小時幾分鐘幾分追到A



解法:

    先算出A,B的速度差diff,在算差距/diff為小時,差距 * 60/diff % 60為分鐘,差距 * 3600/diff % 60為秒


<details> <summary>code</summary>
<pre><code>
package kata

func Race(v1, v2, g int) [3]int {  
  if (v1 > v2) {
    return [3]int{-1, -1, -1}
  }
  
  diff := v2 - v1
  
  return [3]int{
    g / diff,
    g * 60 / diff % 60 ,
    g * 3600 / diff % 60 ,
  }
}
</code></pre>
</details>