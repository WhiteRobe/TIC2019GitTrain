# 第五章 Git服务器
> 深入学习的阅读资料：[服务器上的 Git - 架设服务器](https://git-scm.com/book/zh/v1/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E6%9E%B6%E8%AE%BE%E6%9C%8D%E5%8A%A1%E5%99%A8)

我无意于重复已经存在的教程信息，只准备简单列出本次培训中各位所需要知道的精简信息。
如果你有兴趣，请移步阅读资料中的超链接，更加系统性地进行学习。

- 要想流畅阅读本章，你需要有一定的Linux操作能力、一定的网络通讯基础。

- 本章你将了解到如何假设自己的Git服务器，实现完全属于自己的私人中央服务器。

## 服务器选择

事实上，作为练习，你完全可以通过`127.0.0.1`将本机作为一个服务器，也无所谓是Windows还是Linux系统。

但这年头还拿Windows Server当服务器的不是国企就是学校的老系统，邪道得不行，基本都是上世纪的DOS程序员还这么搞了。

我个人建议上阿里云租一台服务器，学生认证只要10￥一个月，兼职和善得不行。
至于是Unbuntu还是CentOS其实没差，都行，就是之后要记得在控制台开放相应的端口(SSH默认端口为22)。

## 在服务器上设置Git中央仓库
### 安装Git

由于阿里云某些环境镜像自带了Git，所以你可以先看看服务器上是否已经安装好Git了：
`git --version`

如果没有安装Git，你可以通过以下命令安装：

- **Ubuntu**： `sudo apt-get install git`。
- **CentOS**:  `sudo yum install -y git`。

> 如果提示找不到软件源，可以尝试`apt-get update`更新仓库源。

### 创建管理用户

不少教程都会告诉你新建一个用户——`git`：`adduser git`，然后按提示设置完密码；但其实你也可以不将这个用户取名为`git`，也可以叫`mygit`等。

> 以下均以`git`作为代称。

### 创建远程仓库

一般情况下，我们使用刚刚新建的这个用户的主目录作为仓库中央根目录：`git init --bare ~/test.git`

这样，就在用户的主目录下新建了一个叫做`test.git`的仓库。

> 如果你当前以root的身份创建了这个仓库，你需要调整一下这个仓库的所有者：`chown -R git:git ~/test.git`，否则与远程仓库链接时可能会报出以下错误——`insufficient permission for adding an object to repository database ./object`。

### 打开RSA认证

在某些情况下，你可能还需要打开RSA认证：`vim /etc/ssh/sshd_config`，编辑以下这几行成下面所示的值：
```
RSAAuthentication yes     
PubkeyAuthentication yes     
AuthorizedKeysFile  .ssh/authorized_keys
```

> 你可能需要安装`Vim` ：`apt-get install vim`(Ubuntu)、`yun install vim`(CentOS)

### Shell安全策略

我们虽然新建了个用户`git`(假设用户ID为1001)专门用于管理仓库，但我们并不希望他作为一个正常用户。
我们需要把它的Shell登录策略关闭：

1. `vim /etc/passwd`。
2. 把`git:x:1001:1001:,,,:/home/git:/bin/bash` 的末尾改为`
 `git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell`。


## 建立远程仓库联系

现在，回到你的本地机器上，使用之前学过的命令建立链接：`git remote add <name> <url>`。

你可以通过下面的SSH-url建立远程联系：

- `git remote add <mygit> <url>`命令用于建立远程仓库联系。
- **<url>**: `<Git管理账户>@<服务器IP>:<端口，如果是默认端口则可缺省><仓库地址>`，例如`git@180.180.180.180:1234/home/test.git`。(如果是默认端口，端口可缺省不填)。
- 连接时可能会要求你输入`git`账户的密码。如果不希望每次都输入密码，请在服务器上[添加你的SSH公钥](https://git-scm.com/book/zh/v1/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E6%9E%B6%E8%AE%BE%E6%9C%8D%E5%8A%A1%E5%99%A8)：`vim ~/.ssh/authorized_keys`。

最后，你可以尝试`git pull`一下服务器上的仓库或是`git push`文件到你的私人仓库了。

---

[返回目录](/README.md)