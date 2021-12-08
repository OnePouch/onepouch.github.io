---
title: Docker ARG VS ENV
date: 2021-12-08 00:00:00 +0800
categories: [ABC, Tools]
tags: [Tang]     # TAG names should always be lowercase
---

## ARG VS ENV

建立image時使用變數用ARG,

運行container時使用變數用ENV(相同image跑不同的設定,ex:環境變數)

```dockerfile
ARG var
ENV var=${var}
```
可以在建立image時有特定的var值(docker build --build-arg var=abc)
或是運行container時有特別的運行值(docker run -e var=def)

![avatar](https://vsupalov.com/images/docker-env-vars/docker_environment_build_args.png)

（圖片來源：vsupalov.com