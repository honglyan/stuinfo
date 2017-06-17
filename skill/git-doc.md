# git在linux环境下的安装及使用

## 注册一个github账户
使用git我们首先需要在[github](https://github.com/)注册一个账户来存放文件。

## 安装git
使用下列命令安装git工具：  
> sudo apt-get install git

## git的使用
### 1. 创建版本库
* 第一步, 先要创建一个目录, 这个目录就是用来存放仓库的.并且进入这个目录里面
> mkdir html  
> cd html  

* 第二步, 使用git init命令, 将当前目录创建成git仓库.
> git init  

Initialized empty Git repository in /home/user/html/.git/  
马上就把仓库创建成功了, 并提示这是一个空仓库.

### 2. git的基本使用
* 首先在这个目录底下创建一个文件    
> touch README.md   

* 其次打开这个文件编辑一些东西  
> vim README.md    

* 编辑完成后查看仓库的状态  
> git status  

通过这个命令我们可以看到仓库的改变，这里会提醒我们仓库中多了一个新文件README.md并且显示为红色，说明改文件还没有被关注  

* 对文件添加关注 
>git add README.md  

这时候如果在查看状态的话README.md就会变为绿色，表明已经被关注了  

* 提交  
>git commit  

提交需要填写标题和内容，标题和内容中间必空一行。
第一次提交时会要求你提交姓名和email  
> git config --global user.name "你的名字"
> git config --global user.email "email地址"

* 查看提交信息(日志)
>git log  
日志中一般带有commit ID和提交的标题内容，在后面commit ID会被使用.  

* 移除关注  
>git rm -cached README.md  

* 版本回退
>git reset --hard commitID  

版本的时候需要你需要回退到的那个版本的commitID。

### 3. git的分支
在创建仓库的同时会创建一个master的分支。  
以下是基本命令：
* 创建分支  
> git branch branch_name  
* 切换分支  
> git checkout branch_name 
* 显示目前所有的分支  
> git branch -av  
* 删除分支,但是不能删除现在所在的分支，必须先切换到其他分支上。
>git branch -D branch_name   
* 合并分支，合并分支之前先切换到需要合并到的分支上去，如b分支要合并到master上去
> git checkout master 
> git merge b
* 衍合分支
>  git rebase master b

### 4. git与github的连接




