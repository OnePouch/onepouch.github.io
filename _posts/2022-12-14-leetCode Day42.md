---
title: leetCode Day42
date: 2022-12-14 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Minimum Height Trees

題目:

    n為0~n-1的數字,edges為兩個數字的相連關西,此關西能組成一個樹,求哪個數字為根的話有最小的深度



解法:

    因圖型一定為樹,所以找出此樹最外層的點,最外層的點為只有一個相鄰的數字,將最外層的點剝離後,判斷剩下的數字是否只剩下一個或兩個,如果是的話,返回答案,如果不是的話,將繼續把最外層的數字剝離


<details> <summary>code</summary>
<pre><code>
func findMinHeightTrees(n int, edges [][]int) []int {
    if n == 1 {
        return []int{0}
    }
    var next [][]int
    var queue []int
    dagree := make([]int, n)
    for i := 0; i < n; i++ {
        next = append(next, make([]int, 0))
    }
    
    for _, edge := range edges {
        a := edge[0]
        b := edge[1]
        dagree[a]++
        dagree[b]++
        next[a] = append(next[a], b)
        next[b] = append(next[b], a)
    }

    for key, value := range dagree {
        if value == 1 {
            queue = append(queue, key)
        }
    }

    for n > 2 {
        size := len(queue)
        n -= size
        for size > 0 {
            cur := queue[0]
            queue = queue[1:]
            for _, value := range next[cur] {
                dagree[value]--
                if dagree[value] == 1 {
                    queue = append(queue, value)
                }
            }
            size--
        }
    }

    return queue
}
</code></pre>
</details>


# Task Scheduler

題目:

    有一個字母陣列,每個字母代表一個任務,相同的字母代表相同的任務,相同任務執行之間需要n個間隔,每個時間只能執行一個任務或是暫停,求最短完成任務需要幾個時間



解法:

    將每個字母出現次數找出來,把出現頻率由高往低存入queue中,如果queue中有資料持續執行,使用優先隊列,將n的數從queue中取出,並減1,如果大於1,再塞回queue中


<details> <summary>code</summary>
<pre><code>
func leastInterval(tasks []byte, n int) int {
    if n == 0 {
        return len(tasks)
    }

    var result int
    n++
    count := make(map[byte]int, len(tasks))
    for _, value := range tasks {
        count[value]++
    }

    var pq []int
    for _, value := range count {
        pq = append(pq, value)
    }
    sort.Slice(pq, func(i, j int) bool {
        return pq[i] > pq[j]
    })

    for len(pq) > 0 {
        k := min(len(pq), n)
        tmp := make([]int, 0)
        for i:=0; i < k; i++ {
            cur := pq[0]
            pq = pq[1:]
            cur--
            if cur > 0 {
                tmp = append(tmp, cur)
            }
        }
        for _, value := range tmp {
            pq = append(pq, value)
        }
        sort.Slice(pq, func(i, j int) bool {
            return pq[i] > pq[j]
        })
        if len(tmp) == 0 {
            result += k
        } else {
            result += n
        }
    }

    return result
}

func min (a, b int) int {
    if a > b {
        return b
    }
    return a
}
</code></pre>
</details>