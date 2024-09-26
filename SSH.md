# SSH(Secure Shell) 前言

一种通讯协议，用来传输文件或是远程连接。

可以访问学校服务器或是实验室租赁的服务器。

## VSCode 插件

Remote - SSH

# 配置

配置文件位于

~~~sh
~/.ssh  # Linux
C:\User\[username]\.ssh  # Windows
~~~

配置方法

~~~sh
Host cu13
    HostName 192.168.134.9
    User zpwang

Host northern
    HostName 10.10.80.63
    User zpwang
    Port 22
~~~


# 远程连接

~~~sh
ssh cu13  # 根据配置文件中设置的 Host
ssh -p 22 zpwang@192.168.134.9  # 手动输入，不推荐
~~~

## 免密登录

配置密钥

~~~sh
cd ~/.ssh  # 进入目录，windows 同理
ssh-keygen -t rsa -C "your_email@example.com"  # 直接回车跳过询问，生成密钥
~~~

完成后得到两份文件：

* id_rsa: 私钥，放在本地
* id_rsa.pub: 公钥，将里面内容复制到其他服务器的 *~/.ssh/authorized_keys* 文件中用于免密登录，如果没有这个文件可以新建一个

此后，所有配了公钥的服务器登录时都不再需要密码

# SCP 传输文件

~~~sh
scp D:\0--data\实验室\2024下半年组会分享\2024.10.8\Sharing_Coding_2024.9\Git.md t2s:~/test/zpwang/  # 复制文件，从本地到 t2s 服务器下的 ~/test/zpwang/Git.md
scp -r t2s:~/test/zpwang/TEST D:\0--data\实验室\2024下半年组会分享\2024.10.8\Sharing_Coding_2024.9\  # 复制文件夹，从 t2s 服务器到本地
~~~

t2s 为 *~/.ssh/config* 中配置好的远程，scp 可以通过 ssh 的配置传输文件，手写服务器地址同理

配了公钥后，scp 也可以免密传输