PostgreSQL15源码安装教程

### 一、简介

PostgreSQL简称为PG，是一个多进程模型。

### 二、源码编译安装

也可以从gitee上下载，可能速度要快一些。

- [Github代码](https://github.com/postgres/postgres)

- [参考博客](https://blog.csdn.net/weixin_40326748/article/details/128753725)

- pg默认端口是5432


- postgresql.conf


#### 1.下载代码

```
#git clone https://github.com/postgres/postgres.git
# 使用码云加速下载
git clone https://gitee.com/mirrors/PostgreSQL.git
cd postgres
# 切换发行版分支
git checkout REL_15_STABLE
```

#### 2.安装

```
# 安装pg_15
cd postgres
./configure  --enable-debug  --enable-cassert --prefix=/data/yaojun/install_pkg/pg CFLAGS=-O0 --without-icu
make -j 16
make install
```

#### 3.配置环境变量

```
# 环境变量 vim  ~/.bashrc
export PATH=/data/yaojun/install_pkg/pg/bin:$PATH
# 刷新环境变量
source ~/.bashrc
```

#### 4.初始化

```
# 初始化，dest目录没有会自动创建
initdb -D dest
```

#### 5.启动

```
# 启动
pg_ctl start -D dest
# 进入客户端
# -d是指定数据库名称 如果不指定默认是以当前用户名作为数据库名
psql -d postgres -p5432  

```

## 三、后台进程

1.postgres

2.checkpointer

3.background writer

4.walwriter

5.autovacuum launcher

6.logical replication launcher

![image-20240625235843644](image/image-20240625235843644.png)

先进入客户端才能看到local

## 四、GDB调试

- 设置环境变量 vim ~/.gdbinit

```
handle SIGUSR1 noprint nostop
handle SIGUSR2 noprint nostop
set pagination off
```

- 查询后台进程ID


```
select pg_backend_pid();
```

- gdb调试


```
gdb attach pid -tui
```



## 六、注意

- config出错的时候，有可能需要加上\--without-icu


```
 ./configure  --enable-debug  --enable-cassert --prefix=/data/yaojun/pg/pg_install CFLAGS=-O0 --without-icu
```

- beta\_16


```
# PG_16_beta
git checkout -b  REL_16_BETA1
./configure  --enable-debug  --enable-cassert --prefix=/Users/yaojun/MyInstall/pg_install CFLAGS=-O0 --without-icu
```

- 其他


```
pg_ctl -D dest -l logfile start
```

- 环境变量未生效


```
# 可能不需要
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/data/pgyaojun/install_pg/lib
export PATH
```

- 使用默认端口


PG不支持-r参数

```
# 使用默认端口
psql -d postgres
```

- 启动服务器


```
pg_ctl start -D pg_data
```