# git
https://www.liaoxuefeng.com/wiki/896043488029600
https://zhuanlan.zhihu.com/p/369486197
## git简介
* 分布式版本控制系统，开始基于linux，可以在linux，unix，mac，windows运行，git优秀之处在于它跟踪并管理的是修改而非文件，注册时候不要加双引号，不要使用win自带的记事本编辑，路径不要由中文
* git config --global user.name xx 》 git config --global user.email xx 》 git init 》 git add xx 》 git commit 》 

## 时光穿梭机
* git status查看仓库当前状态，比如某文件是否修改是否提交修改；git diff xx查看具体修改内容difference
* git log查看修改历史记录；git log --pretty=oneline简化展示信息；可以看到commit id
* git reset --hard HEAD^，几个^回退几个版本；使用cat xx查看则显示为上一个版本了；此时git log最新一次会消失，需要使用git reset --hard 1094a（版本号前几位即可）回退，因此可以使用git reflog查看各次版本号commit id
* 工作区：含.git的文件夹即为工作区；.git不是工作区，而是版本库repository，在版本库中有暂存区stage和分支master；add 把文件修改放到stage，commit把暂存区所有内容交到当前分支master；所以必须先add再commit否则不能提交
* 撤销修改：
    * 文件只在工作区操作，未add。撤销操作：git restore <file>。结果：工作区文件回退。
    * 文件已add，未commit。撤销操作：git restore --staged <file>。结果：暂存区文件回退，工作区文件未回退，如需继续回退，操按情况1操作。
    * 文件已add，已commit。撤销操作：git reset --hard commit_id或者HEAD^。结果：工作区文件、暂存区文件、本地仓库都回退
* 删除操作：删除本质也是一种修改
    * 文件只在工作区删除（手动或者rm），恢复：git restore <file>。
    * 文件在工作区删除，且已git add（或者git rm等效）、commit，git reset --hard commit_id或者HEAD^
    * 注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！

## 远程仓库
* github提供git仓库托管服务，是一个远程仓库，本地git库与github仓库是远程传输通过ssh加密，需要床架ssh key：ssh-keygen -t rsa -C youremail@example.com；在用户主目录可以找到.ssh文件，id_rsa 、id_rsa.pub分别为公钥和私钥，私不可泄，公加入github中即可；github上免费托管的git仓库任何人都可看到，可以付费私有或者自己动手搭一个git服务器
* 在github中右上角找到“Create a new repo”创建新仓库，reposity name填写需要关联的代码文件夹名字，creare即可。之后可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，把本地仓库的内容推送到GitHub仓库。
* 使用git remote add origin git@github.com:github账户名/learngit.git（错了应为公钥也推不上去），origin是远程库的名字；然后使用git push -u origin master，该命令把当前分支master推送到远程，-u第一次推送关联用，之后只要本地提交过后，就可以使用git push origin master把本地master分支的最新修改推送至github
* git remote -v可以查看远程库信息，使用git remote rm origin删除远程库（非物理上删除，而是解除本地与远程的绑定关系）
* 上面是添加远程库内容（先有本地库后有远程库），接下来是从远程库克隆（先远后本）
* 创建新仓库gitskills，Initialize this repository with a README，克隆本地库git clone git@github.com:github账户名/gitskills.git 。如果多人协作，那么每个人各自从远程克隆一份就可以了。git支持多种协议包括https，但ssh协议最快

### 向github提交代码时的两种情况
1. 本地没有git库，直接git clone远程仓库（之后cd进入），不用git init，git status查看状态，git addr添加，git commit，git push oirigin master（可以先使用git branch查看，可能是main）
2. 本地有仓库，git init，git remote add origin https://github.com/guobinhit/springmvc-tutorial.git，git pull origin master，add commut push origin master

3. 向远程仓库提交代码的时候，一定要先进行pull操作，再进行push操作，防止本地仓库与远程仓库不同步导致冲突的问题，尤其是第二种提交代码的情况，很容易就出现问题。
4. 在Git操作中，推荐在每次对文件进行修改并提交（commit）之后，但在推送（push）到远程仓库之前，先进行拉取（pull）操作以同步远程仓库的最新更改。这样做的主要原因是为了避免代码冲突和保持代码库的同步。

---

## 分支管理