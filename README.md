# learngit

---
## 新建目录并初始化
'''
mkdir learngit
git init
'''

---
## 新建文件并提交
'''
echo "# learngit" >> README.md
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:bigsaltliu/learngit.git
git push -u origin master
'''

---
## 查看状态、差异、日志
'''
git status
git diff
git log
'''

---
## 版本回退
### 上一个版本就是HEAD^，上上一个版本就是HEAD^^，往上100个版本写成HEAD~100
> git reset --hard HEAD^
### 回退到指定版本号。版本号没必要写全，前几位就可以了，Git会自动去找。
> git reset --hard 063f26f
### 通过reflog查找特定版本号
> git reflog

---
## 几个概念
### workingDictionary工作区、stage暂存区、repository版本库
### git add 从工作区提交到暂存区
### git commit 从暂存区提交到版本库的当前分支
### Git跟踪并管理的是修改，而非文件

---
## 撤销修改
### 撤销工作区修改（取版本库内容覆盖工作区内容）
> git checkout -- readme.md
### 撤销暂存区修改（指针移动）
> git reset HEAD readme.md
> git checkout -- readme.md
### 撤销本地版本库修改，参考前面的版本回退，前提是没有推送到远程库。
> git reset --hard HEAD^

---
## 删除文件并提交
### 添加删除到暂存、提交
> git rm test.txt
> git commit -m "remove test.txt"

---
