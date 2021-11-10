---
title: Docker 簡介 哇嗚 好棒
date: 2021-11-07 00:00:00 +0800
categories: [ABC, Tools]
tags: [Tang]     # TAG names should always be lowercase
---

## 何謂容器,為何需要它
> 容器能和主機的操作系統共享資源,因而它的效率高出一個數量級。啟動和停止容器均只需一瞬間。相比在主機上直接運行程序,容器的性能耗損非常低,甚至是零耗損。

> 容器具有可移植性,徹底解決了不同環境的改變導致的問題。

> 容器是輕量的,意味著開發者可以同時運行數十個容器。更容易進行水平擴展。

## Dockerfile

### FROM指定基礎鏡像
> 所謂定制鏡像,那一定是以一個鏡像為基礎,在其上進行定制。

> FROM就是指定鏡像,因此一個Dockerfile中FROM是必備的指令,並且必須為第一條指令。

> Docker Hub上面有許多官方鏡像
* 服務類鏡像,如nginx、redis、mongo、mysql、httpd...等
* 各種語言應用鏡像,如node、python、ruby、golang...等
* 操作系統鏡像,如ubuntu、debian、centos、alpine...等

### RUN執行命令
> RUN指令是用來執行命令的。

> RUN指令在定制鏡像時是最常用的指令之一。其格式有兩種：
* shell格式：RUN <命令>,就像直接在命令行中輸入的命令一樣
```
RUN echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html
```
* exec格式：RUN ["可執行文件", "參數1", "參數2"],這更像是函數調用中的格式
> Dockerfile中每一個指令都會建立一層,RUN也不例外。每一個RUN的行為,都會建立新的一層。由於不必要的層會使鏡像變得臃腫(AUFS最多只能有127層),你會發現許多Dockerfile都把多個命令放在同一個RUN指令中,以減少層的數量。