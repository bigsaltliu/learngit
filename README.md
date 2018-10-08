# learngit

## 本地版本库

### 新建目录并初始化
```
$ mkdir learngit
$ git init
```

### 新建文件并提交
```
$ echo "# learngit" >> README.md
$ git add README.md
$ git commit -m "first commit"
```

### 查看状态、差异、日志
```
$ git status
$ git diff
$ git log
```

### 版本回退
上一个版本就是HEAD^，上上一个版本就是HEAD^^，往上100个版本写成HEAD~100
```
$ git reset --hard HEAD^
```

回退到指定版本号。版本号没必要写全，前几位就可以了，Git会自动去找。
```
$ git reset --hard 063f26f
```

通过reflog查找特定版本号
```
$ git reflog
```

### 几个概念
workingDictionary工作区、stage暂存区、repository版本库

git add 从工作区提交到暂存区

git commit 从暂存区提交到版本库的当前分支

Git跟踪并管理的是修改，而非文件

### 撤销修改
撤销工作区修改（取版本库内容覆盖工作区内容）
```
$ git checkout -- readme.md
```

撤销暂存区修改（指针移动）
```
$ git reset HEAD readme.md
$ git checkout -- readme.md
```

撤销本地版本库修改，参考前面的版本回退，前提是没有推送到远程库
```
$ git reset --hard HEAD^
```

### 删除文件并提交
添加删除到暂存、提交
```
$ git rm test.txt
$ git commit -m "remove test.txt"
```

## 远程版本库

### 生成SSH-Key
创建SSH Key，默认生成到~/.ssh/目录下。
私有key：id_rsa
共有key：id_rsa_pub
```
$ ssh-keygen -t rsa -b 4096 -C "18951810347@189.cn"
```

私有key添加到本地代理
```
$ eval $(ssh-agent -s)
$ ssh-add ~/.ssh/id_rsa
$ ssh-add -l
```

添加github.com的ssh Key
```
$ clip < ~/.ssh/id_rsa.pub
```
登录github.com账号，添加sshKey处，粘贴共有key

确认SSH链接
```
$ ssh -T git@github.com
```

### 初次提交
在github.com新建远程版本库learngit，不要勾选初始化

本地关联并提交
```
$ git remote add origin git@github.com:bigsaltliu/learngit.git
$ git push -u origin master
```

### 在github.com建库，本地从零开始
在github.com新建远程版本库gitskills，勾选初始化

从远程版本库克隆到本地
```
$ git clone git@github.com:bigsaltliu/gitskills.git
$ cd gitskills
$ ls
```

## 分支管理

### 创建与合并分支
创建dev分支并切换到dev上
```
$ git checkout -b dev
Switched to a new branch 'dev'
```

等价于上面的操作
```
$ git branch dev2
$ git checkout dev2
Switched to branch 'dev2'
```

查看分支、当前分支前面会标一个*号
```
$ git branch
  dev
* dev2
  master
```

合并某分支到当前分支
```
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
$ git merge dev2
Updating 58137dc..8e20f1e
Fast-forward
 README.md | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```

删除分支
```
$ git branch -d dev2
Deleted branch dev2 (was 8e20f1e).
$ git branch
  dev
* master
```

### 解决冲突
准备新的feature1分支
```
$ git checkout -b feature1
Switched to a new branch 'feature1'
$ git branch
  dev
* feature1
  master
```

修改文件，在feature1分支上提交
```
$ vi README.md
$ cat README.md
# gitskills
Creating a new branch is quick and simple.
$ git add README.md
$ git commit -m "and simple"
[feature1 98a9c1d] and simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

切换到master分支
```
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
$ git branch
  dev
  feature1
* master
```

修改文件，在master分支上提交
```
$ cat README.md
# gitskills
Creating a new branch is quick.
$ vi README.md
$ cat README.md
# gitskills
Creating a new branch is quick & simple.
$ git add README.md
$ git commit  -m "& simple"
[master 4a17eb4] & simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

合并分支，把feature1合并到master分支上
```
$ git merge feature1
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

查看冲突文件，解决冲突，重新提交
```
$ cat README.md
# gitskills
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick and simple.
>>>>>>> feature1
$ vi README.md
$ cat README.md
# gitskills
Creating a new branch is quick and simple.
$ git add README.md
$ git commit -m "conflict fixed"
[master 8cae3da] conflict fixed
```

查看分支合并情况
```
$ git log
commit 8cae3da2c7dbea3c3a2215898d0a64d6242fc25d
Merge: 4a17eb4 98a9c1d
Author: bigsaltliu <18951810347@189.cn>
Date:   Fri Sep 21 16:45:55 2018 +0800

    conflict fixed

