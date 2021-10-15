# Git 简单使用说明

1安装git：

git是Windows版的Git，从http://msysgit.github.io/下载，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

2 配置用户名：

```
	git config --global user.name "Your Name"
	git config --global user.email "email@example.com"
```

3、创建仓库（或者 克隆一个远程仓库 ）：

```
	git init

	Initialized empty Git repository in /Users/michael/learngit/.git/ （告诉你是一个空的仓库）
```

请确保目录名（包括父目录）不包含中文

4、添加文件到仓库：

把文件（readme.txt）放在创建的仓库内

```
	git add readme.txt  //可反复多次使用，
```

添加多个文件；

```
	git add .
```

（.）点表示当前目录下的所有内容，交给git管理，也就是提交到了git的本地仓库。 用命令git commit告诉Git，把文件提交到仓库：

```
	git commit -m "Update README.md, add the front-end interview questions "
	[master (root-commit) cb926e7] wrote a readme file
	 1 file changed, 2 insertions(+)
	 create mode 100644 readme.txt
```

5、修改文件后，更新仓库

```
	git status   查看仓库当前的状态， 告诉我们，什么文件被修改过了，但还没有准备提交的修改。
	git diff  文件名，  查看具体修改了什么内容
	git add 文件名    更新和添加一样
	git commit
```

6、版本回退：

先 git log 添加的注释

也可以：git reflog 记录你的每一次添加命令和注释 和commit_id：

只回到上一个版本就是HEAD^，

```
	 git reset --hard HEAD^
```

上上一个版本就是HEAD^^ git reset –hard HEAD^^

```
	git reset --hard commit_id。
```

7、暂存区

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。 第一次修改 -> add -> 第二次修改 -> add -> commit

只会提交第一次的修改内容到主分支

8、撤销提交操作（add）

```
	git checkout -- readme.txt   //（--很重要，没有--，就变成了“创建一个新分支”的命令）
```

把readme.txt文件在工作区的修改全部撤销，这里有两种情况： 当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令

```
	git checkout -- file
```

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态； 当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，

第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作

二是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到【最近一次git commit后】 或【git add之前】的状态；

假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？ 可以回退到上一个版本。 不过，这是有条件的，就是你还没有把自己的本地版本库推送到远程。

9、删除文件

```
	git rm test.txt
	rm 'test.txt'
	m "remove test.txt"
	git commit
	-
	//如果删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：
	git checkout -- test.txt
```

10、设置SSH Key

由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要SSH Key

默认存放在 C:\Users\Administrator.ssh id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

```
	ssh-keygen -t rsa -C “mygood@126.com"
```

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的， 而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

11、绑定到远程仓库 （注意格式的gitlab，不支持ssh，请使用http）

```
	关联一个远程库   git remote add origin git@github.com:markyun/beilibao.git
	远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。
```

12、推送到远程仓库

```
	git remote -v //查看你当前项目远程连接的是哪个仓库地址。
	git push -u origin master //将本地的项目提交到远程仓库中。
```

正常情况下这样显示：

```
	git push -u origin master
	Counting objects: 19, done.
	o 4 threads.
	Compressing objects: 100% (
	Delta compression using up
	t19/19), done.
	Writing objects: 100% (19/19), 13.73 KiB, done.
	lliao/learngit.git
	 * [new branch]
	Total 23 (delta 6), reused 0 (delta 0)
	To git@github.com:micha
	e  master -> master
	 to track remote branch master from origin.
	Branch master set u
	p
```

如果提示：

```
	ssh:connect to host github.com port 22:bad file number could not read from remote repository
```

（说不能读取远端库，请确保有正确的访问权限并且仓库存在。看看你本机22端口有没有打开）

```
	ssh github.com 测试是否能正常使用SSH
```

当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

```
	The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
	RSA key fingerprint is xx.xx.xx.xx.xx.
	cting (yes/no)?
	Are you sure you want to continue conn
	e
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。 Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

```
	Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```

这个警告只会出现一次，后面的操作就不会有任何警告了。

13、从服务器上把一个远程仓库中的工程完全的拷贝下来

```
	git clone git@github.com:china-UED/test.git
	假如本地已经存在了这个项目，而仓库中又有一新的更新，如何把更的合并到本地的项目中？
	git fetch origin    //取得远程更新，这里可以看做是准备要取了
	git merge origin/master  //把更新的内容合并到本地分支/master
