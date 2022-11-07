---
title: leetCode Day8
date: 2022-11-07 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Reverse Linked List

題目:

    反轉鏈表



解法:

    


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
    return reverse(head, nil)
}

func reverse(head *ListNode, newNode *ListNode) *ListNode {
    if (head == nil) {
        return newNode
    }
    next := head.Next
    head.Next = newNode
    return reverse(next, head)
}
</code></pre>
</details>


# Majority Element

題目:

    有一個數字陣列,返回多數元素



解法:

    先假設陣列第一個數是最多的數字(num),出現次數為1,跑迴圈,如果出現次數為0的話,表示該數字不是最多的數字,num為另一個數字,設定出現數字為1,如果陣列的值跟num一樣的話,count++,如果不一樣的話count--


<details> <summary>code</summary>
<pre><code>
func majorityElement(nums []int) int {
    count := 1
    num := nums[0]
    
    for i := 1; i < len(nums); i++ {
        if count == 0 {
            num = nums[i]
            count = 1
        } else if nums[i] == num {
            count++
        } else {
            count--
        }
    }
    
    return num
}
</code></pre>
</details>


#  

題目:

    



解法:

    


<details> <summary>code</summary>
<pre><code>

</code></pre>
</details>