commit 4a17eb4b622107f998f55eab9cfc3280c49280af
Author: bigsaltliu <18951810347@189.cn>
Date:   Fri Sep 21 16:38:00 2018 +0800

    & simple

commit 98a9c1d6d6fd510a5cadd26d0fa5a7581a16dae2
Author: bigsaltliu <18951810347@189.cn>
Date:   Fri Sep 21 16:36:33 2018 +0800

    and simple

commit 8e20f1e708fcceb022c85bafaa57478ba979c0d8
Author: bigsaltliu <18951810347@189.cn>
Date:   Fri Sep 21 15:27:51 2018 +0800

    branch test

commit 58137dc6d760d0f5d319504ddf6287d93c965945
Author: bigsaltliu <43402374+bigsaltliu@users.noreply.github.com>
Date:   Thu Sep 20 17:59:31 2018 +0800

    Initial commit

$ git log --graph
*   commit 8cae3da2c7dbea3c3a2215898d0a64d6242fc25d
|\  Merge: 4a17eb4 98a9c1d
| | Author: bigsaltliu <18951810347@189.cn>
| | Date:   Fri Sep 21 16:45:55 2018 +0800
| |
| |     conflict fixed
| |
| * commit 98a9c1d6d6fd510a5cadd26d0fa5a7581a16dae2
| | Author: bigsaltliu <18951810347@189.cn>
| | Date:   Fri Sep 21 16:36:33 2018 +0800
| |
| |     and simple
| |
* | commit 4a17eb4b622107f998f55eab9cfc3280c49280af
|/  Author: bigsaltliu <18951810347@189.cn>
|   Date:   Fri Sep 21 16:38:00 2018 +0800
|
|       & simple
|
* commit 8e20f1e708fcceb022c85bafaa57478ba979c0d8
| Author: bigsaltliu <18951810347@189.cn>
| Date:   Fri Sep 21 15:27:51 2018 +0800
|
|     branch test
|
* commit 58137dc6d760d0f5d319504ddf6287d93c965945
  Author: bigsaltliu <43402374+bigsaltliu@users.noreply.github.com>
  Date:   Thu Sep 20 17:59:31 2018 +0800

      Initial commit

$ git log --graph --pretty=oneline --abbrev-commit
*   8cae3da conflict fixed
|\
| * 98a9c1d and simple
* | 4a17eb4 & simple
|/
* 8e20f1e branch test
* 58137dc Initial commit
```

删除已合并的无用分支feature1
```
$ git branch
  dev
  feature1
* master
$ git branch -d feature1
Deleted branch feature1 (was 98a9c1d).
$ git branch
  dev
* master
```

### 分支管理策略
首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

其次，干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

第三，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

最后，合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

### Bug分支
当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它。

当前正在dev上进行的工作还没有提交，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。

bug修复后，再git stash pop，回到工作现场。

查看缓存清单 git stash list
恢复 git stash apply
删除 git stash drop
恢复并删除 git stash pop

### Feature分支
类似于bug分支
对于不需要合并，强制删除的分支可使用-D参数
```
$ git branch
  dev
* master
$ git checkout -b feature-vulcan
Switched to a new branch 'feature-vulcan'
$ echo "a new feature vulcan" >> vulcan.py
$ git status
On branch feature-vulcan
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        vulcan.py

nothing added to commit but untracked files present (use "git add" to track)
$ git add vulcan.py
warning: LF will be replaced by CRLF in vulcan.py.
The file will have its original line endings in your working directory.
$ git commit -m "add feature vulcan"
[feature-vulcan c446d1d] add feature vulcan
 1 file changed, 1 insertion(+)
 create mode 100644 vulcan.py
$ git branch
  dev
* feature-vulcan
  master
$ git checkout dev
Switched to branch 'dev'
$ git branch -d feature-vulcan
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
$ git branch -D feature-vulcan
Deleted branch feature-vulcan (was c446d1d).
```

### 多人协作
查看远程信息
```
$ git remote -v
origin  git@github.com:bigsaltliu/gitskills.git (fetch)
origin  git@github.com:bigsaltliu/gitskills.git (push)
$ git ls-remote origin
8cae3da2c7dbea3c3a2215898d0a64d6242fc25d        HEAD
58137dc6d760d0f5d319504ddf6287d93c965945        refs/heads/dev
8cae3da2c7dbea3c3a2215898d0a64d6242fc25d        refs/heads/master
```

建立远程关系，推送本地分支到远程
```
$ git branch
* dev
  master
