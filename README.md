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
