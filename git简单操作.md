[TOC]
* * *

- - -
##git简单操作
###remote的相关操作
####*查看当前的远程库*
要查看当前配置有哪些远程仓库,可以用 git remote 命令,它会列出每个远程库的简短名字.在克隆完某个项目后,至少可以看到一个名为 origin 的远程库,Git 默认使用这个名字来标识你所克隆的原始仓库:
- git remote 不带参数，列出已经存在的远程分支
    	进入有.git的目录下
        git remote
    	//一般会显示origin
- git remote -v | --verbose 列出详细信息，在每一个名字后面列出其远程url
    	git remote -v
        origin  http://git.mb.com/HQ01UC333/lxc_java_web_test_selenium.git (fetch）
    	origin  http://git.mb.com/HQ01UC333/lxc_java_web_test_selenium.git (push)
        
- git remote show origin # 查看远程服务器仓库状态
    	git remote show test//查看结果
    	* remote test
        Fetch URL: git@git.mb.com:HQ01UC333/lxc_daily.git
        Push  URL: git@git.mb.com:HQ01UC333/lxc_daily.git
        HEAD branch: master
        Remote branch:
        master tracked
        Local ref configured for 'git push':
        master pushes to master (up to date)
####添加远程仓库
要添加一个新的远程仓库,可以指定一个简单的名字,以便将来引用,运行 git remote add \[shortname\]\[url\]:

		//在远程库已有的地址
        git remote add  test  git@git.mb.com:HQ01UC333/lxc_daily.git
        //实用git remote -v 验证，显示：
        test    git@git.mb.com:HQ01UC333/lxc_daily.git (fetch)
        test    git@git.mb.com:HQ01UC333/lxc_daily.git (push)
        
        
####修改远程库信息
具体看描述，不一一说明了。直接修改.git/config文件也可以。
- git remote set\-url origin URL  (设置url地址)
- git remote set\-branches \[--add\] name branch... （设置分支）
- git remote set-url [--push] name newurl [oldurl]（设置push地址）
- git remote set-url --add name newurl （添加新地址）
- git remote set-url --delete name url  （删除地址）
- git remote rm origin （删除远程连接）

####建立远程仓库

1. 初始化一个空的git仓库
    	git init//初始化本地空间
        可以看到Initialized empty Git repository in D:/aa/.git/
2. 向仓库提交我们写的文件
    	touch a.txt //创建文件a.txt
        git add a.txt//加到库的索引中
        git commit -m "the first file to commit" a.txt//提交到本地库
        //通常也可以git commit -a -m “ ”这么使用。
        
3. 在本地仓库添加一个远程仓库,并将本地的master分支跟踪到远程分支
    	git remote add test git@git.mb.com:HQ01UC333/lxc_daily.git//上面有说明
        git push test master//推到远程库
        
        
###常用指令
####clone的相关操作
1. 最简单直接的命令
    	git clone xxx.git //克隆到当前目录
2. 如果想clone到指定目录
    	git clone xxx.git "指定目录" //克隆都指定目录
        
3. clone时创建新的分支替代默认Origin HEAD（master）

    	git clone -b [new_branch_name]  xxx.git
4. clone 远程分支
git clone 命令默认的只会建立master分支，如果你想clone指定的某一远程分支(如：dev)的话，可以如下：
1.查看所有分支(包括隐藏的)  git branch -a 显示所有分支
2.在本地新建同名的("dev")分支，并切换到该分支

####status的相关操作
- git status命令可以列出当前目录所有还没有被git管理的文件和被git管理且被修改但还未提交(git commit)的文件.
    	On branch master
        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git checkout -- <file>..." to discard changes in working directory)

                modified:   a.txt

        Untracked files:
          (use "git add <file>..." to include in what will be committed)

                2.txt

		no changes added to commit (use "git add" and/or "git commit -a")
   文件a是提交了但是又更改了内容；文件2是新建的文件没有提交。
   
   
   
####log相关操作
1. git log
如果不带任何参数，它会列出所有历史记录，最近的排在最上方，显示提交对象的哈希值，作者、提交日期、和提交说明。如果记录过多，则按Page Up、Page Down、↓、↑来控制显示；按q退出历史记录列表。
2. git log -n
如果不想向上面那样全部显示，可以选择显示前N条。
3. git log --stat -n
显示简要的增改行数统计,每次提交文件的变更统计，-n 同上，前n条，可省略。
    	显示这样的信息：1 file changed, 0 insertions(+), 0 deletions(-)
4. git log -p -n
此命令同上，不过显示更全了。
5. git log --pretty=oneline
一行显示，只显示哈希值和提交说明。
6. gig lot --graph
ASCII 字符串表示的简单图形，形象地展示了每个提交所在的分支及其分化衍合情况
    	git log --pretty=format:"%h %s" --graph
