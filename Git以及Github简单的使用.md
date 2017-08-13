# Git以及Github简单的使用

​	最近下班后比较闲，偶然的机会参与了邢不行老师发起的一个talib库的文档翻译。由于参与人数比较多，我们打算放在Github上进行这个项目。于是我默默的重新捡起了git这个不知道怎么用的软件

## Git安装

​	Git这个软件可以在[这个网址]([https://git-scm.com)下载，由于我用的是windows系统 ，就直接下载windows版本的Git了。文件不大，大约37MB左右，但是需要根据系统的位数下载这个软件，可以从系统属性中看到。

![系统位数](系统位数.jpg)

​	我的是64位的系统，装的就是64位的Git。安装过程挺简单的，一路无脑点下一步就可以了。最终打开Git Bash，确认Git安装完成

![Git Bash](GitBash.jpg)

## Git常用基本语句

​	Git的语句不算多，我用了几天，大概用到了6个语句，分别是**init，add，commit，remote，pull，push**。

### init

作用：初始化本地库

用法与结果：

```shell
11959@SimonXu_Dell MINGW64 /e/test
$ git init
Initialized empty Git repository in E:/test/.git/
```

备注：一个文件夹内只需要进行一次初始化，会生成一个.git的隐藏文件夹

### add

作用：将本地的变更信息加入到暂存库中

用法与结果：

```shell
11959@SimonXu_Dell MINGW64 /e/test (master)
$ git add .
```

备注：

* add后面需要跟空格和“.”，意思是把所有变更提交到暂存库中

### commit

作用：将变更提交到本地库中

用法与结果：

```git
11959@SimonXu_Dell MINGW64 /e/test (master)
$ git commit -a -m "test"
[master (root-commit) f70c375] test
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 fun.txt
```

备注：

 * 命令中-a是把所有变更的文件都提交到本地库中，如果没有-a，那么只提交暂存库中的变更。
 * 命令中-m是直接添加提交信息的意思，提交信息在双引号中

### remote

作用：用于同远程库进行连接

用法与结果：

```shell
11959@SimonXu_Dell MINGW64 /e/test (master)
$ git remote add test https://github.com/xyx518809/test.git

11959@SimonXu_Dell MINGW64 /e/test (master)
$ git remote
test
```

备注：

* 命令中add是添加远程仓库的意思，如果要移除远程仓库，用命令

  ```shell
  git remote remove test
  ```

* 命令中test是给远程仓库取的名字，可以随意去，不过一般默认叫origin

* 直接输入git remote，可以查询远程仓库

### pull

作用：从远程仓库下载到本地仓库

用法与结果：

```shell
11959@SimonXu_Dell MINGW64 /e/test (master)
$ git pull test master
remote: Counting objects: 10, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 10 (delta 2), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (10/10), done.
From https://github.com/xyx518809/test
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> test/master
```

备注：

* 命令中test是前面remote命令给远程库去的名字
* master是指分支的名字叫master

### push

作用：从本地仓库上传到远程仓库

用法与结果：

```shell
11959@SimonXu_Dell MINGW64 /e/test (master)
$ git push test master
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.76 KiB | 1.76 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/xyx518809/test.git
   70c4312..dca8f71  master -> master
```

备注：

* push要在commit以后

## Git与Github连接

​	因为项目在Github上进行，所以Git需要和Github连接。连接方式有两种，一种是https方式，一种是SSH方式。

​	Https方式比较简单，GitHub上提供了每个远程库的https的地址，比如我的github中test的远程库地址为：

```php+HTML
https://github.com/xyx518809/test.git
```

于是本地库要和我的这个远程库连接，只要输入:

```shell
11959@SimonXu_Dell MINGW64 /e/test (master)
$ git remote add test https://github.com/xyx518809/test.git
```

这样，我的本地库就和远程库连接起来了。连接后可以进行pull和push，但是第一次push会要求你输入账号和密码

​	SSH的配置会比较复杂，不过安全性会高一点官网上提供了[配置方法](https://help.github.com/articles/connecting-to-github-with-ssh/)，大家可以试一试。

## 实例

* 移动地址到本地仓库

  ```shell
  11959@SimonXu_Dell MINGW64 ~
  $ cd e:/micloud/github/test

  11959@SimonXu_Dell MINGW64 /e/micloud/github/test
  $
  ```


* 初始化Git

  ```shell
  11959@SimonXu_Dell MINGW64 /e/micloud/github/test
  $ git init
  Initialized empty Git repository in E:/MiCloud/GitHub/test/.git/
  ```

* 连接github上的test，并确认

  ```shell
  11959@SimonXu_Dell MINGW64 /e/micloud/github/test (master)
  $ git remote add test https://github.com/xyx518809/test.git

  11959@SimonXu_Dell MINGW64 /e/micloud/github/test (master)
  $ git remote -v
  test    https://github.com/xyx518809/test.git (fetch)
  test    https://github.com/xyx518809/test.git (push)
  ```

*  从远程仓库pull文件到本地仓库

  ```shell
  11959@SimonXu_Dell MINGW64 /e/micloud/github/test (master)
  $ git pull test master
  remote: Counting objects: 21, done.
  remote: Compressing objects: 100% (12/12), done.
  remote: Total 21 (delta 5), reused 9 (delta 1), pack-reused 0
  Unpacking objects: 100% (21/21), done.
  From https://github.com/xyx518809/test
   * branch            master     -> FETCH_HEAD
   * [new branch]      master     -> test/master
  ```

  ![pull file](pullfile.jpg)

*  在本地编辑文件

*  

* ​