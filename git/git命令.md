# git理论

Git本地有三个工作区域：工作目录（Working Directory）、暂存区(Stage/Index)、资源库(Repository或Git Directory)。如果在加上远程的git仓库(Remote Directory)就可以分为四个工作区域。文件在这四个区域之间的转换关系如下：

![image-20200726102619422](https://gitee.com/cuixiaoyan/uPic/raw/master/uPic/image-20200726102619422.png)

- Workspace：工作区，就是你平时存放项目代码的地方
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

本地的三个区域确切的说应该是git仓库中HEAD指向的版本：

![image-20200726102652107](https://gitee.com/cuixiaoyan/uPic/raw/master/uPic/image-20200726102652107.png)

## 工作流程

git的工作流程一般是这样的：

１、在工作目录中添加、修改文件；

２、将需要进行版本管理的文件放入暂存区域；

３、将暂存区域的文件提交到git仓库。

因此，git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

![image-20200726102724978](https://gitee.com/cuixiaoyan/uPic/raw/master/uPic/image-20200726102724978.png)

## 文件四种状态

## 文件的四种状态

版本控制就是对文件的版本控制，要对文件进行修改、提交等操作，首先要知道文件当前在什么状态，不然可能会提交了现在还不想提交的文件，或者要提交的文件没提交上。

- Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过git add 状态变为Staged.
- Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用git rm移出版本库, 则成为Untracked文件
- Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用git checkout 则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改 !
- Staged: 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified

## 忽略文件

有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等

在主目录下建立".gitignore"文件，此文件有如下规则：

1. 忽略文件中的空行或以井号（#）开始的行将会被忽略。
2. 可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{string1,string2,...}）代表可选的字符串等。
3. 如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。
4. 如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。
5. 如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。

```bash

#为注释
*.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
!lib.txt     #但lib.txt除外
/temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
build/       #忽略build/目录下的所有文件
doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

# 本地git

1. git init 进入文件夹初始化仓库。
2. git add . 将文件添加到本地仓库。
3. git commit -m "注释" 提交到本地仓库。

![image-20200616142051137](https://gitee.com/cuixiaoyan/uPic/raw/master/uPic/image-20200616142051137-20200616144815199.png)

![image-20200713175313173](/Users/cuixiaoyan/Library/Application%20Support/typora-user-images/image-20200713175313173.png)

#  提交gitee

1. git remote add gitee https://gitee.com/cuixiaoyan/docker.git  绑定码云

2. git pull --rebase gitee master  合并一下，如果生成仓库的时候，有生成文件。

3.  git push -u gitee master 提交远程

   

# 提交GitHub

1. git remote add github https://github.com/cuixiaoyan/docker.git   绑定gitbub
2. git pull --rebase github master  合并一下，如果生成仓库的时候，有生成文件。
3. git push -u github master 提交远程



# 常用命令

git remote -v 

![image-20200616144931705](https://gitee.com/cuixiaoyan/uPic/raw/master/uPic/image-20200616144931705.png)

git status 查看修改的文件。

如果文件夹中包含.git文件，在github上文件夹是打不开的，需要本地将文件给删除，然后重新提交

 git rm -r --cached "文件夹的名称" 

修改之后，需要git add 文件名之后，再 git commit -m "修改提交"。

# git分支

分支在GIT中相对较难，分支就是科幻电影里面的平行宇宙，如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，我们就需要处理一些问题了！

![image-20200726102926814](https://gitee.com/cuixiaoyan/uPic/raw/master/uPic/image-20200726102926814.png)

git分支中常用指令：

```bash
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```

![image-20200726103023795](https://gitee.com/cuixiaoyan/uPic/raw/master/uPic/image-20200726103023795.png)

如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是我们可以修改冲突文件后重新提交！选择要保留他的代码还是你的代码！

master主分支应该非常稳定，用来发布新版本，一般情况下不允许在上面工作，工作一般情况下在新建的dev分支上工作，工作完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来。

# 常见问题

## 文件名中文乱码

git config --global core.quotepath false

关于这个选项的介绍，官方原文如下：

Commands that output paths (e.g. ls-files, diff), will quote "unusual" characters in the pathname by enclosing the pathname in double-quotes and escaping those characters with backslashes in the same way C escapes control characters (e.g. \t for TAB, \n for LF, \ for backslash) or bytes with values larger than 0x80 (e.g. octal \302\265 for "micro" in UTF-8). If this variable is set to false, bytes higher than 0x80 are not considered "unusual" any more. Double-quotes, backslash and control characters are always escaped regardless of the setting of this variable. A simple space character is not considered "unusual". Many commands can output pathnames completely verbatim using the -zoption. The default value is true.

大致意思似乎是， 为防止一些转义问题，大于 0x80 以上的编码被认为是 "unusual" ，需要 quote 起来。设置成 false 即以 UTF8 编码解析，解决乱码问题。




![image-20200731152818294](https://gitee.com/cuixiaoyan/uPic/raw/master/uPic/image-20200731152818294.png)