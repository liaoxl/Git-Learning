Git-Learning
============

###Repo for learning git.
---
* Test operations of git
* Test operations with git and github

* Test when changes in local

* Test changes on github

使用Octopress + GitHub来搭建自己的博客，首先得对Octopress的博客环境进行配置，还要对Git版本管理及markdown语法有一定了解。对这两个都进行学习了一下，觉得markdown语法比较简单，多练习一段时间，就可以很自然的掌握了。而Git的版本管理及GitHub的远程仓库管理，让我觉得比较难以理解，所以进行了一些测试学习。学习Git可以去[Pro Git](http://git-scm.com/book)的官方网站，或者这本书的[GitHub](https://github.com/progit/progit)，也可以去新浪共享上面去[下载](http://ishare.iask.sina.com.cn/f/16096245.html)

[我的博客](http://liaoxl.github.io/blog/2013/05/17/git/)

---

推荐安装tig，有有助于对git的理解，对于fedora 17，直接

  $ yum intall tig

<!-- more -->
---

## Git基础

Git的基本用法比较简单，我就从我的理解来记录一些，首先进行一些基本配置：

	$ mkdir git-hub
	$ cd git-hub/

	$ tig
	tig: Not a git repository

	$ git config --list 
	user.name=Xiangli Liao
	user.email=liaoxl2012@gmail.com
	core.editor=vim

这里创建一个目录，作为即将使用git的目录，首先对其初始化：

	$ git init 
	Initialized empty Git repository in /home/moondark/rubydev/git-hub/.git/

它就在当前目录下初始化了git，即最初通过`git init`初始化的是为空的。

	$ vim record.txt
	$ git status
	# On branch master
	#
	# Initial commit
	#
	# Untracked files:
	#   (use "git add <file>..." to include in what will be committed)
	#
	#	record.txt
	nothing added to commit but untracked files present (use "git add" to track)

通常用`git status`来查看当前目录文件的git状态，建议常用，一般情况下，都会有提示操作，如这里的最后一行，按照提示：

	$ git add .
	$ git status
	# On branch master
	#
	# Initial commit
	#
	# Changes to be committed:
	#   (use "git rm --cached <file>..." to unstage)
	#
	#	new file:   record.txt
	#

这里的意思是，你添加的record.txt文件，处于暂存状态`stage`，如果不不想加入这个文件，你可以按照提示用`git rm --cached record.txt`来移除，如果你确定了，那你需要用`git commit -m'Your Message'`来提交你的更改，在这之前，你可以用tig命令查看当前状态：

	$ tig
	tig: No revisions match the given arguments.

它显示当前为一个空的，此时你用`git commit -m'Your Message'`来提交，`Your Message`这里是一个快速提交更新的注释方法，表示你这次提交的描述，最好简明扼要，方便理解，如下：

	$ git commit -m 'First Comment'
	[master (root-commit) 11a8c45] First Comment
	1 file changed, 28 insertions(+)
	create mode 100644 record.txt


	$ tig
	2013-05-16 19:32 Xiangli Liao       I [master] First Comment

tig显示的，是当前分支的提交状态。继续修改record.txt，应用git命令：

	$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#	modified:   record.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

	$ git commit -m 'Try second commit'
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#	modified:   record.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")

此时要提交，根据提示，要么用`git add`或`git commit -a`均可，如果是对于已跟踪的但修改了的文件，用`git commit -a`是个比较快速的方法进行提交更新：

	$ git commit -a -m 'Try second commit'
	[master bf899f5] Try second commit
	 1 file changed, 34 insertions(+)

	$ tig
	2013-05-16 19:37 Xiangli Liao       o [master] Try second commit
	2013-05-16 19:32 Xiangli Liao       I First Comment

git本地的命令基本常用的就以上，还有一个常用的就是`git branch`，用于添加分支的，当然这个对于初学者来说一般不常用到。

---

## Git && GitHub

其实经常使用的，就是利用git与github一起管理自己的代码，其中有一些操作并不是很好理解，所以记录下来，做个笔记。

GitHub这种一般叫做远程仓库，即有一个“虚拟”的仓库，你跟若干个人都能同时用这个仓库进行存取东西。既然是若干个人用，当然就很容易出现一些问题，比如说不同步，或者有不同的分支，又或者有些分支需要合并。

首先，添加远程仓库，在github上创建一个Repo，比如创建一个Repo[Git-Learning](https://github.com/liaoxl/Git-Learning)，你在本地添加远程仓库，采用`git remote`命令添加远程仓库。添加github上面的远程仓库有两种，一种是https，一种是SSH，前一种每一次push需要输入用户名/密码，后一种用SSH连接需要配置一下本地SSH，具体可以见[GitHub SSH Keys](https://help.github.com/articles/generating-ssh-keys)，这样每一次不需要每次输入用户名/密码，感觉更方便一些。

	" https
	git remote add origin https://github.com/liaoxl/Git-Learning.git
	"SSH
	git remote add origin https://github.com/liaoxl/Git-Learning.git

然后可以用`git remote -v`来查看远程仓库。

	$ git remote -v
	origin	git@github.com:liaoxl/Git-Learning.git (fetch)
	origin	git@github.com:liaoxl/Git-Learning.git (push)

推送的话，即将本地已经`commit`的文件推送到远程仓库，即：

	$ git push origin 

在远程仓库上修改代码如何更新到本地呢？最简单的就是，我直接在github上面对自己文件内容进行修改，于是我本地文件中没有这些改变，这个时候就需要更新本地仓库：

	$ git pull origin master
	* branch            master     -> FETCH_HEAD
	Already up-to-date.


我操作发现，push可以默认推送到远程仓库的origin/master分支上，而更新本地文件必须指明分支，否则：

	$ git pull origin 
	You asked to pull from the remote 'origin', but did not specify
	a branch. Because this is not the default configured remote
	for your current branch, you must specify a branch on the command line.

如果想推送到远程分支上，应该怎么办呢？可以首先查看有那些分支：

	$ git branch -a
	* master
	testing
	remotes/origin/master
	remotes/origin/test

推送的时候需要指明本地分支与远程分支：

	$ git push origin master:master
	Everything up-to-date

如果不指定本地分支，**并不是推送默认分支，而是删除远程分支**

	$ git push origin :test
	To git@github.com:liaoxl/Git-Learning.git
	 - [deleted]         test

有了分支，就有合并的问题。如果我在远程仓库上进行了更新，本地文件我也进行了更新，在`git push`之前必须先用`git pull`来先更新本地仓库，否则：

	$ git push origin master 
	Username for 'https://github.com': liaoxl
	Password for 'https://liaoxl@github.com': 
	To https://github.com/liaoxl/Git-Learning.git
	 ! [rejected]        master -> master (non-fast-forward)
	 error: failed to push some refs to 'https://github.com/liaoxl/Git-Learning.git'
	 hint: Updates were rejected because the tip of your current branch is behind
	 hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
	 hint: before pushing again.
	 hint: See the 'Note about fast-forwards' in 'git push --help' for details.

而用`git pull`更新本地仓库，又将涉及到合并(merge)的问题，git会自动尝试帮你合并(做一些最简单的合并），如果它自动合并失败，会提示有冲突，需要手动合并，如下是自动合并的：

	$ git pull https://github.com/liaoxl/Git-Learning.git " 这里也可用 git pull origin master
	remote: Counting objects: 4, done.
	remote: Compressing objects: 100% (3/3), done.
	remote: Total 3 (delta 0), reused 0 (delta 0)
	Unpacking objects: 100% (3/3), done.
	From https://github.com/liaoxl/Git-Learning
	 * branch            HEAD       -> FETCH_HEAD
	 Updating fd38d27..6a01674
	 Fast-forward
	 README.md | 4 ++++
	 1 file changed, 4 insertions(+)
	  create mode 100644 README.md
	
以下是不能自动合并的：

	$ git commit -a -m 'Changes on local'
	[master 78c9b6f] Changes on local
	 1 file changed, 3 insertions(+), 1 deletion(-)

	 $ git pull https://github.com/liaoxl/Git-Learning.git
	 From https://github.com/liaoxl/Git-Learning
	  * branch            HEAD       -> FETCH_HEAD
		Auto-merging morefile
		CONFLICT (content): Merge conflict in morefile
		Automatic merge failed; fix conflicts and then commit the result.

这个时候就需要自己手动合并，合并之后必须重新`commit`，才能用`git push`完成推送命令，即合并之后文件改变了，需要提交更新。

在经过若干次操作之后，用tig命令查看当前分支的状态，就显得比较直观了，非常推荐：

	$ tig
	2013-05-18 10:46 Xiangli Liao       o [master] [origin/master] update record.tx~
	2013-05-17 00:49 Xiangli Liao       M─┐ merge master and testing
	2013-05-17 00:44 Xiangli Liao       │ o [testing] new file test.rb
	2013-05-17 00:47 Xiangli Liao       o │ new file test.rb master
	2013-05-17 00:10 Xiangli Liao       M─┐ after Merge conflict
	2013-05-17 00:07 Xiangli Liao       │ o changes github
	2013-05-17 00:08 Xiangli Liao       o │ changes local morefile
	2013-05-16 23:52 Xiangli Liao       M─┐ try manually merg local
	2013-05-16 23:48 Xiangli Liao       │ o change readme on github
	2013-05-16 23:49 Xiangli Liao       o │ changes on local
	2013-05-16 23:41 Xiangli Liao       o─┘ Update README.md
	2013-05-16 23:31 Xiangli Liao       o source2 local
	2013-05-16 23:16 Xiangli Liao       o source1 local
	2013-05-16 23:13 Xiangli Liao       o New dir local
	2013-05-16 22:57 Xiangli Liao       o do changes on morefile
	2013-05-16 22:50 Xiangli Liao       M─┐ some changes on morefile
	2013-05-16 22:34 Xiangli Liao       │ o More changes
	2013-05-16 22:36 Xiangli Liao       o │ Changes on local
	2013-05-16 22:32 Xiangli Liao       o─┘ Update morefile
	2013-05-16 21:38 Xiangli Liao       o Create README.md
	2013-05-16 20:32 Xiangli Liao       o some changes
	2013-05-16 19:53 Xiangli Liao       o Test commit -a for new file
	2013-05-16 19:37 Xiangli Liao       o Try second commit
	2013-05-16 19:32 Xiangli Liao       I First Comment
	[main] 1b98974d93252a884ef07e071072f5a6df063ad1 - commit 1 of 24 (100%)

---
## Git 与 Octopress

来看看Octopress用的git命令，我起初一直不理解为何要：

	$ git push origin source

这说明在本地已经有了一个source分支

	$ git branch
	master
	* source

这一步是在`rake setup_github_pages`产生的，看看其Rakefile
	
	desc "Set up _deploy folder and deploy branch for Github Pages deployment"
	task :setup_github_pages, :repo do |t, args|

其中这一步是控制git branch的

	unless (`git remote -v` =~ /origin.+?octopress(?:\.git)?/).nil?
		# If octopress is still the origin remote (from cloning) rename it to octopress
		system "git remote rename origin octopress"
		if branch == 'master'
			# If this is a user/organization pages repository, add the correct origin remote
			# and checkout the source branch for committing changes to the blog source.
			system "git remote add origin #{repo_url}"
			puts "Added remote #{repo_url} as origin"
			system "git config branch.master.remote origin"
			puts "Set origin as default remote"
			system "git branch -m master source"
			puts "Master branch renamed to 'source' for committing your blog source files"
		else
			unless !public_dir.match("#{project}").nil?
				system "rake set_root_dir[#{project}]"
			end
		end
	end

可以查看自己Octopress目录中的所有分支：

	$ git branch -a
	master
	* source
	remotes/octopress/2.1
	remotes/octopress/HEAD -> octopress/master
	remotes/octopress/colorize
	remotes/octopress/gh-pages
	remotes/octopress/guard
	remotes/octopress/linklog
	remotes/octopress/master
	remotes/octopress/migrator
	remotes/octopress/plugins
	remotes/octopress/refactor_with_tests
	remotes/octopress/rubygemcli
	remotes/octopress/site
	remotes/octopress/site-2.1
	remotes/origin/source


