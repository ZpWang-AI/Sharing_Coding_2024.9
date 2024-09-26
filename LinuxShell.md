# Linux Shell 部分常用命令

* 后台运行

~~~sh
nohup [cmd] > output.log 2> error.log &  # output.log 是正常输出的文件，error.log 是报错输出的文件
nohup [cmd] > output.log 2>&1 &  # 将输出都输进 output.log
# [cmd] 是要运行的命令，比如：python a.py, sh a.sh -p 123
~~~

* 查看进程

~~~sh
ps -aux  # 查看所有进程
grep xxx  # 查找包含 xxx 的行
grep -v xxx  # 查找不包含 xxx 的行
ps -aux | grep python | grep -v gpustat | grep -v .vscode-server  # 查找所有进程中包含 python，不包含 gpustat 和 .vscode-server 的行
~~~

组合 ps 和 grep 命令来打印自己想找的程序

* 查看显卡占用

~~~sh
conda activate base  # 开 conda 环境
pip install gpustat  # 下载 gpustat 这个包
gpustat -ip  # 实时展示显卡占用
gpustat -p  # 展示占用显卡的程序的进程号 pid
watch --color -n1 gpustat -cpu --color  # 实时展示显卡占用且展示进程号
~~~


* 查看硬盘的内存占用

~~~sh
df -h  # 所有硬盘的占用情况
du -sh  # 当前文件夹大小
du -h -d 1 | sort -hr  # 当前文件夹下各文件/文件夹的大小
~~~

* 查看端口占用（用于前后端开发）

~~~sh
lsof -t -i:[port]  # [port] 是要查询的端口号，比如：8793，返回结果是对应的程序进程号 pid
~~~

## P.S.

Shell 的写法与 Python 有较大不同，可以常询问 GPT 来获取解答

