---
title: git常用命令
date: 2019-06-24 11:46:13
categories:
- git
tags: git
---

## 创建远程分支
```
git checkout -b my-test  //在当前分支下创建my-test的本地分支分支
git push origin my-test  //将my-test分支推送到远程
git branch --set-upstream-to=origin/my-test //将本地分支my-test关联到远程分支my-test上   
```
## Git仓库迁移而不丢失log的两种方法
要求能保留原先的commit记录，应该如何迁移呢？ 
同时，本地已经clone了原仓库，要配置成新的仓库地址，该如何修改呢？
### 建立新仓库
1). 从原地址克隆一份裸版本库，比如原本托管于 GitHub。 
```
git clone --bare git://github.com/username/project.git  
```
2). 然后到新的 Git 服务器上创建一个新项目，比如 GitCafe。  
3). 以镜像推送的方式上传代码到 GitCafe 服务器上。  
```
cd project.git
git push --mirror git@gitcafe.com/username/newproject.git
```
4). 删除本地代码
```
cd ..
rm -rf project.git
```
5). 到新服务器 GitCafe 上找到 Clone 地址，直接 Clone 到本地就可以了。
```
git clone git@gitcafe.com/username/newproject.git
```
这种方式可以保留原版本库中的所有内容。
### 切换remote_url
先查看remote的名字
```
git branch -r
```
假设你的remote是origin，用git remote set_url 更换地址
```
git remote set-url origin remote_git_address
remote_git_address更换成你的新的仓库地址。
```
第二种切换remote_url的方法更直接，直接更改.git/conf配置文件里的ip地址就行。

## Git忽略文件权限或者拥有者改变导致的git状态变化

在当前git仓库下执行：
```
 git config core.filemode false
 git config --list
```
如果想对全局git库生效
```
git config --global core.fileMode false
```
对比一下 当前库命令如下
```
 git config core.filemode false
```
当然也可以在命令行下对文件进行编辑：本例已mac osx系统为例
```
cd ~/
vi  .gitconfig
fileMode = false
```
实际过程中发现 已经clone下来的项目 在使用全局设置后无用 需要对当前项目做单独设置
```
 git config core.filemode false
cd ~/xxx/.git
vi config
fileMode = false
```
删除配置
```
git config --unset --global core.fileMode false
```