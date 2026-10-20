## pwd

### 预期效果

显示当前工作目录

### 实际效果

```text
/home/jy
```

## mkdir .ssh

### 预期效果

创建.ssh目录

### 实际效果

*无回显*

`ls`表明创建成功

## vim .ssh/authorized_keys

### 预期效果

用vim编辑器打开`.ssh/authorized_keys`，以便写入ssh公钥

### 实际效果

> 交互式界面，不便记录

## rm *.md

### 预期效果

删除所有当前目录md文档，这里用来删除已弃用的Slurm文档

### 实际效果

*无回显*

`ls`表明创建成功

## ll

### 预期效果

等价于`ls --color=auto -alF`，以彩色详细信息列出当前目录所有文件

### 实际效果

```text
total 44
drwxr-x---  6 jy   jy   4096 Oct 19 09:11 ./
drwxr-xr-x 34 root root 4096 Oct 15 16:54 ../
-rw-------  1 jy   jy    345 Oct 19 09:11 .bash_history
-rw-r--r--  1 jy   jy    220 Jan  7  2022 .bash_logout
-rw-r--r--  1 jy   jy   3772 Oct 19 09:09 .bashrc
drwx------  2 jy   jy   4096 Oct 15 21:08 .cache/
drwxr-xr-x  5 jy   jy   4096 Oct 15 21:29 .config/
drwx------  3 jy   jy   4096 Oct 15 21:08 .local/
-rw-r--r--  1 jy   jy    807 Jan  7  2022 .profile
drwxrwxr-x  2 jy   jy   4096 Oct 15 21:27 .ssh/
-rw-------  1 jy   jy   1812 Oct 19 09:11 .viminfo
```

## vim .bashrc

### 预期效果

用vim编辑器打开`.bashrc`，这里用于关闭`ls`的自动颜色显示（注释掉alias ls='ls --color=auto'）

### 实际效果

> 交互式界面，不便记录

## source .bashrc

### 预期效果

用.bashrc刷新shell

### 实际效果

无效果
> source的作用是把<file>中的内容“叠加”到当前shell，不会刷新shell。而`alias ls="ls --color=auto"`已经在登录的时候执行过了

## 这里进行了一次重新登录

## alias

### 预期效果

列出所有当前正在生效的alias

### 实际效果

```text
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
```

## btop

### 预期效果

打开`btop`性能监视器

### 实际效果

```text
Command 'btop' not found, but can be installed with:
snap install btop  # version 1.4.7, or
apt  install btop  # version 1.2.3-2
See 'snap info btop' for additional versions.
```

## htop

### 预期效果

打开`htop`性能监视器

### 实际效果

> 交互式界面，不便展示

## neofetch

### 预期效果

显示系统信息

### 实际效果

```text
            .-/+oossssoo+/-.               jy@hzcu-hpct 
        `:+ssssssssssssssssss+:`           ------------ 
      -+ssssssssssssssssssyyssss+-         OS: Ubuntu 22.04.5 LTS x86_64 
    .ossssssssssssssssssdMMMNysssso.       Host: NF5280-M7-A0-R0-00 0 
   /ssssssssssshdmmNNmmyNMMMMhssssss/      Kernel: 5.15.0-191-generic 
  +ssssssssshmydMMMMMMMNddddyssssssss+     Uptime: 38 days, 22 hours, 40 mins 
 /sssssssshNMMMyhhyyyyhmNMMMNhssssssss/    Packages: 2442 (dpkg), 8 (snap) 
.ssssssssdMMMNhsssssssssshNMMMdssssssss.   Shell: bash 5.1.16 
+sssshhhyNMMNyssssssssssssyNMMMysssssss+   Resolution: 1024x768 
ossyNMMMNyMMhsssssssssssssshmmmhssssssso   Terminal: /dev/pts/1 
ossyNMMMNyMMhsssssssssssssshmmmhssssssso   CPU: Intel Xeon Gold 6430 (128) @ 3.400GHz 
+sssshhhyNMMNyssssssssssssyNMMMysssssss+   GPU: NVIDIA 1f:00.0 NVIDIA Corporation Device 2684 
.ssssssssdMMMNhsssssssssshNMMMdssssssss.   GPU: NVIDIA ac:00.0 NVIDIA Corporation Device 2684 
 /sssssssshNMMMyhhyyyyhdNMMMNhssssssss/    Memory: 241440MiB / 515575MiB 
  +sssssssssdmydMMMMMMMMddddyssssssss+
   /ssssssssssshdmNNNNmyNMMMMhssssss/                              
    .ossssssssssssssssssdMMMNysssso.                               
      -+sssssssssssssssssyyyssss+-
        `:+ssssssssssssssssss+:`
            .-/+oossssoo+/-.

```

