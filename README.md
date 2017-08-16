
learn git &amp; github
===

主要是整理 廖雪峰 网站中 git 教程。在此感谢 廖老师 提供的教程。
附 git 教程地址：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

---

## 1.Git简介：
	Git是什么？
	Git是目前世界上最先进的分布式版本控制系统（没有之一）。

### 1.1Git的诞生：
	感谢 linus，感谢 linux，感谢全世界的大师们。

### 1.2集中式vs分布式：

## 2.安装Git：
	在Linux上安装Git:
		试着输入 git ，像下面的命令，有很多 Linux 会友好地告诉你 Git 没有安装，还会告诉你如何安装 Git。
			$ git
			The program 'git' is currently not installed. You can install it by typing:
			sudo apt-get install git
		如果是其他Linux版本，可以直接通过源码安装。先从 Git 官网下载源码，然后解压，
		依次输入：./config，make，sudo make install这几个命令安装就好了。
	在Mac OS X上安装Git:
		一是安装 homebrew ，然后通过 homebrew 安装 Git ，具体方法请参考 homebrew 的文档：http://brew.sh/。
		第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，
		你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，
		选择“Command Line Tools”，点“Install”就可以完成安装了。
	在Windows上安装Git:
		msysgit是Windows版的 Git，从 https://git-for-windows.github.io
		下载（网速慢的同学请移步国内镜像，国内镜像为早期版本），然后按默认选项安装即可。
	
	安装完成后，还需要最后一步设置，在命令行输入：
	$ git config --global user.name "Your Name"
	$ git config --global user.email "email@example.com"
	
## 3.创建版本库 repository:
	初始化一个 Git 仓库，使用 git init 命令。
	添加文件到 Git 仓库，分两步：
	第一步，使用命令 git add <file> ，注意，可反复多次使用，添加多个文件；
	第二步，使用命令 git commit ，完成。
	
## 4.时光机穿梭：
	要随时掌握工作区的状态，使用 git status 命令。
	如果 git status 告诉你有文件被修改过，用 git diff 可以查看修改内容。
	
### 4.1版本回退：
	在 Git 中，用 HEAD 表示当前版本，上一个版本就是 HEAD^ ，上上一个版本就是 HEAD^^ ，
	当然往上100个版本写100个 ^ 比较容易数不过来，所以写成 HEAD~100 。
		
	HEAD 指向的版本就是当前版本，因此，Git 允许我们在版本的历史之间穿梭，使用命令 git reset --hard commit_id。
	穿梭前，用 git log 可以查看提交历史，以便确定要回退到哪个版本。
	要重返未来，用 git reflog 查看命令历史，以便确定要回到未来的哪个版本。
		
### 4.2工作区和暂存区：
	Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。
	工作区（Working Directory）：存放所有和版本控制相关的文件（包括程序文件等）的目录。
	版本库（Repository）：工作区有一个隐藏目录 .git ，这个不算工作区，而是 Git 的版本库。
	Git 的版本库里存了很多东西，其中最重要的就是称为 stage (或者叫 index) 的暂存区，还有 Git 为我们自动创建的第一个分支 master ，
	以及指向 master 的一个指针叫 HEAD 。
	
	把文件往 Git 版本库里添加的时候，是分两步执行的：
		第一步是用 git add 把文件添加进去，实际上就是把文件修改添加到暂存区；
		第二步是用 git commit 提交更改，实际上就是把暂存区的所有内容提交到当前分支。
		
	git add 命令实际上就是把要提交的所有修改放到暂存区 (Stage)，然后，执行 git commit 就可以一次性把暂存区的所有修改提交到分支。
		
### 4.3管理修改：
	Git 跟踪并管理的是修改，而非文件。
	提交后，用 git diff HEAD -- file 命令可以查看工作区和版本库里面最新版本的区别：
	每次修改，如果不 add 到暂存区，那就不会加入到 commit 中。
	
### 4.4撤销修改：
	命令 git checkout -- file 意思就是，把 file 文件在工作区的修改全部撤销，
	有两种情况：
	一种是 file 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
	一种是 file 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
	总之，就是让这个文件回到最近一次 git commit 或 git add 时的状态。
	git checkout -- file 命令中的 -- 很重要，没有 -- ，就变成了“切换到另一个分支”的命令。
	
	如果文件已被 git add 到暂存区，并且未提交，用命令 git reset HEAD file 可以把暂存区的修改撤销掉（unstage），重新放回工作区：
	
	如果文件被提交到了版本库，使用版本回退。
		
### 4.5删除文件：
	在 Git 中，删除也是一个修改操作。
	一：确实要从版本库中删除该文件，用命令 git rm 删掉，并且 git commit 。文件就从版本库中被删除了。
	二：删错了，因为版本库里还有，所以可以很轻松地把误删的文件恢复到最新版本： git checkout -- file
		git checkout 其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
		
	命令git rm用于删除一个文件。
	如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
		
