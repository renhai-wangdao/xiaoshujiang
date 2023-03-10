---
title: docker mssql 安装 - 使用手册
tags: 王道
category: 安装手册
---
# 
## 安装 mssql
```plaintext?linenums
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=123@qweR" -p 1433:1433 --name mssql --hostname mssql  -d  mcr.microsoft.com/mssql/server:2022-latest
```
## 修改密码
```plaintext?linenums
docker exec -it mssql /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "旧密码" -Q "ALTER LOGIN SA WITH PASSWORD='新密码'"
```
## 还原数据库
### 拷贝BAK文件至DOCKER容器中
```plaintext?linenums
docker cp "/{bak文件}.bak" mssql:/
```
### 进入DOCKER容器中
```plaintext?linenums
docker exec -i -t   mssql /bin/bash
```
### 使用RESTORE FILELISTONLY命令列出备份数据文件的逻辑名
```plaintext?linenums
/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P '123@qwe' -Q 'RESTORE FILELISTONLY FROM DISK = "/{bak文件}.bak"' | tr -s ' ' | cut -d ' ' -f 1-2
```
### 还原数据库
```plaintext?linenums
/opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '{数据库密码}' -Q 'RESTORE DATABASE {数据库名称} FROM DISK = "/{bak文件}.bak" WITH MOVE "{旧的逻辑名}" TO "/var/opt/mssql/data/{数据库名称}.mdf" , MOVE "{旧的逻辑名}_log" TO "/var/opt/mssql/data/{数据库名称}.ldf"'
```
## 备份数据库
### 打开数据库控制台
```plaintext?linenums
/opt/mssql-tools/bin/sqlcmd -U sa -P 123@qwe
```
### 覆盖 init
```plaintext?linenums
BACKUP DATABASE [DataFlow] TO DISK = N'/var/opt/mssql/backup/DataFlow.bak' WITH NOFORMAT, init
```
### 追加 noinit
```plaintext?linenums
BACKUP DATABASE [DataFlow] TO DISK = N'/var/opt/mssql/backup/DataFlow.bak' WITH NOFORMAT, noinit
```
