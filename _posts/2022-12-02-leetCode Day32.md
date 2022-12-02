---
title: leetCode Day32
date: 2022-12-02 00:00:00 +0800
categories: [leetCode]
tags: [Tang]     # TAG names should always be lowercase
---

# Time Based Key-Value Store

題目:

    以時間儲存的key-value,set的timestamp皆為正時間序



解法:

    設定一個key裡面儲存了value和timestamp,設定時將timestamp和value儲存至key中,get時如果key不存在或是傳入的timestamp比儲存的timestamp小的話,返回空,如果比較大的話,使用binary search找出最大小於timestamp的值


<details> <summary>code</summary>
<pre><code>
type TimeValue struct {
    Value string
    Timestamp int
}
type TimeMap struct {
    m map[string][]TimeValue
}


func Constructor() TimeMap {
    return TimeMap{m: make(map[string][]TimeValue)}
}


func (this *TimeMap) Set(key string, value string, timestamp int)  {
    if _, ok := this.m[key]; !ok {
        this.m[key] = []TimeValue{}
    }
    this.m[key] = append(this.m[key], TimeValue{value, timestamp,})
}


func (this *TimeMap) Get(key string, timestamp int) string {
    if len(this.m[key]) == 0 || this.m[key][0].Timestamp > timestamp {
        return ""
    }
    left := 0
    right := len(this.m[key])
    for left < right {
        mid := (left + right) / 2
        if this.m[key][mid].Timestamp == timestamp {
            return this.m[key][mid].Value
        }
        if this.m[key][mid].Timestamp > timestamp {
            right = mid
        } else {
            left = mid + 1
        }
    }
    return this.m[key][right - 1].Value
}


/**
 * Your TimeMap object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Set(key,value,timestamp);
 * param_2 := obj.Get(key,timestamp);
 */
</code></pre>
</details>
