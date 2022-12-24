---
title: leetCode Day49
date: 2022-12-24 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Remove Nth Node From End of List

題目:

    有一個列表,刪除從後面數來第n個節點



解法:

    因為我們要找出後面數來第n個,所以我們可以用初始點和出點後往後n個當作依據,同時往後,執到後面那個跑到最後一個,前面的就會是需要刪除節點的前一個節點,把前一個節點的下一個節點,設定為下兩個節點,就可以刪除該節點


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    left := head
    right := head

    for i := 0; i < n; i++ {
        right = right.Next
    }

    if right == nil {
        return left.Next
    }

    for right.Next != nil {
        right = right.Next
        left = left.Next
    }

    left.Next = left.Next.Next

    return head
}
</code></pre>
</details>