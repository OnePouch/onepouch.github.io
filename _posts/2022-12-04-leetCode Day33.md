---
title: leetCode Day33
date: 2022-12-04 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Accounts Merge

題目:

    有一個字串矩陣,第一個字串為姓名,後面為信箱,如果遇到姓名與信箱有一樣代表為同一個人,需把信箱合併,信箱需排序



解法:

    設定一個信箱的陣列,裡面存的是信箱屬於哪個帳號,如果信箱之前就存在過的話,把之前擁有者的所屬換為現在的所屬,之後我們將屬於同一個帳號的連結起來,最後組成題目要的格式並將信做作排序


<details> <summary>code</summary>
<pre><code>
func accountsMerge(accounts [][]string) [][]string {
    emailMap := make(map[string]int)
    
    indexConnections := make([]int, len(accounts))
    for i := range indexConnections {
        indexConnections[i] = i
    }
    
    for accountIdx, emails := range accounts {
        for i := 1; i < len(emails); i++ {
            if existIdx, exist := emailMap[emails[i]]; exist {
                for {
                    if indexConnections[existIdx] == existIdx {
                        indexConnections[existIdx] = accountIdx
                        break
                    }
                    existIdx = indexConnections[existIdx]
                }
            } else {
                emailMap[emails[i]] = accountIdx
            }
        }
    }
    
    for i := len(indexConnections)-1; i >= 0; i-- {
		indexConnections[i] = indexConnections[indexConnections[i]]
	}
    
    magic := make(map[int][]string)
	for email, index := range emailMap {
		if _, exist := magic[indexConnections[index]]; !exist {
			magic[indexConnections[index]] = []string{accounts[index][0]}
		}
		magic[indexConnections[index]] = append(magic[indexConnections[index]], email)
	}
    
    retSlice := make([][]string, 0, len(magic))
	for _, v := range magic {
		sort.Strings(v[1:])
		retSlice = append(retSlice, v)
	}
	return retSlice
}
</code></pre>
</details>


# Sort Colors

題目:

    有一個數字陣列,裡面只有0,1,2,0代表紅色,1代表白色,2代表藍色,求紅白藍排序



解法:

    定義左跟右還有正在執行的i三個變數,左和i為0,右為陣列長度-1,如果陣列i為0的話,需要跟左邊互換,左和i都+1,如果陣列i為2的話,需要和右邊互換,右邊-1,如果陣列i為1,i+1


<details> <summary>code</summary>
<pre><code>
func sortColors(nums []int)  {
    left := 0
    right := len(nums) - 1
    i := 0
    
    for i <= right {
        if nums[i] == 0 {
            nums[left], nums[i] = nums[i], nums[left]
            left++
            i++
        } else if nums[i] == 2 {
            nums[i], nums[right] = nums[right], nums[i]
            right--
        } else {
            i++
        }
    }
}
</code></pre>
</details>

# Word Break

題目:

    有一個字串,和一個字串陣列,如果字串能被字串陣列所組成,回傳true,不能回傳false,字串陣列中的字串沒有使用次數



解法:

    使用動態規劃,如果字串在字典裡面有的話,就設定為true,最後看字串是否為true


<details> <summary>code</summary>
<pre><code>
func wordBreak(s string, wordDict []string) bool {
    dp := make([]bool, len(s) + 1)
    dp[0] = true
    dict := make(map[string]int)
    
    for _, value := range wordDict {
        dict[value] = 1
    }
    
    for i := 1; i <= len(s); i++ {
        for j := 0; j < i; j++ {
            if dp[j] {
                substr := s[j:i]
                if _, ok := dict[substr]; ok {
                    dp[i] = true;
                    break
                }
            }
        }
    }
    
    return true
}
</code></pre>
</details>