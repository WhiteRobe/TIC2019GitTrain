# 第二章 Git的基本使用
> 深入学习的阅读资料：[git-recipes: 4.1 图解 Git 命令](https://github.com/geeeeeeeeek/git-recipes/wiki/4.1-%E5%9B%BE%E8%A7%A3-Git-%E5%91%BD%E4%BB%A4)

我无意于重复已经存在的教程信息，只准备简单列出本次培训中各位所需要知道的精简信息。
如果你有兴趣，请移步阅读资料中的超链接，更加系统性地进行学习。

- 本章你将了解到如何使用Git，主要以Git GUI的使用为主，辅以部分需要Git Bash键入的git指令。完全萌新向和速成向。

- 本章结束后会留有一个小练习。你应当在使用Git GUI完成练习后，移步上面的学习资料了解更多相关的Git指令。

## 第一步：建立一个本地仓库

在[上一章](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/git_and_github.md)中，我们利用GUI建立了一个Git本地仓库。

我们回顾一下做法：

1. 随便新建一个文件夹，叫啥不重要，进入文件夹，右键空白处，选择`Git GUI Here`。
2. 选择`Create New Repository`，`Browse`到你新建的文件夹，点击`Creat`建立仓库。

利用GUI建立一个仓库非常简单，但这里我们要稍微涉及一点Git指令，讲一讲如何使用git指令建立一个仓库：

1. 随便新建一个文件夹，叫啥不重要，进入文件夹，右键空白处，选择`Git Bash Here`。(你也可以直接打开`CMD`或者`Powershell`等shell终端，`cd`到这个目录中)。
2. 输入命令`git init`，此时这个仓库一样建立起来了(你应该会看到一个名为`.git`的隐藏文件夹)。

看，实际上Git指令没那么复杂，甚至和GUI一样和善。

**关于仓库**

现在，我们要补充一些关于仓库的知识：

- **本地仓库** 在上文中，当我们使用`git init`创建仓库时，建立的就是一个带**工作目录**的本地Git仓库。因为它存在于你的本地环境中，且并不与任何人直接进行交互。


- **远程仓库** 相对的，放在服务器上的自然就是远程仓库咯。比如Github上新建一个`Repository`，实际上就为你提供了一个远程仓库。


- **共享仓库** 一般来说，远程仓库都是共享仓库，所有开发者与共享仓库进行直接交互，从而达到间接交互的目的。

> 那么如何建立一个共享仓库呢？按照上面的步骤，将输入`git init`改为输入`git init --bare test.git`，你会发现目录下多出了一个名为`test.git`的共享仓库，它并不带有工作目录，假如你的电脑是一台服务器，那么别人就可以通过`your_account@url:port/$PATH/test.git`访问到这个共享。

- **工作目录** 工作目录中的文件收到Git的控制。参考下图中的`代码文件x.xxx`，它们所在的区域就是工作目录。

![](/pic/WorkDirectory.jpg)

## 第二步：设置你的个性化信息

Git是一个团队开发工作，你对团队的每次贡献都会有相应的记录。所以此时你应该告诉这个仓库你的个人信息，主要包括两个：

- **邮箱** 邮箱是别人联系你的途径，当然你应当留意你的个人隐私问题，这个内容我们会放到之后的几章中讲，此处你可以随便填写一个邮箱。
- **姓名** 你可以填真名，或是化名，取决于你的实际开发和写作环境。

让我们先从Git GUI入手：

1. 右键空白处，选择`Git GUI Here`打开你的仓库。
2. 按照下图操作，打开Git Config。

![](/pic/SetConfig.jpg)

3. 如下图所示，我所建立的这个仓库名为`test`，所以左侧是这个仓库的配置。右侧是全局的配置，“全局配置”的意思是在这个机子中每次建立一个仓库时会默认使用右侧的配置，除非左侧的配置项与右侧的不同。

![](/pic/SetConfig2.jpg)

接着我们来学学使用Git指令该怎么进行以上操作：

1. 打开Git Bash界面，我们输入指令`git config --help`来查看`git config`的帮助文档。【--help】是一个很有用的指令参数，当你忘了某个指令的使用方法，你都可以如此进行搜寻。
2. 我们可以看到如此一行：


```
**user.email**

	Your email address to be recorded in any newly created commits. Can be overridden by the GIT_AUTHOR_EMAIL, GIT_COMMITTER_EMAIL, and EMAIL environment variables. See git-commit-tree(1).
```
3. 使用`git config user.email <你的Email>`进行邮箱的设置。同样的，`git config user.name <你的名字或化名>`可以设置该本地仓库的所有者姓名。
   

当你设置完这些值之后，可以打开`.gti/config`，查看到你刚刚所设置邮箱和姓名。

> 推荐使用[VS Code](https://code.visualstudio.com/)或[NotePad++](https://notepad-plus-plus.org/)等软件打开文本文件，Windows自带的笔记本实际上是有问题的，会在每个文档的首行不受控地添加一个【0xefbbbf】。

## 第三步 工作区与缓冲区

接下来，我们要说如何