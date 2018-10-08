# learngit

## ���ذ汾��

### �½�Ŀ¼����ʼ��
```
$ mkdir learngit
$ git init
```

### �½��ļ����ύ
```
$ echo "# learngit" >> README.md
$ git add README.md
$ git commit -m "first commit"
```

### �鿴״̬�����졢��־
```
$ git status
$ git diff
$ git log
```

### �汾����
��һ���汾����HEAD^������һ���汾����HEAD^^������100���汾д��HEAD~100
```
$ git reset --hard HEAD^
```

���˵�ָ���汾�š��汾��û��Ҫдȫ��ǰ��λ�Ϳ����ˣ�Git���Զ�ȥ�ҡ�
```
$ git reset --hard 063f26f
```

ͨ��reflog�����ض��汾��
```
$ git reflog
```

### ��������
workingDictionary��������stage�ݴ�����repository�汾��

git add �ӹ������ύ���ݴ���

git commit ���ݴ����ύ���汾��ĵ�ǰ��֧

Git���ٲ���������޸ģ������ļ�

### �����޸�
�����������޸ģ�ȡ�汾�����ݸ��ǹ��������ݣ�
```
$ git checkout -- readme.md
```

�����ݴ����޸ģ�ָ���ƶ���
```
$ git reset HEAD readme.md
$ git checkout -- readme.md
```

�������ذ汾���޸ģ��ο�ǰ��İ汾���ˣ�ǰ����û�����͵�Զ�̿�
```
$ git reset --hard HEAD^
```

### ɾ���ļ����ύ
���ɾ�����ݴ桢�ύ
```
$ git rm test.txt
$ git commit -m "remove test.txt"
```

## Զ�̰汾��

### ����SSH-Key
����SSH Key��Ĭ�����ɵ�~/.ssh/Ŀ¼�¡�
˽��key��id_rsa
����key��id_rsa_pub
```
$ ssh-keygen -t rsa -b 4096 -C "18951810347@189.cn"
```

˽��key��ӵ����ش���
```
$ eval $(ssh-agent -s)
$ ssh-add ~/.ssh/id_rsa
$ ssh-add -l
```

���github.com��ssh Key
```
$ clip < ~/.ssh/id_rsa.pub
```
��¼github.com�˺ţ����sshKey����ճ������key

ȷ��SSH����
```
$ ssh -T git@github.com
```

### �����ύ
��github.com�½�Զ�̰汾��learngit����Ҫ��ѡ��ʼ��

���ع������ύ
```
$ git remote add origin git@github.com:bigsaltliu/learngit.git
$ git push -u origin master
```

### ��github.com���⣬���ش��㿪ʼ
��github.com�½�Զ�̰汾��gitskills����ѡ��ʼ��

��Զ�̰汾���¡������
```
$ git clone git@github.com:bigsaltliu/gitskills.git
$ cd gitskills
$ ls
```

## ��֧����

### ������ϲ���֧
����dev��֧���л���dev��
```
$ git checkout -b dev
Switched to a new branch 'dev'
```

�ȼ�������Ĳ���
```
$ git branch dev2
$ git checkout dev2
Switched to branch 'dev2'
```

�鿴��֧����ǰ��֧ǰ����һ��*��
```
$ git branch
  dev
* dev2
  master
```

�ϲ�ĳ��֧����ǰ��֧
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

ɾ����֧
```
$ git branch -d dev2
Deleted branch dev2 (was 8e20f1e).
$ git branch
  dev
* master
```

### �����ͻ
׼���µ�feature1��֧
```
$ git checkout -b feature1
Switched to a new branch 'feature1'
$ git branch
  dev
* feature1
  master
```

�޸��ļ�����feature1��֧���ύ
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

�л���master��֧
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

�޸��ļ�����master��֧���ύ
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

�ϲ���֧����feature1�ϲ���master��֧��
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

�鿴��ͻ�ļ��������ͻ�������ύ
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

�鿴��֧�ϲ����
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

ɾ���Ѻϲ������÷�֧feature1
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

### ��֧�������
���ȣ�master��֧Ӧ���Ƿǳ��ȶ��ģ�Ҳ���ǽ����������°汾��ƽʱ����������ɻ