$ git push origin dev
Total 0 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'dev' on GitHub by visiting:
remote:      https://github.com/bigsaltliu/gitskills/pull/new/dev
remote:
To github.com:bigsaltliu/gitskills.git
 * [new branch]      dev -> dev
$ git push
fatal: The current branch dev has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin dev
$ git push --set-upstream origin dev
Everything up-to-date
Branch dev set up to track remote branch dev from origin.
$ git push
Counting objects: 3, done.
Writing objects: 100% (3/3), 286 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:bigsaltliu/gitskills.git
   58137dc..070613a  dev -> dev
$ git push origin dev
Everything up-to-date
```

克隆版本后修改提交，另外一人修改后提交，冲突，解决后再提交。
``` User A
$ cd /c/DataBak/liuzh/
$ mkdir gitskills2
$ cd gitskills2
$ git clone git@github.com:bigsaltliu/gitskills
Cloning into 'gitskills'...
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 16 (delta 3), reused 12 (delta 2), pack-reused 0
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (3/3), done.
$ cd gitskills/
$ ll
total 1
-rw-r--r-- 1 liuzhenhua 197121 57 9月  25 15:22 README.md
$ git branch
* master
$ git checkout -b dev origin/dev
Switched to a new branch 'dev'
Branch dev set up to track remote branch dev from origin.
$ echo "test remote conflict" >> env.txt
$ git add env.txt
$ git commit -m "add env"
[dev 62afc84] add env
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt
$ git push
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:bigsaltliu/gitskills
   070613a..62afc84  dev -> dev
$ git branch
* dev
  master
$ ll
total 2
-rw-r--r-- 1 liuzhenhua 197121 21 9月  25 15:25 env.txt
-rw-r--r-- 1 liuzhenhua 197121 38 9月  25 15:24 README.md
$ cat env.txt
test remote conflict
```

``` User B
$ git branch
* dev
  master
$ echo "env" >> env.txt
$ git add env.txt
$ git commit -m "add new env2"
[dev 1d6bb83] add new env2
 1 file changed, 1 insertion(+)
 create mode 100644 env.txt
$ git push
To github.com:bigsaltliu/gitskills.git
 ! [rejected]        dev -> dev (fetch first)
error: failed to push some refs to 'git@github.com:bigsaltliu/gitskills.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
$ git pull
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:bigsaltliu/gitskills
   070613a..62afc84  dev        -> origin/dev
Auto-merging env.txt
CONFLICT (add/add): Merge conflict in env.txt
Automatic merge failed; fix conflicts and then commit the result.
$ cat env.txt
<<<<<<< HEAD
env
=======
test remote conflict
>>>>>>> 62afc84c85aca0891bb1b6a2037861ea2d9061ea
$ vi env.txt
$ git add env.txt
$ git commit -m "env conflict fixed"
[dev c9515d5] env conflict fixed
$ git push
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 582 bytes | 0 bytes/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To github.com:bigsaltliu/gitskills.git
   62afc84..c9515d5  dev -> dev
$ cat env.txt
env
test remote conflict
conflict is fixed
$ git log --graph
*   commit c9515d5e693b15214c162a43498c225cff767edc
|\  Merge: 1d6bb83 62afc84
| | Author: bigsaltliu <18951810347@189.cn>
| | Date:   Tue Sep 25 15:32:47 2018 +0800
| |
| |     env conflict fixed
| |
| * commit 62afc84c85aca0891bb1b6a2037861ea2d9061ea
| | Author: bigsaltliu <18951810347@189.cn>
| | Date:   Tue Sep 25 15:26:15 2018 +0800
| |
| |     add env
| |
* | commit 1d6bb839025861caf30f8ca50a4cb7ecd9565347
|/  Author: bigsaltliu <18951810347@189.cn>
|   Date:   Tue Sep 25 15:28:37 2018 +0800
|
|       add new env2
|
* commit 070613a043b914a787061d9e872c0f9eb5106f7f
| Author: bigsaltliu <18951810347@189.cn>
| Date:   Tue Sep 25 15:12:26 2018 +0800
|
|     add content: develop branch
|
* commit 58137dc6d760d0f5d319504ddf6287d93c965945
  Author: bigsaltliu <43402374+bigsaltliu@users.noreply.github.com>
  Date:   Thu Sep 20 17:59:31 2018 +0800

      Initial commit
```

``` User A
$ git branch
* dev
  master
