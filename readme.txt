Git is a free software.
Creating a new branch is quick.
Creating a new branch is quick AND simple.

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





