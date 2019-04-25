##GIT

--1.拉取和上传
git pull
git push 
切记：一定是在pull之后再进行push，否则有可能会覆盖其他代码
强制提交：git push -u origin master -f

--2.切换分支
查看远程分支：git branch -a 
本地创建一个分支： git checkout -b dev 
远程分支拉取到本地： git checkout -b 本地分支名 origin/远程分支名 

--3.提交一次代码流程
git add /xx/xx/*   可单个或多个
git commit -m "影像系统加入OSS相关操作接口代码"  提交到本地库，并带有说明
git pull  或 git pull origin dev
git push 或 git push origin dev

--4.保护工作区现场
git stash
git stash list
git stash pop stash@{num}。num 就是你要恢复的工作现场的编号。
git stash clear 
git stash apply stash@{num}方法 除了不在stash队列删除外其他和git stash pop 完全一样。

git checkout -- file  未add以及commit，回退到编辑前
git reset HEAD file 已commit的回退

4、推送本地分支local_branch到远程分支 remote_branch并建立关联关系
      a.远程已有remote_branch分支并且已经关联本地分支local_branch且本地已经切换到local_branch
          git push
     b.远程已有remote_branch分支但未关联本地分支local_branch且本地已经切换到local_branch
         git push -u origin/remote_branch
     c.远程没有有remote_branch分支并，本地已经切换到local_branch
        git push origin local_branch:remote_branch
例子： git  push origin dev:dev
github上已经有master分支 和dev分支
在本地
git checkout -b dev 新建并切换到本地dev分支
git pull origin dev 本地分支与远程分支相关联
在本地新建分支并推送到远程
git checkout -b test
git push origin test   这样远程仓库中也就创建了一个test分支


5、删除本地分支local_branch
      git branch -d local_branch
6、删除远程分支remote_branch
     git push origin  :remote_branch
     git branch -m | -M oldbranch newbranch 重命名分支，如果newbranch名字分支已经存在，则需要使用-M强制重命名，否则，使用-m进行重命名。
   git branch -d | -D branchname 删除branchname分支
   git branch -d -r branchname 删除远程branchname分支

7。标签（tag）可以针对某一时间点的版本做标记，常用于版本发布。
列出标签
// 在控制台打印出当前仓库的所有标签
$ git tag 
// 搜索符合模式的标签
$ git tag -l ‘v0.1.*’ 
打标签
git标签分为两种类型：轻量标签和附注标签。轻量标签是指向提交对象的引用，附注标签则是仓库中的一个独立对象。建议使用附注标签。

// 创建轻量标签
$ git tag v0.1.2-light
// 创建附注标签
$ git tag -a v0.1.2 -m “0.1.2版本”
创建轻量标签不需要传递参数，直接指定标签名称即可。
创建附注标签时，参数a即annotated的缩写，指定标签类型，后附标签名。参数m指定标签说明，说明信息会保存在标签对象中。
切换到标签
与切换分支命令相同，用git checkout [tagname]
查看标签信息
用git show命令可以查看标签的版本信息：
$ git show v0.1.2
删除标签
误打或需要修改标签时，需要先将标签删除，再打新标签。
// 删除标签
$ git tag -d v0.1.2 
参数d即delete的缩写，意为删除其后指定的标签。
给指定的commit打标签
打标签不必要在head之上，也可在之前的版本上打，这需要你知道某个提交对象的校验和（通过git log获取）。
// 补打标签
$ git tag -a v0.1.1 9fbc3d0
标签发布
通常的git push不会将标签对象提交到git服务器，我们需要进行显式的操作：
# 将v0.1.2标签提交到git服务器
$ git push origin v0.1.2 
# 将本地所有标签一次性提交到git服务器
$ git push origin –tags 
 
注意：如果想看之前某个标签状态下的文件，可以这样操作
1.git tag   查看当前分支下的标签
2.git  checkout v0.21   此时会指向打v0.21标签时的代码状态，（但现在处于一个空的分支上）
3. cat  test.txt   查看某个文件

廖雪峰git博客地址：
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000