$ ll
total 2
-rw-r--r-- 1 liuzhenhua 197121 21 9月  25 15:25 env.txt
-rw-r--r-- 1 liuzhenhua 197121 38 9月  25 15:24 README.md
$ cat env.txt
test remote conflict
$ git push
To github.com:bigsaltliu/gitskills
 ! [rejected]        dev -> dev (fetch first)
error: failed to push some refs to 'git@github.com:bigsaltliu/gitskills'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
$ git pull
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (4/4), done.
Unpacking objects: 100% (6/6), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
From github.com:bigsaltliu/gitskills
   62afc84..c9515d5  dev        -> origin/dev
Updating 62afc84..c9515d5
Fast-forward
 env.txt | 2 ++
 1 file changed, 2 insertions(+)
$ cat env.txt
env
test remote conflict
conflict is fixed
$ git log --graph
*   commit c9515d5e693b15214c162a43498c225cff767edc
|\  Merge: 1d6bb83 62afc84
| | Author: bigsaltliu <18951810347@189.cn>
| | Date:   Tue Sep 25 15:32:47 2018 +0800
| |
| |     env conflict fixed
| |
| * commit 62afc84c85aca0891bb1b6a2037861ea2d9061ea
| | Author: bigsaltliu <18951810347@189.cn>
| | Date:   Tue Sep 25 15:26:15 2018 +0800
| |
| |     add env
| |
* | commit 1d6bb839025861caf30f8ca50a4cb7ecd9565347
|/  Author: bigsaltliu <18951810347@189.cn>
|   Date:   Tue Sep 25 15:28:37 2018 +0800
|
|       add new env2
|
* commit 070613a043b914a787061d9e872c0f9eb5106f7f
| Author: bigsaltliu <18951810347@189.cn>
| Date:   Tue Sep 25 15:12:26 2018 +0800
|
|     add content: develop branch
|
* commit 58137dc6d760d0f5d319504ddf6287d93c965945
  Author: bigsaltliu <43402374+bigsaltliu@users.noreply.github.com>
  Date:   Thu Sep 20 17:59:31 2018 +0800

      Initial commit
```

### Rebase
rebase操作可以把本地未push的分叉提交历史整理成直线

rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。

## 标签管理
tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起

### 创建标签
查看所有标签 git tag

在最新提交上打标签 git tag <name>
```
$ git tag v1.0
$ git tag
v1.0
```

给指定commit打标签
```
$ git log --pretty=oneline --abbrev-commit
8cae3da conflict fixed
4a17eb4 & simple
98a9c1d and simple
8e20f1e branch test
58137dc Initial commit
$ git tag v0.9 8e20f1e
$ git tag
v0.9
v1.0
$ git show v0.9
commit 8e20f1e708fcceb022c85bafaa57478ba979c0d8
Author: bigsaltliu <18951810347@189.cn>
Date:   Fri Sep 21 15:27:51 2018 +0800

    branch test

diff --git a/README.md b/README.md
index e87becc..64331a4 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
-# gitskills
\ No newline at end of file
+# gitskills
+Creating a new branch is quick.
```

打标签完整命令
```
$ git log --pretty=oneline --abbrev-commit
8cae3da conflict fixed
4a17eb4 & simple
98a9c1d and simple
8e20f1e branch test
58137dc Initial commit
$ git tag -a v0.1 -m "version 0.1 released" 58137dc
$ git show v0.1
tag v0.1
Tagger: bigsaltliu <18951810347@189.cn>
Date:   Tue Sep 25 16:28:39 2018 +0800

version 0.1 released

commit 58137dc6d760d0f5d319504ddf6287d93c965945
Author: bigsaltliu <43402374+bigsaltliu@users.noreply.github.com>
Date:   Thu Sep 20 17:59:31 2018 +0800

    Initial commit

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..e87becc
--- /dev/null
+++ b/README.md
@@ -0,0 +1 @@
+# gitskills
\ No newline at end of file
$ git tag
v0.1
v0.9
v1.0
```

### 操作标签
删除本地标签
```
$ git tag -d v0.9
Deleted tag 'v0.9' (was 8e20f1e)
```

标签默认存储在本地，可推送特定标签到远程
```
$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0)
To github.com:bigsaltliu/gitskills.git
 * [new tag]         v1.0 -> v1.0
```

一次性推送全部尚未推送到远程的本地标签
```
$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 165 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To github.com:bigsaltliu/gitskills.git
 * [new tag]         v0.1 -> v0.1
```

删除远程标签，先删除本地，再推送到远程
```
```

## 其他
查看远程分支
```
$ git branch -a
  dev
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
```

查看远程标签及相关信息
```
$ git ls-remote
$ git show-ref --tags
$ git show-ref --tags --dereference
```
