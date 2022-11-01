---
title: leetCode Day2
date: 2022-11-01 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Merge Two Sorted Lists

題目:

    擁有兩個順序的列表,將兩個列表合併成一個順序的列表



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
func mergeTwoLists(list1 *ListNode, list2 *ListNode) *ListNode {
    if list1 == nil {
        return list2
    }
    
    if list2 == nil {
        return list1
    }
    
    result := new(ListNode)
    
    if list1.Val >= list2.Val {
        result.Val = list2.Val
        result.Next = mergeTwoLists(list1, list2.Next)
    } else {
        result.Val = list1.Val
        result.Next = mergeTwoLists(list1.Next, list2)
    }
    
    return result
}
</code></pre>
</details>


# Best Time to Buy and Sell Stock

題目:

    有一組陣列,key為天數,value為金額,你可以選擇一天買入,在另一天賣出(賣出沒辦法在買入之前),求最多賺多少金額?



解法:

    先設定一個最小值(minNum)為陣列中可能出現的最大數和一個最大值(max)為0,跑陣列迴圈,如果值比minNum小,minNum=當前的值,如果當前值-minNum比max大,max為當前值-minNum,最後回傳max


<details> <summary>code</summary>
<pre><code>
func maxProfit(prices []int) int {
    var max int
    minNum := 10000
    for _, value := range prices {
        if minNum > value {
            minNum = value
        }
        if value - minNum > max {
            max = value - minNum
        }
    }
    
    return max
}
</code></pre>
</details>