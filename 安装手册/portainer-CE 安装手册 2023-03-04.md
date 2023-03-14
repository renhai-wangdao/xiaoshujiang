---
title: portainer-CE 安装手册 2023-03-04
tags: 王道
category: /安装手册
grammar_cjkRuby: true
---
#安装命令
```sh?linenums
docker run -d --restart=always --name="portainer" -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock 6053537/portainer-ce
```