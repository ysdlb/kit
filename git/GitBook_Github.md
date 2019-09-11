# 将GitBook发布到GitHub pages
根据仓库分支以及分支存放内容的不同，将GitBook的项目的内容托管到GitHub page有多种
方法，下面简单记载一下我个人比较中意的一种方案。

一个仓库中有两个分支，master存放项目的源码，不包含gitbook生成_book文件，_book文件
放在gh-pages（github page的默认位置之一）分支里用来展示。master正常更新，保留
commit记录，而gh-pages分支每次覆盖push，不保留commit记录。

# 上传源码
1. 在github上新建一个仓库，暂且起名为`repo`吧，最好选择自动生成关于gitbook的`.gitignore`文件，那样我们就不用自己写了。
1. 回到本地的gibbook项目根目录，克隆新建的远程仓库`git clone git@github.com:<username>/repo.git`
1. 然后将文件`add`到暂存区、`commit`、`push`到远程仓库
```bash
git add .
# commit可以加--amend参数覆盖上次的提交，不过push的时候就得加-f参数强行push了。
git commit -m "your commit"
#git pull
git push
```

# 上传gitbook的生成文件到`gh-pages`分支
一般生成文件就在项目根目录下的`_book`文件夹里，我们进入该文件夹，先键一个空的
git仓库
```bash
git init
```
然后关联远程仓库
```bash
git remote add origin git@github.com:<username>/repo.git
```
`origin`是一个代表后面远程仓库地址的别名，大家习惯性的将远程仓库的别名叫做origin，
当然你也可以起别的名字。

然后新建一个上传用的gh-pages分支，`add`文件，`commit`，`push`到远程仓库
```bash
git checkout -b gh-pages		# 新建一个分支并切换到该分支
git add .
git commit -m "your commit"
# 它会在远程仓库新建一个gh-pages分支（如果没有的话），然后上传内容
git push -u origin gh-pages -f  # 不要往期commit记录，直接覆盖push就好
```
`-u`是`--set-upstream`的缩写，用来设置提交到哪个分支

## 常见错误
##### ref相关
```bash
error: src refspec gh-pages does not match any.
error: failed to push some refs to 'git@github.com:<username>/repo.git'
```

出现该错误会有两种情况
1. 当前分支是空的，从未commit过（默认空分支无法commit），使用`git commit --allow-empty`提交一次就好了
2. 本地当前分支与要push的远程分支名字不同，那么就要新建一个名字一样的本地分支。

##### github page仍然是404
推送到github上的gh-pages分支后，`<username>.github.io/repo`仍然是404错误，这时在
GitHub对应仓库的`Setting-->GitHub Pages`里选一个主题就好了。

开始是这样的：<br>
![github theme][1]

选完是这样的：<br>
![github theme][2]



[1]: ../source/000001.png "设置主题前"
[2]: ../source/000002.png "设置主题后"
