# Git笔记
## 使用命令+文字描述以下过程：
### 实现在桌面中创建一个git项目，在项目中添加文件，并提交到本地仓库的操作步骤
+ mkdir app
+ cd app
+ git init
+ touch 1.txt
+ git add *
+ git commit -m 第一次提交


### 在公司里面，我自己在github中创建了一个空仓库，为了把本地代码上传到这个仓库中，我应该执行哪些操作
+ mkdir app
+ cd app
+ git init
+ touch 1.txt
+ git add *
+ git commit -m 第一次提交
+ git push 远程仓库地址 master

### 在公司里面，领导让我对某个github的项目进行二次开发，比如我要开发一个新功能(比如添加test.html文件)，我应该执行哪些步骤从而将test.html文件提交到服务器中
+ mkdir app
+ cd app
+ git init
+ git pull 远程仓库地址 master
    - 一方面下载了代码，另一方面也是将本地仓库和远程仓库形成了关联
+ touch test.html
+ git add *
+ git commit -m 添加了新内容
+ git push 远程仓库地址 master



### 如果当前位于cart分支，我需要将cart分支合并到master分支，我应该执行哪些操作
+ git checkout master
+ git merge cart


## 命令默写
### 创建新分支
+ git branch 分支名称

### 删除某个分支
+ git branch -d 分支名称

### 切换分支
+ git checkout 分支名称

### 分支合并
+ git merge 分支名称

### 查看所有分支-->并说明如何辨别当前位于哪个分支
+ git branch
+ 分支名称前面的*表示当前位于的分支

## 分支操作步骤
+ 在mater里面提交了登录功能
+ 创建分支：shouye
+ 切换分支：shouye
+ 在shouye分支中完成了一部分的首页的功能
+ 先把首页的这部分功能提交(☆)
+ 切换分支到master
+ 在master分支中修改登录功能的bug，并提交
+ 切换分支到shouye
+ 完成shouye的剩下功能吧，并提交
+ 切换分支到master
+ 将shouye分支合并到master中
+ 把shouye分支给删除

## 查看分支的问题
+ 如果一个仓库中没有任何提交操作，那么通过git branch命令没有任何输出，相对应的这个时候创建分支也是无法实现的

## 分支之间的关系
![](分支之间的关系.png)

## 比较文件差异：git diff
1、比较工作区和暂存区的代码比较
2、如果暂存区没有文件，则将工作区和最近一次提交的代码进行对比

### git diff --cached
将暂存区的文件和工作区的文件进行对比

### git diff HEAD^ HEAD
比较上次提交commit和上上次提交

### git diff SHA1 SHA2
+ 其中SHA1 和SHA2分别表示2个版本的ID号
+ 比较两个历史版本之间的差异

### tortoiseGit基本操作
+ git init -->右击文件夹空白处，选择新建版本库
+ git add /git commit -->右击仓库空白处，选择commit菜单输入相应的备注信息，点击commit按钮，即可完成提交
    - 如果说一个文件是新创建的，要注册commit的时候要先从文件列表中选中该文件，之后才能完成正常提交，否则该文件无法提交成功
+ git pull
    - 在仓库的空白处右击选择pull命令即可
        - 之后需要在Arbitrary URL栏中，输入服务器地址(HTTPS)
+ git push
    - 在仓库的空白处右击选择push命令即可

#### 几种图标
+ 新创建的文件上没有任何图标
+ 如果新创建的文件已经被添加到暂存区，将会显示 +号
+ 如果一个文件被修改了，将会显示 !号
+ 如果一个文件已经被提交到本地主仓库了，将会显示：√符号

## git clone 远程仓库地址 master
+ 可以一次性的完成git init + git pull的操作



## git add更多用途
### git add *
+ 把整个仓库中所哟逇未追踪的以及修改的文件添加到暂存区
☆注意☆：不包括删除

### git add 目录名称
默认为将修改操作的文件和未跟踪新添加的文件添加到git系统的暂存区
☆注意☆：不包括删除

### git add -u 等价于 git add --update
把修改的文件和删除的文件都一次性的添加到暂存区

### git add -A  等价于 git add --all
把修改的文件与删除的文件、未跟踪的文件都一次性的添加到暂存区。



## 删除服务器中的文件
### 第一种方式：
+ rm 文件名
+ git add 文件名
+ git commit -m 提交
+ git push 远程服务器 master

### 第二种方式：
+ git rm 文件名
+ git commit -m 提交
+ git push 远程服务器 master



## 单文件特殊操作
### git reset HEAD 1.txt
+ 实现：将暂存区的文件取出来，对工作目录的代码不会造成影响
+ 实际上它就是git add 命令的反操作

### git checkout -- 1.txt
+ 优先从暂存区恢复指定文件内容内容到工作区
+ 如果暂存区没有内容，会从本地仓库恢复指定文件内容到工作区



## 多文件特殊操作
### git reset --hard
+ 实现将工作区的代码恢复到指定版本内容
+ 不仅可以往前恢复，也可以往后恢复(提交日志)
    - 如果往前恢复，后面提交的内容就无法通过git log获取提交日志，无法获取版本号，但是这个时候可以通过git reflog 查看到之后的版本号
+ ps：提交的版本号(可以只写前几位,但是一定要唯一)

### git reflog 查看历史记录
这些历史记录包括：a、每一次提交的信息；b、每一次版本回滚的操作；c、分支切换操作



## 设置文件不让git管理
1. 在.git同级目录添加一个文件，叫<font color=red size=5>.gitignore</font>
    + 创建这个文件名的时候，有以下2种方式可以创建：
        + 文件名：<font size=5>.gitignore.</font>
        + bash命令：touch .gitignore
2. 打开.gitignore进行编辑，一行一行的添加不需要git管理的文件
    + 可以设置同类型的文件：*.js *.css
    + 也可以设置整个目录：
        a/*-->a目录下面的所有文件
        a/*.js-->a目录下面的所有js文件

