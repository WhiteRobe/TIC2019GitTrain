# 第三章(进阶2) 了解基于Git的协同工作流
> 阅读资料：[git-recipes: 3.5-常见工作流比较](https://github.com/geeeeeeeeek/git-recipes/wiki/3.5-%E5%B8%B8%E8%A7%81%E5%B7%A5%E4%BD%9C%E6%B5%81%E6%AF%94%E8%BE%83)

我无意于重复已经存在的教程信息，只准备简单列出本次培训中各位所需要知道的精简信息。
如果你有兴趣，请移步阅读资料中的超链接，更加系统性地进行学习。

要流畅阅读本章，你应该对 [第三章:多人协同开发](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/cooperation_with_git.md) 和 [第三章(进阶1):干净的仓库历史](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/better_history.md) 有较好的理解。

- 本章你将了解到各种Git工作流，即如何科学地使用Git进行多人协同工作。

- 你将学习到一个新的指令`git tag`。

## 中心化工作流

这个观点我们在之前就已经提到过了，它也是Git的基础运作方式：

![](/pic/GitRemoteServer.jpg)

多个开发者拥有自己的本地仓库、自己的本地分支和一些本地-远程分支(如`master`分支)。每个开发者在各自的仓库和本地分支上进行开发，最终通过本地`merge`、`rebase`等方法与远程分支建立练习，推送到中心仓库并暴露这些更改给所有人。

开发者需要通过`fetch`等指令定期拉取这些变更，从而完成协同工作。(当然，这种工作方式会导致非常多的merge和conflict solve问题)。

## 版本化

开发者每次提交也许只是添加了几个新功能或是完成了几个页面，那怎么判断这个工程可以向外发布了呢？

让我们先切换到准备对外发行的分支，使用`git tag`来标记当前提交为可对外发行的版本：

- `git tag -a <版本号> -m <tab message>`，如`git tag -a v1.0 -m "first release"`。

你的仓库历史出现一个`tag`标记：

![](/pic/GirRelease.jpg)

--- 

将该打了标签的分支推送到远程仓库，以Github为例

![](/pic/CreateAReleaseOnGithub.jpg)

我们常说的——“你去Github下一个代码啊”，指的一般就是下载一个发行版，而不是直接`git clone`一份代码(尽管这在某些时候等价于下载一个发行版)。

## Git Flow工作流


> 阅读资料：
>
> - [comparing-workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
> - [a-successful-git-branching-model](https://nvie.com/posts/a-successful-git-branching-model/)
> - [Git工作流指南：Gitflow工作流](https://www.cnblogs.com/jiuyi/p/7690615.html)

以上几篇文章已经很好的讲述了Git工作流的工作方式，如果你对如何科学开发有兴趣，任选一篇仔细阅读即可。为了避免数据的丢失，我做了一些备份工作：[备份资料](https://github.com/WhiteRobe/TIC2019GitTrain/tree/master/backup/gitflow)

![](/pic/git-model.png)

如上图所示，其大致思路如下：

- 存在两个恒定的分支`master`和`develop`分支。`master`分支只负责版本化的`commit`记录，而开发者在`develop`分支上持续进行开发。
- 当有新功能要加入时，从`develop`分支上分出功能分支`feature_x`，新功能完成后再合并到`develop`分支上。
- 当发行版发现一些恶性bug、需要进行热修复(hotfix)时，从`master`分支开出一条热修复分支，修复完成后合并到`master`(同时更新一个新的发行版)和`develop`分支。
- 当`develop`分支准备发行一个新的版本时，开出一个预发行分支`pre_release`，在这个分支上进行测试和bug修复，然后合并到`master`(同时更新一个新的发行版)和`develop`分支。
- 从`develop`上开出的功能分支统统进入一个叫做发布循环的队列中，一旦当开发者觉得可以交工了，向`develop`分支推送(相应的可能会被推送到预发行分支`pre_release`)之后，该功能分支应当被【冻结】，除非有新的功能升级需求或bug修复需要，才能再进行改动——此时需要再从`develop`分支拉回某些变更完成同步，修正bug或完成需求后，等待下个发布循环再推送到`develop`上。

---

[返回目录](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/README.md)