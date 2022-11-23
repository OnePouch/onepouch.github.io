---
title: leetCode Day23
date: 2022-11-23 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Longest Substring Without Repeating Characters

題目:

    給一個二分樹,返回節點級別的順序遍歷



解法:

    定義一個空矩陣和節點級別,遞歸,如果二分樹為空的話,返回結果,如果結果矩陣的長度比節點級別+1還小的話,將空陣列塞入矩陣,將節點值塞入矩陣中,遍歷左節點和右節點,節點級別需+1


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
func levelOrder(root *TreeNode) [][]int {
    var result [][]int
    
    return getResult(root, result, 0)
}

func getResult(root *TreeNode, result [][]int, level int) [][]int {
    if root == nil {
        return result
    }
    
    if len(result) < level + 1 {
        result = append(result, []int{})
    }
    result[level] = append(result[level], root.Val)
    
    result = getResult(root.Left, result, level + 1)
    result = getResult(root.Right, result, level + 1)
    
    return result
}
</code></pre>
</details>


# Clone Graph

題目:

    複製一個給定的 graph



解法:

    使用bfs,將連接的兩點存入queue中,每次從queue中拋出第一個值,並將此值的連接兩個點存入queue中,如果此點已經執行過,就不再重複執行,直到queue為空


<details> <summary>code</summary>
<pre><code>
/**
 * Definition for a Node.
 * type Node struct {
 *     Val int
 *     Neighbors []*Node
 * }
 */

func cloneGraph(node *Node) *Node {
    if node == nil {
        return nil
    }
    
    visited := make(map[*Node]*Node)
    queue := []*Node{node}
    visited[node] = &Node{Val: node.Val}
    
    for len(queue) > 0 {
        pop := queue[0]
        queue = queue[1:]
        
        for _, value := range pop.Neighbors {
            if _, ok := visited[value]; !ok {
                visited[value] = &Node{Val:value.Val}
                queue = append(queue, value)
            }
            visited[pop].Neighbors = append(visited[pop].Neighbors, visited[value])
        }
    }
    
    return visited[node]
}
</code></pre>
</details>