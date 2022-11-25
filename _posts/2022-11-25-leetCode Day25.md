---
title: leetCode Day25
date: 2022-11-25 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Implement Trie (Prefix Tree)

題目:

    前綴樹,根節點不包含字符,每一個節點都只有一個字符



解法:

    定義樹結構,有children有26個字母的樹結構和是否為結束的狀態,Insert時就跑字串,如果不存在於樹結構中,就建立樹結構,最後的樹結構的狀態為true,Search時就跑字串,如果字串不存在於樹結構中就返回false,如果字串跑完,就返回該樹結構的狀態,StartsWith時就跑字串,如果字串不存在於陣列中返回false,如果都存在返回true


<details> <summary>code</summary>
<pre><code>
type Trie struct {
    children [26]*Trie
    isEnd bool
}


func Constructor() Trie {
    return Trie{}
}


func (this *Trie) Insert(word string)  {
    curr := this
    for _, value := range word {
        idx := value - 'a'
        if curr.children[idx] == nil {
            curr.children[idx] = &Trie{}
        }
        curr = curr.children[idx]
    }
    curr.isEnd = true
}


func (this *Trie) Search(word string) bool {
    curr := this
    for _, value := range word {
        idx := value - 'a'
        if curr.children[idx] == nil {
            return false
        }
        curr = curr.children[idx]
    }

    return curr.isEnd
}


func (this *Trie) StartsWith(prefix string) bool {
    curr := this
    for _, value := range prefix {
        idx := value - 'a'
        if curr.children[idx] == nil {
            return false
        }
        curr = curr.children[idx]
    }

    return true
}


/**
 * Your Trie object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Insert(word);
 * param_2 := obj.Search(word);
 * param_3 := obj.StartsWith(prefix);
 */
</code></pre>
</details>


# Coin Change

題目:

    有一個數字陣列代表了不同幣值的硬幣,需要找出符合金額的最少硬幣數量



解法:

    使用DP,預設1至amount的值都為amount+1,取出coins陣列,將每個值都會為該點和(該點-coin)的值+1的最小值,最後DP[amount]就為最小的硬幣數量


<details> <summary>code</summary>
<pre><code>
func coinChange(coins []int, amount int) int {
    dp := make([]int, amount + 1)
        
    for i := 1; i <= amount; i++ {
        dp[i] = amount + 1
    }
    
    for _, coin := range coins {
        for i := coin; i <= amount; i++ {
            dp[i] = min(dp[i], dp[i - coin] + 1)
        }
    }
    
    if dp[amount] == amount + 1 {
        return -1
    }
    
    return dp[amount]
}

func min (a int, b int) int {
    if a > b {
        return b
    }
    return a
}
</code></pre>
</details>