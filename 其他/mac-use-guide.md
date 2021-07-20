# Mac使用技巧汇总

## 安装 Homebrew

[码云地址](https://gitee.com/cunkai/HomebrewCN)

[参考地址](https://www.jianshu.com/p/10864a5a5e10)

```shell script
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

更改相应目录权限
```shell script
sudo chown -R XXX  /usr/local/Homebrew       ##XXX改为自己的用户名
sudo chown -R XXX $(brew --prefix)/*  
sudo mkdir /usr/local/Frameworks            ##有这个文件夹就不操作
sudo chown -R XXX /usr/local/Frameworks

```

## 查看端口占用 
1、查看端口占用

```
lsof -i tcp:8080
```
![](../assets/mac-use-guide/1.jpeg)

字段说明

| 名称 | 说明 |
| --- | ---- |
| COMMAND | 进程名称 |
| PID | 进程ID |
| USER | 所属用户 |
| FD | 文件描述符，应用程序通过文件描述符识别该文件 |
| TYPE | 文件类型，文件 REG、目录 DIR、字符 CHR、块设备 BLK、UNIX域套接字 UNIX、先进先出队列 FIFO、IP套接字 IPv4 |
| DEVICE | 指定磁盘的名称 |
| SIZE/OFF	 | 文件的大小 |
| NODE | 索引节点(文件在磁盘上的标识) |
| NAME | 打开文件的确切名称 |

2、杀掉进程
```
kill 1622
```

[参考地址](https://blog.csdn.net/zwkkkk1/article/details/88797044)






## Mac怎么打出反引号

mac 的反引号就在数字1的左边，按住option(alt)键并且在英文状态下即可。

> 以下这个仅针对黑苹果用户。更改完类型后，按照上述方法即可。˚

系统偏好设置 ->  键盘 -> 更改键盘类型 -> 选择 ISO 欧洲
- ISO / IEC 9995 标准键盘





## Mac SourceTree 添加 ssh key



config文件

```
Host *
   UseKeychain yes
   AddKeysToAgent yes
   IdentityFile ~/.ssh/id_rsa
   IdentityFile ~/.ssh/github_rsa
```



1、生成sshkey

2、执行`ssh-add ~/.ssh/id_rsa` 将`sshkey`添加到sourceTree

3、执行`ssh-add -K ~/.ssh/id_rsa` 将`sshkey`添加到钥匙串

4、`cd` 到  `.ssh`目录下, 用`touch config`命令创建`config`文件

5、执行`open config`, 打开config文件.

6、输入上面的配置内容, 保存·`config`文件



这样就可以开机自动加载sshkey啦