7. git log --pretty=format:" "
控制显示的记录格式，常用的格式占位符写法及其代表的意义如下：
    	选项	 说明
        %H	提交对象（commit）的完整哈希字串
        %h	提交对象的简短哈希字串
        %T	树对象（tree）的完整哈希字串
        %t	树对象的简短哈希字串
        %P	父对象（parent）的完整哈希字串
        %p	父对象的简短哈希字串
        %an	作者（author）的名字
        %ae	作者的电子邮件地址
        %ad	作者修订日期（可以用 -date= 选项定制格式）
        %ar	作者修订日期，按多久以前的方式显示
        %cn	提交者(committer)的名字
        %ce	提交者的电子邮件地址
        %cd	提交日期
        %cr	提交日期，按多久以前的方式显示
        %s	提交说明
如下操作：
    	git log --pretty=format:"%h -%an,%ar : %s"
        d5dc16c -李学成,3 days ago : the first file to commit
8. 指定路径
比如说，指定项目路径下的所有以a.txt结尾的文件的提交历史：
    	git log --pretty=oneline a.txt
    	会显示：d5dc16ca9be3bb51ae7928b6d1aa8ff4099c64b5 the first file to commit
        
 只需要加上文件路径作为参数即可。
9. 指定日期、关键字、作者
- 如两天前的提交历史：git log --since=2.days
- 如指定作者为"BeginMan"的所有提交:$ git log --author=BeginMan
- 如指定关键字为“init”的所有提交：$ git log --grep=init
- 如指定提交者为"Jack"的所有提交：$ git log --committer=Jack
*注意作者与提交者的关系：作者是程序的修改者，提交者是代码提交人。*
- 如指定2天前，作者为“BeginMan”的提交含有关键字'init'的前2条记录：$ git log --since=2.days --author=BeginMan --grep=init -2
*注意：上面选项后面的参数可以带单双引号，如--author="BeginMan"*
        选项 说明

        -(n) 仅显示最近的 n 条提交

        --since, --after 仅显示指定时间之后的提交。

        --until, --before 仅显示指定时间之前的提交。

        --author 仅显示指定作者相关的提交。

        --committer 仅显示指定提交者相关的提交。
 参考：git log 的相关属性
        -p 按补丁格式显示每个更新之间的差异。

        --stat 显示每次更新的文件修改统计信息。

        --shortstat 只显示 --stat 中最后的行数修改添加移除统计。

        --name-only 仅在提交信息后显示已修改的文件清单。

        --name-status 显示新增、修改、删除的文件清单。

        --abbrev-commit 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。

        --relative-date 使用较短的相对时间显示（比如，“2 weeks ago”）。

        --graph 显示 ASCII 图形表示的分支合并历史。

        --pretty 使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式）。

- ** git 图形客户端的使用**
使用gitk图形客户端查看历史记录。输入 gitk即可打开。

#### 创建别名
    	git config alias.logs "log --pretty=format:'%h -%an,%ar:%s'"
        git config alias.logs
        会显示log --pretty=format:'%h -%an,%ar:%s'
        git logs
        会显示：d5dc16c -李学成,3 days ago:the first file to commit
  配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。
配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中：
    	[alias]
		logs = log --pretty=format:'%h -%an,%ar:%s'
别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。
而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中，配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。

####add的相关操作
git add命令主要用于把我们要提交的文件的信息添加到索引库中。当我们使用git commit时，git将依据索引库中的内容来进行文件的提交。
- git add <path>表示 add to index only files created or modified and not those deleted 
通常是通过git add <path>的形式把我们<path>添加到索引库中，<path>可以是文件也可以是目录。
git不仅能判断出<path>中，修改（不包括已删除）的文件，还能判断出新添的文件，并把它们的信息添加到索引库中。
- git add -u 表示 add to index only files modified or deleted and not those created
git add \-u \[path\]: 把<path>中所有tracked文件中被修改过或已删除文件的信息添加到索引库。它不会处理untracted的文件。
*省略<path>表示.,即当前目录。*
- git add \-A: \[path\]表示把<path>中所有tracked文件中被修改过或已删除文件和所有untracted的文件信息添加到索引库。
*省略path表示.,即当前目录。*

- git add -i
可以通过git add -i [path]命令查看<path>中被所有修改过或已删除文件但没有提交的文件，
并通过其revert子命令可以查看<path>中所有untracted的文件，同时进入一个子命令系统。
//我操作失败了，期待后续研究。

####branch相关操作
- 查看分支
  git branch或者git branch -v ，git branch -a 列出本地分支和远程分支，-r显示远程分支。
- 创建分支
git branch test2
- 切换分支 
git checkout test2

- git branch -m | -M oldbranch newbranch 重命名分支，如果newbranch名字分支已经存在，则需要使用-M强制重命名，否则，使用-m进行重命名。
- 删除分支
git branch -d test2  //如果该分支没有合并到主分支会报错
git branch -D test2   //强制删除
git branch -d -r branchname 删除远程branchname分支

