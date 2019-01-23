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

工程配置仓库的默认配置文件：
ocean@mhc:~/MYGIT/ocean$ cat .repo/manifest.xml 

<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <default sync-j="2"/>
  <remote fetch="https://ocean.gitlab.com/A9/MAINAPP" name="A9MAINAPP" />
  <project remote="A9MAINAPP" revision="master" name="LinuxClient_I_zhushi" path="sources/MAINAPP/LinuxClient_I_zhushi"/>
</manifest>

}

```
