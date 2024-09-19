git init:初始化仓库
git status:显示暂存区状态

git add <filenameA>:添加文件A到暂存区
git commit -m "<logname>":将暂存区文件添加到仓库
git commit -am "<logname>":直接将文件移动到仓库
git commit -amend:回到上一步命令

git branch <branchname-A>:创建分支A 
git checkout <branchname-A>:进入分支A
git checkout -b <branchname-A>:创建并进入分支A

git log （--graph）：查看日志
git log -p:显示修改前后的日志
git reflog:查看所有日志
git reset --hard <hashvalueA>: 回到合并前的状态

git merge --no-ff <branchname-B>:合并分支B

git diff:查看暂存区和工作区的差别
git diff head: 查看与最新提交的差别

git remote add origin <ssh>:将对应仓库设为远程仓库，名称设为origin
git clone <ssh>:获取对应内容
