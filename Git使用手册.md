#####  git 使用手册

* 创建版本库

```
mkdir learngit -- 创建新文件夹learngit，默认安装在C盘，可以切换盘符安装在其他盘（cd /d）
cd learngit  -- 定位到该文件夹
cd .. -- 退回上一级
pwd -- 显示当前目录
\Users\ewfem\learngit -- 显示的目录地址
```

* 把目录改成 git 可以管理的仓库

```
git init
```

* 把文件添加到版本库

```
1. 在learngit目录下创建一个文件readme.txt -- 不要用windows自带的笔记本，容易出问题，用vscode
2. git add readme.txt -- 把文件添加到仓库
3. git commit -m"wrote a new file" -- 把文件提交到仓库
```

* 查询仓库当前状态以及查询更改

```
git status	
git diff readme.txt
```

* 查看历史修改

```
git log -- 详细版
git log --pretty=oneline -- 精简版
```

* 版本回退

```
git reset --hard HEAD^ -- 上一个版本
-- 上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100
git reset --hard 1094a -- 1094a是版本号前面几位
git reflog -- git提供了一个命令用来记录你的每一次命令，可以查询到版本号，随时回退
cat readme.txt -- 查看文档内容
```

* 撤销修改

```
git checkout -- readme.txt 
-- a. 文件修改后并未放入暂存区，撤销后直接回到版本库一样的状态，工作区修改作废
   b. 文件已添加暂存区后又作修改，撤销使文件回到暂存区初始状态
【git checkout -- file】没有 -- 就变成切换分支的命令
git reset HEAD readme.txt -- 可以把暂存区的修改回退到工作区
```

* 删除文件

```
rm test.txt -- 直接在资源管理器删除或者rm命令删除
-- 删除后工作区和版本库不一致，如果要从版本库也删除，用命令git rm删掉，并且git commit
```

* 添加远程库

```
在github上创建一个新仓库，命名learngit
git remote add origin git@github.com:EWFEMLTY-D/learngit.git
-- 把EWFEMLTY-D替换成自己github的账户名
-- origin是默认的远程库名字，也可以改成别的
git push -u origin master -- 第一次推送需要加上 -u，可以把本地的master分支和远程的master分支关联起来
git push origin master -- 后续推送命令
```

* 删除远程库

```
git remote -v -- 查看远程库信息
git remote rm origin -- 删除远程库origin，这里的删除指的是解除本地与远程库的联系，真正删除需要在GitHub操作
```

* 从远程克隆

```
先创建一个新的github仓库，随意命名 test1，勾选下面的自动创建readme文件
git clone git@github.com:EWFEMLTY-D/test1.git

```

* 创建与合并分支

```
git checkout -b dev -- 创建且切换到分支dev，【git switch -c dev】相同效果
git branch dev -- 创建分支dev
git checkout dev -- 切换到分支dev，【git switch dev】相同效果
git branch -- 查看当前分支
git merge dev -- 把dev合并到master
git branch -d dev -- 删除分支dev
```

* 解决冲突

```
把文件修改一样后提交
git log --graph --pretty=oneline --abbrev-commit
-- 可以用来查看分支合并情况
git log --graph -- 可以用来查看分支合并图
```

* 分子管理策略

```
合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息；如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit
git merge --no-ff -m "merge with no-ff" dev -- 合并后创建了一个新的commit，分支信息保留
```

* BUG分支

```
git stash -- 把工作区储藏起来
git stash apply -- 恢复，但是stash内容不删除
git stash drop -- 删除stash内容
git stash pop -- 恢复并且删除stash内容
git stash list -- 查看stash清单
git stash apply stash@{0} -- 多个stash时，恢复指定的stash
git cherry-pick 4c805e2 -- 在master分支上修复了bug后，想把形同的修改复制到dev上【
$ git branch
* dev
  master
$ git cherry-pick 4c805e2】
```

* 删除一个分支

```
git branch -D <name> -- 丢弃一个没有被合并过的分支
```