## 5.远程仓库：
	注册 github 账户，以免费获得 Git 远程仓库。
	本地 Git 仓库和 GitHub 仓库之间的传输是通过 SSH 加密的。
	需要一点设置：
	第1步：创建 SSH Key。
	在用户主目录下，看看有没有 .ssh 目录，如果有，再看看这个目录下有没有 id_rsa 和 id_rsa.pub 这两个文件，如果已经有了，可直接跳到下一步。
	如果没有，打开 Shell（Windows下打开 Git Bash），创建 SSH Key：ssh-keygen -t rsa -C "youremail@example.com"
	id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
	第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面，
	然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。

### 5.1添加远程库：
	在 github 创建一个空仓库，在本地仓库运行命令：
	git remote add origin git@server-name:path/repo-name.git
	可以把本地库的所有内容推送到远程库上：
	git push -u origin master
	
	要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
	关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
	此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改。
	
### 5.2从远程库克隆
	最好的方式是先创建远程库，然后，从远程库克隆。最好选择创建 README.md 文件。
	用命令 git clone 克隆一个本地库：git clone git@server-name:path/repo-name.git
	Git 支持多种协议，包括 https ，但通过 ssh 支持的原生 git 协议速度最快。

## 6.分支管理
	
### 6.1创建与合并分支
	主分支， master ， HEAD 指向当前分支。
	创建并切换到分支：git checkout -b branchname , git checkout 命令加上-b参数表示创建并切换。
	创建分支： git branch branchname
	切换分支： git checkout branchname
	查看当前分支： git branch
	合并分支： git merge branchname ，将 branchname 分支合并至当前分支
	删除分支： git branch -d branchname
	因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，
	这和直接在master分支上工作效果是一样的，但过程更安全。
	
### 6.2解决冲突
	合并分支时，当文件产生冲突，必须手动解决冲突后再提交。
	Git 用<<<<<<<，=======，>>>>>>>标记出不同分支的内容
	用带参数的git log也可以看到分支的合并情况： git log --graph --pretty=oneline --abbrev-commit
	当 Git 无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
	用 git log --graph 命令可以看到分支合并图。
	
### 6.3分支管理策略
	合并分支时，如果可能，Git 会用 Fast forward 模式，但这种模式下，删除分支后，会丢掉分支信息。
	如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
	禁用 Fast forward ： git merge --no-ff -m "merge with no-ff" branchname 
	因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。
	git log 查看历史将看到合并历史
	分支策略：
		在实际开发中，我们应该按照几个基本原则进行分支管理：
		首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
		干活都在dev分支上，也就是说，dev分支是不稳定的，
		到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
		每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
		团队合作的分支看起来就像这样：
		O-————-——————————————————————————O————————————————————————O------------master 
		 \                              /                        /
		  O——————————————O—————————————O—————————O——————————————O————O---------dev 
		  /\            / \           /         /              /    /
		  \ O——————————O——/——————————O————O————/————O—————————O————/———O-------michoel
		   \             |                    /                   /
			O————————————O——————————O————————O———————————————————O-------------bob
			
### 6.4 Bug 分支
	在 Git 中，由于分支是如此的强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。
	Git 还提供了一个 stash 功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作： git stash
	首先确定要在哪个分支上修复bug，假定需要在 master 分支上修复，就从 master 创建临时分支，
	修复完成后，切换到 master 分支，并完成合并，最后删除 issue-101 分支。
	git stash list 命令查看缓存区：
	恢复两个办法： 
	一是用 git stash apply 恢复，但是恢复后，stash 内容并不删除，你需要用 git stash drop 来删除；
	另一种方式是用git stash pop，恢复的同时把stash内容也删了。
	
### 6.5 Feature 分支
	每添加一个新功能，最好新建一个 feature 分支，在上面开发，完成后，合并，最后，删除该 feature 分支。
	如果开发完成但未合并分支，可以删除 feature 分支，但 git branch -d feature 不能删除，因为没有合并分支，
	需要强行删除， git branch -D feature
	
### 6.6多人协作
	当从远程仓库克隆时，实际上 Git 自动把本地的 master 分支和远程的 master 分支对应起来了，并且，远程仓库的默认名称是 origin。
	要查看远程库的信息，用 git remote： 用 git remote -v 显示更详细的信息。
	
#### 推送分支：
	推送分支，就是把该分支上的所有本地提交推送到远程库。
	推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上： git push origin master
	
#### 抓取分支：
	当从远程库 clone 时，默认情况下，只能看到本地的master分支，
	要在 dev 分支上开发，就必须创建远程 origin 的 dev 分支到本地： git checkout -b dev origin/dev
	
#### 多人协作模式：
	1：首先，可以试图用 git push origin branch-name 推送自己的修改；
	2：如果推送失败，则因为远程分支比你的本地更新，需要先用 git pull 试图合并；
	3：如果合并有冲突，则解决冲突，并在本地提交；
	4：没有冲突或者解决掉冲突后，再用 git push origin branch-name 推送就能成功！
	
	如果 git pull 提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，
	用命令 git branch --set-upstream branch-name origin/branch-name。
		   git branch --set-upstream-to=origin/<branch> dev
		   
	


	
	
	
	
	
	
	
	
	












