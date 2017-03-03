# gitstudy
This is study git demo  <br>
学习git练习  <br>

####本地仓库
#####创建版本库
  * git add -A                  // 加入暂存区
  * git commit -m "说明"         // 提交到历史版本
  * git push origin master      //再推送到远程

######小结：
    * 初始化一个Git仓库，使用git init命令。
    * 添加文件到Git仓库，分两步：
        * 第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；
        * 第二步，使用命令git commit，完成。
    * 每次修改，如果不add到暂存区，那就不会加入到commit中。

#####查看仓库当前状态
  * git status

######小结：
    * 要随时掌握工作区的状态，使用git status命令。

#####查看修改内容
  * git diff 文件名
  * git diff HEAD --文件名     //查看工作区与版本库里面最新版本的区别

######小结：
    * 如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

#####版本回退  <br>
  * git log			 //查看提交历史
  * git reflog 		 //查看命令历史
  * git reset --hard HEAD^  //回到上一个版本
  * git reset --hard commit id(版本号)  //回到某个版本
  * 上一个版本就是HEAD^，上上一个版本就是HEAD^^，往上100个版本 HEAD~100

######小结：
    * HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
    * 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
    * 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

#####工作区与暂存区
  * Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
  * 把文件往Git版本库里添加的时候，是分两步执行的：
    * 第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
    * 第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
  * 因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
  * 可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

#####撤销修改
  * git checkout -- file  //可以丢弃工作区的修改：
  * 命令git checkout -- file 意思就是，把file文件在工作区的修改全部撤销，这里有两种情况：
    * 一种是file自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
    * 一种是file已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
  * 总之，就是让这个文件回到最近一次git commit或git add时的状态。
  * __git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令__。
  * 如果修改完后git add 到暂存区，但是在git commit，可以用git reset HEAD file把暂存区的修改撤销掉，重新放回工作区。
  * 用git reset HEAD file 后再用git checkout -- file 可以丢弃掉工作区的修改。
  * git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。
  * 当改错了东西，还从暂存区提交到了版本库时，可以用 *版本回退* 回退到上一个版本。前提是还没有把本地版本推送到远程。

######小结：
    * 场景1：当改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
    * 场景2：当不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，
            就回到了场景1，第二步按场景1操作。
    * 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，用版本回退，不过前提是没有推送到远程库。

#####删除文件
  * 当在文件管理器中把没用的文件删了，或者用rm命令删了时，有两种情况：
    * 一种是确实要从版本库中删除该文件，那就用命令 git rm file 删掉，并且 git commit；
    * 一种情况是删错了，因为版本库里还有，所以可以用 git checkout -- file 把误删的文件恢复到最新版本。
  * git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

######小结：
    * 命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，
      但是要小心，你只能恢复文件到最新版本，你会丢失 __最近一次提交后你修改的内容__

####远程仓库
#####添加远程库（先有本地库，后有远程库）
  * 关联远程库：git remote add origin git@server-name:path/repo-name.git。
  * 关联后，把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
  * 第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
    还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
  * 把本地master分支的最新修改推送至GitHub：git push origin master。

######小结：
    * 要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
    * 关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
    * 此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改。

#####从远程库克隆（先有远程库，后有本地库）
  * 先在GitHub上创建一个新的仓库，然后使用 git clone git@server-name:path/repo-name.git 克隆一个本地库。
  * Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议.

######小结：
    * 要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
    * Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

####分支管理
#####创建于合并分支
  * 在Git里HEAD指向主分支master，而master指向提交，所以HEAD指向的就是当前分支。
  * master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点；
    每次提交，master分支都会向前移动一步，这样，随着不断提交，master分支的线也越来越长。
  * 当创建新的分支时，例如dev，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上；
    从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变。
  * Git分支合并最简单的方法，就是直接把master指向dev的当前提交，就完成了合并。

######小结：
    * 查看分支：git branch       //git branch命令会列出所有分支，当前分支前面会标一个*号
    * 创建分支：git branch <name>
    * 切换分支：git checkout <name>
    * 创建+切换分支：git checkout -b <name>
    * 合并某分支到当前分支：git merge <name>
    * 删除分支：git branch -d <name>

#####创建于合并分支
  * Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容。
  * git log --graph --pretty=oneline --abbrev-commit        //查看分支的合并情况

######小结：
    * 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
    * 用git log --graph命令可以看到分支合并图。

#####分支管理策略
  * 通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
  * 如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
  * git merge --no-ff -m "描述" 分支名。
  * 分支管理基本原则：
    * 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
    * 干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
    * 每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

######小结：
    * 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，
      而fast forward合并就看不出来曾经做过合并。

#####Bug分支
  * 软件开发中，bug就像家常便饭一样。在Git中，由于分支是如此的强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。
  * 当需要修复bug而分支上的工作还没完成时，可以用git stash功能将当前的工作现场“储存”起来，等以后恢复现场后继续工作。
  * 用git stash list查看“储存”起来的工作现场列表。
  * 恢复工作现场有两种方法：
    * 一时用git stash apply恢复，但是恢复后，stash内容并不删除；
    * 另一种方式是用git stash pop，恢复的同时把stash内容也删了
  * 可以多次stash，恢复的时候，先用git stash list查看，然后用git stash apply stash@{0}恢复指定的stash

######小结：
    * 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
    * 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。


</br>
</br>
</br>
</br>
</br>
原文：[git 廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)