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



## Git基本命令

```
$ cd F:/daily/xuanjin/notes		// 改变目录
$ cd ..		// 回退到上一个目录
$ pwd		// 打印工作目录，它会显示我们当前所在的目录路径
$ ls		// 列出当前目录中的所有文件
$ ll 		// 详细列出当前目录中的所有文件
$ touch      // 新建一个文件 如 touch index.js 
$ rm		// remove，删除一个文件
$ mkdir		// make directory 新建一个目录,就是新建一个文件夹
$ rm -r		// 删除一个文件夹， r (recusive 是递归的意思)， 删除用的就是递归，先删除文				件夹里面的内容，再删除文件夹
$ mv		// 移动文件, mv index.html src   index.html 是我们要移动的文件, src 是				目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下.
$ reset		// 清屏，把git bash命令窗口中的所有内容清空
$ exit 		// 可以直接退出窗口

```

命令行的快捷操作：

　　1， 我们可以使用**上下箭头**来查找我们以前输入的命令。这个尤其适合npm 命令。当我们输入npm run dev的时候，开启开发模式。但在开发过程中要安装一个组件，如axios, 这时我们就要按ctrl+ c 停止服务器。npm install axios --save.安装完成后，我们要重新启动dev 服务器进行开发，输入npm run dev. 其实这时候，可以不用输入命令，直接按两次向上箭头，命令行中就会npm run dev 命令。当我们打开git bash 窗口后，它就会记录我们输过的命令，按上下箭头，就可以查询历史，找到我们已前输出的命令。

　　2，**左右箭头**移动光标修改命令。当我们输入命令的时候，突然发现某个单词拼错了，这时可以按左右箭头来移动光标到拼错的单词或字母上，再Delete 或Backspace 来删除该字母。其实这里有好多的快捷键来快速修改命令。

　　移动光标： 按左右键头只能一个一个移动光标，如果我们能一个单词一个单词来移动就快多了。**Alt + B** 和 **Alt + F** 来解决问题， 一个是向左移动，一个是向右移动。**Ctrl + A** 则是移动光标到整条命令的起始位置。**Ctrl + E** 则是移动光标到整条命令的结束位置。

　　对于编辑或删除来说，有几个快捷键也可以同样完成任务。 Ctr+D, 相当于Delete， Ctrl + H 相当于Backspace。 Ctrl + U 删除光标左侧的所有内容， Ctrl + K删除光标右侧的所有内容。Ctrl + W 删除光标左侧的单词， Alt + D 删除光标右侧的单词。

　　3 **Tab 键的使用**。 当我们想进入到一个目录或文件夹时，如果文件名很长，要一个一个输入，那是一件很麻烦的事情。这时tab 的作用就来了，当我们输入文件名的前几个字母时，按tab， 如果有文件名可以匹配，它就会显示出完整的文件名，如果有多个文件名匹配到，它会显示最先找到的一个。再按一次tab，它就会匹配的下一个，我们可以不停地按 tab键在匹配的文件名中来回切换，直到找到我们文件名为止。



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
$ git reflog  			// 记录你的每一次命令,找回曾经版本的commit_id
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

把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

```
$ git add javaAndLife.md
$ git add MySQL.md
$ git commit -m "other notes"
$ git remote add origin git@github.com:xuan-jin/learngit.git
$ git push -u origin master

// 之后的简化命令（从现在起，只要本地作了提交，就可以通过命令，把本地master分支的最新修改推送至GitHub）
$ git push origin master
```



### 从远程库克隆

登陆GitHub，创建一个新的仓库

勾选`Initialize this repository with a README`，这样GitHub会自动为我们创建一个`README.md`文件

远程库已经准备好了，下一步是用命令`git clone`克隆一个本地库

```
$ git clone git@github.com:xuan-jin/huangfu.git
```



## 分支管理

你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

### 创建与合并分支

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上

```
$ git checkout -b dev			// 创建并切换到dev分支
$ git switch -c dev				// 同上

$ git branch dev				// 创建dev分支
$ git checkout dev				// 切换到dev分支

$ git branch					// 查看分支，当前分支前有*。

$ git checkout master			// 切换回master分支
$ git merge dev					//把dev分支的工作合并到master分支上
(合并某分支到当前分支)

$ git branch -d dev				 // 删除dev分支
```



### 解决冲突

在不同的分支对同一个文件分别进行提交，则可能会造成冲突。

手动修改后，再进行提交。

```
$ git log --graph --pretty=oneline --abbrev-commit
// 查看分支合并情况（图）
```



### 分支管理策略

通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

```
$ git merge --no-ff -m "merge with no-ff" dev
// --no-ff表示禁用Fast forward

$ git log --graph --pretty=oneline --abbrev-commit
// 我们用git log看看分支历史
```

分支策略

master分支应该保持非常稳定，也就是仅用来发布新版本，平时不能在上面干活；

干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。



### Bug分支

软件开发，bug常有。Git分支强大，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

若修复bug工作和你手头正在进行的工作冲突，则可通过stash功能吧当前工作现场“存储”起来，等恢复现场后继续工作。

