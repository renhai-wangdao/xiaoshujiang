---
title: mysql docker 安装手册 2023-03-12
tags: '安装手册,王道'
category: /安装手册
grammar_cjkRuby: true
---

# mysql 安装手册

## docker 安装
### 命令详情
```sh?linenums
docker run #在docker中启动一个容器实例
-d  #该容器在后台运行
-p 3306:3306 # 容器与主机映射端口为， 3306（主机端口，即外部连接mysql使用的端口号）: 3306（容器端口）
--name mysql #容器运行后的名称
-v /mysqldata/mysql/log:/var/log/mysql #将容器/var/log/mysql目录下的数据，备份到主机的 /mysqldata/mysql/log目录下
-v /mysqldata/mysql/data:/var/lib/mysql #将容器/var/lib/mysql目录下的数据，备份到主机的 /mysqldata/mysql/data目录下
-v /mysqldata/mysql/conf:/etc/mysql #将容器/etc/mysql目录下的数据，备份到主机的 mysqldata/mysql/conf目录下
-e MYSQL_ROOT_PASSWORD=root #设置当前mysql实例的密码为root
mysql:5.7 #需要运行的容器名称以及版本号
```
### 命令
```sh?linenums
docker run -d -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=root mysql:8.0.32
```