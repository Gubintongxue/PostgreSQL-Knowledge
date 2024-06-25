# 【PostgreSQL源码解析】GDB调试和PG缓冲池分享

## 一、GDB常用命令

```
gdb attach pid #关联进程
gdb -p pid #关联进程
set args name 18 #设置参数
b test.c:9 #根据文件名称+行数 设置断点
b funcName #根据函数名称 设置断点
info breakpoints #查看断点
d breakNumber #删除断点
```

实际调试常用的命令

```
r #运行
c #继续执行
q #退出
s #进入
n #下一步
p blockNum #打印数据
layout src #显示源码
```



## 二、Linux命令

一个文件改为一个用户专属的

```
chown yao:yao /tmp/data -R #更改用户和组
chmod 755 /data #更改权限 111 101 101  101：可读不可写
uesradd yao #增加用户
userdel yao #删除用户

```



```
lsblk #查看设备
mount /dev/vdb /data #挂载/dev/vdb磁盘到/data目录
cat /etc/os-release #查看系统配置
ps aux | grep postgres #查看指定进程
```

