---
title: 基于hexo+github搭建独立博客
date: 2020-03-31 20:57:14
categories:
- [博客, 环境安装]

---

参考文章

* [干掉mackeeper](https://manual.mackeeper.com/overview/uninstall/)
* [hexo+github`1`](https://www.cnblogs.com/MuYunyun/p/5927491.html)
* [搭建自己的云服务器&解析域名](http://www.cnblogs.com/MuYunyun/p/5922099.html)
* [blog=github+hexo+git`2`](http://blog.csdn.net/li740207611/article/details/52142852)
* [静态博客框架之Hexo & Jekyll](https://www.jianshu.com/p/ce1619874d34)
* [博客搭建可行性方案(jekyll, hexo, Wordpress)](https://www.jianshu.com/p/c4f145fdd637)
* [测试Node.js 和npm](http://blog.csdn.net/u011619283/article/details/52368759)
* [Hexo Docs](https://hexo.io/zh-cn/docs/index.html)

<!--more-->
## 安装Hexo

1.准备

```
nodejs + git
```

2.安装

```
npm install -g hexo-cli:需加sudo，否则会报权限错误
```

3.建站  
  
```
hexo init blog
:INFO  Cloning hexo-starter to ~/hexo/blog
:Cloning into '/Users/lixing/hexo/blog'...
:INFO  Install dependencies
:INFO  Start blogging with Hexo!
cd blog
npm install
```
		
4.启动

```
hexo server
:INFO  Start processing
:INFO  Hexo is running at http://localhost:4000/. 
Press Ctrl+C to stop.
并且会生成一个db.json文件。
```
[Hello World](http://localhost:4000)
		
5.生成静态页面

```
hexo new "hell, hexo article"
：INFO  Created: ~/hexo/blog/source/_posts/hell-hexo-article.md
server未关闭时，创建的文章，自动同步到本地网页
```
		
## 关联Github
hexo本地设置好后，接下来就是开始关联github

#### 1.创建ssh-key，添加ssh-agent(避免每次访问github要输入账号密码)，上传公钥至github sshkeys.

###### 为github生成shendawei0727@163.com ssh公私密钥。

ssh密码为手机号

	➜  .ssh ssh-keygen -t rsa -b 4096 -C "shendawei0727@163.com"
	Generating public/private rsa key pair.
	Enter file in which to save the key (/Users/lixing/.ssh/id_rsa): 
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 
	Your identification has been saved in /Users/lixing/.ssh/id_rsa.
	Your public key has been saved in /Users/lixing/.ssh/id_rsa.pub.
	The key fingerprint is:
	SHA256:13pg4amiMEiqktqC1KMmSMKf2hP2Gpyk4h2oTZwnghU shendawei0727@163.com
	The key's randomart image is:
	+---[RSA 4096]----+
	|                 |
	|                 |
	|  E       .      |
	|   .     . +     |
	|..o.    S * .    |
	|=B=*.    + o     |
	|%+@=* . . . .    |
	|%BoOoo .   .     |
	|O++++            |
	+----[SHA256]-----+
	➜  .ssh 

###### 添加ssh key到ssh-agent,存储ssh密码(passphrase)到keychain

	后台开启ssh-agent
	➜  .ssh eval "$(ssh-agent -s)"
	Agent pid 21038
	执行添加
	➜  .ssh ssh-add -K id_rsa       
	Enter passphrase for id_rsa: 
	Passphrase updated in keychain: id_rsa
	Identity added: id_rsa (id_rsa)
	➜  .ssh 

###### 上传ssh-key到github
```
pbcopy < ~/.ssh/id_rsa.pub
将拷贝内容粘贴到github ssh-keys
```
![image](image/上传ssh-key.png)

###### 测试ssh-key是否成功

```
ssh -T git@github.com
Hi sgz-xiaowu! You've successfully authenticated, but GitHub does not provide shell access.
```

#### 2.在github创建新仓库(不勾选Initialize项，即不在服务端初始化仓库，而是由本地初始化仓库并上传至服务端)
###### 创建仓库
在网页端创建sgz-xiaowu.github.io.git
![image](image/创建仓库.png)
###### 初始化仓库[选择在本地命令行创建repo]
终端Terminal，进入hexo blog目录，初始化git
![image](image/在哪初始化仓库.png)

```
创建README.md
echo "# sgz.github.io" >> README.md
初始化仓库
git init
Initialized empty Git repository in /Users/lixing/hexo/blog/.git/
本地自动创建master分支
提交文件
git add .
git commit -m "***"
上传仓库：远端添加origin
git remote add origin git@github.com:sgz-xiaowu/sgz-xiaowu.github.io.git
上传分支（此处将master上传到remote origin的hexo分支：存储blog原始文件）
git push -u origin master:hexo
Counting objects: 114, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (103/103), done.
Writing objects: 100% (114/114), 522.97 KiB | 41.00 KiB/s, done.
Total 114 (delta 0), reused 0 (delta 0)
To github.com:sgz-xiaowu/sgz-xiaowu.github.io.git
 * [new branch]      master -> hexo
Branch master set up to track remote branch hexo from origin.
```

###### 查看分支状态

```
➜  blog git:(master) git branch -a
* master
  remotes/origin/hexo
  ➜  blog git:(master) git branch -av
* master              d167f5f first hexo commit
  remotes/origin/hexo d167f5f first hexo commit
```

###### 创建origin/master分支,存储发布的静态网页

```
此时远端只有hexo分支，而blog生成的静态html文件需推送到远端master分支，因为github pages要求使用master分支。
在远端github上创建master分支：通过网页操作（master是基于hexo创建的，所以会有一次first commit，不影响）
git pull
From github.com:sgz-xiaowu/sgz-xiaowu.github.io
 * [new branch]      master     -> origin/master
Already up-to-date.
git status
On branch master
Your branch is up-to-date with 'origin/hexo'.
nothing to commit, working tree clean
//说明：只是拉取了一下远端分支的状态，表明远端创建了一个master分支（网页创建），并不是本地master分支指向了origin/master
git branch -a
* master -> origin/hexo
  remotes/origin/hexo
  remotes/origin/master
```

###### 提交博客原始md文件

```
git push origin HEAD:hexo
##git push
报错
fatal: The upstream branch of your current branch does not match
the name of your current branch.  To push to the upstream branch
on the remote, use
    git push origin HEAD:hexo
    或
    git push origin master:hexo
To push to the branch of the same name on the remote, use
    git push origin master
    或
    git push origin master:master
因为本地master分支已配置指定远端分支为hexo，而此时配置流分支名已不相同，故push时需指明master:hexo或HEAD:hexo
```

###### 查阅帮助git help push,了解push分支含义

声明：以下match分支流指的是“~~若本地分支已指定远端分支流，则推送到指定分支流；否则推送到和本地分支名相同的分支流~~ 本地分支名与远端分支名相同的分支流“。被推送的远端分支流，均用match分支流表示。

```
git push <==> git push origin //推送当前本地分支到远端match分支流
git push origin :  //推送本地所有和origin match的分支到远端match分支流
git push origin master //查找本地master分支并推送到远端match分支流
git push origin HEAD //一种快捷方式，推送当前分支到远端match分支流
git push origin HEAD:master //推送当前分支到远端master分支
git push origin master:hexo //推送本地master分支到远端hexo分支，若远端没有hexo分支，则通过copy当前master分支，在origin创建hexo分支。
git push origin :hexo //冒号前没有分支名，意为查找远端hexo分支，删除hexo分支
--------
综上结论：1.命令中origin后的冒号，之前指代本地分支名，之后指代远端分支名。
        2.有冒号，有本地分支名，无远端分支名：推送到远端同名分支
        3.有冒号，无本地分支名，有远端分支名：删除远端分支
        4.有冒号，本地分支名&远端分支名均没有：推送本地所有分支到远端同名分支
        5.有冒号，本地分支名&远端分支名均有：推送本地分支到指定远端分支
        6.无冒号，无分支名：推送本地当前分支到远端同名分支
        7.无冒号，有一个分支名（只能有一个分支名）：推送本地指定分支到远端同名分支
```

## 发布博客到Github
```
运行
hexo s
---
终端打开新标签
发布
hexo d -g 或hexo g -d //重新生成发布所有post
检测文件变化，发布
hexo g -w -d //只生成发布变化的post
---
如果报错
:ERROR Deployer not found: git
安装git配置器
npm install hexo-deployer-git --save
```
[生成并部署到网站](https://hexo.io/zh-cn/docs/generating.html)

## Hexo&Github流程
* hexo init必须在空目录下执行，会生成一个.gitignore文件

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```
		
* git init会创建.git/目录
* hexo-deployer-git会创建.deploy_git/目录,并且初始化一个master分支，将本地public的内容发布到这里，并发布到github仓库origin master分支。

```
修改_config.yml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:sgz-xiaowu/sgz-xiaowu.github.io.git
  branch: master
```

![blog目录](image/blog目录.png)