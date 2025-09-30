

## 简洁版

```
clone（克隆）：从远程仓库中克隆代码到本地仓库

checkout（检出）：从本地仓库中检出一个仓库分支然后进行修订

add（添加）：在提交前先将代码提交到暂存区

commit（提交）：提交到本地仓库。本地仓库中保存修改的各个历史版本

fetch（抓取）：从远程仓库，抓取到本地仓库，不进行任何的合并动作，一般操作比较少

pull（拉取）：从远程仓库拉到本地仓库，自动进行合并(merge)，然后放到工作区，相当于fetch+merge

push（推送）：修改完成后，需要和团队成员共享代码时，将代码推送到远程仓库。


1. 查看本地分支

命令：git branch


2. 创建本地分支

命令：git branch 分支名


3. 切换分支

命令：git checkout 分支名

   还可以直接切换到一个不存在的分支（创建并切换）

命令：git checkout -b 分支名


4.合并分支

一个分支上提交的可以合并到另一个分支

命令：git merge 分支名 （将其他分支合并到当前分支）


5. 删除分支

注：不能删除当前分支，只能删除其他分支

命令：git branch -d 分支名 删除分支时，需要做各种检查

命令：git branch -D 分支名 不做任何检查，强制删除（一般是当前分支数据未合并到master）
```

## git命令

`git -v` 或者 `git --version` 查看当前版本



**【首次必须】设置签名用户、邮箱**

设置用户名、设置邮箱名、查询用户名、查询邮箱名：

```git
git config --global user.name USERNAME	//设置用户名
git config --global user.email EMAIL	//设置邮箱
git config --global user.name			//查询用户名
git config --global user.email			//查询邮箱
git config -l							//查看全部配置信息
```



**初始化本地仓库**

输入命令，将这个文件夹初始化为 git 仓库

```git
git init	
```



**查看本地库状态**

通过这个指令可以查看当前文件夹内的文件状态

```git
git status
```



**创建文件**

然后按 `i` 进入编辑模式，按Esc后 `yy` 复制，`p` 粘贴，编辑完成，按Esc后输入 `:wq` 退出，此时使用 `ll` 指令，显示文件，会发现已经创建了 `a.txt` 文件，然后查看文件内容，使用 `cat a.txt` 显示

```shell
vim a.txt
```



### 提交命令

**添加文件至暂存区**

```git
添加单个文件 git add filename

添加所有文件 git add .
```



**清除暂存区文件**

```git
git rm --cached <filename>
```



**提交仓库**

```git
git commit -m "内容" filename
```

可以将 `git add filename` 和 `git commit -m "message" filename` 合并成一条指令: `git commit -am "message"`



### 版本命令

**版本信息**

`reflog` 可查看所有历史记录，包括提交、切换和删除，`log` 可查看详细历史记录到当前 `HEAD` 所指向的记录，如果历史记录比较多，可以通过 `-n` 来显示前n行记录，当记录很多的时候，会显示`:`，按回车可以继续显示，按`Q`退出，如果觉得 `git log` 显示的信息太多，可以使用 `git log --pretty=oneline`

```git
查看版本信息：git reflog
查看详细信息：git log
```



**版本切换**

使用 `git reset --hard 版本号` 或者 `git reset --hard head@{index}`



**版本退回**
如果要退回上一个版本，可以使用`git reset --hard HEAD^`

如果退回上两个版本，可以使用`git reset --hard HEAD^^`

还可以使用个数n来，可以使用`git reset --hard HEAD~n`

未提交的操作版本，可以使用`git checkout -- 文件名（路径）`，也可以使用`git rm --cached 文件名（路径）`删除缓存区文件



### 分支命令

**查看分支**

`git branch -v`



**创建分支**

`git branch 分支名`



**切换分支**

`git checkout 分支名|版本号`



**合并分支**

`git merge 分支名`  将分支名合并到当前分支，如果没有冲突，则可以合并成功，如果有冲突，需要人为修改后提交合并



> 合并部分提交的代码

指令：`git cherry-pick 提交ID1 提交ID2…`

首先切换到需要合并到的分支，然后执行指定的`提交ID`，可以是多个分支，当没有冲突的时候，合并完成，当有冲突的时候，需要按照前面内容修改冲突内容后再次提交，也可以撤销此次提交操作，撤销指令：`git cherry-pick --abort` 冲突文件修改好了之后提交，会有`cherry-pick`的标记：



**删除分支**

`git branch -d 分支名`



**分支差异对比**

`git diff 当前分支 其他分支`



### 标签命令

`git tag`	查看所有标签

`git tag 版本号`	给当前最新的commit打上标签

`git tag 版本号 提交ID`	给指定的commit-id打上标签

`git tag -a 版本号 -m 描述信息`	 提交ID给指定的commit-id打上标签并附上说明文字

`git tag -d 版本号`	删除标签

## 连接Git Hub

### 1.克隆远程仓库到本地

指令：`git clone 远程地址`

### 2.查看当前远程别名

指令：`git remote -v`

查看当前所有远程地址别名

指令：`git remote add 别名 远程连接`

远程连接起别名

**其他操作**

查看远程仓库：`git remote -v`

添加远程仓库：`git remote add [name] [url]`

删除远程仓库：`git remote rm [name]`

修改远程仓库：`git remote set-url --push [name] [newUrl]`

### 3.拉取推送

拉取远程仓库：`git pull [remoteName] [localBranchName]`

推送远程仓库：`git push [remoteName] [localBranchName]`

将本地的分支提交到远程仓库，并作为master分支或者其他分支

可使用：`git push origin 本地分支:远程分支`

推送到远程一般使用：git push origin master，第一次会提示登录，需要登录相关账号