# gitstudy
This is study git demo  <br>
学习git练习  <br>

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
  * git reset --hard HEAD^  //回到上一个版本
  * git reset --hard commit id(版本号)  //回到某个版本
  * 上一个版本就是HEAD^，上上一个版本就是HEAD^^，往上100个版本 HEAD~100

######小结：
    * HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
    * 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
    * 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

#####查看提交历史
  * git log

#####查看命令历史
  * git reflog

#####工作区与暂存区
  * Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
  * 把文件往Git版本库里添加的时候，是分两步执行的：
    * 第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
    * 第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
  * 因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
  * 可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。


</br>
</br>
</br>
</br>
</br>
原文：[git 廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)