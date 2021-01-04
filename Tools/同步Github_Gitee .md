Github 如何和 Gitee 进行同步？

---

更新于2021-01-01

1、首先关联Github和Gitee的远程仓库；

```shell
git remote add github git@github.com:code/demo.git
git remote add gitee git@gitee.com:code/demo.git
```

2、然后打开“.git”文件夹内的配置文件；接着修改remote改两个，一个Github库另一个Gitee库；

```shell
[core]
  repositoryformatversion = 0
  filemode = true
  bare = false
  logallrefupdates = true
[remote "origin"]
  url = git@github.com:chloneda/demo.git
  fetch = +refs/heads/*:refs/remotes/github/*
[branch "master"]
  remote = origin
  merge = refs/heads/master
```

将上述文件内容[remote "origin"]内容复制，修改origin名称，内容如下：

```shell
[core]
  repositoryformatversion = 0
  filemode = true
  bare = false
  logallrefupdates = true
[remote "github"]
  url = git@github.com:chloneda/demo.git
  fetch = +refs/heads/*:refs/remotes/github/*
[remote "gitee"]
  url = git@gitee.com:chloneda/demo.git
  fetch = +refs/heads/*:refs/remotes/gitee/*
[branch "master"]
  remote = origin
  merge = refs/heads/master
```

3、代码分别提交到Github和Gitee即可。

提交到github

```shell
git push github master
```

提交到码云

```shell
git push gitee master
```



