---
title: leetCode Day26
date: 2022-11-26 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Product of Array Except Self

題目:

    一個數字陣列,算出數字總和,除了自己



解法:

    算出每個點左邊的總和,和右邊的總和,兩個相加


<details> <summary>code</summary>
<pre><code>
func productExceptSelf(nums []int) []int {
    length := len(nums)
    result := make([]int, length)
    
    result[0] = 1
    for i := 1; i < length; i++ {
        result[i] = result[i - 1] * nums[i - 1]
    }
    
    right := 1
    for i :=  length - 1; i >= 0; i-- {
        result[i] *= right
        right *= nums[i]
    }
    
    return result
}
</code></pre>
</details>


# Min Stack

題目:

    最小棧,有新增,拋出,顯示最上面的值,顯示最小值的功能



解法:

    


<details> <summary>code</summary>
<pre><code>
type HeadStack struct {
    Val int
    Min int
    Next *HeadStack
}

func NewHeadStack(val int, min int, stack *HeadStack) *HeadStack {
    return &HeadStack{
        Val: val,
        Min: min,
        Next: stack,
    }
}

type MinStack struct {
    head *HeadStack
}


func Constructor() MinStack {
    return MinStack{head: nil}
}


func (this *MinStack) Push(val int)  {
    if this.head == nil {
        this.head = NewHeadStack(val, val, nil)
    } else {
        this.head = NewHeadStack(val, min(val, this.head.Min), this.head)
    }
}


func (this *MinStack) Pop()  {
    this.head = this.head.Next
}


func (this *MinStack) Top() int {
    return this.head.Val
}


func (this *MinStack) GetMin() int {
    return this.head.Min
}

func min(a int, b int) int {
    if a > b {
        return b
    }
    return a
}


/**
 * Your MinStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(val);
 * obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.GetMin();
 */
</code></pre>
</details>