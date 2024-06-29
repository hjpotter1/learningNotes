#### 常用的命令

- ls 、ls -al 查看当前文件夹内容 -h 显示文件大小
- pwd 查看当前所在文件夹
- cd [目录名] 切换文件夹 cd - 最近两个文件夹切换
- cd ..
- touch [文件名] 创建文件
- mkdir [目录名] 创建目录
- rm [文件名] 删除指定文件 -rf， 循环，强制删除
- clear 清屏
- ctrl + shift + = 放大终端
- 敲 /xx 之后，按 Tab 键可以自动补全
- 查询终端命令帮助信息 ：命令 --help / man 命令， ex: mkdir --help
  - man 下操作：空格键 下一屏
  - b 回滚一屏
  - f 前滚一屏
  - q 退出
- cp 拷贝, -i 为覆盖文件前提示， -r 是文件夹递归
- mv 移动 -i 为覆盖文件前提示
- cat 文件 显示文件内容, -n 输出所有行编号， -b 对非空输出行编号
- more 文件名 分屏显示内容，使用类似 man
- grep 查找包含文本的搜索工具
  - -i 忽略大小写
  - -v 显示不包含匹配文本的所有行（相当于求反）
  - -n 显示匹配行及行号
  - 查找模式 行首： ^a 搜索以a 开头的行
  - 查找模式 行尾： ke$ 搜索以 ke 结尾的行
- echo 文字内容。
  - echo > 文件 输出覆盖文件内容
  - echo >> 文件 表示追加，追加到文件末尾
- | 管道，将前一查询结果同步到后一语句，如： ls -alh | more
- which 查看文件位置， ex : which passwd

#### 远程管理

##### 关机 / 重启

- shutdown -r now 重启
- shutdown now 立刻关机
- shutdown 20:25 定时关机
- shutdown + 10 十分钟后自动关机
- shutdown -c 取消之前的定时关机计划

##### 网络管理

- ifconfig 查看/配置计算机网卡配置信息 ex： ifconfig | grep inet
- ping ip地址 检测到目标ip地址链接是否正常

##### 远程登录和复制

- ssh [-p port] [-i 文件路径] user@remote 默认端口为22，ex: ssh root@12.2.2.2 -i /Users/xxx/xxx/xxx/xxx/xxx.pem -p 8888
- scp -P port 01.py user@remote:目录/文件 将文件复制到远程
- scp -P port user@remote:/目录/文件 o1.py 将远程文件复制到本地 文件夹需要 -r
- ssh-copy-id -p port user@remote 让远程服务器记住我们的公钥
- ssh 别名 即可登录，需要在 ~/.ssh/config 文件中设置

```
Host ecs
    HostName xxxx.com
    User root
    Port xxxx
    IdentityFile /xxxx/ecs_key.pem
```

##### 用户权限

- 文件权限
  - r read 读权限 4
  - w write 写权限 2
  - x excute 执行权限 1
- ls -l 显示示意

```
drwxr-xr-x 4 root root      4096 6月  11 10:21 _cache_dir
drwxr-xr-x 7 root root      4096 6月   5 21:20 abc
-rwxr-xr-x 1 root root         0 6月  15 14:29 a.txt
权限        硬链接数  拥有者 组 大小  时间   名称
权限细分说明：
目录   | 拥有者权限 |  组权限  |  其他用户权限 |
d         rwx         r-x         r-x     abc
-         rwx         r-x         r-x     a.txt 被赋值为可执行权限
```

- chmod 简单使用

  - chmod +/- r/w/x 文件名|目录 ex: chmod -rw a.txt 去除读写权限
  - chmod +x a.txt 设置执行权限， 会变成绿色
  - 如果一个目录没有可执行权限 x，则无法操作，不能cd ls
  - 如果一个目录没有可读权限，则无法 ls
  - 如果一个目录没有可写权限，则不能创建新文件

- 超级用户

  - su 是以另一用户身份执行
  - sudo 命令用其他身份执行，预设为root
  - 日常需要用普通用户

- 组管理

  - groupadd 组名 添加组
  - groupdel 组名 删除组
  - cat /etc/group 确认组信息
  - chgrp 组名 文件/目录名 修改文件/目录属性 -R 是递归执行，ex: chgrp -R dev python/

- 用户管理

  - useradd -m -g 组 新建用户名 添加新用户 ex: useradd -m -g dev frank

    - -m 自动创建用户home目录
    - -g 指定用户所在的组，否则会建立一个和同名的组

  - passwd 用户名 设置用户密码 如果是普通用户， 直接用 passwd 可以修改自己的账号密码 ,

    - 密码文件位于：/etc/passwd ex: cat /etc/passwd -n

    ```
    29	frank:x:1004:1004::/home/frank:/bin/bash
    ```

  - userdel -r 用户名 删除用户 ， -r 会自动删除用户home 目录

    - 如果忘记创建home 目录，最简单的方法是：1.删除用户 2.重写创建
    - 验证 cat /etc/passwd | grep 用户名/lisi

