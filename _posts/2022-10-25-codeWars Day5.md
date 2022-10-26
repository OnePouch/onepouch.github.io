---
title: codeWars Day5
date: 2022-10-25 00:00:00 +0800
categories: [codeWars]
tags: [Tang]     # TAG names should always be lowercase
---

# Statistics for an Athletic Association

題目:

    有多個時間用逗點區分,需要找出時間的範圍,平均,中位數



解法:

    先把字串做切割,再把每個時間換算成秒數,存在另一個陣列arr,計算範圍,平均,中位數


<details> <summary>code</summary>
<pre><code>
package kata

import "strings"
import "fmt"
import "sort"
import "strconv"

func Stati(strg string) string {
  var sum, total int
  var arr []int
  
  if strg == "" {
    return ""
  }
  
  for _, value := range strings.Split(strg, ", ") {
    sum = 0
    for _, value1 := range strings.Split(value, "|") {
      time, _ := strconv.Atoi(value1)
      sum = 60 * sum + time
    }
    arr = append(arr, sum)
    total += sum
  }
  
  sort.Ints(arr)
  rangeValue := arr[len(arr)-1] - arr[0]
  averageValue := total / len(arr)
  medianValue := 0
  
  if len(arr) % 2 == 1 {
    medianValue = arr[len(arr) / 2]
  } else {
    medianValue = (arr[len(arr) / 2] + arr[len(arr) / 2 - 1]) / 2
  }
  
  return fmt.Sprintf("Range: %02d|%02d|%02d Average: %02d|%02d|%02d Median: %02d|%02d|%02d",
                     rangeValue / 3600, rangeValue % 3600 / 60, rangeValue % 60,
                     averageValue / 3600, averageValue % 3600 / 60, averageValue % 60,
                     medianValue / 3600, medianValue % 3600 / 60, medianValue % 60,
                    )
}
</code></pre>
</details>

# Highest Rank Number in an Array

題目:

    有一組數字陣列,找出出現頻率最高的數字,如果出現頻率有多個相同,找出數字最大的


解法: 

    遍歷陣列,找出頻率最高的數字寫入另一個陣列arr,排序arr,返回arr的最後一個數字


<details> <summary>code</summary>
<pre><code>
package kata

import "sort"

func HighestRank(nums []int) int {
  var arr1 []int
  
  arr := map[int]int{}
  maxCount := 0
  for _, value := range nums {
    arr[value]++
    
    if arr[value] > maxCount {
      maxCount = arr[value]
      arr1 = []int{value}
    } else if arr[value] == maxCount {
      arr1 = append(arr1, value)
    }
  }
  
  sort.Ints(arr1)
  return arr1[len(arr1) - 1]
}
</code></pre>
</details>