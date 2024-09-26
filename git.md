# Git 前言

## Git 是什么

一种常用的版本管理的工具，其余类似有：SVN、CVS、VSS。

与 Github 联系：
* Github 是基于 Git 的远程代码管理平台，Gitee 是国内类似平台，~~以及CSDN的GitCode~~
* Github 基于 Git，而运行 Git 不一定需要在 Github 上有对应库


## 为什么要用 Git

1. 同步代码（备份、在不同服务器上使用）
2. 版本管理（回退改动、不同分支开发不同部分）
3. 多人协作（项目、公司）

~~如准备删库跑路，请逆练此法~~


## VSCode 插件

Git Graph 可视化分支和推送

# 初始化

初始化当前目录

```sh
git init
```

如果需要可以带目录路径

```sh
git init /home/user/test/zpwang/TEST/repoA
```

# 复制库

```sh
git clone [ssh/https_address]
```

### 从 Github 复制

推荐用 ssh 地址

https 地址：https://github.com/ZpWang-AI/Sharing_Coding_2024.9.git

ssh 地址：git@github.com:ZpWang-AI/Sharing_Coding_2024.9.git

```sh
git clone git@github.com:ZpWang-AI/Sharing_Coding_2024.9.git
```

### 从本地复制

当前电脑上有个库 repoA，路径为 /home/user/test/zpwang/TEST/repoA

出于某些目的（比如多人协作），需要克隆一个到另一个目录：/home/user/test/zpwang/TEST/foldA

```sh
cd /home/user/test/zpwang/TEST/foldA
git clone /home/user/test/zpwang/TEST/repoA
```

### 从另一个服务器复制到本地

先设置本地 .ssh/config，比如设置如下：

```sh
Host t2s
    HostName 1.94.176.246
    Port 19900
    User user
```

Windows/Linux CMD （Windows 推荐用 powershell）进入要复制的本地文件夹，然后克隆

```sh
cd ./target_fold
git clone t2s:/home/user/test/zpwang/TEST/repoA
```

另一种方式是手写IP和端口，不推荐

```sh
git clone ssh://user@1.94.176.246:19900/home/user/test/zpwang/TEST/repoA
```

### 从服务器A复制到服务器B

同"从另一个服务器复制到本地"，但是需要配置服务器B的~/.ssh/config

### 从本地复制到服务器

无法 git clone，除非本地做穿透，让服务器可以 ssh 访问

# 保存改动

~~~sh
git add .  # 缓存全部改动
git add [file_path]  # 缓存对应文件的改动
git commit -m "Commit Message"  # 保存改动
~~~

更推荐用 VSCode 里的插件，使用 Source Control 部分来进行改动的缓存和保存

# 设置远程连接(remote)

假设本地、服务器都有相同的库，需要将服务器的库连上本地的库，后续可以用本地库更新服务器的库或者反过来

进入本地库，设置 remote

```sh
git remote add t2s_repoA t2s:/home/user/test/zpwang/TEST/repoA
# t2s_repoA 为自定义的名字，用于后续pull/push
# t2s 为 .ssh/config 中的服务器
# /home/user/test/zpwang/TEST/repoA 为路径
```

设置完后可以在 .git/config 中查看

相关命令

```sh
git remote  # 查看所有remote
git remote remove t2s_repoA  # 删除remote
```

# 分支 branch

```sh
git branch  # 查看所有branch
git branch checkout master
git merge [branch_name]  # 合并分支
```

# 获取更新、推送更改

```sh
git pull  # 拉，获取更新
git push  # 推，推送更改
```

~~~sh
git pull t2s_repoA
# t2s_repoA 为remote的名字
# 默认分支因git版本而不同，可能是主分支，也可能是当前分支，建议手动指定

git pull t2s_repoA main:master
# 远程main -> 本地master

git push t2s_repoA master:main
# 本地master -> 远程main
~~~

# 实际应用

### 如果要在本地、服务器A、服务器B，各自维护相同一套代码，如何用 git 实现同步？

本地库与 A、B 建立 remote，AB 的更新 pull 到本地，本地的更新 push 到 AB

### 服务器上多人开发同一份代码，如何方便调试开发？

git clone 到自己的文件夹下，完成改动后 git pull 到主库的次分支并 git merge


