#### git 基础知识
1. git是一个分布式版本控制系统，与SVN这样的集中式版本控制系统不一样，git在本地也维护着一个本地仓库，这样即使没有网络也可以正常进行工作，只要最后将自己的修改同步到远端即可，而SVN就很依赖于网络连接，并且要求的带宽很高。
2. git分为工作区workspace、暂存区stage|idnex、本地仓库(历史区)local repository、远程仓库remote repository；
    + workspace：工作区，平时存放代码的地方；文件状态有四个：未被追踪untracked、未被修改unmodified、已修改modified、staged已暂存；
        - untracked：未被追踪，一般是在当前仓库中新增的文件，之前未存在于该仓库；这样的文件可以通过git add将状态修改为staged添加到仓库中；添加图片进来。
        - unmodified：未被修改，一般是该仓库中原来的文件，没有进行任何操作；这样的文件有两种去处：
            + 修改文件内容变将状态变为modified；
            + 通过git rm 文件名 --cache将文件从仓库中删除，即不追踪该文件，状态变为untracked。git rm的其余操作看这儿
        - modified：已修改，一般指仓库中被修过的文件；
        - staged：暂存，一般指在workspace通过git add提交过来的文件
    + stage：暂存区，将工作区的内容提交过来变为暂存状态

#### git rm
1. git rm 文件：首先会将工作区的文件删除，并且会将这次删除记录到stage中，就相当于rm + git add的操作；
    + rm：下图是rm操作及回撤：
    + git rm：下图是git rm操作及回撤：
2. git rm 文件 --cache：将文件从追踪状态中撤离，变为untracked状态。

#### git rm
1. git rm 文件：首先会将工作区的文件删除，并且会将这次删除记录到stage中，就相当于rm + git add的操作；
    + rm：下图是rm操作及回撤：
    + git rm：下图是git rm操作及回撤：
2. git rm 文件 --cache：将文件从追踪状态中撤离，变为untracked状态。

#### git checkout和git reset回撤
1. git checkout：
    + git checkout 文件：将暂存区的文件回撤到工作区,例如修改某个文件，但是不想要这些修改可以回撤，删除也是，如果暂存区没有这个文件回撤不了；
    + git checkout commit 文件：将某次提交的commit的文件回撤覆盖暂存区和工作区。
2. git reset：
    + git reset 文件：回撤暂存区的文件。例如add进来的文件可以通过这个回撤，删除也可以；
    + git reset --hard：重置工作区和暂存区，与上一次commit保持一致；
    + git reset commit：将HEAD指向commit，更新暂存区，工作区不变；
    + git reset --hard commit：回撤版本到commit，工作区和暂存区都改变。
#### git stash
当开发被中断时，并且不想提交commit，可以采取stash。
1. git stash：将工作区的文件修改都放在stash隐藏栈中，这样可以进行pull操作等等，之后再取出来即可；
2. git stash list：查看当前被stash的内容；
2. git stash pop：将保存进去的内容取出来。

#### git commit
commit可以将暂存区中的文件提交到本地仓库历史区中。
1. git commit -m 'message'：提交一个版本，message为提交的信息；
2. git commit -a：基于上次提交，将工作区的文件直接提交成一个版本，对新增文件无效，不建议使用；
3. git commit -v：提交时展示所有的diff信息；
4. git commit --amend -m 'message'：使用一次新的commit，替代上一次提交，如果代码没有任何新变化，则用来改写上一次commit的提交信息；
5. git commit --amend [file1] [file2]：重做上一次提交，包含新文件更新。


首先可以通过两种方式创建git仓库和远程仓库进行连接：
**git init**
在本地先通过git init创建一个本地的git仓库，再通过git remote add origin [git地址]进行关联。
关联之后可以通过 git remote -v 查看连接到关联名和仓库地址;
<!-- TODO 将图片加进来 -->
如果不想要再关联，那么可以使用git remote remove [关联名]；
如果本地的分支为main，而远程的为master，那么直接git push是不行的，需要先创建一个远程分支main，可以通过git push origin main创建远程分支并且上传上去，后续的话每一次提交都需要指定主机和分支名，可以通过git push --set-upstream [主机] [分支名]来进行绑定，后续就不需要指定了。
仓库中的分支都是互相不影响的，当功能开发完成可以进行合并。
**git clone [git地址]**
直接通过git clone进行项目克隆。
通过clone的自动建立了--set-upstream连接，不需要指定分支名（只限克隆下来的master或者main分支），对于新创建的分支也需要像git init一样操作。

直接克隆远程分支：

1. git clone [远程地址] 
   git fetch origin [远程分支名] (这一条是针对老项目，如果是新项目直接clone不需要fetch就是最新的)
    git checkout -b [本地分支名] origin/[远程分支名] （将两个分支产生连接关系），push不需要指明了
2. git clone -b [远程分支名] [地址]

新建分支与远端产生追踪关系：

#### git的流程
1. git init 
2. git clone 



**新建分支**
可以在当前分支分离出一个新的分支，是基于当前分支。
通过git checkout -b [分支名]进行创建并切换
git checkout [分支名] 切换分支
git branch 查看本地分支
git branch -r 查看远程分支
git branch -a 查看本地和远程分支