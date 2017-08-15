# learn-git		by Allan 15-08-2017
learn git &amp; github

主要是整理 廖雪峰 网站中 git 教程。在此感谢 廖老师 提供的教程。
附 git 教程地址：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

/*************************************  以下为正文  ************************************/
Git简介：
	Git是什么？
	Git是目前世界上最先进的分布式版本控制系统（没有之一）。

Git的诞生：
	感谢 linus，感谢 linux，感谢全世界的大师们。

集中式vs分布式：

安装Git：
	在Linux上安装Git:
		试着输入git，像下面的命令，有很多Linux会友好地告诉你Git没有安装，还会告诉你如何安装Git。
			$ git
			The program 'git' is currently not installed. You can install it by typing:
			sudo apt-get install git
		如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，
		依次输入：./config，make，sudo make install这几个命令安装就好了。
	在Mac OS X上安装Git:
		一是安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：http://brew.sh/。
		第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，
		你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，
		选择“Command Line Tools”，点“Install”就可以完成安装了。
	在Windows上安装Git:
		msysgit是Windows版的Git，从https://git-for-windows.github.io
		下载（网速慢的同学请移步国内镜像），然后按默认选项安装即可。
	
	安装完成后，还需要最后一步设置，在命令行输入：
	$ git config --global user.name "Your Name"
	$ git config --global user.email "email@example.com"
	
创建版本库 repository:
	初始化一个Git仓库，使用git init命令。
	添加文件到Git仓库，分两步：
	第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；
	第二步，使用命令git commit，完成。
	
时光机穿梭：
	要随时掌握工作区的状态，使用git status命令。
	如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
	
版本回退：
	在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，
	当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
		
	HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令 git reset --hard commit_id。
	穿梭前，用 git log 可以查看提交历史，以便确定要回退到哪个版本。
	要重返未来，用 git reflog 查看命令历史，以便确定要回到未来的哪个版本。
		
工作区和暂存区：
	Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。
	工作区（Working Directory）：存放所有和版本控制相关的文件（包括程序文件等）的目录。
	版本库（Repository）：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
	Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，
	以及指向master的一个指针叫HEAD。
	
	把文件往Git版本库里添加的时候，是分两步执行的：
		第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
		第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
		
	git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。
		
管理修改：
	Git跟踪并管理的是修改，而非文件。
	提交后，用 git diff HEAD -- file 命令可以查看工作区和版本库里面最新版本的区别：
	每次修改，如果不 add 到暂存区，那就不会加入到 commit 中。
	
撤销修改：
	命令 git checkout -- file 意思就是，把 file 文件在工作区的修改全部撤销，
	有两种情况：
	一种是 file 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
	一种是 file 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
	总之，就是让这个文件回到最近一次git commit或git add时的状态。
	git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令。
	
	如果文件已被 git add 到暂存区，并且未提交，用命令 git reset HEAD file 可以把暂存区的修改撤销掉（unstage），重新放回工作区：
	
	如果文件被提交到了版本库，使用版本回退。
		
删除文件：
	在Git中，删除也是一个修改操作。
	一：确实要从版本库中删除该文件，用命令 git rm 删掉，并且 git commit 。文件就从版本库中被删除了。
	二：删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本： git checkout -- file
		git checkout 其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
		
	命令git rm用于删除一个文件。
	如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
		

	


















