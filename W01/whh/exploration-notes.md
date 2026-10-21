1.服务器连接。
/1为什么通过ssh指令加上ip和端口可以远程连接到服务器
在b站上找讲解&问ai
10.61.***.*是一个ipv4地址，端口相当于计算机中的房间号，用来找到目标进程。ssh被称为安全远程登录协议，可以加密传输中的内容，从而不被别人截取
sshd在服务端运行，等待ssh连接，ssh通过ip和端口定位服务器上的sshd（通过ip确认机器，通过端口定位sshd），然后协商密钥，然后建立加密隧道并通过密码或公钥来进行身份验证。
/2如何免密登录
免密：通过在本地生成公钥，然后复制到~/.shh/authorized_keys中，此后每次连接服务器时客户端声明使用公钥认证，并且告诉服务器自己的公钥，服务器查询到相应的公钥则继续，然后服务器生成一个会话标识发给客户端，客户端用自己的私钥对该随机数据签名，把签名发回服务器，最后验证成功。
2.
#探索
**~/1/~**cat /etc/os-release 用来查看系统的版本             #RETTY_NAME="Ubuntu 22.04.5 LTS"   完整的系统名
NAME="Ubuntu"   
VERSION_ID="22.04"   #=版本号
VERSION="22.04.5 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
UBUNTU_CODENAME=jammy# 
**~/2/~**nproc  用来查看cpu的核数   (base) whh@hzcu-hpct:~$ nproc
                          128
**~/3/~**free -h  用来查看cpu内存(base) whh@hzcu-hpct:~$ free -h
               total（物理内存总量）        used       free      shared      buff/cache   available
Mem:           503Gi                       91Gi        16Gi       144Gi       396Gi       264Gi
Swap:          8.0Gi                       732Mi       7.3Gi
**~/4/~**pwd  查看当前目录路径(base) whh@hzcu-hpct:~$ pwd
/home/whh
**~/5/~**ls -la  查看当前目录下的所有文件(base) whh@hzcu-hpct:~$ ls -la
total 158420
drwxr-x--- 12 whh  whh       4096 Oct 19 12:31 .
drwxr-xr-x 34 root root      4096 Oct 15 16:54 ..
-rw-------  1 whh  whh        399 Oct 19 12:35 .bash_history
-rw-r--r--  1 whh  whh        220 Jan  7  2022 .bash_logout
-rw-r--r--  1 whh  whh       4242 Oct 18 14:01 .bashrc
drwx------  4 whh  whh       4096 Oct 15 21:22 .cache
drwxrwxr-x  2 whh  whh       4096 Oct 18 14:01 .conda
drwxr-xr-x  4 whh  whh       4096 Oct 15 21:21 .config
drwx------  4 whh  whh       4096 Oct 15 21:22 .copilot
drwxrwxr-x  3 whh  whh       4096 Oct 15 21:22 .dotnet
drwxrwxr-x  3 whh  whh       4096 Oct 18 13:15 ict-practice
drwx------  3 whh  whh       4096 Oct 15 21:08 .local
drwxrwxr-x 19 whh  whh       4096 Oct 18 14:01 miniconda3
-rw-r--r--  1 whh  whh  162129736 Oct 18 13:58 Miniconda3-latest-Linux-x86_64.sh
-rw-r--r--  1 whh  whh        807 Jan  7  2022 .profile
drwx------  2 whh  whh       4096 Oct 19 12:31 .ssh
-rw-------  1 whh  whh       1450 Oct 19 12:31 .viminfo
drwxr-x---  5 whh  whh       4096 Oct 19 12:35 .vscode-server
-rw-rw-r--  1 whh  whh        183 Oct 15 21:20 .wget-hsts
-rw-r--r--  1 whh  whh       5447 Mar 18  2026 超算队服务器资源管理与Slurm使用指南.md
**~/6/~**nvidia-smi查看显卡占用。

#创建
###新建
1.touch *.txt创建后缀为txt的文件
2.echo "*****" > *.txt创建并写入内容
3.mkdir ***创建目录
4.mkdir -p */*/*依次创建多级目录
###查看
1.cat *.txt显示文件内的内容
2.pwd 查看当前目录的路径
3.ls 显示当前目录下的文件和目录内的目录（不包括隐藏项(base) whh@hzcu-hpct:~$ ls
app.py  ict-practice  miniconda3  Miniconda3-latest-Linux-x86_64.sh  超算队服务器资源管理与Slurm使用指南.md
4.ls -a包括隐藏项(base) whh@hzcu-hpct:~$ ls (base) whh@hzcu-hpct:~$ ls -a
.              .bash_logout  .config       .local                             .python_history  .wget-hsts
..             .bashrc       .copilot      miniconda3                         .ssh             超算队服务器资源管理与Slurm使用指南.md
app.py         .cache        .dotnet       Miniconda3-latest-Linux-x86_64.sh  .viminfo
.bash_history  .conda        ict-practice  .profile                           .vscode-server
###编辑
1.vim *.txt编辑文件内容，按eswc后输入:wq推出并保存
2.nano *.txt
^G Help         ^O Write Out    ^W Where Is     ^K Cut          ^T Execute      ^C Location     M-U Undo        M-A Set Mark    M-] To Bracket
^X Exit         ^R Read File    ^\ Replace      ^U Paste        ^J Justify      ^/ Go To Line   M-E Redo        M-6 Copy        ^Q Where Was编辑文件，并且底部有快捷键显示。
###启动程序
1.python *.py运行python程序(base) whh@hzcu-hpct:~$ python app.py
[start] app.py is running, pid=848287
[hint] press Ctrl+C in foreground, or use kill PID from another terminal
[heartbeat] pid=848287 tick=1
[heartbeat] pid=848287 tick=2
[heartbeat] pid=848287 tick=3    ctrl+c中止
2.python *.py&使程序在后台运行
3.kill+pid结束进程使程序在后台运行
[signal] received signal 15, preparing to exit
(base) whh@hzcu-hpct:~$ [stop] app.py exited, pid=848797
4.bash启动脚本 bash