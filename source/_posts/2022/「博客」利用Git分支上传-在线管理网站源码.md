---
title: 「博客」利用Git分支上传+在线管理网站源码
tags:
  - Git
  - Hexo
cover: https://s2.loli.net/2022/07/06/3pzqfb2NIOACJX6.jpg
date: 2022-07-10 11:15:55
---




---

# <center>上传源码

{% btn 'http://fangzh.top/2018/2018090715/',「[hexo教程:基本配置+更换主题+多终端工作+coding page部署分流(2) | Fangzh的个人博客 | 人工智能拯救世界]」,far fa-hand-point-right,block outline right blue larger %}

1. 在***「GitHub」***新建分支***「Hexo」***，并设置为默认分支

2. 本地任意目录***「Git Bash」***，将***「Hexo」***分支的仓库复制到本地

   ~~~bash
   git clone https://github.com/wangmin-1995/wangmin-1995.github.io.git
   ~~~

   生成的文件夹名为***「wangmin-1995.github.io」***，可重命名为***「博客」***

3. 删除***「博客」***中除***「.git」***外的所有文件夹，***「.git」***默认是隐藏的

4. 将本地仓库下所有文件转移到***「博客」***，之前的仓库文件夹可以删除了

5. 删除***「博客」***下的***「.deploy.git」***、`博客/theme/butterfly`下的***「.git」***，这两个文件夹不能上传

6. ***「博客」***下***「Git Bash」***

   ~~~bash
   git add . && git commit -m 'first push' && git push
   ~~~

   在***「GItHub」***切换***「Hexo」***分支，可见所有网站源码已上传至仓库

7. 每次在本地编辑文章后，要上传到远程仓库
   目的一：备份源码
   目的二：更新网站
   
   ~~~bash
   git add . && git commit -m 'new' && git push && hexo clean && hexo g && hexo d
   ~~~

---

# <center>在线编辑

1. 在「_config.yml」中打开，详见

   {% btn 'https://minge.live/2022/「博客」详解Butterfly主题配置文件-config-butterfly-yml/#「在线编辑」',[「博客」详解 Butterfly 主题配置文件_config.butterfly.yml | Minge],far fa-hand-point-right,block outline right blue larger %}

   注意目录要精确到***「source」***

2. 在网页中点击文章名旁边的编辑按钮，会跳到***「GitHub」***源文件，编辑后***「commit」***云端保存

   <img src="https://s2.loli.net/2022/07/06/uiewjN4Rq6H2TyM.png" style="zoom:67%;" />

3. 当本地源码没有更改，而远程源码更改，想要将远程的更改拉取到本地

   ~~~bash
   git pull
   ~~~

---

# <center>疑难杂症

- 网络原因导致的失败

  ~~~
  fatal: unable to access 'https://github.com/wangmin-1995/wangmin-1995.github.io.git/': OpenSSL SSL_read: Connection was aborted, errno 10053
  ~~~

  见

  {% btn 'https://minge.live/2022/「软件」解决Git慢速问题-Clash全局代理/#Clash全局代理',[「软件」解决 Git 慢速问题 + Clash 全局代理 | Minge],far fa-hand-point-right,block outline right blue larger %}

- 若***「commit」***成功，但***「push」***出错，此时不允许再次***「commit」***，以下指令可以撤销上次***「commit」***

  ~~~bash
  git reset --soft head~1
  ~~~

- ***「push」***出错

  ~~~
  hint: Updates were rejected because the tip of your current branch is behind
  hint: its remote counterpart. Integrate the remote changes (e.g.
  hint: 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  ~~~

  解决

  ~~~bash
  git pull --rebase origin master
  ~~~

  ***「master」***要替换为当前分支名

---