## cat /proc/meminfo

### 预期效果

查看内存信息

### 实际效果

```text
MemTotal:       527949400 kB
MemFree:        16857208 kB
MemAvailable:   277270780 kB
Buffers:         7764128 kB
Cached:         390914092 kB
SwapCached:        12172 kB
Active:         147918252 kB
Inactive:       337174044 kB
Active(anon):   40611136 kB
Inactive(anon): 197421744 kB
Active(file):   107307116 kB
Inactive(file): 139752300 kB
Unevictable:       27828 kB
Mlocked:           27828 kB
SwapTotal:       8388604 kB
SwapFree:        7639036 kB
Dirty:               220 kB
Writeback:             0 kB
AnonPages:      86430044 kB
Mapped:         152286184 kB
Shmem:          151610004 kB
KReclaimable:   16779424 kB
Slab:           20488044 kB
SReclaimable:   16779424 kB
SUnreclaim:      3708620 kB
KernelStack:      116352 kB
PageTables:       558448 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:    272363304 kB
Committed_AS:   247506828 kB
VmallocTotal:   13743895347199 kB
VmallocUsed:     1948268 kB
VmallocChunk:          0 kB
Percpu:           704000 kB
HardwareCorrupted:     0 kB
AnonHugePages:  49246208 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
FileHugePages:         0 kB
FilePmdMapped:         0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
DirectMap4k:    27376204 kB
DirectMap2M:    325617664 kB
DirectMap1G:    185597952 kB
```

## echo "ping 127.0.0.1" > example

### 预期效果

在当前目录创建一个名为`example`，内容为`ping 127.0.0.1`的文件

### 实际效果

*无回显（成功）*

## chmod 777 example

### 预期效果

把`example`权限修改为所有人可读可写可执行

### 实际效果

*无回显（成功）*

## ./example

### 预期效果

执行`./example`

### 实际效果

```text
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.081 ms
64 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.043 ms
64 bytes from 127.0.0.1: icmp_seq=3 ttl=64 time=0.032 ms
64 bytes from 127.0.0.1: icmp_seq=4 ttl=64 time=0.036 ms
64 bytes from 127.0.0.1: icmp_seq=5 ttl=64 time=0.063 ms
64 bytes from 127.0.0.1: icmp_seq=6 ttl=64 time=0.047 ms
64 bytes from 127.0.0.1: icmp_seq=7 ttl=64 time=0.028 ms
64 bytes from 127.0.0.1: icmp_seq=8 ttl=64 time=0.030 ms
^C
--- 127.0.0.1 ping statistics ---
8 packets transmitted, 8 received, 0% packet loss, time 7147ms
rtt min/avg/max/mdev = 0.028/0.045/0.081/0.017 ms
```
> 注：ping不会自动停止，而我没有设置timeout，所以这里用ctrl+C终止程序

## echo $PATH

### 预期效果

打印`PATH`环境变量

### 实际效果

