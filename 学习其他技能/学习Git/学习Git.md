# 命令

## 零碎命令

1. git version    查看git的版本
   1. git --version 也行，具体什么原因暂且不知道
2. 7.7.07 介绍mac的操作
3. ctrl+l = clean  清屏

## 版本控制

### 用git管理文件夹大体步骤

1. 进入工作区）
2. 初始化工作区
3. 进行文件管理
4. 生成版本

### 个人信息配置

- 配置用户名、邮箱【一次即可】

```
git config --global user.email "邮箱"--引号、横线可省略
git config --global user.name "用户名"--引号、横线可省略
```

### 具体操作

1. 进入工作区

2. 初始化

   1. 命令：git init
   2. 结果：生成.git文件
      1. 拓展：.git 文件中存储着该文件夹下的配置和版本信息

3. 管理过程

   1. 检测文件夹的状态

      1. 命令：git status
      2. 现象：
         1. 红色文件名-工作区中新增的或修改的
         2. 绿色文件名-提交至暂存区的

   2. 筛选需要工作区的文件

      1. 命令：git add 文件名、git add . --全部文件夹被提交至暂存区
         1. 也可以加*变成通配符---暂时不知道干嘛的
      2. 效果：被添加到暂存区的文件名变绿

   3. 提交至版本库并生成版本

      1. 命令：git commit -m ' 信息'  也可以是引号 " 信息 "

   4. 查看版本信息

      1. 命令：git log

   5. 回滚版本

      1. 回滚一次版本

         ```
         git reset --hard 版本号
         ```

         - 版本号在版本信息中的commit后面

         ![](学习Git.assets/回滚版本号.png)

      2. 回滚到消失的版本（因为回滚所以在git log中查看不到）

         - 此时版本号需要另一个命令查找
           - 命令：git reflog

         1. 回滚命令
            1. git reset --hard 版本号
               - 版本号在版本信息的最前面

         ![](学习Git.assets/回滚到回滚前的.png)

# 紧急bug修复

1. 10.10理论讲解
2. 操作命令
   1. 查看分支
      1. 命令：git branch
   2. 创建分支
      1. 命令：git branch dev 可加 ' ' 
         1. dev指的是development，即开发的分支
      2. 注意：
         1. 此时分支dev是处在master的分支上创建的分支，且dev指向了当前master上最新版本
   3. 切换分支
      1. 命令：git checkout dev
      2. 切换分支就是切换一个环境，在dev分支中开发时不影响master分支上的内容
         1. 示例：从mas git@github.com:SuperCoder1999/Spring5_sgg.gitter分支切换到dev分支进行修改，再生成版本，此时查看历史版本，会发现此次版本在dev分支上。切换回master分支，打开文件，文件没有被修改
   4. 合并分支（注意需要在master上-即在需要修改的分支上获取修改内容）
      1. 命令：git merge 分支名
   5. 删除分支
      1. 命令：git branch -d bug
3. 修复bug具体操作
   1. 在master分支上创建一个bug分支（dev分支上已经形成版本的内容就会被暂且搁置。具体需不需要在切换分支前生成版本暂时不清楚）
      1. 命令：git branch bug
   2. 切换到bug分支上，修改bug分支目前的文件（文件状态和master上（最新版本）一样）
   3. 切换回master分支，合并。
      1. 命令：git merge bug
   4. 删除分支
4. 继续开发新功能
   1. 此时发现，dev分支下的文件中没有修复bug的内容。不用在意，这条分支仅仅用于开发新功能。（如果必须在修复了bug的基础上进行开发，可在dev分支上合并master即可）
   2. 继续开发，直到完成
5. 将开发的内容合并到master
   1. 切换回master分支  git checkout master
   2. 合并  git merge dev
   3. 此时会产生冲突---有个软件能解决冲突
      1. 原因是因为，master分支已经被修改了，和dev当时被创建时不一样。也或许因为，dev修改的那行在master中也修改了，此时不确定哪一个是最新版本。
      2. 冲突会在文件中具体显示，手动修改即可。
         1. 将冲突的地方进行修改
         2. 再将出现冲突标记的标记语言删除
      3. 解决完冲突，进行git add . ----git commit -m ’结局冲突‘ 

### git 操作对应专业术语

1. 6.6.06视频中介绍

![](学习Git.assets/8.08 git三大区域.jpg)

图片中checkout的文字说明是：对修改的文件有效

- 举例git checkout 从工作区红色返回已控制状态

  ```
  git checkout --文件名
  ```

  - 效果：修改后的文件又回到已经被管理时的样子。仅仅在工作区内切换

- 举例git reset HEAD

  ```
  git reset HEAD 文件名
  ```

  - 效果：从暂存区（绿色）状态回到工作区（红色）状态