��Σ��ɻ��dev��֧�ϣ�Ҳ����˵��dev��֧�ǲ��ȶ��ģ���ĳ��ʱ�򣬱���1.0�汾����ʱ���ٰ�dev��֧�ϲ���master�ϣ���master��֧����1.0�汾��

������ÿ���˶����Լ��ķ�֧��ʱ��ʱ����dev��֧�Ϻϲ��Ϳ����ˡ�

��󣬺ϲ���֧ʱ������--no-ff�����Ϳ�������ͨģʽ�ϲ����ϲ������ʷ�з�֧���ܿ��������������ϲ�����fast forward�ϲ��Ϳ����������������ϲ���

### Bug��֧
����ӵ�һ���޸�һ������101��bug������ʱ������Ȼ�أ����봴��һ����֧issue-101���޸�����

��ǰ����dev�Ͻ��еĹ�����û���ύ��Git���ṩ��һ��stash���ܣ����԰ѵ�ǰ�����ֳ������ء����������Ժ�ָ��ֳ������������

bug�޸�����git stash pop���ص������ֳ���

�鿴�����嵥 git stash list
�ָ� git stash apply
ɾ�� git stash drop
�ָ���ɾ�� git stash pop

### Feature��֧
������bug��֧
���ڲ���Ҫ�ϲ���ǿ��ɾ���ķ�֧��ʹ��-D����
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

### ����Э��
�鿴Զ����Ϣ
```
$ git remote -v
origin  git@github.com:bigsaltliu/gitskills.git (fetch)
origin  git@github.com:bigsaltliu/gitskills.git (push)
$ git ls-remote origin
8cae3da2c7dbea3c3a2215898d0a64d6242fc25d        HEAD
58137dc6d760d0f5d319504ddf6287d93c965945        refs/heads/dev
8cae3da2c7dbea3c3a2215898d0a64d6242fc25d        refs/heads/master
```

����Զ�̹�ϵ�����ͱ��ط�֧��Զ��
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

��¡�汾���޸��ύ������һ���޸ĺ��ύ����ͻ����������ύ��
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
-rw-r--r-- 1 liuzhenhua 197121 57 9��  25 15:22 README.md
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
-rw-r--r-- 1 liuzhenhua 197121 21 9��  25 15:25 env.txt
-rw-r--r-- 1 liuzhenhua 197121 38 9��  25 15:24 README.md
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
-rw-r--r-- 1 liuzhenhua 197121 21 9��  25 15:25 env.txt
-rw-r--r-- 1 liuzhenhua 197121 38 9��  25 15:24 README.md
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
rebase�������԰ѱ���δpush�ķֲ��ύ��ʷ�����ֱ��

rebase��Ŀ����ʹ�������ڲ鿴��ʷ�ύ�ı仯ʱ�����ף���Ϊ�ֲ���ύ��Ҫ�����Աȡ�

rebase�������ص㣺�ѷֲ���ύ��ʷ��������һ��ֱ�ߣ�����ȥ��ֱ�ۡ�ȱ���Ǳ��صķֲ��ύ�Ѿ����޸Ĺ��ˡ�

## ��ǩ����
tag����һ���������׼�ס������������֣�����ĳ��commit����һ��

### ������ǩ
�鿴���б�ǩ git tag

�������ύ�ϴ��ǩ git tag <name>
```
$ git tag v1.0
$ git tag
v1.0
```

��ָ��commit���ǩ
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

���ǩ��������
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

### ������ǩ
ɾ�����ر�ǩ
```
$ git tag -d v0.9
Deleted tag 'v0.9' (was 8e20f1e)
```

��ǩĬ�ϴ洢�ڱ��أ��������ض���ǩ��Զ��
```
$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0)
To github.com:bigsaltliu/gitskills.git
 * [new tag]         v1.0 -> v1.0
```

һ��������ȫ����δ���͵�Զ�̵ı��ر�ǩ
```
$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 165 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To github.com:bigsaltliu/gitskills.git
 * [new tag]         v0.1 -> v0.1
```

ɾ��Զ�̱�ǩ����ɾ�����أ������͵�Զ��
```
```

## ����
�鿴Զ�̷�֧
```
$ git branch -a
  dev
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
```

�鿴Զ�̱�ǩ�������Ϣ
```
$ git ls-remote
$ git show-ref --tags
$ git show-ref --tags --dereference
```
