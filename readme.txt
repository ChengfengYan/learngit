Git is a free software.
Git is a free software ...
Creating a new branch is quick.
Creating a new branch is quick AND simple.
Creating a new branch is quick and simple.
q
q

<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> new_branch

Creating a new branch is quick and simple.


初始化一个Git仓库，使用git init命令。

添加文件到Git仓库，分两步：
使用命令git add <file>，注意，可反复多次使用，添加多个文件；
使用命令git commit -m <message>，完成。(git commit -m "add 3 files.")
前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
每次修改，如果不用git add到暂存区，那就不会加入到commit中。

要随时掌握工作区的状态，使用git status命令。
如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。 如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--oneline参数：
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
rm 用于删除本地文件。命令git rm用于删除版本库中文件。删除后并git commit。若误删则可以使用git checkout来使用版本库中版本替代工作区版本。

GitHub Git远程仓库托管服务网站 也可自己搭建运行Git的服务器作为Git远程仓库。
从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。

要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
(git remote add origin git@github.com:ChengfengYan/learngit.git)
关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，当有网络的时候，再把本地提交推送一下就完成了同步.

要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。(git clone git@github.com:ChengfengYan/gitskills.git)
Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>
Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容
git log --graph --pretty=oneline可以看提交的历史版本
git log --graph --pretty=oneline --abbrev-commit可以看分支合并情况
git merge --no-ff -m "merge with no-ff" name 可以在分支历史上看出分支信息
在实际开发中，我们应该按照几个基本原则进行分支管理：
首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场
git stash list 可查看stash状态

开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

要查看远程库的信息，用git remote
用git remote -v显示更详细的信息
git push origin master可推送本地master

master分支是主分支，因此要时刻与远程同步；
dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

因此，多人协作的工作模式通常是这样：
首先，可以试图用git push origin <branch-name>推送自己的修改；
如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
如果合并有冲突，则解决冲突，并在本地提交；
没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。





