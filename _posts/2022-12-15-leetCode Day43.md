---
title: leetCode Day43
date: 2022-12-15 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# LRU Cache

題目:

    有一個暫存只有capacity個容量,如果資料超過容量,會把最早使用過的資料刪除



解法:

    一個存容量一個存資料,如果容量不夠還需要存入,把資料最前面的刪除,再存入,因為取得資料也算是使用,所以取得如果有找到,需要把資料放到最後面


<details> <summary>code</summary>
<pre><code>
type Node struct {
    Key int
    Val int
    Prev *Node
    Next *Node
}

type LRUCache struct {
    Cap int
    Data map[int]*Node
    Head *Node
    Tail *Node
}


func Constructor(capacity int) LRUCache {
    return LRUCache{capacity, make(map[int]*Node), nil, nil}
}


func (this *LRUCache) Get(key int) int {
    node, ok := this.Data[key]
    if ok {
        this.Remove(node)
        this.Add(node)
        return node.Val
    }

    return -1
}


func (this *LRUCache) Put(key int, value int)  {
    node, ok := this.Data[key]
    if ok {
        this.Remove(node)
        this.Add(node)
        node.Val = value
    } else {
        node = &Node{Key: key, Val: value}
        this.Data[key] = node
        this.Add(node)
    }

    if len(this.Data) > this.Cap {
        delete(this.Data, this.Head.Key)
        this.Remove(this.Head)
    }
}

func (this *LRUCache) Add(node *Node) {
    node.Next = nil
    node.Prev = this.Tail
    if this.Tail != nil {
        this.Tail.Next = node
    }
    this.Tail = node

    if this.Head == nil {
        this.Head  = node
    }
}

func (this *LRUCache) Remove(node *Node) {
    if node == this.Head {
        this.Head = node.Next
    } else {
        node.Prev.Next = node.Next
    }

    if node == this.Tail {
        this.Tail = node.Prev
    } else {
        node.Next.Prev = node.Prev
    }
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * obj := Constructor(capacity);
 * param_1 := obj.Get(key);
 * obj.Put(key,value);
 */
</code></pre>
</details>


# Kth Smallest Element in a BST

題目:

    在二分搜尋樹中找出第K個小個數



解法:

    因為樹為二分收尋樹,所以inorder就會為樹的順序排列遍歷,所以我們往最走邊找出最小的值,再往右往上找出,第K個最小值


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func kthSmallest(root *TreeNode, k int) int {
    var stack []*TreeNode

    for true {
        for root != nil {
            stack = append(stack, root)
            root = root.Left
        }

        root = stack[len(stack) - 1]
        stack = stack[:len(stack) - 1]

        k--
        if k == 0 {
            return root.Val
        }
        root = root.Right
    }

    return 0
}
</code></pre>
</details>