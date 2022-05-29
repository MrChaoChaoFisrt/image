*git**
===

**git是分布式版本控制工具**

**Git分支 分支特性 分支创建 分支转换 分支合并 代码合并冲突解决**

git的常用命令
===

```shell
git config --global user.name 用户名 
git config --global user.email 邮
```



```shell
-- 初始化命令
git init
$ git init
Initialized empty Git repository in G:/2022/git/Git-Space/git-test/.git/

-- 添加暂存区
git add
$ git add git.test
warning: LF will be replaced by CRLF in git.test.
The file will have its original line endings in your working directory

-- 从暂存区删除文件
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git rm --cached git.test
rm 'git.test'

-- 提交本地库
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git commit -m 'firt commit'
[master (root-commit) 3ae6db9] firt commit
 1 file changed, 11 insertions(+)
 create mode 100644 git.test

-- 查看状态
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git status
On branch master
nothing to commit, working tree clean

-- 查看版本信息 简要信息
$ git reflog
3ae6db9 (HEAD -> master) HEAD@{0}: commit (initial): firt commit

-- 查看版本信息  详细信息
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git log
commit 3ae6db902d0258044c4bd68bda7634b7cfec870a (HEAD -> master)
Author: konglc <chao@inovance.com>
Date:   Sun May 29 01:31:41 2022 +0800

    firt commit

-- 修改文件

-- 添加暂存区
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git add *
warning: LF will be replaced by CRLF in git.test.
The file will have its original line endings in your working directory

-- 提交本地库
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git commit -m 'second commit'
[master 995b6a8] second commit
 1 file changed, 101 insertions(+)

-- 查看版本信息
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git log
commit 995b6a8deb73c1014fc2eddce7c086c7c4cc7928 (HEAD -> master)
Author: konglc <chao@inovance.com>
Date:   Sun May 29 01:38:09 2022 +0800

    second commit

commit 3ae6db902d0258044c4bd68bda7634b7cfec870a
Author: konglc <chao@inovance.com>
Date:   Sun May 29 01:31:41 2022 +0800

    firt commit

$ git reflog
995b6a8 (HEAD -> master) HEAD@{0}: commit: second commit
3ae6db9 HEAD@{1}: commit (initial): firt commit


-- 放弃工作区文件的改变
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git restore git.test


-- 修改文件查看git状态
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git.test

no changes added to commit (use "git add" and/or "git commit -a")

-- 将修改之后文件添加至暂存区
$ git add git.test
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   git.test


-- 版本回退
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git reflog
82a8932 (HEAD -> master) HEAD@{0}: commit: third commit
995b6a8 HEAD@{1}: commit: second commit
3ae6db9 HEAD@{2}: commit (initial): firt commit

ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git reset --hard 3ae6db9
HEAD is now at 3ae6db9 firt commit


$ git reflog
3ae6db9 (HEAD -> master) HEAD@{0}: reset: moving to 3ae6db9
82a8932 HEAD@{1}: commit: third commit
995b6a8 HEAD@{2}: commit: second commit
3ae6db9 (HEAD -> master) HEAD@{3}: commit (initial): firt commit


```



git 分支 操作
===

```shell
## 查看分支
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git branch -v
* master 82a8932 third commit


## 创建分支
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git branch hot-fix
	
## 再次查看分支 
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git branch -v
  hot-fix 82a8932 third commit
* master  82a8932 third commit

## 切换分支
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git checkout hot-fix
Switched to branch 'hot-fix'

## 查看分支
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (hot-fix)
$ git branch -v
* hot-fix 82a8932 third commit
  master  82a8932 third commit
  
  
 ## 在分支上修改文件 查看分支状态
 ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (hot-fix)
$ vim git.test

ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (hot-fix)
$ git status
On branch hot-fix
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git.test

no changes added to commit (use "git add" and/or "git commit -a")

## 提交暂存区
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (hot-fix)
$ git add git.test

ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (hot-fix)
$ git status
On branch hot-fix
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   git.test

## 提交本地库
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (hot-fix)
$ git commit -m 'hot-fix first commit' git.test
[hot-fix fa86d9a] hot-fix first commit
 1 file changed, 3 insertions(+)
```



git  分支合并
---

