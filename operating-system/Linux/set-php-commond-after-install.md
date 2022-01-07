# 源码安装PHP后添加php快捷命令



1、打开用户根目录下的 `.bash_profile`

```
vi ~/.bash_profile
```



2、修改后保存

```
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs

PATH=$PATH:$HOME/bin

export PATH

alias php=/usr/local/php/bin/php
```



3、执行

```
source ~/.bash_profile
```





第二种方法：

设置环境变量 ：修改/etc/profile文件使其永久性生效，并对所有系统用户生效，在文件末尾加上如下两行代码

```
PATH=$PATH:/usr/local/php/bin
export PATH
```

然后执行生效命令

```
source /etc/profile
```

查看PHP版本信息

```
php -v
```



