---
title: Linux下安装mysql-8.0.19
categories: "Linux"
tags:
  - Linux
  - MYSQL
abbrlink: 45793
---
### 下载解压   
```shell
wget https://cdn.mysql.com/archives/mysql-8.0/mysql-8.0.19-linux-glibc2.12-x86_64.tar.xz    

tar xvf mysql-8.0.19-linux-glibc2.12-x86_64.tar.xz
```

### 移动
```shell
mv mysql-8.0.19-linux-glibc2.12-x86_64 /usr/local/mysql
```

### 创建data文件    
```shell
mkdir /usr/local/mysql/data
```

### 创建用户    
```shell
useradd mysql
```


### 更改mysql目录下所有的目录及文件夹所属的用户组和用户，以及权限
```shell
chown -R mysql:mysql /usr/local/mysql
chmod -R 755 /usr/local/mysql
```


​    
### 编译安装并初始化mysql,务必记住初始化输出日志末尾的密码（数据库管理员临时密码）
```shell
cd /usr/local/mysql/bin
./mysqld --initialize --user=mysql --datadir=/usr/local/mysql/data --basedir=/usr/local/mysql
```

### 新增

创建data目录

```shell
mkdir -p /url/local/mysql/data    
chown -R mysql:mysql /url/local/mysql
```



### 编辑配置文件my.cnf，添加配置如下

vi /etc/my.cnf

```shell
    # MySQL 配置文件，
#参考:http://blog.51cto.com/zhangxinqi/2178407  
#     https://www.cnblogs.com/lyq863987322/p/8074749.html

# 数据库目录 /data/mysql
[client]
port=3306
# mysql socket 文件存放地址 
socket=/tmp/mysql.sock
# 默认字符集
default-character-set=utf8

[mysqld]
server-id=1
# 端口
port=3306
# 运行用户
user=mysql
# 最大连接
max_connections=200
socket=/tmp/mysql.sock
# mysql 安装目录（解压后文件的目录）
basedir=/usr/local/mysql
# 数据目录（这里放在我们新建的 /data/mysql 下）
datadir=/url/local/mysql/data
pid-file=/url/local/mysql/data/mysql.pid
init-connect='SET NAMES utf8'
character-set-server=utf8
# 数据库引擎
default-storage-engine=INNODB
log_error=/data/mysql/mysql-error.log
slow_query_log_file=/data/mysql/mysql-slow.log

# 跳过验证密码
#skip-grant-tables

[mysqldump]
quick
max_allowed_packet=16M
EOF
```


​    
### 启动mysql
```shell
/usr/local/mysql/support-files/mysql.server start
```

### 添加软连接，并重启服务
```shell
ln -s /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql（init.d里面存放的是一些服务）
ln -s /usr/local/mysql/bin/mysql /usr/bin/mysql (usr/bin存放的是一些命令)
service mysql restart
```


​    
### 登录mysql，修改密码
```shell
mysql -u root -p密码
ALTER USER USER() IDENTIFIED BY 'password';
flush privileges;
```

### 开放远程连接
```shell
use mysql;
update user set user.Host='%' where user.User='root';
flush privileges;
```

### 设置开机自启
```shell
1、将服务文件拷贝到init.d下，并重新命名为mysqld
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld
2、赋予可执行权限
chmod +x /etc/init.d/mysqld
3、添加服务
chkconfig --add mysqld
4、显示服务列表
chkconfig --list
```





    
##     参考连接
>https://blog.csdn.net/weixin_43744799/article/details/84562761