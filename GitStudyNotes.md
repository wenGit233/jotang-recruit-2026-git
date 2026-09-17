# Git Study Notes

## 1.Git介绍

> 分布式版本控制系统
### 分布式

>每人都有完整版本库  

**优点**
*安全(多备份)*
*无需联网*
*分支管理*

## 2.安装配置

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
>优先级：本地（local仅当前仓库）>全局（global该用户所有仓库）>系统（system所有用户）
>按优先级扫描叠加


## 3.创建版本库

- 创建空目录
```bash
$ mkdir gitnote //创建
$ cd gitnote  //进入
$ pwd  //显示目录
/Users/michael/gitnote //显示的结果
```
- 变为可管理仓库
```bash
$ git init
Initialized empty Git repository in /Users/michael/gitnote/.git/
```

- 添加文件到版本库

`$ git add <文件名.文件类型>` //可以add多个一并commit

`$ git commit -m "提交的说明" `//把文件提交到仓库

>Git命令必须在Git仓库目录内执行(先cd)
>用`ls`或者`dir`查看当前目录的文件

## 4.修改

- `git add`添加修改至暂存区
- `git status`显示仓库当前的状态（暂存区是否commit，工作区的改动和新文件）
- `git diff`查看修改内容
- `git log`查看提交日志

## 5.传送

### 1.传送至某次commit
- `git reset --hard HEAD^`回退到上个版本，上上一个版本就是`HEAD^^`
- `git reset --hard <commit编码>`回退到某次commit
- `--hard`会回退到上个版本的已提交状态，而`--soft`会回退到上个版本的未提交状态，`--mixed`会回退到上个版本已添加但未提交的状态

*HEAD指针指向当前版本，回退使HEAD指向某版本号*
- `git log`查看提交历史，确定要回退到哪个版本。
- `git reflog`记录命令，确定前往哪个已回退的未来版本

## 6.工作区和暂存区
- 工作区(修改)---git add---暂存区----git commit---版本库

- 版本库中有*暂存区，历史快照与文件内容，标签和指针*

## 7.修改管理

- **多次修改**可修改后仅add，再一并提交
- **撤销修改**`git checkout -- gitnote.md`  
回到最近一次`git commit`或`git add`状态
- **撤销暂存区修改并放回工作区**`$ git reset HEAD <文件名.文件类型>`
- **修改了还提交了**版本回退
- **删除文件**`rm <>`再commit

## 8.远程连接

- `git remote add origin git@server-name:path/repo-name.git`//origin是起的仓库别名
- `git push -u origin main`推送main分支的所有内容
- 之后`git push origin main`更新修改
- `git remote rm origin`删除远程仓库（删除别名且不能推送）  

- `git clone git@github.com:用户名/仓库名.git`克隆GitHub仓库
//Git支持多种协议，包括https，但ssh协议（git@开头）速度最快

## 9.分支管理

时间线就是一个分支，仅一条分支时叫主分支（main分支）。HEAD指向的就是当前分支，so创建一个指针来创建新分支
- 查看分支：`git branch`
- 创建分支：`git branch <name>`
- 切换分支：`git checkout <name>或者git switch <name>`
- 创建+切换分支：`git checkout -b <name>或者git switch -c <name>`
- 合并某分支到当前分支：`git merge <name>`
- 删除分支：`git branch -d <name>`

**冲突**
当Git无法自动合并分支时，先解决冲突，把Git合并失败的文件手动编辑，再提交，完成合并
`git merge --no-ff -m "merge with no-ff" dev `//使历史有分支可见
`git log --graph --pretty=oneline --abbrev-commit` //显示图表
>管理策略:不在main,在其他分支上修改并合并

**bug**
- 未提交工作且要改bug  
1.`git stash`储藏工作区
2.从要修改的分支出新建分支，修改，合并，删除分支
3.`git stash list`查看储存的工作区
4.恢复：用`git stash apply`恢复，用`git stash drop`来删除stash内容；
or用`git stash pop`，恢复的同时把stash内容也删了
5.修改其他分支：`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支

**丢弃分支**
- 丢弃一个没有被合并过的分支`git branch -D <name>`强行删除。

## 10.标签

- `git tag <name>`打一个标签

- `git tag`查看标签

- `git tag -a <tagname> -m "blablabla..."`可以指定标签信息；

- `git show <tagname>`查看标签信息

- `git push origin <tagname>`可以推送一个本地标签；
- `git push origin --tags`可以推送全部未推送过的本地标签；
- `git tag -d <tagname>`可以删除一个本地标签；
- `git push origin :refs/tags/<tagname>`可以删除一个远程标签。