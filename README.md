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
