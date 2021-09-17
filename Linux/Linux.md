# Linux账户

root密码：N331150871
主机名：AppleTree
普通用户：SuperCoder（XShell中小写登录）
密码：N331150871
root用户：root
密码：N331150871
普通用户2：tom
密码：N331150871

1. 单机虚拟机屏幕或Ctrl+G(不太会用)即可 使鼠标活跃在 虚拟机中。CTRL+alt 释放鼠标。

# 笔记

1. ls -lh /root/hello.txt    ：以人能阅读的方式显示文件信息。
2. zip -r myhome.zip /home/* 指的是只将home文件夹下的文件压缩，不包含home文件夹

# 指令

1. gcc -v ：查看是否安装gcc。安装标志：出现版本信息
2. ifconfig ：查看ip地址。inet 后面的数字
3. ping(windows平台也适用) ：检验两个ip（设备）能否链接通畅
4. su - root ：切换成系统管理员身份。 su - 用户名 ：切换到用户名所指的用户（低\同权限到高权限用户需要输入密码。反之不需要）
5. logout 注销用户 ：如果当前账户是由一个账户切换过来的，则logout会返回之前的账户。如果当前账户是第一次登录的账户，则logout会退出链接（XShell中）。<img src="Linux.assets/image-20210917014623684.png" alt="image-20210917014623684" style="zoom:50%;" />
   logout 在图形界面中无效，适用于 运行级别 3(非图形界面)。应该用exit，exit退出终端，无法退出用户。
6. 

# 远程指令

1. reboot ：重启系统
2. vim/vi + 文档名 ：编辑文档，如果没有该文档就会创建一个。
3. 只输入 shutdown ：代表 shutdown -h 1 
4. shutdown -h 1 ：向所有远程登录Linux系统的用户发送通知："hello, 1分钟后会关机"
5. passwd 不输入任何用户名 ：默认是修改当前登录用户的密码 只能修改当前用户密码或依靠root修改其他用户密码
6. 用户删除不能删除自己，也不能删除别的用户。只能靠root用户删除。而且依靠切换用户的情况下，之前的用户并没有完全退出。所以也不要删除之前登录的用户。

# Vim命令

![vim键盘图](https://img-blog.csdn.net/20170325161428570?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc2luYXRfMzYxMDEzNTQ=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

1. i 、a、o、r ：进入编辑模式
2. esc ：返回一般模式
   1. 一般模式下的命令：
      1. 复制 ：yy 、5yy 。p 粘贴
      2. 删除 ：dd、4dd 。 
      3. G ：最末行   g ：最首行
      4. u ：撤销
      5. 20 + shift +g ：快速定位到20行
3. " : "、” / “ ：进入命令模式
   1. 命令模式下的命令： 
      1. wq ：保存退出、q ：退出 、q! ：强制退出
      2. 直接输入 关键字 ：回车-查找 、 输入 n - 查找下一个
      3. set nu ：显示行数  set nonu ：关闭行数
      4. 