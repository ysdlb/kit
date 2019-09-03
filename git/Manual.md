# Blog
Share my ideas in this repository
#### git config
配置环境变量，可以针对所有用户、本用户
#### git status
1. 当前目录下是否有未跟踪的文件
1. 是否有文件在上次提交后更改过

#### git add
1. 开始跟踪新文件
1. 把已跟踪文件放到暂存区(修改过的)
1. 合并时把有冲突的文件标记为已解决状态
#### git diff
显示还没有暂存起来的改动，注意并不是这次工作和上次提交之间的差异，即单单git diff不过是显示还没有暂存起来的改动。若要查看已经暂存起来的文件和上次提交时的快照之间的差异，可以用`git dif --cached`命令，更高版本还允许用`git diff --staged`。

#### git commit
提交已经暂存起来的文件，所以每次提交前，用git status查看一下，确认还有什么修改过的或新建的文件还没有git add过。
* 在shell下执行此命令会启用shell的环境变量`$EDITOR`所指定的软件，用户也可以使用`git config --global core.editor`命令设置其他的编辑软件。
* 在调出的编辑软件中，默认的提交消息包含最后依次运行git status的输出，它们都被放到注释行里，用户也可以用-v选项将修改差异的每一行都包含到注释中去；**退出编辑器时，Git会丢掉注释行，将说明内容和本次更新提交到仓库。
* `-a`选项自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过git add步骤
* `-m`选项添加后不会进入编辑器，直接在`-m`参数后面加提交说明。
* `--amend`，修改最后一次提交，可以修改暂存区域，也可以修改提交说明

#### git rm
git rm后(一般该文件已经删除了)的文件不再纳入版本管理了。如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项`-f`，以防误删除文件后丢失修改的内容

如果只想把文件从Git仓库中删除（即暂存区），但仍然希望保留在当前工作目录中，要用--cached选项。

#### git mv
一般相当与下面三条命令：<br>
```bash
$ mv source dest
$ git rm source
$ git add dest
```
#### git log
查看提交记录，`git log -p -n <number>`可以限制输出的长度

#### git reset HEAD <fimename>
取消暂存

#### git checkout -- <file>
取消对文件的修改


##### git remote
列出远程仓库

* `-v`，在每个远程仓库名后显示对应的克隆地址，好像只有用SSH URL链接的那个远程仓库，我们才能推送数据上去（一般形式是git@github.com:username/depo.git
