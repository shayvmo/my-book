##  Ubuntu-LNMP （基于wsl 的 Ubuntu 编译安装 LNMP）

最近更新时间：2020年12月21日

进度：未完成



### 一、更新软件源

1、查看Ubuntu 版本

```shell
cat /proc/version
# 列出
Linux version 4.4.0-18362-Microsoft (Microsoft@Microsoft.com) (gcc version 5.4.0 (GCC) ) #1-Microsoft Mon Mar 18 12:02:00 PST 2019


cat /etc/lsb-release
#列出
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.1 LTS"

uname -a
# 列出
Linux MM-202009071515 4.4.0-18362-Microsoft #1-Microsoft Mon Mar 18 12:02:00 PST 2019 x86_64 x86_64 x86_64 GNU/Linux

#或者 lsb_release -a
lsb_release -a

# 列出
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.1 LTS
Release:        20.04
Codename:       focal
```





2、查找对应的版本，更新软件源 [清华大学源地址](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

```shell
# 覆盖了源地址之后，执行命令更新
apt-get update
```



二、准备阶段

1、安装编译要用到的库和工具

```shell
apt install build-essential libtool gcc automake autoconf make
```

