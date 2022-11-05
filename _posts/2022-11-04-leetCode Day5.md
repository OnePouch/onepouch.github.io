---
title: leetCode Day5
date: 2022-11-04 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Flood Fill

題目:

    給一個二維陣列,每個欄位都有顏色,給一個座標需染成目標色,如果鄰近的座標顏色都相同的話,會一起被染成目標色



解法:

    


<details> <summary>code</summary>
<pre><code>
func floodFill(image [][]int, sr int, sc int, color int) [][]int {
    if image[sr][sc] == color {
        return image
    }
    var offset = [][]int{{0, 1}, {0, -1}, {1, 0}, {-1, 0}}

    oldColor := image[sr][sc]
    m := len(image)
    n := len(image[0])
    
    image[sr][sc] = color
    for _, value := range offset {
        x := sr + value[0]
        y := sc + value[1]
        if x >= 0 && x < m && y >= 0 && y < n && image[x][y] == oldColor {
            floodFill(image, x, y, color)
        }
    }
    
    return image
}
</code></pre>
</details>