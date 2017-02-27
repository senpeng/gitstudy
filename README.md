# gitstudy
This is study git demo  <br>
学习git练习  <br>

加入暂存区，提交到历史版本，再推送到远程  <br>
  * git add -A
  * git commit -m "说明"
  * git push origin master

查看仓库当前状态  <br>
  * git status

查看修改内容  <br>
  * git diff 文件名

回退版本  <br>
  * git reset --hard HEAD^  //回到上一个版本 <br>
  * git reset --hard commit id(版本号)  //回到某个版本 <br>
  * 上一个版本就是HEAD^，上上一个版本就是HEAD^^，往上100个版本 HEAD~100

查看提交历史  <br>
  * git log

查看命令历史  <br>
  * git reflog