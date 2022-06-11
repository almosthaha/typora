# Git学习

## 1.Git命令

### 1.1用户签名![image-20220529195433386](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220529195433386.png)

签名的作用是区分不同操作者身份。用户的签名信息在每一个版本的提交信息能够看到，以此确认本次提交是谁做的。git在首次安装必须设置一下用户签名，否则无法提交代码。

注意：这路设置用户签名和将来登录github（或其它代码托管平台）的账号并没有任何关系

### 1.2初始化本地库

（可以相关文件（git-demo）右键git打开）

git init

![image-20220529201043180](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220529201043180.png)

![image-20220529200953596](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220529200953596.png)



### 1.3查看被地库课程

git status（查看状态命令）

命令：i 进入编辑模式

​			esc 退出编辑模式

​			要退出后才能进行复制粘贴，

​            复制:yy

​			粘贴:p

​            :wq保存

### 1.4添加暂缓区

绿色变成了红色，说明git已经知道了这个文件

![image-20220529203849954](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220529203849954.png)

git rm --cached hello.txt 删除缓存区的文件，但是工作区的文件并没有被删除

ctrl+l 清空本地缓存

### 1.5提交本地库

将暂存区提交到本地库，形成历史版本

基本语法

commit -m 日志信息，文件名

![image-20220530173856590](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220530173856590.png)

### 1.6修改文件

vim.txt 进入文件

对文件进行修改 修改后保存(:wq)

只要有文件修改，就可以查看本地库状态(git status)

但是修改后的文件还没有被追踪

要添加暂存区 git add hello.txt

提交到本地库：commit -m  日志信息,文件名

查看文件 cat hello.txt



### 1.7历史版本

查看历史信息 基本语法

​				git reflog 查看版本信息

​				git log 查看版本详细信息

复制版本号:ctrl+insert

粘贴版本号:shift+insert

版本穿梭:git reset --hard  版本信息

![image-20220530223213700](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220530223213700.png)

## 2.Git分支

### 2.1分支的优点

### 2.2分支的操作

查看分支：git branch  -v

创建分支：git branch hot-file

分支转换：git checkout master

### 2.3分支合并

git branch hot-file

### 2.4 冲突合并

手动合并代码



## 3.Git团队协作机制

### 3.1团队内协作

### 3.2 跨团队协作

## 4.GitHub操作

### 4.1创建远程库

1.点击右上角加号

2.取远程库名称

3.点击下方的create repository

![image-20220531103907830](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531103907830.png)

![image-20220531103947579](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531103947579.png)

4.选择https 后会有一个链接生成

![image-20220531104352410](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531104352410.png)

https://github.com/almosthaha/git-demo.git



5.执行以下命令

语法：

git remote -v 查看当前所有远程库的别名

git remote add 别名，远程地址

git remote add git-demo https://github.com/almosthaha/git-demo.git （创造别名 别名最好跟库名保持一致）

别名会出现两个，可以拉取，也可以推送

![image-20220531105126602](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531105126602.png)



### 4.2 推送本地库（本地库代码）到远程库

语法：

git config --global http.proxy http://127.0.0.1:1080

**git config --global --unset http.proxy** 

![image-20220531112058887](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531112058887.png)

git push 别名 分支



![image-20220531111955102](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531111955102.png)

![image-20220531113153342](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531113153342.png)

### 4.3拉取远程库到本地库

语法：

git-push git-demo3 master

![image-20220531122401289](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220531122401289.png)

查看拉取后状态：如果一样，说明远程库跟本地库同步成功

### 4.4克隆远程仓库到本地

语法:

git clone 远程地址

克隆不用你登录任何账号

小结：clone会做如下操作。1.拉取代码 2.初始化本地库 3.创建bi

## 5.idea操作

### 5.1分享代码到github上

点击vcs，里面有一个分享到github

### 5.2 推送代码

添加或者删除代码

本地库到远程库

![image-20220603162934625](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220603162934625.png)



![image-20220603164230243](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220603164230243.png)

### 5.3 拉取代码

在github中修改代码

![image-20220603164820323](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220603164820323.png)

修改完代码后在idea中pull



![image-20220603164803289](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220603164803289.png)

### 5.4 从github克隆项目的idea上

复制该项目的地址

![image-20220603170844876](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220603170844876.png)



点击get from vcs

![image-20220603170937224](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220603170937224.png)

![image-20220603171412329](C:\Users\almost\AppData\Roaming\Typora\typora-user-images\image-20220603171412329.png)

### 5.5 操作中可能遇到的问题



## 6.gitee操作