- 分支合并
比如，如果要将开发中的分支（develop），合并到稳定分支（master），
首先切换的master分支：git checkout master。
然后执行合并操作：git merge develop。
如果有冲突，会提示你，调用git status查看冲突文件。
解决冲突，然后调用git add或git rm将解决后的文件暂存。
所有冲突解决后，git commit 提交更改。

- clone远程分支
git clone -b release_branch  url

- 另外
git checkout -b -newbranch [start_point]
这样用可以创建新的分支并切换到新分支上去，b代表branch的意思，newbranch 是新分支的名称，如果没有指定提交点（start_point），默认从HEAD指向的提交创建分支。
git branch branchname [start_point]
创建新的分支，但是不会切换到新建的分支上，如果没有指定start_point，默认从HEAD指向的提交创建分支。


####checkout相关操作
  在日常的git操作中，git checkout——检出，是我们的常用命令。最为常用的两种情形是创建分支和切换分支。同时也是一个很危险的命令，因为这条命令会重写工作区。
1. git checkout [-q] [commit] [\-\-] paths
2. git checkout [branch]
3. git checkout [-m] [ [-b | -- orphan ] [new_branch]  [start_point] 

用法2比用法1的区别在于，用法1包含了路径。为了避免路径和引用（或提交ID）同名而发生冲突，可以在paths前用两个连续的连字符作为分隔。用法1的commit是可选项，如果省略，则相当于从暂存区进行检出。
- 第1种用法（包含paths的用法）不会改变HEAD头指针，主要使用于指定版本的文件覆盖工作区中对应的文件。如果省略commit，则会用暂存区的文件覆盖工作区中的文件，否则用指定提交中的文件覆盖暂存区和工作区中的对应文件。
- 对于第2种用法，不是检出某个具体文件的的时候，即不指定paths的时候，单纯的检出某个commit或分支，是会改变HEAD头指针的。而且只有当HEAD切换到某个分支的时候才可以对提交进行跟踪，否则就会进入“分离头指针”的状态。如果省略用法2后面的branch，则默认对工作区进行状态检查。
- 第3种用法主要是创建和切换到新的分支（new_branch），新的分支从start_point指定的提交开始创建。新分支和我们熟悉的master分支没有什么实质的不同，都是在refs/heads命名空间下的引用。
1. git branch branch start point
	   以某个commit创建新分支。 在通常情况下，我们都会在当前分支的基础上，创建新分支。
           	git branch test2  c820f6e//这是提交时的sha
2. git checkout -B branch
这个命令，可以强制创建新的分支，为什么加-B呢？如果当前仓库中，已经存在一个跟你新建分支同名的分支，那么使用普通的git checkout -b branch这个命令，是会报错的，且同名分支无法创建。如果使用-B参数，那么就可以强制创建新的分支，并会覆盖掉原来的分支。
3. git checkout --orphan branch
假如你的某个分支上，积累了无数次的提交，你也懒得去打理，打印出的log也让你无力吐槽，那么这个命令将是你的神器，它会基于当前所在分支新建一个赤裸裸的分支，没有任何的提交历史，但是当前分支的内容一一俱全。新建的分支，严格意义上说，还不是一个分支，因为HEAD指向的引用中没有commit值，只有在进行一次提交后，它才算得上真正的分支。
4. git checkout --merge branch
这个命令适用于在切换分支的时候，将当前分支修改的内容一起打包带走，同步到切换的分支下。

 *注意：如果当前分支和切换分支间的内容不同的话，容易造成冲突。
切换到新分支后，当前分支修改过的内容就丢失了。*

5. git checkout -p branch
这个命令可以用来打补丁。这个命令主要用来比较两个分支间的差异内容，并提供交互式的界面来选择进一步的操作。这个命令不仅可以比较两个分支间的差异，还可以比较单个文件的差异哦！//我没有成功操作。
  
####commit相关操作
在用git来进行版本控制时，我需要执行git commit命令，将索引内容添加到仓库中。
首先使用git status 查看文件状态

    	PS D:\aa> git status
        On branch master
        Changes to be committed:
          (use "git reset HEAD <file>..." to unstage)

                new file:   co.txt

        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git checkout -- <file>..." to discard changes in working directory)

                modified:   a.txt

        Untracked files:
          (use "git add <file>..." to include in what will be committed)

                bb.txt


- git commit  -m "提交的描述信息"
如果我们这里不用-m参数的话，git将调到一个文本编译器（通常是vim）来让你输入提交的描述信息，git commit 提交的是暂存区里面的内容，也就是 Changes to be committed 中的文件。
可能一天下来，你对工作树中的许多文档都进行了更新（文档添加、修改、删除），但是我忘记了它们的名字，此时若将所做的全部更新添加到索引中，比较轻省的做法就是：
- git commit -a -m "提交的描述信息"
git commit -a 除了将暂存区里的文件提交外，还提交 Changes bu not updated 或者Changes not staged for commit中的文件。
- git commit --amend
对于已经修改提交过的注释，如果需要修改，可以借助 git commit --amend 来进行。会跳出编辑页面，修改保存后，关闭，就修改成功了。

####diff的相关操作
- 查看尚未暂存的文件更新了哪些部分，不加参数直接输入。
git diff
此命令比较的是工作目录(Working tree)和暂存区域快照(index)之间的差异
也就是修改之后还没有暂存起来的变化内容。
- 查看已经暂存起来的文件(staged)和上次提交时的快照之间(HEAD)的差异
git diff --cached
    git diff --staged//都一样的意思
显示的是下一次commit时会提交到HEAD的内容(不带-a情况下)
- 显示工作版本(Working tree)和HEAD的差别
	git diff HEAD
- 直接将两个分支上最新的提交做diff
git diff test2 master 或 git diff test2..master
- 输出自topic和master分别开发以来，master分支上的changed。
 git diff topic...master
- 查看简单的diff结果，可以加上--stat参数
git diff --stat
- 查看当前目录和另外一个分支的差别
 git diff test
- 比较上次提交commit和上上次提交
 git diff HEAD^ HEAD
- 比较两个历史版本之间的差异
git diff SHA1 SHA2


####目录树初步了解
![目录树](http://img.my.csdn.net/uploads/201208/06/1344242125_1840.png)
图中左侧为工作区，右侧为版本库。在版本库中标记为 "index" 的区域是暂存区（stage, index），标记为 "master" 的是 master 分支所代表的目录树。
图中我们可以看出此时 "HEAD" 实际是指向 master 分支的一个“游标”。所以图示的命令中出现 HEAD 的地方可以用 master 来替换。
图中的 objects 标识的区域为 Git 的对象库，实际位于 ".git/objects" 目录下。
当对工作区修改（或新增）的文件执行 "git add" 命令时，暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID 被记录在暂存区的文件索引中。
当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。
当执行 "git reset HEAD" 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。
当执行 "git rm --cached <file>" 命令时，会直接从暂存区删除文件，工作区则不做出改变。
当执行 "git checkout ." 或者 "git checkout -- <file>" 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区的改动。
当执行 "git checkout HEAD ." 或者 "git checkout HEAD <file>" 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。
#####目录树的浏览
 git ls-tree -l HEAD 查看HEAD（版本库中当前提交）指向的目录树 -l参数可以显示文件大小
输出的文件条目从左至右，第一个字段是文件的属性，第二个字段（blob）说明是Git对象库中的一个blob对象（文件），第三个字段是该文件在对象库中对应的ID——一个40位的SHA1哈希值格式的ID，第四个字段是文件大小，第五个字段是文件名。
在浏览暂存区的目录树之前，首先清除工作区当前的改动。
git clean -fd 清除当前工作区中没有加入版本库的文件和目录（非跟踪文件和目录），然后执行git checkout .命令，用暂存区内容刷新工作区。
git ls-files -s 显示暂存区的目录树，其中第三个字段不是文件大小而是暂存区编号
若想针对暂存区的目录树使用git ls-tree命令，需要先将暂存区的目录树写入Git对象库，然后针对该目录树执行git ls-tree命令
git write-tree 输出的就是写入Git对象库的TreeID，这个ID将作为下一条命令的输入
5b873f747ccb268e4491f289eb37fc675ff5825b
git ls-tree -l 5b873f747 只需写前几位，只要不与其他对象的ID冲突即可
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad      12test
可以看出到处都是40位的SHA1哈希值格式的ID，可以用于指代文件内容（blob）、目录树（tree）和提交。
 git write-tree | xargs git ls-tree -l -r -t 递归显示目录内容使用-r参数，显示递归过程中遇到的每棵树而不是只显示最终文件使用-t参数
#####不要使用git commit -a
带上此参数，对本地所有变更的文件执行提交操作，包括对本地修改的文件和删除的文件，但不包括未被版本库跟踪的文件。可以简化一些操作，减少用git add命令标识变更文件的步骤，但是丢掉了对提交内容进行控制的能力。
#####保存当前工作进度
- git stash 运行完此命令后再查看工作区状态，会发现工作区尚未提交的改动（包括暂存区的改动）全都不见了。备份当前的工作区的内容，从最近的一次提交中读取相关内容，让工作区保证和上次提交的内容一致。同时，将当前的工作区内容保存到Git栈中。
- git stash pop: 从Git栈中读取最近一次保存的内容，恢复工作区的相关内容。由于可能存在多个Stash的内容，所以用栈来管理，pop会从最近的一个stash中读取内容并恢复。
- git stash list: 显示Git栈内的所有备份，可以利用这个列表来决定从那个地方恢复。
- git stash clear: 清空Git栈。此时使用gitg等图形化工具会发现，原来stash的哪些节点都消失了
- git stash apply和pop差不多的目的。
但是两者有什么区别呢。
刚才说过，git stash 可以形成list 集合。通过git stash list 可以看到list下的suoy
使用git stash apply @{x} ，可以将编号x的缓存释放出来，但是该缓存还存在于list中
而 git stash apply，会将当前分支的最后一次缓存的内容释放出来，但是刚才的记录还存在list中
而 git stash pop，也会将当前分支的最后一次缓存的内容释放出来，但是刚才的记录不存在list中

####fetch相关操作
一旦远程主机的版本库有了更新(Git术语叫做commit)，需要将这些更新取回本地，这时就要用到git fetch命令。
- git fetch 远程主机名
将某个远程主机的更新，全部取回本地。
默认情况下，git fetch取回所有分支(branch)的更新。如果只想取回特定分支的更新，可以指定分支名。
这一步其实是执行了两个关键操作:
1.创建并更新所有远程分支的本地远程分支.
2.设定当前分支的FETCH_HEAD为远程服务器的master分支 (上面说的第一种情况)
*需要注意的是: 和push不同, fetch会自动获取远程`新加入'的分支.*
- git fetch 远程主机名 分支名
比如，取回origin主机的master分支。
    	git fetch origin master

 设定当前分支的 FETCH_HEAD' 为远程服务器的master分支`.
注意: 在这种情况下, 不会在本地创建本地远程分支, 这是因为:
这个操作是git pull origin branch1的第一步, 而对应的pull操作,并不会在本地创建新的branch.
一个附加效果是:
这个命令可以用来测试远程主机的远程分支master是否存在, 如果存在, 返回0, 如果不存在, 返回128, 抛出一个异常.
- git fetch origin branch1:branch2
首先执行上面的fetch操作
使用远程branch1分支在本地创建branch2(但不会切换到该分支), 
如果本地不存在branch2分支, 则会自动创建一个新的branch2分支, 
如果本地存在branch2分支, 并且是`fast forward', 则自动合并两个分支, 否则, 会阻止以上操作.
git fetch origin :branch2
等价于: git fetch origin master:branch2

- 其他
所取回的更新，在本地主机上要用”远程主机名/分支名”的形式读取。比如origin主机的master，就要用origin/master读取。
git branch命令的-r选项，可以用来查看远程分支，-a选项查看所有分支。取回远程主机的更新以后，可以在它的基础上，使用git checkout命令创建一个新的分支。此外，也可以使用git merge命令或者git rebase命令，在本地分支上合并远程分支。

####init相关操作
- git init 本地仓库，包含.git目录和工作目录
- git init --bare 裸仓库，只有.git目录下的内容.适合作为服务器仓库.
- 相互转换 
 git clone --bare 从仓库导出bare仓库
 如果服务仓库以git init仓健，当用户向它提交代码时，会出现报错，解决办法是使用git clone --bare 克隆出.git内容作为服务器仓库.
 
####rm相关操作
在git中我们可以通过git rm命令把一个文件删除，并把它从git的仓库管理系统中移除。但是注意最后要执行git commit才真正提交到git仓库。
- git rm 1.txt
删除1.txt文件，并把它从git的仓库管理系统中移除。
- git rm -r myFolder
删除文件夹myFolder，并把它从git的仓库管理系统中移除。
- git rm --cached 10.txt 
把文件10.txt从git的索引库中移除,但是对文件10.txt本身并不进行任何操作。
- 还原被删掉的文件可以使用git add -i 中的revert后checkout找回来。

####reset的相关操作
- 在git的一般使用中，如果发现错误的将不想staging的文件add进入index之后，想回退取消，则可以使用命令：git reset HEAD file...，同时git add完毕之后，git也会做相应的提示。
- git reset [--hard|soft|mixed|merge|keep] [commit或HEAD]
将当前的分支重设（reset）到指定的<commit>或者HEAD（默认，如果不显示指定commit，默认是HEAD，即最新的一次提交），并且根据[mode]有可能更新index和working directory。mode的取值可以是hard、soft、mixed、merged、keep。下面来详细说明每种模式的意义和效果。
1.  --hard：重设（reset） index和working directory，自从<commit>以来在working directory中的任何改变都被丢弃，并把HEAD指向<commit>。 例如：git reset --hard HEAD~1
2.  --soft：index和working directory中的内容不作任何改变，仅仅把HEAD指向<commit>。这个模式的效果是，执行完毕后，自从<commit>以来的所有改变都会显示在git status的"Changes to be committed"中。 例如：git reset --soft(默认) HEAD~1
```
  在使用git进行协作开发时，我们经常需要将自己的修改生成patch发给被人，但是在修改代码的过程中我们进行了很多次的提交，如何生成从最初的代码状态到最终代码状态的patch呢？下面要介绍的功能是应对这中情况。
现假设我们git软件仓库中的分支情况如下：
a-->b-->c
也就是说我们的代码从状态a修改到状态b，进行一次提交，然后再修改到状态c，进行一次提交。这时我们已经肯定由a到c的修改是正确的，不再需要状态b了，并且要把从a到c的变化生成一个patch发送给别人。如果直接打包的话会生成两个path，那么如何生成一个patch呢，这时就需要git-reset命令。
首先给状态a创建一个tag，假设名称为A，然后执行
git-reset --soft A
这样我们的软件仓库就变为
a
状态b和状态c都已经被删除了，但是当前的代码并没有被改变，还是状态c的代码，这时我们做一次提交，软件仓库变成下面的样子：
a-->d
状态d和状态c所对应的代码是完全相同的，只是名字不同。现在就可以生成一个patch打包发给别人了
```
3.   --mixed：仅reset index，但是不reset working directory。这个模式是默认模式，即当不显示告知git reset模式时，会使用mixed模式。这个模式的效果是，working directory中文件的修改都会被保留，不会丢弃，但是也不会被标记成"Changes to be committed"，但是会打出什么还未被更新的报告。
4.   --merge和--keep用的不多。

######常用示例
下面列出一些git reset的典型的应用场景： 
A) 回滚add操纵 
引用
$ edit                                     (1) 
$ git add frotz.c filfre.c 
$ mailx                                    (2) 
$ git reset                                (3) 
$ git pull git://info.example.com/ nitfol  (4) 

(1) 编辑文件frotz.c, filfre.c，做了些更改，并把更改添加到了index 
(2) 查看邮件，发现某人要你pull，有一些改变需要你merge下来 
(3) 然而，你已经把index搞乱了，因为index同HEAD commit不匹配了，但是你知道，即将pull的东西不会影响已经修改的frotz.c和filfre.c，因此你可以revert这两个文件的改变。revert后，那些改变应该依旧在working directory中，因此执行git reset。 
(4) 然后，执行了pull之后，自动merge，frotz.c和filfre.c这些改变依然在working directory中。 

B) 回滚最近一次commit 
引用
$ git commit ... 
$ git reset --soft HEAD^      (1) 
$ edit                        (2) 
$ git commit -a -c ORIG_HEAD  (3) 

(1) 当提交了之后，你又发现代码没有提交完整，或者你想重新编辑一下提交的comment，执行git reset --soft HEAD^，让working tree还跟reset之前一样，不作任何改变。 
HEAD^指向HEAD之前最近的一次commit。 
(2) 对working tree下的文件做修改 
(3) 然后使用reset之前那次commit的注释、作者、日期等信息重新提交。注意，当执行git reset命令时，git会把老的HEAD拷贝到文件.git/ORIG_HEAD中，在命令中可以使用ORIG_HEAD引用这个commit。commit 命令中 -a 参数的意思是告诉git，自动把所有修改的和删除的文件都放进stage area，未被git跟踪的新建的文件不受影响。commit命令中-c <commit> 或者 -C <commit>意思是拿已经提交的commit对象中的信息（作者，提交者，注释，时间戳等）提交，那么这条commit命令的意思就非常清晰了，把所有更改的文件加入stage area，并使用上次的提交信息重新提交。 

C) 回滚最近几次commit，并把这几次commit放到叫做topic的branch上去。 
引用
$ git branch topic/wip     (1) 
$ git reset --hard HEAD~3  (2) 
$ git checkout topic/wip   (3)

(1) 你已经提交了一些commit，但是此时发现这些commit还不够成熟，不能进入master分支，但你希望在新的branch上润色这些commit改动。因此执行了git branch命令在当前的HEAD上建立了新的叫做 topic/wip的分支。 
(2) 然后回滚master branch上的最近三次提交。HEAD~3指向当前HEAD-3个commit的commit，git reset --hard HEAD~3即删除最近的三个commit（删除HEAD, HEAD^, HEAD~2），将HEAD指向HEAD~3。 

D) 永久删除最后几个commit 
引用
$ git commit ... 
$ git reset --hard HEAD~3   (1)

(1) 最后三个commit（即HEAD, HEAD^和HEAD~2）提交有问题，你想永久删除这三个commit。 

E) 回滚merge和pull操作 
引用
$ git pull                         (1) 
Auto-merging nitfol 
CONFLICT (content): Merge conflict in nitfol 
Automatic merge failed; fix conflicts and then commit the result. 
$ git reset --hard                 (2) 
$ git pull . topic/branch          (3) 
Updating from 41223... to 13134... 
Fast-forward 
$ git reset --hard ORIG_HEAD       (4)

(1) 从origin拉下来一些更新，但是产生了很多冲突，你暂时没有这么多时间去解决这些冲突，因此你决定稍候有空的时候再重新pull。 
(2) 由于pull操作产生了冲突，因此所有pull下来的改变尚未提交，仍然再stage area中，这种情况下git reset --hard 与 git reset --hard HEAD意思相同，即都是清除index和working tree中被搞乱的东西。 
(3) 将topic/branch合并到当前的branch，这次没有产生冲突，并且合并后的更改自动提交。 
(4) 但是此时你又发现将topic/branch合并过来为时尚早，因此决定退滚merge，执行git reset --hard ORIG_HEAD回滚刚才的pull/merge操作。说明：前面讲过，执行git reset时，git会把reset之前的HEAD放入.git/ORIG_HEAD文件中，命令行中使用ORIG_HEAD引用这个commit。同样的，执行pull和merge操作时，git都会把执行操作前的HEAD放入ORIG_HEAD中，以防回滚操作。 

F) 在被污染的working tree中回滚merge或者pull 
引用
$ git pull                         (1) 
Auto-merging nitfol 
Merge made by recursive. 
nitfol                |   20 +++++---- 
... 
$ git reset --merge ORIG_HEAD      (2)

(1) 即便你已经在本地更改了一些你的working tree，你也可安全的git pull，前提是你知道将要pull的内容不会覆盖你的working tree中的内容。 
(2) git pull完后，你发现这次pull下来的修改不满意，想要回滚到pull之前的状态，从前面的介绍知道，我们可以执行git reset --hard ORIG_HEAD，但是这个命令有个副作用就是清空你的working tree，即丢弃你的本地未add的那些改变。为了避免丢弃working tree中的内容，可以使用git reset --merge ORIG_HEAD，注意其中的--hard 换成了 --merge，这样就可以避免在回滚时清除working tree。 

G) 被中断的工作流程 
在实际开发中经常出现这样的情形：你正在开发一个大的feature，此时来了一个紧急的bug需要修复，但是目前在working tree中的内容还没有成型，还不足以commit，但是你又必须切换的另外的branch去fix bug。请看下面的例子 
引用
$ git checkout feature ;# you were working in "feature" branch and 
$ work work work       ;# got interrupted 
$ git commit -a -m "snapshot WIP"                 (1) 
$ git checkout master 
$ fix fix fix 
$ git commit ;# commit with real log 
$ git checkout feature 
$ git reset --soft HEAD^ ;# go back to WIP state  (2) 
$ git reset                                       (3)

(1) 这次属于临时提交，因此随便添加一个临时注释即可。 
(2) 这次reset删除了WIP commit，并且把working tree设置成提交WIP快照之前的状态。 
(3) 此时，在index中依然遗留着“snapshot WIP”提交时所做的uncommit changes，git reset将会清理index成为尚未提交"snapshot WIP"时的状态便于接下来继续工作。 

(H) Reset单独的一个文件 
假设你已经添加了一个文件进入index，但是而后又不打算把这个文件提交，此时可以使用git reset把这个文件从index中去除。 
引用
$ git reset -- frotz.c                      (1) 
$ git commit -m "Commit files in index"     (2) 
$ git add frotz.c                           (3)

(1) 把文件frotz.c从index中去除， 
(2) 把index中的文件提交 
(3) 再次把frotz.c加入index 

(I) 保留working tree并丢弃一些之前的commit 
假设你正在编辑一些文件，并且已经提交，接着继续工作，但是现在你发现当前在working tree中的内容应该属于另一个branch，与这之前的commit没有什么关系。此时，你可以开启一个新的branch，并且保留着working tree中的内容。 
引用
$ git tag start 
$ git checkout -b branch1 
$ edit 
$ git commit ...                            (1) 
$ edit 
$ git checkout -b branch2                   (2) 
$ git reset --keep start                    (3)

(1) 这次是把在branch1中的改变提交了。 
(2) 此时发现，之前的提交不属于这个branch，此时你新建了branch2，并切换到了branch2上。 
(3) 此时你可以用reset --keep把在start之后的commit清除掉，但是保持working tree不变。

####revert相关操作
git revert 撤销 某次操作，此次操作之前和之后的commit和history都会保留，并且把这次撤销作为一次最新的提交。
- git revert HEAD                  撤销前一次 commit
- git revert HEAD^               撤销前前一次 commit
- git revert commit （比如：fa042ce57ebbe5bb9c8db709f719cec2c58ee7ff）撤销指定的版本，撤销也会作为一次提交进行保存。
git revert是提交一个新的版本，将需要revert的版本的内容再反向修改回去，
版本会递增，不影响之前提交的内容
- git revert 和 git reset的区别 
1. git revert是用一次新的commit来回滚之前的commit，git reset是直接删除指定的commit。 
2. 在回滚这一操作上看，效果差不多。但是在日后继续merge以前的老版本时有区别。因为git revert是用一次逆向的commit“中和”之前的提交，因此日后合并老的branch时，导致这部分改变不会再次出现，但是git reset是之间把某些commit在某个branch上删除，因而和老的branch再次merge时，这些被回滚的commit应该还会被引入。 
3. git reset 是把HEAD向后移动了一下，而git revert是HEAD继续前进，只是新的commit的内容和要revert的内容正好相反，能够抵消要被revert的内容。

####merge相关操作
git merge branchname
如果没有冲突的话，merge完成。有冲突的话，git会提示那个文件中有冲突.

####tag相关操作
- 列出标签
git tag # 在控制台打印出当前仓库的所有标签
it tag -l ‘v0.1.*’ # 搜索符合模式的标签
- 打标签
git标签分为两种类型：轻量标签和附注标签。轻量标签是指向提交对象的引用，附注标签则是仓库中的一个独立对象。建议使用附注标签。
创建轻量标签
$ git tag v0.1.2-light

 创建附注标签
$ git tag -a v0.1.2 -m “0.1.2版本”

 创建轻量标签不需要传递参数，直接指定标签名称即可。
创建附注标签时，参数a即annotated的缩写，指定标签类型，后附标签名。参数m指定标签说明，说明信息会保存在标签对象中。

- 切换到标签
与切换分支命令相同，用git checkout [tagname]
查看标签信息
用git show命令可以查看标签的版本信息：
$ git show v0.1.2

- 删除标签
误打或需要修改标签时，需要先将标签删除，再打新标签。
$ git tag -d v0.1.2 # 删除标签
参数d即delete的缩写，意为删除其后指定的标签。

- 给指定的commit打标签
打标签不必要在head之上，也可在之前的版本上打，这需要你知道某个提交对象的校验和（通过git log获取）。
补打标签
$ git tag -a v0.1.1 9fbc3d0
- 标签发布
通常的git push不会将标签对象提交到git服务器，我们需要进行显式的操作：
$ git push origin v0.1.2 # 将v0.1.2标签提交到git服务器
$ git push origin –tags # 将本地所有标签一次性提交到git服务器

####pull相关操作
git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并。它的完整格式稍稍有点复杂。
- git pull 远程主机名 远程分支名:本地分支名
git pull origin next:master//比如，取回origin主机的next分支，与本地的master分支合并，需要写成下面这样。
- 如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
  git pull origin next
上面命令表示，取回origin/next分支，再与当前分支合并。实质上，这等同于先做git fetch，再做git merge。
- 在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系(tracking)。比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动”追踪”origin/master分支。
Git也允许手动建立追踪关系。
    	git branch --set-upstream master origin/next
上面命令指定master分支追踪origin/next分支。
如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名。
    	git pull origin
上面命令表示，本地的当前分支自动与对应的origin主机”追踪分支”(remote-tracking branch)进行合并。
- 如果当前分支只有一个追踪分支，连远程主机名都可以省略。
     	git pull
上面命令表示，当前分支自动与唯一一个追踪分支进行合并。
- 如果合并需要采用rebase模式，可以使用–rebase选项。
    	git pull --rebase 远程主机名 远程分支名:本地分支名

####push相关操作
git push命令用于将本地分支的更新，推送到远程主机。它的格式与git pull命令相仿。
- git push 远程主机名 本地分支名:远程分支名
注意，分支推送顺序的写法是<来源地>:<目的地>，所以git pull是<远程分支>:<本地分支>，而git push是<本地分支>:<远程分支>。
- 如果省略远程分支名，则表示将本地分支推送与之存在”追踪关系”的远程分支(通常两者同名)，如果该远程分支不存在，则会被新建。
    	git push origin master
上面命令表示，将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建。
- 如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。

    	git push origin :master
        等同于
		 git push origin --delete master
上面命令表示删除origin主机的master分支。

- 如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。

    	git push origin
		
		
上面命令表示，将当前分支推送到origin主机的对应分支。

- 如果当前分支只有一个追踪分支，那么主机名都可以省略。
    	 git push

- 如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push。
    	git push -u origin master
上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。
- 不带任何参数的git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。如果要修改这个设置，可以采用git config命令。
    	 git config --global push.default matching
		 或者
		 git config --global push.default simple
- 还有一种情况，就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用–all选项。

    	git push --all origin
上面命令表示，将所有本地分支都推送到origin主机。
- 如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做git pull合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用–force选项。
    	git push --force origin
上面命令使用–force选项，结果导致在远程主机产生一个”非直进式”的合并(non-fast-forward merge)。除非你很确定要这样做，否则应该尽量避免使用–force选项。
- 最后，git push不会推送标签(tag)，除非使用–tags选项。
    	git push origin --tags

* * *

- - -

[TOC]

