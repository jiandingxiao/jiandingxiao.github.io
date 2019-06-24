---
title: git常用命令
date: 2019-06-24 11:46:13
categories:
- git
tags: git
---
[toc]
## 创建远程分支
```
git checkout -b my-test  //在当前分支下创建my-test的本地分支分支
git push origin my-test  //将my-test分支推送到远程
git branch --set-upstream-to=origin/my-test //将本地分支my-test关联到远程分支my-test上   
```