```
$ git stash
// "储藏"当前工作现场

$ git stash list
// 查看已存储的工作区

$ git stash apply			// 恢复存储的工作区
$ git stash drop			// 删除存储的工作区
$ git stash pop				// 恢复的同时把stash也删了
$ git stash apply stash@{0}  多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash
# 通常在 dev 分支开发时,需要有紧急 bug 需要马上处理,保存现在修改的文件等,先修复 bug 后再回来继续工作的情况

$ git cherry-pick <commit> 
// 复制一个特定的提交到当前分支(当前分支的内容需要先 commit,然后冲突的文件需要解决冲突,然后 commit)
// 在master分支上修复bug后，对于之前从master分支出来的dev上也存在bug，简单的处理办法

```

### Feature分支

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。



### 多人协作

```
$ git remote 			// 查看远程库的信息
$ git remote -v			// 查看远程库更详细的信息

$ git push origin master
$ git push origin dev		// 推送master或dev分支到远程库

// 当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。
// 要在dev分支上开发，就必须创建远程origin的dev分支到本地
$ git checkout -b dev origin/dev

// 两人对同一文件更改后，在提交时会发生冲突，解决：
$ git pull
// 如果git pull失败，原因是没有指定本地dev分支与远程origin/dev分支的链接
$ git branch --set-upstream-to=origin/dev dev
$ git pull

```



### Rebase

把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。

- rebase操作可以把本地未push的分叉提交历史整理成直线；
- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

```
$ git rebase
```



## 标签管理

发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。

tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。

```
$ git branch		// 显示所有分支
$ git checkout master	// 切换到某分支
$ git tag v1.0		// 打上一个名为 v1.0 的标签，默认标签是打在最新提交的commit上的。
$ git tag			// 查看所有标签

$ git log --pretty=oneline --abbrev-commit 	// 找到历史提交的commit id
$ git tag v0.9 f52c633		// 为之前的commit id为f52c633的提交打上标签v0.9
// 注意，标签不是按时间顺序列出，而是按字母排序的。
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
// 还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字

$ git tag -d v1.0 		// 删除标签
$ git push origin v1.0   // 推送v1.0标签到远程
$ git push origin --tags // 一次性推送所有尚未推送到远程的标签

// 如果标签已经推送到远程,先从本地删除,然后，从远程删除
$ git tag -d v1.0					// 删除本地
$ git push origin :refs/tags/v1.0	  // 删除远程
```



## 使用GitHub

在GitHub上，可以任意Fork开源仓库；

自己拥有Fork后的仓库的读写权限；

可以推送pull request给官方仓库来贡献代码。



## 自定义Git



```
// 让Git显示颜色，会让命令输出看起来更醒目
$ git config --global color.ui true

```

### 忽略特殊文件

有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件啦，等等，每次`git status`都会显示`Untracked files ...`

好在Git考虑到了大家的感受，这个问题解决起来也很简单，在Git工作区的根目录下创建一个特殊的`.gitignore`文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

不需要从头写`.gitignore`文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore

忽略文件的原则是：

1. 忽略操作系统自动生成的文件，比如缩略图等；
2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的`.class`文件；
3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。



### 配置别名

偷懒的方法

```
$ git config --global alias.st status		// 告诉Git，以后st就表示status
$ git config --global alias.co checkout		
$ git config --global alias.ci commit
$ git config --global alias.br branch

// --global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。
// 加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。
// 每个仓库的Git配置文件都放在.git/config文件中：
```



### 搭建GIt服务器

搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的`apt`命令就可以完成安装。

假设你已经有`sudo`权限的用户账号，下面，正式开始安装。

第一步，安装`git`：

```
$ sudo apt-get install git
```

第二步，创建一个`git`用户，用来运行`git`服务：

```
$ sudo adduser git
```

第三步，创建证书登录：

收集所有需要登录的用户的公钥，就是他们自己的`id_rsa.pub`文件，把所有公钥导入到`/home/git/.ssh/authorized_keys`文件里，一行一个。

第四步，初始化Git仓库：

先选定一个目录作为Git仓库，假定是`/srv/sample.git`，在`/srv`目录下输入命令：

```
$ sudo git init --bare sample.git
```

Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以`.git`结尾。然后，把owner改为`git`：

```
$ sudo chown -R git:git sample.git
```

第五步，禁用shell登录：

出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑`/etc/passwd`文件完成。找到类似下面的一行：

```
git:x:1001:1001:,,,:/home/git:/bin/bash
```

改为：

```
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```

这样，`git`用户可以正常通过ssh使用git，但无法登录shell，因为我们为`git`用户指定的`git-shell`每次一登录就自动退出。

第六步，克隆远程仓库：

现在，可以通过`git clone`命令克隆远程仓库了，在各自的电脑上运行：

```
$ git clone git@server:/srv/sample.git
Cloning into 'sample'...
warning: You appear to have cloned an empty repository.
```

剩下的推送就简单了。

### 使用SourceTree

Git有很多图形界面工具，这里我们推荐[SourceTree](https://www.sourcetreeapp.com/)，它是由[Atlassian](https://www.atlassian.com/)开发的免费Git图形界面工具，可以操作任何Git库。