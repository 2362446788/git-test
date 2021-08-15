#### git 基础知识
1. git是一个分布式版本控制系统，与SVN这样的集中式版本控制系统不一样，git在本地也维护着一个本地仓库，这样即使没有网络也可以正常进行工作，只要最后将自己的修改同步到远端即可，而SVN就很依赖于网络连接，并且要求的带宽很高。
2. git分为工作区workspace、暂存区stage|idnex、本地仓库(历史区)local repository、远程仓库remote repository；
    + workspace：工作区，平时存放代码的地方；文件状态有四个：未被追踪untracked、未被修改unmodified、已修改modified、staged已暂存；
        - untracked：未被追踪，一般是在当前仓库中新增的文件，之前未存在于该仓库；这样的文件可以通过git add将状态修改为staged添加到仓库中；添加图片进来。
        - unmodified：未被修改，一般是该仓库中原来的文件，没有进行任何操作；这样的文件有两种去处：
            + 修改文件内容变将状态变为modified；
            + 通过git rm 文件名 --cache将文件从仓库中删除，即不追踪该文件，状态变为untracked。
        - modified：已修改，一般指仓库中被修过的文件；
        - staged：暂存，一般指在workspace通过git add提交过来的文件
    + stage：暂存区，将工作区的内容提交过来变为暂存状态



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