```

—————-待补充————–

14、创建与合并分支

15、冲突的处理

16、多人协作

17、其他

```
 git config --list 查看配置
 git config --global core.autocrlf false  关闭 github的换行符自动转换”功能
```

补充 Git 命令快速查询表

```
命令		简要说明
git add	添加至暂存区
git add–interactive	交互式添加
git apply	应用补丁
git am	应用邮件格式补丁
git annotate	同义词，等同于 git blame
git archive	文件归档打包
git bisect	二分查找
git blame	文件逐行追溯
git branch	分支管理
git cat-file	版本库对象研究工具
git checkout	检出到工作区、切换或创建分支
git cherry-pick	提交拣选
git citool	图形化提交，相当于 git gui 命令
git clean	清除工作区未跟踪文件
git clone	克隆版本库
git commit	提交
git config	查询和修改配置
git describe	通过里程碑直观地显示提交ID
git diff	差异比较
git difftool	调用图形化差异比较工具
git fetch	获取远程版本库的提交
git format-patch	创建邮件格式的补丁文件。参见 git am 命令
git grep	文件内容搜索定位工具
git gui	基于Tcl/Tk的图形化工具，侧重提交等操作
git help	帮助
git init	版本库初始化
git init-db*	同义词，等同于 git init
git log	显示提交日志
git merge	分支合并
git mergetool	图形化冲突解决
git mv	重命名
git pull	拉回远程版本库的提交
git push	推送至远程版本库
git reBase	分支变基
git rebase–interactive	交互式分支变基
git reflog	分支等引用变更记录管理
git remote	远程版本库管理
git repo-config*	同义词，等同于 git config
git reset	重置改变分支“游标”指向
git rev-parse	将各种引用表示法转换为哈希值等
git revert	反转提交
git rm	删除文件
git show	显示各种类型的对象
git stage*	同义词，等同于 git add
git stash	保存和恢复进度
git status	显示工作区文件状态
git tag	里程碑管理
```

2、对象库操作相关命令

```
命令	简要说明
git commit-tree	从树对象创建提交
git hash-object	从标准输入或文件计算哈希值或创建对象
git ls-files	显示工作区和暂存区文件
git ls-tree	显示树对象包含的文件
git mktag	读取标准输入创建一个里程碑对象
git mktree	读取标准输入创建一个树对象
git read-tree	读取树对象到暂存区
git update-index	工作区内容注册到暂存区及暂存区管理
git unpack-file	创建临时文件包含指定 blob 的内容
git write-tree	从暂存区创建一个树对象
```

3、引用操作相关命令

```
命令	简要说明
git check-ref-format	检查引用名称是否符合规范
git for-each-ref	引用迭代器，用于shell编程
git ls-remote	显示远程版本库的引用
git name-rev	将提交ID显示为友好名称
git peek-remote*	过时命令，请使用 git ls-remote
git rev-list	显示版本范围
git show-branch	显示分支列表及拓扑关系
git show-ref	显示本地引用
git symbolic-ref	显示或者设置符号引用
git update-ref	更新引用的指向
git verify-tag	校验 GPG 签名的Tag
```

4、版本库管理相关命令

```
命令	简要说明
git count-objects	显示松散对象的数量和磁盘占用
git filter-branch	版本库重构
git fsck	对象库完整性检查
git fsck-objects*	同义词，等同于 git fsck
git gc	版本库存储优化
git index-pack	从打包文件创建对应的索引文件
git lost-found*	过时，请使用 git fsck –lost-found 命令
git pack-objects	从标准输入读入对象ID，打包到文件
git pack-redundant	查找多余的 pack 文件
git pack-refs	将引用打包到 .git/packed-refs 文件中
git prune	从对象库删除过期对象
git prune-packed	将已经打包的松散对象删除
git relink	为本地版本库中相同的对象建立硬连接
git repack	将版本库未打包的松散对象打包
git show-index	读取包的索引文件，显示打包文件中的内容
git unpack-objects	从打包文件释放文件
git verify-pack	校验对象库打包文件
```

5、数据传输相关命令

```
命令	简要说明
git fetch-pack	执行 git fetch 或 git pull 命令时在本地执行此命令，用于从其他版本库获取缺失的对象
git receive-pack	执行 git push 命令时在远程执行的命令，用于接受推送的数据
git send-pack	执行 git push 命令时在本地执行的命令，用于向其他版本库推送数据
git upload-archive	执行 git archive –remote 命令基于远程版本库创建归档时，远程版本库执行此命令传送归档
git upload-pack	执行 git fetch 或 git pull 命令时在远程执行此命令，将对象打包、上传
```

6、邮件相关命令

```
命令	简要说明
git imap-send	将补丁通过 IMAP 发送
git mailinfo	从邮件导出提交说明和补丁
git mailsplit	将 mbox 或 Maildir 格式邮箱中邮件逐一提取为文件
git request-pull	创建包含提交间差异和执行PULL操作地址的信息
git send-email	发送邮件
```

7、协议相关命令

```
命令	简要说明
git daemon	实现Git协议
git http-backend	实现HTTP协议的CGI程序，支持智能HTTP协议
git instaweb	即时启动浏览器通过 gitweb 浏览当前版本库
git shell	受限制的shell，提供仅执行Git命令的SSH访问
git update-server-info	更新哑协议需要的辅助文件
git http-fetch	通过HTTP协议获取版本库
git http-push	通过HTTP/DAV协议推送
git remote-ext	由Git命令调用，通过外部命令提供扩展协议支持
git remote-fd	由Git命令调用，使用文件描述符作为协议接口
git remote-ftp	由Git命令调用，提供对FTP协议的支持
git remote-ftps	由Git命令调用，提供对FTPS协议的支持
git remote-http	由Git命令调用，提供对HTTP协议的支持
git remote-https	由Git命令调用，提供对HTTPS协议的支持
git remote-testgit	协议扩展示例脚本
```

8、版本库转换和交互相关命令

```
命令	简要说明
git archimport	导入Arch版本库到Git
git bundle	提交打包和解包，以便在不同版本库间传递
git cvsexportcommit	将Git的一个提交作为一个CVS检出
git cvsimport	导入CVS版本库到Git。或者使用 cvs2git
git cvsserver	Git的CVS协议模拟器，可供CVS命令访问Git版本库
git fast-export	将提交导出为 git-fast-import 格式
git fast-import	其他版本库迁移至Git的通用工具
git svn	Git 作为前端操作 Subversion
```

9、合并相关的辅助命令

```
命令	简要说明
git merge-base	供其他脚本调用，找到两个或多个提交最近的共同祖先
git merge-file	针对文件的两个不同版本执行三向文件合并
git merge-index	对index中的冲突文件调用指定的冲突解决工具
git merge-octopus	合并两个以上分支。参见 git merge 的octopus合并策略
git merge-one-file	由 git merge-index 调用的标准辅助程序
git merge-ours	合并使用本地版本，抛弃他人版本。参见 git merge 的ours合并策略
git merge-recursive	针对两个分支的三向合并。参见 git merge 的recursive合并策略
git merge-resolve	针对两个分支的三向合并。参见 git merge 的resolve合并策略
git merge-subtree	子树合并。参见 git merge 的 subtree 合并策略
git merge-tree	显式三向合并结果，不改变暂存区
git fmt-merge-msg	供执行合并操作的脚本调用，用于创建一个合并提交说明
git rerere	重用所记录的冲突解决方案
```

10、 杂项

```
命令	简要说明
git bisect–helper	由 git bisect 命令调用，确认二分查找进度
git check-attr	显示某个文件是否设置了某个属性
git checkout-index	从暂存区拷贝文件至工作区
git cherry	查找没有合并到上游的提交
git diff-files	比较暂存区和工作区，相当于 git diff –raw
git diff-index	比较暂存区和版本库，相当于 git diff –cached –raw
git diff-tree	比较两个树对象，相当于 git diff –raw A B
git difftool–helper	由 git difftool 命令调用，默认要使用的差异比较工具
git get-tar-commit-id	从 git archive 创建的 tar 包中提取提交ID
git gui–askpass	命令 git gui 的获取用户口令输入界面
git notes	提交评论管理
git patch-id	补丁过滤行号和空白字符后生成补丁唯一ID
git quiltimport	将Quilt补丁列表应用到当前分支
git replace	提交替换
git shortlog	对 git log 的汇总输出，适合于产品发布说明
git stripspace	删除空行，供其他脚本调用
git submodule	子模组管理
git tar-tree	过时命令，请使用 git archive
git var	显示 Git 环境变量
git web–browse	启动浏览器以查看目录或文件
git whatchanged	显示提交历史及每次提交的改动
git-mergetool–lib	包含于其他脚本中，提供合并/差异比较工具的选择和执行
git-parse-remote	包含于其他脚本中，提供操作远程版本库的函数
git-sh-setup	包含于其他脚本中，提供 shell 编程的函数库
```