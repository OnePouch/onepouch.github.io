---
title: codeWars Day3
date: 2022-10-22 00:00:00 +0800
categories: [codeWars]
tags: [Tang]     # TAG names should always be lowercase
---

# Two fighters, one winner.

題目:

    有兩個決鬥者物件,都擁有名稱,血量,每下攻擊力這三個屬性,現在兩個決鬥者互毆判斷誰是獲勝者



解法:

    先判斷誰先攻,然後跑一個迴圈,誰的血量先低於0,誰就輸了



# Shortest Word

題目:

    給你一串詞,返回其中最短的字串, 字串不會為空,也不需要考慮其他數據形態


解法: 

    將詞用空白切割成每個字串,然後預設最小值為第一個字串的長度,然後一一比對每個詞的長度,直到陣列跑完

