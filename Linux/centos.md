## Centos



1、切换国内源

```shell
// 备份原有
mv /etc/yum.repos.d/CentOS-Base.repo  /etc/yum.repos.d/CentOS-Base.repo_bak

// 先安装wget
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
 
yum makecache
 
yum -y update
```



2、没有 ifconfig 命令

```shell
yum install net-tools
```