```shell
## 切换回主干分支 此时看到的文件是主干分支下的
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (hot-fix)
$ git checkout master
Switched to branch 'master'

## 分支合并 在主干分支上合并hot-fix分支
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git merge hot-fix

##正常合并
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git merge hot-fix
Updating 82a8932..fa86d9a
Fast-forward
 git.test | 3 +++
 1 file changed, 3 insertions(+)

ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git status
On branch master
nothing to commit, working tree clean

## 合并冲突
$ git merge hot-fix
Auto-merging git.test
CONFLICT (content): Merge conflict in git.test
Automatic merge failed; fix conflicts and then commit the result.

ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master|MERGING) ## 正在合并中

## 查看文件
chaochaochaochaochao
chaochaochaochaochao
chaochaochaochaochao
chaochaochaochaochao
chaochaochaochaochao
chaochaochaochaochao
chaochaochaochaochao
chaochaochaochaochao
chaochaochaochaochao
chaochaochaochaochao


<<<<<<< HEAD
yangYuQi
=======
yangQi
MrChao
>>>>>>> hot-fix


## 修改并未被追踪
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   git.test

no changes added to commit (use "git add" and/or "git commit -a")

## 提交至暂存区
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master|MERGING)
$ git add git.test

ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master|MERGING)
$ git commit -m 'merge-test'
[master daa818c] merge-test

## 查看引用日志
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-test (master)
$ git reflog
daa818c (HEAD -> master) HEAD@{0}: commit (merge): merge-test
862e97f HEAD@{1}: checkout: moving from hot-fix to master
c52a1ff (hot-fix) HEAD@{2}: commit: hot-fix-test
fa86d9a HEAD@{3}: checkout: moving from master to hot-fix
862e97f HEAD@{4}: commit: master-test
fa86d9a HEAD@{5}: merge hot-fix: Fast-forward
82a8932 HEAD@{6}: checkout: moving from hot-fix to master
fa86d9a HEAD@{7}: commit: hot-fix first commit
82a8932 HEAD@{8}: checkout: moving from master to hot-fix
82a8932 HEAD@{9}: reset: moving to 82a8932
995b6a8 HEAD@{10}: reset: moving to 995b6a8
3ae6db9 HEAD@{11}: reset: moving to 3ae6db9
3ae6db9 HEAD@{12}: reset: moving to 3ae6db9
82a8932 HEAD@{13}: commit: third commit
995b6a8 HEAD@{14}: commit: second commit
3ae6db9 HEAD@{15}: commit (initial): firt commit

```





github
===

```shell
github网址 :
	https://github.com/
```



## 创建新的仓库

![image-20220529212100997](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529212100997.png)



两种不同协议的

http协议和ssh协议

![image-20220529212144423](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529212144423.png)



git 拉取 推送 基本操作
---

```shell
## git 创建别名
git remote add git-github-test https://github.com/MrChaoChaoFisrt/git-github-test.git

## 查看当前远程地址的别名
git remote -v 
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-github-test (master)
$ git remote -v

## 取代码 上传代码
git-github-test https://github.com/MrChaoChaoFisrt/git-github-test.git (fetch)
git-github-test https://github.com/MrChaoChaoFisrt/git-github-test.git (push)


## 推送本地分支到远程仓库
git push 别名 分支

## 把master分支推送到远程库
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-github-test (master)
$ git push git-github-test master


##移除仓库
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-github-test (master)
$ git remote rm git-github-test

##添加仓库别名
git remote add git-github-test https://github.com/MrChaoChaoFisrt/git-github-test.git


## 推送到远程仓库
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-github-test (master)
$ git push git-github-test master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 272 bytes | 272.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/MrChaoChaoFisrt/git-github-test.git
 * [new branch]      master -> master
 
 ## 从远程库拉取
 git pull 别名 分支
 ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-github-test (master)
$ git pull git-github-test master
```



![image-20220529214452701](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529214452701.png)



克隆 
---

```shell
## 克隆远程代码到本地库 克隆代码是不需要创建库的
## 到仓库下: https://github.com/MrChaoChaoFisrt/git-github-test
$ git clone https://github.com/MrChaoChaoFisrt/git-github-test.git
```



![image-20220529215913571](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529215913571.png)

克隆出现的问题:

![image-20220529220333236](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529220333236.png)



```tex
克隆会做如下的操作
1 拉取代码
2 初始化本地库
3 创建别名
```



自动创建别名

![image-20220529220547421](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529220547421.png)



克隆代码  修改 推送到远程仓库
---

克隆代码之后 修改代码 提交暂存区 提交本地库

```shell
## 修改代码
vim git.test
………………………………………………………………
## 添加暂存区
git add git.test

## 提交本地库
git commit  -m 'modify by chaochao'

## 推送代码到远程库
$ git push https://github.com/MrChaoChaoFisrt/git-github-test.git master
```



修改 -> 提交暂存区 -> 提交本地库

