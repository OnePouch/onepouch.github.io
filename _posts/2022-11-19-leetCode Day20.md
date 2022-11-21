---
title: leetCode Day20
date: 2022-11-19 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Insert Interval

題目:

    有一個二維陣列,每個陣列中第一個數代表開始,第二個數代表結束,陣列是順序的,先在需要插入一個陣列,讓此二維陣列一樣維持順序排列



解法:

    把陣列分成三段,陣列中結束的數字比插入陣列開始還小,和陣列中開始比插入陣列結束還大,都直接丟入陣列,如果陣列結束大於等於插入開始和陣列開始小於等於插入結束時,開始為兩陣列中開始的最小值,結束為兩陣列中結束的最大值,再將插入的陣列丟入陣列中


<details> <summary>code</summary>
<pre><code>
func insert(intervals [][]int, newInterval []int) [][]int {
    var result [][]int
    
    i := 0

    for i < len(intervals) && intervals[i][1] < newInterval[0] {
        result = append(result, intervals[i])
        i++
    }
    
    for i < len(intervals) && intervals[i][1] >= newInterval[0] && intervals[i][0] <=  newInterval[1] {
        if intervals[i][0] < newInterval[0] {
            newInterval[0] = intervals[i][0]
        }
        
        if intervals[i][1] > newInterval[1] {
            newInterval[1] = intervals[i][1]
        }
        i++
    }
    result = append(result, newInterval)
    
    for i < len(intervals) && intervals[i][0] > newInterval[1] {
        result = append(result, intervals[i])
        i++
    }
    
    return result
}
</code></pre>
</details>
