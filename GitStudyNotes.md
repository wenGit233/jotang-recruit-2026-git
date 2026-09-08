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
$ mkdir learngit //创建
$ cd learngit  //进入
$ pwd  //显示目录
/Users/michael/learngit //显示的结果
```
- 变为可管理仓库
```bash
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

- 添加文件到版本库

`$ git add readme.txt` //可以add多个一并commit

`$ git commit -m "提交的说明" `//把文件提交到仓库

>Git命令必须在Git仓库目录内执行(先cd)
>用`ls`或者`dir`查看当前目录的文件

## 5.修改

- `git add`添加修改至暂存区
- `git status`显示仓库当前的状态
- `git diff`查看修改内容
- `git log`查看提交日志

## 6.传送

### 1.传送至某次commit
- `git reset --hard HEAD^`回退到上个版本，上上一个版本就是`HEAD^^`
- `git reset --hard <commit编码>`回退到某次commit
- `--hard`会回退到上个版本的已提交状态，而`--soft`会回退到上个版本的未提交状态，`--mixed`会回退到上个版本已添加但未提交的状态

*HEAD指针指向当前版本，回退使HEAD指向某版本号*
- `it log`查看提交历史，确定要回退到哪个版本。
- `git reflog`记录命令，确定前往哪个已回退的未来版本

### 2.
