```
contribute:

git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/ocjyocto/repo_usage.git
git push -u origin master
```


```
Git Repo 镜像使用帮助 https://mirror.tuna.tsinghua.edu.cn/help/git-repo/
｛
下载
curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -o repo
chmod +x repo

更新
repo的运行过程中会尝试访问官方的git源更新自己，如果想使用tuna的镜像源进行更新，可以将如下内容复制到你的~/.bashrc里
export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo/'

｝

参考：
1. Manifest和Repo使用详解 https://cloud.tencent.com/info/7c879cfb83fd469fda1819f0ffa8ab17.html 
2. 阅读imx6的yocto启动手册，下载yocto repo，阅读其repo中的manifest。


实测：
{
mkdir repo_demo && cd repo_demo
~/bin/repo init -u https://github.com/ocjyocto/repo_demo_manifests.git -b master
~/bin/repo sync

第2步通过repo调用git下载工程配置仓库，在本地生成.repo管理文件夹。
第3步通过repo解读工程配置仓库的配置文件，调用git下载相关的代码仓库等，并做一些配置文件内规定好的诸如拷贝之类的动作。

-------------------

经过第一步：
ocean@mhc:~/MYGIT/ocean$ ls .repo/*
.repo/manifest.xml

.repo/manifests:
default.xml  README.md

.repo/manifests.git:
branches  config  description  FETCH_HEAD  HEAD  hooks  info  logs  objects  refs  rr-cache

.repo/repo:
color.py    command.pyc  editor.py   error.pyc        git_config.py   git_refs.pyc  main.py           pager.py     progress.pyc  repo                tests
color.pyc   COPYING      editor.pyc  git_command.py   git_config.pyc  git_ssh       manifest_xml.py   pager.pyc    project.py    subcmds             trace.py
command.py  docs         error.py    git_command.pyc  git_refs.py     hooks         manifest_xml.pyc  progress.py  project.pyc   SUBMITTING_PATCHES  trace.pyc

经过第一步工程配置仓库的默认配置文件：
ocean@mhc:~/MYGIT/ocean$ cat .repo/manifest.xml 

<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <default sync-j="2"/>
  <remote fetch="https://github.com/ocjyocto/" name="repodemocode" />
  <project remote="repodemocode" revision="master" name="repo_demo_code1" path="sources/repodemocode/repo_demo_code1"/>
</manifest>

-------------------

经过第二步：
ocean@mhc:~/MYGIT/ocean$ ls .repo/*
.repo/manifest.xml  .repo/project.list

.repo/manifests:
default.xml  README.md

.repo/manifests.git:
branches  config  description  FETCH_HEAD  HEAD  hooks  info  logs  objects  refs  rr-cache

.repo/projects:
sources

.repo/repo:
color.py    command.pyc  editor.py   error.pyc        git_config.py   git_refs.pyc  main.py           pager.py     progress.pyc  repo                tests
color.pyc   COPYING      editor.pyc  git_command.py   git_config.pyc  git_ssh       manifest_xml.py   pager.pyc    project.py    subcmds             trace.py
command.py  docs         error.py    git_command.pyc  git_refs.py     hooks         manifest_xml.pyc  progress.py  project.pyc   SUBMITTING_PATCHES  trace.pyc

ocean@mhc:~/MYGIT/ocean$ ls .repo/projects/sources/repodemocode/repo_demo_code1.git/
branches  config  description  FETCH_HEAD  HEAD  hooks  info  logs  objects  packed-refs  refs  rr-cache


ocean@mhc:~/MYGIT/ocean$ ls sources/repodemocode/repo_demo_code1/
build.sh  main.go

ocean@mhc:~/MYGIT/ocean$ ls .repo/projects/sources/repodemocode/repo_demo_code1.git/
branches  config  description  FETCH_HEAD  HEAD  hooks  info  logs  objects  packed-refs  refs  rr-cache

}

```
