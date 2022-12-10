---
title: leetCode Day39
date: 2022-12-10 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Container With Most Water

題目:

    有一組數字陣列,值代表高度,index差距代表寬度,求能載入最大水量的面積是多少



解法:

    預設頭尾為最大的面積,頭為i尾為j,如果i的高度大於j的高度,j--,反之i++,即可求得最大面積


<details> <summary>code</summary>
<pre><code>
func maxArea(height []int) int {
    var result int
    i, j := 0, len(height) - 1

    for i < j {
        result = max(result, min(height[i], height[j]) * (j - i))
        if height[i] > height[j] {
            j--
        } else {
            i++
        }
    }

    return result
}

func min(a int, b int) int {
    if a > b {
        return b
    }
    return a
}

func max(a int, b int) int {
    if a > b {
        return a
    }
    return b
}
</code></pre>
</details>