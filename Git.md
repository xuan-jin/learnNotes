# Git

## Git简介

Git是目前世界上最先进的分布式版本控制系统（没有之一）。

### Git的诞生

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！

### 集中式vs分布式

**集中式版本控制系统**：版本库集中存放在中央服务器，工作时先从中央服务器取得最新版本，然后工作完，再将自己的版本推送给中央服务器。

缺陷：必须联网才能工作；受网速限制。

**分布式版本控制系统**：没有“中央服务器”，每个人的电脑上都是一个完整的版本库。实际使用过程中，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但其作用仅仅是用来方便”交换“大家的修改。

优势：安全性高；不必联网；分支管理强大。



## 安装Git

### 在Linux上安装Git

首先输入 git 查看系统是否安装Git

对于Debian或Ubuntu Linux，输入命令

```
$ sudo apt-get install git
```

即可完成安装。

### 在Windows上安装Git

直接官网下载安装程序，按默认选项安装即可。安装完成找到Git Bash，运行即可。

完成安装后，还需最后一步设置,(自报家门)

```
$ git config --global user.name "Your Name"
$ git config --global user.name "email@example.com"
```



## 创建版本库

### 1.选择合适的位置，创建一个空目录

```
$ mkdir learngit
$ cd learngit
$ pwd			// 用于显示当前目录
```

Windows系统必须保证目录名（包括父目录）不包含中文名！

### 2.通过 git init 命令把这个目录变成Git可以管理的仓库

```
$ git init
```

创建好仓库后，当前目录下多了一个  .git  文件夹，这个目录是Git用来跟踪管理版本库的。

### 3.把文件添加到版本库

所有的版本控制系统只能跟踪文本文件的改动，比如TXT文件，网页，代码程序等。而图片视频等这些二进制文件，虽然也能管理，但没法跟踪文件的变化，到底改动了啥，没法知道。

Microsoft的Word格式是二进制，因此版本控制系统是没法跟踪word文档的改动。另外，千万不要使用Windows自带的记事本编辑任何文件。原因是其记事本开发时在每个文件开头添加了0xefbbbf（十六进制）的字符，会遇到很多问题。

编写一个txt文件

要将文件放到learngit目录或其子目录下，因为这是一个Git仓库，否则无法找到；

第一步用命令git add告诉Git，把文件**添加到暂存区**

第二步，用命令git commit告诉Git，把文件**提交到仓库**

```
$ git add readme.txt
$ git commit -m "wrote a readme file"
```

执行第一条的命令，没有任何显示，Unix的哲学是“没有消息就是好消息”，说明添加成功。

-m 后面输入的是本次提交的说明，最好是相关的更改信息，方便日后查看



## 时光机穿梭



```
$ git status			// 查看仓库当前状态
$ git diff readmen.txt	 // 查看文件readme.txt具体的修改内容

 // 提交修改，同样是两步
 $ git add readme.txt
 $ git commit -m "add some wrds"
 
```

### 版本回退

```
$ git log					//  显示从最近到最远的提交日志
$ git log --pretty=oneline	  //   同上（显示较少的信息）

$ git reset --hard HEAD^		// 退回上一个版本
$ GIT reset --hard <commit_id>

// HEAD 表示当前版本
// HEAD^ 上一个版本
// HEAD^^ 上上一个版本
// HEAD~100 往上100个版本

// 回退到 commit_id 对应的版本，commid_id 为版本号，只需要前几位就行了
$ cat readme.txt		// 查看文件内容
$ git reflog  			// 找回曾经版本的commit_id
```



### 工作区和暂存区

**工作区**：电脑中能看到的目录。

**版本库**：工作区有一个隐藏目录  .git 是Git 的版本库。

​			版本库中最重要的就是stage（或者叫做index）的暂存区，还有Git自动创建的第一个分支master，以及指向master的一个指针HEAD。



### 管理修改

Git之所以比其他版本控制系统设计的优秀，因为Git跟踪并管理的是修改，而非文件。

Git管理的是修改，当你用`git add`命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，`git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

```
$ git diff HEAD -- readme.txt		// 查看工作区和版本库里面新版本的区别
```



### 撤销修改

丢弃工作区 (Working Directory) 的修改

```
$ git restore <file>  (建议使用) (如: git restore readme.txt)
$ git checkout -- <file>
# 命令中 -- 很重要，没有就变成 “切换到另一个分支” 的命令
```

丢弃暂存区 (stage/index) 的修改

```
# 第一步: 把暂存区的修改撤销掉(unstage)，重新放回工作区
$ git restore --staged <file>

# 第二步: 撤销工作区的修改
$ git restore <file>

```

小结

当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git restore <file>`。

当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git restore --staged <file>`，就回到了场景1，第二步按场景1操作。

已经提交了不合适的修改到版本库时，想要撤销本次提交，参考 *版本回退* 一节，不过前提是没有推送到远程库。



### 删除文件

```
$ rm readme.txt 			// 删除文件

// 确实要删除，从版本库中删除文件
$ git rm readme.txt
$ git commit -m "remove .txt"

// 删错了要恢复，
$ git checkout -- readme.txt
```



## 远程仓库

第1步：创建SSH Key。

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

点“Add Key”，你就应该看到已经添加的Key：

### 添加远程仓库

首先，登陆GitHub，然后，在右上角找到“new repository”按钮，创建一个新的仓库：

在Repository name填入`learngit`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：

目前，在GitHub上的这个`learngit`仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

请千万注意，把上面的`michaelliao`替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。

下一步，就可以把本地库的所有内容推送到远程库上：