- 查看用户信息

  - id 用户名 查看用户信息 ， ex: id frank

  ```
  [root@ home]# id frank
  uid=1004(frank) gid=1004(dev) 组=1004(dev)
  [root@ home]# cat -n /etc/passwd | grep frank
      29	frank:x:1004:1004::/home/frank:/bin/bash
  说明：    
      29 为行号
      x 为密码是加密的
      1004 是用户id UID
      1004 是组id GID
      后面是家目录
  ```

  - 查看组信息

    ```
    cat -n /etc/group | grep dev
       47	dev:x:1004:
    id
      uid=0(root) gid=0(root) 组=0(root)
    ```

  - who 查看当前所有登录的用户列表

  - whoami 查看当前登录用户的账户名

- 修改用户组

  - -g 主组：usermode -g 组 用户名
  - -G 附加组：usermod -G 组 用户名

  ```
  [root@ home]#     cat -n /etc/group | grep root
     1	root:x:0:
  [root@ home]# usermod -G root frank
  [root@ home]#     cat -n /etc/group | grep root
     1	root:x:0:frank
  [root@ home]# cat -n /etc/passwd | grep frank
    29	frank:x:1004:1004::/home/frank:/bin/bash
  ```

  - 主组是创建用户时候指定的，附加组是在 etc/group 中添加的，用于指定用户的附加权限。
  - 可以将用户放入到 sudo 的附加组中

##### 文件权限

- chown 修改拥有者
  - chown 用户名 文件名| 目录名
- chgrp 修改组
  - chgrp -R 组名 文件名| 目录名
- chmod 修改权限
  - chmod -R 755 文件名| 目录名 755 对应的是：拥有者/组/和其他用户的权限
  - chmod +/- rwx 文件名|目录名
  - 7： r+w+x 4+2+1, R=4 W=2 X=1 都是算出来的， 常用的有 755、640、777

#### 系统命令

- date 日期

- cal 日历

- 查看 CentOS 系统版本： cat /etc/redhat-release

- df -h 磁盘剩余空间

  ```
  文件系统        容量  已用  可用 已用% 挂载点
  /dev/vda1        40G  7.6G   30G   21% /
  devtmpfs        1.9G     0  1.9G    0% /dev
  tmpfs           1.9G     0  1.9G    0% /dev/shm
  tmpfs           1.9G  472K  1.9G    1% /run
  tmpfs           1.9G     0  1.9G    0% /sys/fs/cgroup
  tmpfs           380M     0  380M    0% /run/user/1001
  tmpfs           380M     0  380M    0% /run/user/0
  ```

- du -h 目录名 显示目录下的占用信息

##### 进程信息

- ps aux 查看进程状态的详细信息
- top 动态显示运行中的进程并排序
- kill -9 进程代号 -9为强制终止

##### 其他命令

- find 查找文件

  - find -name "*1*" 搜索当前目录下文件名包含 xx 的文件
  - find -name "*.txt" 搜索当前目录下文件名扩展名为.txt 的文件
  - find -name "1*" 搜索当前目录下文件以1开头的文件

- ln 软连接

  - ln -s 被链接的源文件 链接文件 就是windows 的快捷方式， 没有 -s 则是硬链接，不这么使用。

  ```
  touch a.py
  echo #!/usr/bin/python >> a.py
  echo print(123) >> a.py
  ./a.py
      123
  ln -s a.py   p
  ./p 
      123
  ls -l
  总用量 287444
  -rwxr-xr-x 1 root root        29 6月  15 15:55 a.py
  lrwxrwxrwx 1 root root         4 6月  15 15:55 p -> a.py
  ```

- tar 打包和压缩

  - tar -cvf 打包文件.tar 被打包的文件/路径... c 生成档案文件，创建打包文件
  - tar -xvf 打包文件.tar x 解开档案文件 v 列出过程，显示进度 f 指定文件名称 f 后一定是 .tar 文件
  - tar 只打包，但不压缩，用 gzip 进行压缩 tar 后的文件，扩展名为 xxx.tar.gz
  - 在 tar 命令中添加 -z 可以调用 gzip 实现压缩和解压。 ex: tar -zcvf xxx.tar.gz 被打包路径
  - 解包可以指定路径 -C 目标路径： tar -zxvf 打包文件.tar -C 目标路径
  - bzip2 是 tar 包 被压缩了。 将 z 换成 j 就行了

- 软件安装 pip 、yum