```text
/opt/anaconda3/bin:/opt/anaconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

## du -sh ../*

### 预期效果

查看上级目录的所有子目录的磁盘占有情况

### 实际效果

```text
4.0K    ../bzh
du: cannot read directory '../cyl': Permission denied
4.0K    ../cyl
du: cannot read directory '../cyp': Permission denied
4.0K    ../cyp
du: cannot read directory '../cyx': Permission denied
4.0K    ../cyx
du: cannot read directory '../cz/.nv': Permission denied
du: cannot read directory '../cz/.local/share': Permission denied
du: cannot read directory '../cz/.cache': Permission denied
du: cannot read directory '../cz/.vscode-server/extensions': Permission denied
du: cannot read directory '../cz/.vscode-server/data': Permission denied
du: cannot read directory '../cz/snap': Permission denied
2.0G    ../cz
du: cannot read directory '../fml': Permission denied
4.0K    ../fml
du: cannot read directory '../gbh/.java/.userPrefs': Permission denied
du: cannot read directory '../gbh/.nv': Permission denied
du: cannot read directory '../gbh/.pki': Permission denied
du: cannot read directory '../gbh/.codex/tmp/arg0': Permission denied
du: cannot read directory '../gbh/.config/Code/agent-host/local-endpoint': Permission denied
du: cannot read directory '../gbh/.config/procps': Permission denied
du: cannot read directory '../gbh/.config/google-chrome-for-testing': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/extensions': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1787377622898_731824/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1787218552752_419022/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1787551964944_206980/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1787163183422_614223/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1786871551890_621794/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1787065887419_770214/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1787731673335_419111/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1788329275202_430521/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1787460301817_912302/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/manager-logs/1787731510448_819319/perf_sdk': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3468554/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3426007/ee4fa80/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3172417/1ef3be2/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3256267/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1311881/09a1e8c/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2143368/6a939b0/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1982957/47a8a0b/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1577795/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2320542/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/37564/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1574299/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/765164/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3633315/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/31065/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2521490/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3754401/0a3ec60/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1471187/2c00292/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2252197/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2043952/47a8a0b/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3085247/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1274007/6a939b0/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2564376/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3925294/3a8e351/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2306127/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/337345/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3479014/5ef571c/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1677035/6a939b0/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2233915/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3744278/3a8e351/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1883430/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3057540/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/815164/2c00292/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2262950/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3609708/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2067922/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3974280/3a8e351/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2305926/ee4fa80/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/365523/2b112f4/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1713150/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1354687/98a341e/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3112883/98a341e/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3050721/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3599626/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/810062/5ef571c/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/948803/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/332958/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3444891/ee4fa80/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3976904/3a8e351/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2341064/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/340494/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/51135/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/315333/1bf48bf/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/841214/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3485509/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/4049559/2b112f4/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3472768/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3025300/bb6e8bb/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3030319/bb6e8bb/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/4161678/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3878163/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3010463/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3483245/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2259322/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1643341/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2332822/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2422053/5ef571c/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/1660968/5ef571c/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/4143747/0a3ec60/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3266584/e30d15c/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3177764/09a1e8c/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3122118/4de6fa3/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3027955/bb6e8bb/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2256876/fff89fe/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2346258/ee4fa80/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/3761699/6754090/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/socks/2072398/98a341e/aha': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/Crashpad/new': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/Crashpad/attachments': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/Crashpad/completed': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/ai-agent/command-execution': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/data': Permission denied
du: cannot read directory '../gbh/.trae-cn-server/network-service/ttnet': Permission denied
du: cannot read directory '../gbh/.intel/vtune/settings': Permission denied
du: cannot read directory '../gbh/.intel/vtune/report': Permission denied
du: cannot read directory '../gbh/.intel/vtune/analysis_type': Permission denied
du: cannot read directory '../gbh/.intel/vtune/connection_type': Permission denied
du: cannot read directory '../gbh/.intel/vtune/target_type': Permission denied
du: cannot read directory '../gbh/.intel/vtune/viewpoint': Permission denied
du: cannot read directory '../gbh/.claude': Permission denied
du: cannot read directory '../gbh/.trae-server/extensions': Permission denied
du: cannot read directory '../gbh/.trae-server/trae-sockets/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2997954/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/611403/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1682078/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3526906/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2956656/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1222577/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3380491/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/4093088/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/427067/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/392001/fb47834/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/4164826/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3846484/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2467207/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2212975/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2302600/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/394141/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3045095/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2900979/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/525076/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3743742/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3407135/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/164790/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1151456/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1359021/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1563743/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3774820/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/197057/fb47834/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2092156/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3443555/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1826210/475a2f5/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/200199/fb47834/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1963258/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1677885/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1079570/fb47834/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2978295/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1272809/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1241578/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/782812/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2999767/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3039920/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2698433/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2604204/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3615307/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3001845/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3428653/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/20970/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3131215/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1747690/fb47834/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1259242/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/592695/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2898413/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/221352/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/324266/475a2f5/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2950994/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/668573/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/850dc8d/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/873696/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3228099/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2830324/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1537747/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2538624/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1254406/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2567802/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1521750/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/9492afc/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3850446/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2114134/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3778882/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1439016/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3713639/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1721181/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/c68ec30/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/74529d0/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1335547/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/271585/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/4297/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3095865/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/4189423/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/288499/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3532062/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/660065/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3452644/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/853434/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2921626/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2806408/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/720245/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/474562/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3948730/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3600992/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3062764/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1410711/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2199209/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1815425/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/752065/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/857724/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/502047/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/851482/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3353378/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3938620/fb47834/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1684133/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1344298/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2250990/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3942761/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3179301/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2272140/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3036623/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1431189/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/102f37e/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/246898/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/813474/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/4115583/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/635528/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/4100343/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1516494/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/557285/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/120fb78/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2898574/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3195195/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/2961458/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/62b10a8/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1809597/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1267221/0f408c1/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1275951/1f480cb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1409383/475a2f5/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/3231875/cce6734/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/socks/1617660/224f2fb/aha': Permission denied
du: cannot read directory '../gbh/.trae-server/data': Permission denied
du: cannot read directory '../gbh/.trae-server/network-service/ttnet': Permission denied
du: cannot read directory '../gbh/.vscode-server/extensions': Permission denied
du: cannot read directory '../gbh/.vscode-server/cli': Permission denied
du: cannot read directory '../gbh/.vscode-server/data': Permission denied
du: cannot read directory '../gbh/snap': Permission denied
du: cannot read directory '../gbh/.copilot': Permission denied
du: cannot read directory '../gbh/.antigravity-server/extensions': Permission denied
du: cannot read directory '../gbh/.antigravity-server/data': Permission denied
83G     ../gbh
du: cannot read directory '../gh0st': Permission denied
4.0K    ../gh0st
du: cannot read directory '../gyh': Permission denied
4.0K    ../gyh
du: cannot read directory '../hur/.windsurf-server/extensions': Permission denied
du: cannot read directory '../hur/.windsurf-server/data': Permission denied
du: cannot read directory '../hur/.cursor-server/extensions': Permission denied
du: cannot read directory '../hur/.cursor-server/data': Permission denied
du: cannot read directory '../hur/.ssh': Permission denied
du: cannot read directory '../hur/.nv': Permission denied
du: cannot read directory '../hur/.oneapi-cli': Permission denied
du: cannot read directory '../hur/.local/share/nvim': Permission denied
du: cannot read directory '../hur/.local/state': Permission denied
du: cannot read directory '../hur/.cache': Permission denied
du: cannot read directory '../hur/.config': Permission denied
du: cannot read directory '../hur/.intel/vtune/settings': Permission denied
du: cannot read directory '../hur/.intel/vtune/report': Permission denied
du: cannot read directory '../hur/.intel/vtune/analysis_type': Permission denied
du: cannot read directory '../hur/.intel/vtune/connection_type': Permission denied
du: cannot read directory '../hur/.intel/vtune/target_type': Permission denied
du: cannot read directory '../hur/.intel/vtune/viewpoint': Permission denied
du: cannot read directory '../hur/.ipython/profile_default/pid': Permission denied
du: cannot read directory '../hur/.ipython/profile_default/security': Permission denied
du: cannot read directory '../hur/.vscode-server/extensions': Permission denied
du: cannot read directory '../hur/.vscode-server/data': Permission denied
du: cannot read directory '../hur/snap': Permission denied
16G     ../hur
172K    ../jy
du: cannot read directory '../lgj': Permission denied
4.0K    ../lgj
du: cannot read directory '../ljc/.nv': Permission denied
du: cannot read directory '../ljc/.local/share/containers': Permission denied
du: cannot read directory '../ljc/.local/share/jupyter/runtime': Permission denied
du: cannot read directory '../ljc/.cache': Permission denied
du: cannot read directory '../ljc/work/作业2': Permission denied
du: cannot read directory '../ljc/.pki': Permission denied
du: cannot read directory '../ljc/.config/libreoffice/4': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/extensions': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/manager-logs/1785497361783_247149/perf_sdk': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/manager-logs/1789824334864_503514/perf_sdk': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/manager-logs/1785506918219_310137/perf_sdk': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/trae-sockets/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/381274/78ec6e0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/4144579/6754090/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2864599/d9ad807/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1617606/4963c15/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2602869/18a1ac5/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2202892/4bd8472/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1859446/18a1ac5/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1177790/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2116856/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2119852/54012f4/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3671364/4963c15/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2320888/73aef0e/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1986663/78ec6e0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3887758/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2158935/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/587869/f045835/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3553956/f82b86c/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3323783/e0cee49/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/640474/78ec6e0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1095523/2a19268/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2945463/73aef0e/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2749896/4bd8472/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/41859/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3252073/e0cee49/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/9492afc/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1925907/b1df1d6/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1845199/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3437104/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2408832/ab4cfd8/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/184625/78ec6e0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3393988/78ec6e0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/120054/3a8e351/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3417634/78ec6e0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/792594/54012f4/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/575444/54012f4/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2050230/2a19268/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2077109/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/239932/1fae916/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1048357/2a19268/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2407060/46532f6/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2357623/4963c15/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2913461/2a19268/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/2659432/4011fbb/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/572328/54012f4/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/126369/428b344/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3219711/6a939b0/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/483237/4963c15/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1491741/d017801/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/62b10a8/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3858542/4963c15/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/3813422/4963c15/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/socks/1564860/bae5b29/aha': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/Crashpad/new': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/Crashpad/attachments': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/Crashpad/completed': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/ai-agent/command-execution': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/data': Permission denied
du: cannot read directory '../ljc/.trae-cn-server/network-service/ttnet': Permission denied
du: cannot read directory '../ljc/.ipython/profile_default/pid': Permission denied
du: cannot read directory '../ljc/.ipython/profile_default/security': Permission denied
du: cannot read directory '../ljc/.vscode-server': Permission denied
50G     ../ljc
du: cannot read directory '../ljw/.nv': Permission denied
du: cannot read directory '../ljw/.cache': Permission denied
du: cannot read directory '../ljw/.config': Permission denied
du: cannot read directory '../ljw/.intel/vtune/settings': Permission denied
du: cannot read directory '../ljw/.intel/vtune/report': Permission denied
du: cannot read directory '../ljw/.intel/vtune/analysis_type': Permission denied
du: cannot read directory '../ljw/.intel/vtune/connection_type': Permission denied
du: cannot read directory '../ljw/.intel/vtune/target_type': Permission denied
du: cannot read directory '../ljw/.intel/vtune/viewpoint': Permission denied
du: cannot read directory '../ljw/.vscode-server/extensions': Permission denied
du: cannot read directory '../ljw/.vscode-server/data': Permission denied
7.6G    ../ljw
du: cannot read directory '../llk': Permission denied
4.0K    ../llk
du: cannot read directory '../llm/milvus/volumes/milvus/etcd': Permission denied
du: cannot read directory '../llm/.cache': Permission denied
97G     ../llm
du: cannot read directory '../lost+found': Permission denied
16K     ../lost+found
du: cannot read directory '../lyj/.java/.userPrefs': Permission denied
du: cannot read directory '../lyj/.nv': Permission denied
du: cannot read directory '../lyj/.local/share/jupyter/runtime': Permission denied
du: cannot read directory '../lyj/.cache': Permission denied
du: cannot read directory '../lyj/.config/procps': Permission denied
du: cannot read directory '../lyj/.config/htop': Permission denied
du: cannot read directory '../lyj/.config/glib-2.0': Permission denied
du: cannot read directory '../lyj/.ipython/profile_default/pid': Permission denied
du: cannot read directory '../lyj/.ipython/profile_default/security': Permission denied
du: cannot read directory '../lyj/.vscode-server': Permission denied
17G     ../lyj
34G     ../public
du: cannot read directory '../qsz': Permission denied
4.0K    ../qsz
du: cannot read directory '../qwj': Permission denied
4.0K    ../qwj
du: cannot read directory '../scd/.ssh': Permission denied
du: cannot read directory '../scd/.nv': Permission denied
du: cannot read directory '../scd/.local/share': Permission denied
du: cannot read directory '../scd/.cache': Permission denied
du: cannot read directory '../scd/.codex/tmp/arg0': Permission denied
du: cannot read directory '../scd/.config/procps': Permission denied
du: cannot read directory '../scd/.vscode-server/extensions': Permission denied
du: cannot read directory '../scd/.vscode-server/data': Permission denied
du: cannot read directory '../scd/snap': Permission denied
du: cannot read directory '../scd/.copilot': Permission denied
73G     ../scd
du: cannot read directory '../syn/.nv': Permission denied
du: cannot read directory '../syn/.local/share': Permission denied
du: cannot read directory '../syn/.cache': Permission denied
du: cannot read directory '../syn/.config': Permission denied
du: cannot read directory '../syn/.intel/vtune/settings': Permission denied
du: cannot read directory '../syn/.intel/vtune/report': Permission denied
du: cannot read directory '../syn/.intel/vtune/analysis_type': Permission denied
du: cannot read directory '../syn/.intel/vtune/connection_type': Permission denied
du: cannot read directory '../syn/.intel/vtune/target_type': Permission denied
du: cannot read directory '../syn/.intel/vtune/viewpoint': Permission denied
du: cannot read directory '../syn/.vscode-server/extensions': Permission denied
du: cannot read directory '../syn/.vscode-server/data': Permission denied
du: cannot read directory '../syn/.copilot': Permission denied
29G     ../syn
du: cannot read directory '../wcy': Permission denied
4.0K    ../wcy
du: cannot read directory '../whh': Permission denied
4.0K    ../whh
44K     ../wsy
du: cannot read directory '../wyt': Permission denied
4.0K    ../wyt
4.0K    ../xn
du: cannot read directory '../xxn/.nv': Permission denied
du: cannot read directory '../xxn/.local/share/containers': Permission denied
du: cannot read directory '../xxn/.local/share/nano': Permission denied
du: cannot read directory '../xxn/.local/state/pipa-agent': Permission denied
du: cannot read directory '../xxn/.qoder/enterprise': Permission denied
du: cannot read directory '../xxn/.cache': Permission denied
du: cannot read directory '../xxn/.qoder-server/extensions': Permission denied
du: cannot read directory '../xxn/.qoder-server/data': Permission denied
du: cannot read directory '../xxn/.pki': Permission denied
du: cannot read directory '../xxn/.codex': Permission denied
du: cannot read directory '../xxn/.config': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/extensions': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/1708857/78ec6e0/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3258350/4011fbb/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3276244/19157aa/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/2761269/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/667253/008e1c7/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/1894560/4011fbb/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/260177/18a1ac5/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/4097554/29284ef/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/4134919/29284ef/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3842865/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3862472/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3150778/19157aa/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/665705/008e1c7/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/1556163/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/54919/e30d15c/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/2624111/fff89fe/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/4019181/fff89fe/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3868225/18a1ac5/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/2065745/fff89fe/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3393411/4011fbb/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/582144/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/969589/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3047828/fff89fe/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3934640/4011fbb/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/1709803/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/159262/29284ef/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/616736/fff89fe/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3360324/73aef0e/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/408939/d9ad807/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/2067768/fff89fe/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/4092668/29284ef/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/1707370/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/624887/fff89fe/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/3405776/73aef0e/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/2622636/fff89fe/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/472744/3a8e351/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/socks/954200/29284ef/aha': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/Crashpad/new': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/Crashpad/attachments': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/Crashpad/completed': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/data': Permission denied
du: cannot read directory '../xxn/.trae-cn-server/network-service/ttnet': Permission denied
du: cannot read directory '../xxn/.intel/vtune/settings': Permission denied
du: cannot read directory '../xxn/.intel/vtune/report': Permission denied
du: cannot read directory '../xxn/.intel/vtune/analysis_type': Permission denied
du: cannot read directory '../xxn/.intel/vtune/connection_type': Permission denied
du: cannot read directory '../xxn/.intel/vtune/target_type': Permission denied
du: cannot read directory '../xxn/.intel/vtune/viewpoint': Permission denied
du: cannot read directory '../xxn/.ipython/profile_default/pid': Permission denied
du: cannot read directory '../xxn/.ipython/profile_default/security': Permission denied
du: cannot read directory '../xxn/.claude': Permission denied
du: cannot read directory '../xxn/.vscode-server/extensions': Permission denied
du: cannot read directory '../xxn/.vscode-server/cli': Permission denied
du: cannot read directory '../xxn/.vscode-server/data': Permission denied
du: cannot read directory '../xxn/snap': Permission denied
du: cannot read directory '../xxn/.copilot': Permission denied
du: cannot read directory '../xxn/.kimi-code': Permission denied
212G    ../xxn
du: cannot read directory '../yb': Permission denied
4.0K    ../yb
du: cannot read directory '../yyt/.ssh': Permission denied
du: cannot read directory '../yyt/.local': Permission denied
du: cannot read directory '../yyt/.cache': Permission denied
du: cannot read directory '../yyt/.config/Code/agent-host/local-endpoint': Permission denied
du: cannot read directory '../yyt/.config/libvirt': Permission denied
du: cannot read directory '../yyt/.config/htop': Permission denied
du: cannot read directory '../yyt/.vscode-server': Permission denied
du: cannot read directory '../yyt/.copilot': Permission denied
248G    ../yyt
du: cannot read directory '../zgb': Permission denied
4.0K    ../zgb
```