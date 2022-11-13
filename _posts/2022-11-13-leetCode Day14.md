---
title: leetCode Day14
date: 2022-11-13 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Longest Common Prefix

題目:

    一個陣列裡面有許多字串,找出這些字串的共同前綴,如果沒有返回空



解法:

    先找出最短陣列的長度,跑迴圈判斷每個陣列的字母是否都一樣,把字串串起來,如果不一樣,返回字串


<details> <summary>code</summary>
<pre><code>
func longestCommonPrefix(strs []string) string {
    var result string
    minLen := len(strs[0])
    
    for key := range strs {
        if len(strs[key]) < minLen {
            minLen = len(strs[key])
        }
    }
    
    for i:=0; i<minLen; i++ {
        str := ""
        for _, value := range strs {
            if str == "" {
                str = value[i:i+1]
            } else {
                if str != value[i:i+1] {
                    return result
                }
            }
        }
        result = result + str
    }
    
    return result
}
</code></pre>
</details>


# Single Number

題目:

    一個不為空的數字陣列,每個數字都會出現兩次,只有一個數字出現一次,找出該數字



解法:

    陣列排序,如果偶數key的值和他下一個數字不相同的話,該數字就是獨立的數字,如果都相同,最後一個數為獨立的


<details> <summary>code</summary>
<pre><code>
import "sort"

func singleNumber(nums []int) int {
    sort.Ints(nums)
    
    for i:=0; i<len(nums)-1; i+=2 {
        if nums[i] != nums[i+1] {
            return nums[i]
        }
    }
    
    return nums[len(nums)-1]
}
</code></pre>
</details>


# Palindrome Linked List

題目:

    有一個連結串,判斷是否回文



解法:

    先用龜兔賽跑找出中間點,如果為奇數,第二段為中間數的下一個,將第二段反轉,跑迴圈判斷第二段跟第一段的值是否相同


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func isPalindrome(head *ListNode) bool {
    fast, slow := head, head
    for fast != nil && fast.Next != nil {
        fast = fast.Next.Next
        slow = slow.Next
    }
    
    if fast != nil {
        slow = slow.Next
    }
    
    slow = reverse(slow)
    
    for slow != nil {
        if slow.Val != head.Val {
            return false
        }
        slow = slow.Next
        head = head.Next
    }
    
    
    return true
}

func reverse(head *ListNode) *ListNode {
    var tmp *ListNode
    for head != nil {
        next := head.Next
        head.Next = tmp
        tmp = head
        head = next
    }
    
    return tmp
}
</code></pre>
</details>