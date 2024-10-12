git init:初始化仓库(本质是一个文件夹.git)
git status:显示暂存区状态
状态变换指令：

工作区：
git add <filenameA>:添加文件A到暂存区
git add <dirname>:添加文件夹及文件到暂存区
git add .：添加所有文件到暂存区（使用.gitignore配置忽略文件）
git diff：比较工作区与暂存区
git clean -f(d)：强制删除工作区文件(文件夹)

暂存区：
git commit -m "<messagename>":将暂存区所有文件添加到仓库
git commit -am "<messagename>":直接将文件移动到仓库
git commit -amend:回到上一步命令
git ls-files：查看暂存区中的文件信息
git rm --cacheed <filename>：移除暂存区文件

分支指令：
git branch (-r)：查看（远程）分支
git branch <branchname-A>:创建分支A 
git checkout <branchname-A>:进入分支A
git checkout -b <branchname-A>:创建并进入分支A
git merge --no-ff <branchname-B>:合并分支B
git merge <branchname-B> --allow-unrelated-histories：合并没有共同提交历史的分支
git reset --hard origin/<branchnameB>：强制重置为远程分支

历史跳转指令：
git log （--graph）：查看日志
git log -p:显示修改前后的日志
git reflog:查看所有日志

远程仓库操作：
git fetch origin：获取默认远程分支内容
git pull origin <remotebranchname>：<localbranchname>
git push origin <localbranchname>:<remotebranchname>：若远程没有分支则创建远程分支
git remote remove origin：删除远程仓库连接
git remote add origin <ssh>:将对应仓库设为远程仓库，名称设为origin
git clone <ssh>:获取对应内容
git push -f：强制完全修改远程仓库至本地仓库


git进阶操作：
git stash ：将当前修改存到暂存区，用于消除pull冲突
git stash pop：取出暂存区文件
git reset --hard：重置所有分支至上一次提交
git reset --hard <hashvalueA>: 回到合并前的状态（回退指针，丢失新纪录）
git revert <hashvalueA>：回退到指定版本，(生成新纪录)
git checkout <filename>：还原单个文件至最新提交
git rm --cache：将暂存区文件移回工作区
git clean -f(-d)：清空工作区文件(文件夹)