![image-20220529221031323](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529221031323.png)



推送代码到远程库

![image-20220529221400073](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529221400073.png)



查看远程仓库代码

![image-20220529221534083](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529221534083.png)

在远程仓库代码的最后 可以看到我们在本地修改的内容 说明代码推送成功



拉取其他成员 到代码仓库

![image-20220529222310856](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529222310856.png)



邀请成员

![image-20220529222924932](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529222924932.png)







ssh免密登录
---

```shell
## -v提示即将进行的操作
rm -rfv d1 d2 d3

$ rm -rfv chao chaochao/ lingchao/ yuqi/
```

![image-20220529235332209](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529235332209.png)

添加ssh公钥

```shell
## 删除~/.ssh目录
ASUS@chaozi MINGW64 ~/.ssh
$ rm -rfv ~/.ssh/
removed '/c/Users/ASUS/.ssh/id_rsa'
removed '/c/Users/ASUS/.ssh/id_rsa.pub'
removed '/c/Users/ASUS/.ssh/known_hosts'
removed '/c/Users/ASUS/.ssh/known_hosts.old'
removed directory '/c/Users/ASUS/.ssh/'


##运行命令生成秘钥目录
ssh-keygen -t rsa -C konglc@asianinfo.com
```



![image-20220529235952371](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220529235952371.png)



到 githup账号下 : 

![image-20220530000427617](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530000427617.png)



点击 new ssh key

![image-20220530000509076](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530000509076.png)





此时说明ssh key添加成功

![image-20220530000803972](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530000803972.png)









```shell
## 使用ssh协议拉取代码

```

![image-20220530001101583](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530001101583.png)



![image-20220530001212176](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530001212176.png)



```shell
git clone git@github.com:MrChaoChaoFisrt/git-github-test.git
```





在 github上修改代码

![image-20220530001506168](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530001506168.png)



使用ssh协议拉取代码

```shell
git pull git@github.com:MrChaoChaoFisrt/git-github-test.git
```

![image-20220530001620696](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530001620696.png)

可以看到我们在github上所作的修改



在本地修改代码 使用ssh协议推送代码到远程库

![image-20220530001943414](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530001943414.png)





```shell
## 使用ssh协议推送代码到远程仓库
ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-ssh-test/git-github-test (master)
$ git push git@github.com:MrChaoChaoFisrt/git-github-test.git master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 297 bytes | 297.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
To github.com:MrChaoChaoFisrt/git-github-test.git
   12c686d..ad35f3e  master -> master

ASUS@chaozi MINGW64 /g/2022/git/Git-Space/git-ssh-test/git-github-test (master)

```



从github上看 远程仓库的代码也是被我们修改过的一份

![image-20220530002108742](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530002108742.png)









使用git上传本地文件到github
---

在远程库上新建仓库

![image-20220530002722350](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530002722350.png)



1.  初始化本地仓库

   ```shell
   git init
   ```

2. 添加到暂存区

   ```shell
   git add *
   ```

3. 提交本地库

   ```shell
   git commit -m 'Mr chao mysql'
   ```

4. 推送代码到远程库

   ```shell
   $ git push git@github.com:MrChaoChaoFisrt/mysql.git master
   ```

   ![image-20220530003013832](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530003013832.png)

   

5. 从 github上查看上传结果

   ![image-20220530003251053](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20220530003251053.png)

   上传 上去 图片显示不出来 

   解决办法:

   ​	安装 node js 参考博客路径 : `https://blog.csdn.net/qq_48485223/article/details/122709354` PicGo

   查看node js是否安装成功

   

   ![image-20220530011103589](G:\2022\git\image-20220530011103589.png)

   将全模块所在路径和缓存路径放在我node.js安装的文件夹中

   ```shell
   npm config set prefix "E:\nodejs\node_global"
   npm config set cache "E:\nodejs\node_cache"
   ```




```shell
## dos查看进程
tasklist|findstr PIC
```

![image-20220530013622620](G:\2022\git\image-20220530013622620.png)



```shell
## DOS杀进程
taskkill /pid 2472 -t -f;
C:\Users\ASUS>taskkill /pid 7720 -t -f

## 清屏快捷键
cls

```



![image-20220530013754850](G:\2022\git\image-20220530013754850.png)



![image-20220530014120756](G:\2022\git\image-20220530014120756.png)







PicGo+GitHub使用
===

参考博文 `https://blog.csdn.net/qq_43367829/article/details/104882071`

```shell
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
```

![image-20220530015705481](G:\2022\git\image-20220530015705481.png)