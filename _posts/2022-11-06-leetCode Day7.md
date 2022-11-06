---
title: leetCode Day7
date: 2022-11-06 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Implement Queue using Stacks

題目:

    使用兩個堆棧實現先進先出的佇列



解法:

    因為是先進先出,所以定義了正反兩個陣列,在push的時候,如果反陣列為空,就把值丟進正陣列,如果反陣列不為空,先將反陣列反向丟回正陣列,在pop的時候,如果正陣列不為空,先將正陣列反向丟到反陣列中,取出反陣列中最後一個數字,在peek的時候,如果反陣列為空,輸出正陣列的第一個數,反陣列不為空,輸出反陣列最後一個數,empty的時候,如果正反兩陣列都不為空,回傳false


<details> <summary>code</summary>
<pre><code>
type MyQueue struct {
    Input []int
    Output []int
}


func Constructor() MyQueue {
    return MyQueue{}
}


func (this *MyQueue) Push(x int)  {
    for len(this.Output) != 0 {
        this.Input = append(this.Input, this.Output[len(this.Output) - 1])
        this.Output = this.Output[:len(this.Output) - 1]
    }
    this.Input = append(this.Input, x)
}


func (this *MyQueue) Pop() int {
    for len(this.Input) != 0 {
        this.Output = append(this.Output, this.Input[len(this.Input) - 1])
        this.Input = this.Input[:len(this.Input) - 1]
    }
    pop := this.Output[len(this.Output) - 1]
    this.Output = this.Output[:len(this.Output) - 1]
    return pop
}


func (this *MyQueue) Peek() int {
    if len(this.Output) == 0 {
        return this.Input[0]
    }
    return this.Output[len(this.Output) - 1]
}


func (this *MyQueue) Empty() bool {
    return len(this.Input) == 0 && len(this.Output) == 0
}


/**
 * Your MyQueue object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Peek();
 * param_4 := obj.Empty();
 */
</code></pre>
</details>


# First Bad Version

題目:

    有一個1,2,3....,n的版本號,提供一個api可以查詢版本的好壞,找出最早出現壞的版本的版本號



解法:

    跑迴圈,如果start<=end,mid = (start + end) / 2,如果mid的版本號為壞的,end = mid - 1,如果版本號為好的,start = end + 1,直到迴圈跑完,就可找到最早出現的壞版本


<details> <summary>code</summary>
<pre><code>
/** 
 * Forward declaration of isBadVersion API.
 * @param   version   your guess about first bad version
 * @return 	 	      true if current version is bad 
 *			          false if current version is good
 * func isBadVersion(version int) bool;
 */

func firstBadVersion(n int) int {
    start, mid, version := 1, 0, 1
    
    for start <= n {
        mid = (start + n) / 2
        if isBadVersion(mid) {
            version = mid
            n = mid - 1
        } else {
            start = mid + 1
        }
    }
    
    return version
}
</code></pre>
</details>


#  Ransom Note

題目:

    給兩個字串, 判斷A陣列是否可以由B陣列組成



解法:

    將兩字串出現字母的次數存入兩陣列中,如果A陣列字母出現的次數比B多的話,返回false


<details> <summary>code</summary>
<pre><code>
func canConstruct(ransomNote string, magazine string) bool {
    aArr, bArr := make(map[string]int), make(map[string]int)
    
    for key := range ransomNote {
        aArr[ransomNote[key:key + 1]]++
    }
    
    for key := range magazine {
        bArr[magazine[key:key + 1]]++
    }
    
    for key, value := range aArr {
        if bArr[key] < value {
            return false
        }
    }
    
    return true
}
</code></pre>
</details>


#  

題目:

    爬梯子一次能爬1或2層,請問到n層總共有幾種方法



解法:

    爬到n層會是n-1層+n-2層,所以定義第0層和第1層為1,跑迴圈算出第n層有幾種方法


<details> <summary>code</summary>
<pre><code>
func climbStairs(n int) int {
    level := 2
    arr := make(map[int]int)
    arr[0] = 1
    arr[1] = 1
    
    for level <= n {
        arr[level] = arr[level - 1] + arr[level - 2]
        level++
    }
    
    return arr[level - 1]
}
</code></pre>
</details>


#  Longest Palindrome

題目:

    給你一串陣列,返回可組成最大回文的字母數量



解法:

    算出出現奇數的數量,如果出現奇數數量 > 0,出現奇數數量 = 出現奇數數量 - 1,回文最大長度為總長度-出現奇數數量


<details> <summary>code</summary>
<pre><code>
func longestPalindrome(s string) int {
    var oddCount int
    arr := make(map[string]int)
    
    for key := range s {
        arr[s[key:key + 1]]++
    }
    
    for _, value := range arr {
        if value % 2 == 1 {
            oddCount++
        }
    }
    
    if (oddCount > 0) {
        oddCount--
    }
    
    return len(s) - oddCount
}
</code></pre>
</details>