# 工作流

1. 工作规范：至少有两个分支
   1. master---永远是已经确定的版本
   2. dev--在上面开发
2. 





---

# 使用过程中的问题解决

1. git软件的默认分支名是master,导致git push 后在remote上创建了master分支.
   解决方法:1.要么在装git时,默认名称更改为main,要么使用git branch -m master main更改已经存在的名称

2. 创建新仓库后的命令

   ```
   echo "# test2" >> README.md
   git init
   git add README.md
   git commit -m "first commit"
   git branch -M main
   git remote add origin git@github.com:SuperCoder1999/test2.git
   git push -u origin main
   
   git remote add origin git@github.com:SuperCoder1999/LanQiaoCup.git
   git branch -M main
   git push -u origin main
   ```

---

3. 如何在新电脑上，操作已经存在的数据库：

   > 一：使用ssh
   > (前提，初始化ssh：先让本地公钥，被github认可，之后可以用ssh的链接，免密操作以下步骤)
   > 1.git init
   > 初始化 本地库
   > 2.$ git pull git@github.com:SuperCoder1999/LanQiaoCup.git(https链接不能用于pull)
   > 从远程库 拉代码，（必须要的）(这里也可以用git clone,之后的操作和下面一样)
   >
   > 3.git remote add origin git@github.com:SuperCoder1999/LanQiaoCup.git
   > 获取远程库操作权限
   > 4.git push --set-upstream origin main
   > 设置 本地库上传 的分支(master,看remote上的默认分支名进行更改)
   > 5.git add . ->git commit -m 1 -> git push就可以正常使用了。

   > 二：直接用http链接
   > 1.git init
   > 初始化 本地库
   > 2.$ git pull https://github.com/SuperCoder1999/Tic-tac-toe.git
   > 从远程库 拉代码，（必须要的）
   > 3.git remote add origin git@github.com:SuperCoder1999/LanQiaoCup.git
   > 获取远程库操作权限 (这里如果用http链接, 需要登录)
   > 4.git push --set-upstream origin main
   > 设置 本地库上传 的分支
   > 此时就会 要求登录 GitHub(ssh就是帮助免去这一步的)。登陆方式有两种，我暂时用了网页登录。
   > 5.git add . ->git commit -m 1 -> git push就可以正常使用了。

   ```git
   Pinocchio@PinocchioPC MINGW64 /f/Github/LanQiaoCup
   $ git init (初始化文件夹)
   Initialized empty Git repository in F:/Github/LanQiaoCup/.git/
   
   Pinocchio@PinocchioPC MINGW64 /f/Github/LanQiaoCup (master)
   $ git pull git@github.com:SuperCoder1999/LanQiaoCup.git (拉取代码)
   remote: Enumerating objects: 43, done.
   remote: Counting objects: 100% (43/43), done.
   remote: Compressing objects: 100% (29/29), done.
   remote: Total 43 (delta 8), reused 43 (delta 8), pack-reused 0
   Unpacking objects: 100% (43/43), 1.05 MiB | 528.00 KiB/s, done.
   From github.com:SuperCoder1999/LanQiaoCup
    * branch            HEAD       -> FETCH_HEAD
   
   Pinocchio@PinocchioPC MINGW64 /f/Github/LanQiaoCup (master)
   $ git remote add origin git@github.com:SuperCoder1999/LanQiaoCup.git (获取操作权限)
   
   Pinocchio@PinocchioPC MINGW64 /f/Github/LanQiaoCup (master)
   $ git push
   fatal: The current branch master has no upstream branch.
   To push the current branch and set the remote as upstream, use
   
   git push --set-upstream origin master
   
   Pinocchio@PinocchioPC MINGW64 /f/Github/LanQiaoCup (master)
   $  git push --set-upstream origin master (设置提交的分支)
   ```

4. 拉取代码的方式

   1. git clone 可以用 http 和 ssh链接 

      1. http可能因为网络原因clone失败.解决方法是将https换成git

         ```
         git clone https://github.com/SuperCoder1999/Spring5_sgg.git(连接失败)
         git clone git://github.com/SuperCoder1999/Spring5_sgg.git
         ```

      2. ssh 链接很稳定.

   2. git pull .使用https和ssh链接都可以 (将https改成git的链接不能用于pull)
   
5. 更改远程仓库 (就是更改:git remote add origin git@github.com:SuperCoder1999/LanQiaoCup.git)

   ```
   方法一：
   git remote set-url origin git@192.168.1.18:mStar/OTT-dual/K3S/supernova
   方法二：
   git remote rm origin 
   git remote add origin git@192.168.1.18:mStar/OTT-dual/K3S/supernova
   ```

6. 偶然情况: git clone后,直接可以git push
