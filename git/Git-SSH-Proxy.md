# 为GitHub配置ssh代理
因为GitHub可以上传ssh公钥，以此免去每次提交输入密码的麻烦，所以个人更喜欢ssh的连接方式。

当前协议是否为ssh可用`git remote -v`查看，ssh协议的会有一个链接为`git@github.com:username/depo.git`的分支。

## ssh的config设置
在`~/.ssh/config`中根据域名添加以下配置
```
Host github.com
Hostname github.com
ProxyCommand nc -x 127.0.0.1:1080 %h %p
```
ssh客户端在处理github.com域名时会自动使用nc命令为自己设置代理，代理以`ip:port`
的形式指明，我这里使用的是127.0.0.1:1080

## permission错误
在config文件明明拥有读写权限的情况下出现permission错误
```bash
$ git clone git@github.com:ysdlb/java
Cloning into 'java'...
Bad owner or permissions on /home/ysdlb/.ssh/config
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
```bash
$ ll ~/.ssh/
total 8
drwx------ 1 ysdlb ysdlb  512 Sep  2 21:31 ./
drwxr-xr-x 1 ysdlb ysdlb  512 Sep  2 21:31 ../
-rw-rw-rw- 1 ysdlb ysdlb   76 Sep  2 21:31 config
-rw------- 1 ysdlb ysdlb 1675 Aug 31 13:51 id_rsa
-rw-r--r-- 1 ysdlb ysdlb  403 Aug 31 13:51 id_rsa.pub
-rw-r--r-- 1 ysdlb ysdlb 2656 Sep  2 11:28 known_hosts
```

##### 原因及解决方案
在`man ssh`中有如下描述

    Because of the potential for abuse, this file must have strict permissions: 
    read/write for the user, and not writable by others. It may be group-writable 
    provided that the group in question contains only the user.

为了避免`~/.ssh/config`配置文件被（他人）滥用，`config`文件必须有严格的权限要求：
**对用户自己必须是可读可写的，对其他人必须是不可写的**。

那么满足这两个条件的比较优雅的权限分配方案是
```bash
$ chmod 600 ~/.ssh/config
或
$ chmod 644 ~/.ssh/config
```

## 最后附上HTTP协议的配置
```git
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```
