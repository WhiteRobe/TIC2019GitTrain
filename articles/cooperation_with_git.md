# 第三章 多人协同开发
> 阅读资料：<[git-recipes: 3.4 使用分支](https://github.com/geeeeeeeeek/git-recipes/wiki/3.4-%E4%BD%BF%E7%94%A8%E5%88%86%E6%94%AF)>、<[git-recipes: 3.2 保持同步](https://github.com/geeeeeeeeek/git-recipes/wiki/3.2-%E4%BF%9D%E6%8C%81%E5%90%8C%E6%AD%A5)>

我无意于重复已经存在的教程信息，只准备简单列出本次培训中各位所需要知道的精简信息。
如果你有兴趣，请移步阅读资料中的超链接，更加系统性地进行学习。

要流畅阅读本章，你应该对 [第二章:Git的基本使用](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/how_to_use_git.md) 有较好的理解。

- 本章你将了解到分支及如何处理冲突，同时你将首次接触Github，进行多人协同开发的初体验。

- 本章内容较多，建议分两次学习和练习，以便更好掌握相关内容。

## 了解什么是分支(branch)

再[上一章](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/how_to_use_git.md)中我们了解了`add`、`commit`和"仓库历史"，但你一定会有一个问题：

- 基于以上操作，确实可以实现版本控制，但都听说Git可以进行多人协作、共同开发，我们应该怎样实现呢？

在解决这个问题前，我们需要了解另外一个概念：**分支(branch)**。

在上一章中，我们一直在对一个分支进行操作，即`master`分支。有时候我们也叫它"主分支"或"默认分支"，当你创建一个新的仓库时，这个分支就会被默认创建，在单分支模型中，之后的所有分支都会是该分支的子分支。

> 尽管你可以通过`git branch -m <oldbranch> <newbranch>`来进行分支的重命名，但我建议你应当保留`master`分支的原名，并将其作为主分支/默认分支。

你可以把分支认为是一条独立的工作流水线，多个分支可以共同进行开发，最终汇总到默认分支进行最终输出。这样，每个人都可以在各自的分支上同时进行工作，然后通过`merge`操作汇总各自的代码到默认分支上，从而完成团队协同工作。

![](/pic/GitBranchs.jpg)

你不必知道别人的分支上都发生了啥，你的本地库上也不需要保存别人的分支，只需要即将进行合并时处理一下**冲突(Conflict)**就行了。有关处理冲突的内容我们将会在下文提到。

- 实际上每个分支都可以认为是一个`fork`，我们会在[下一章](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/welcome_to_github.md)中提到。

## 管理分支

在Git GUI中，你可以通过`Branch`-`Create`来创建一个分支或是通过`Branch`-`Delete`来删除一个分支、通过`Branch`-`Checkout`切换当前所工作的分支：

![](/pic/CreateBranchWithGUI.jpg)

通过Git Bash操作时，需要用到指令`git branch`：

- `git branch` 可以查看所有本地分支，当前正在使用的分支会加上一个【*】标记。相对的，`git branch -r`可以查看远程分支、`git branch -a`可以同时查看本地和远程分支。
- `git branch <new_branch>` 会从当前正在使用的分支创建一个子分支。注意创建子分支时并不会自动切换到新创建的子分支，需要通过`git checkout <new_branch>`切换过去。
- `git branch -d <branch>` 可以安全删除一个分支。"安全"的意思是，如果当前分支未向父分支合并，Git会阻止操作并给出提示。如果你想暴力地、不想保留当前分支地所有工作地进行删除，请使用【-D】参数。
- `git branch -m <new_name>` 可以把当前正在使用地分支进行重命名。

至于如何使用Git GUI查看分支，那就十分简单啦：点击`Repository`-`Visualize All Branch History`，大部分情况下你只会看到一条历史线，当你的项目足够复杂时，它可能长这样：

![](/pic/GitBranchTree.jpg)

## 合并分支与冲突处理

- `git merge <branch>` 可以把一个分支向当前分支进行合并。

在Git Bash中，假设我们已经`git checkout feature_1`切换到了`feature`分支，接着我们可以使用`git merge feature_2`来把该分支向上合并，就像下图所示的那样：

![](/pic/F2MergeF1.jpg)

但是，还有一种情况，观察下图：

![](/pic/CreateBranchWithGUI.jpg)

当`master`分支在`feature_1`分支创建后提交了两个新的历史，而此时`feature_1`分支上也存在一个提交，如果这些提交修改的都是不同的文件，那么`feature_1`向上合并时就会顺畅无比，就像`feature_2`向`feature_1`合并一样。

而如果二者同时都修改了某一个文件，那么合并时到底以哪个分支的修改为准呢？这就提到了**冲突解决(Conflict Solve)**。

**练习：**(下面的练习以Git Bash为示例，你也可以使用Git GUI进行训练)

1. 建立一个新仓库，新建一个文件`text.txt`，键入内容【master分支1】，提交。
2. `git branch feature_1`创建一个新分支，并`git checkout feature_1`切换过去。
3. 修改`text.txt`的内容为【feature_1分支1】，提交。
4. `git checkout master`，修改`text.txt`的内容为【master分支2】，提交。
5. 通过`git merge feature_1`指令，把`featrue_1`分支向`master`分支合并。
6. 观察是否有冲突发生。

---

此时我们已经知道了，两个分支上的最新记录都同时修改了`text.txt`的内容，分别应为：【master分支2】和【feature_1分支1】，我们在进行合并操作时，会看到以下提示：

![](/pic/MergeConflict.jpg)

它提示了你发生冲突的文件，打开`test.txt`，你会看到以下内容：
> 推荐使用[VS Code](https://code.visualstudio.com/)作为文本编辑器，你会看到完整的冲突记录和以颜色进行区别的显示效果。下图也是基于VS Code得到的。 ♪(^∇^*)

![](/pic/ConflictsResult.jpg)

`========`上方的是当前分支的内容，下方的是进行合并的分支要传入的内容，它们发生了冲突，你需要二选一。

假如我选择保留原`master`分支的内容，我只需要留下【master分支2】，其它全删去即可。

保存`test.txt`后，执行`git add test.txt`和`git commit`指令即可最终完成解决冲突后的合并，仓库历史会变成这样：

![](/pic/HistoryAfterMerge.jpg)

> 我建议每次进行合并都立刻进行一次`commit`，方便版本的追溯。
> 
> - 你可以使用`git merge --abort`放弃正在进行的合并操作。
> - `merge`一共有三种方式，此处介绍的是最基本的合并方式，也称为**完整合并**，其它方式我们将到[第四章：拥抱Github](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/welcome_to_github.md)中进行讲述。

## 远程仓库

在[上一章](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/how_to_use_git.md)中我们提到了"本地仓库和"远程仓库"的概念，我们可以回顾一下这张图：

![](/pic/GitRemoteServer.jpg)

我们需要怎么让本地库与远程库建立联系呢？在此之前，我们先要拥有一个远程库，比如在Github上搭建一个。

## 初见Github、建立远程联系

首先，你需要建立一个Github账号。在顶部导航栏、你的头像附近有一个加号，点击它，在弹出的下拉框中选择`New repository`，你会看到如下界面：

![](/pic/CreatARepository.jpg)

非常简明易懂，目前我不建议你们生成库时添加LICENSE和gitignore文件，因此那两个框请选择`None`。接下来，要获取这个仓库的SSH地址(`Ctrl+C`拷贝下来)：

![](/pic/GithubSSHAddress.jpg)

使用命令`git remote add <name> <url>`来给本地库添加一个远程库的关联。

- 例如`git remote add github git@github.com:WhiteRobe/TIC2019GitTrain.git`就给定了一个库名为`github`、地址为`git@github.com:WhiteRobe/TIC2019GitTrain.git`的远程库。
> 有些教程会用`remote`或者`origin`来作为远程库名。
> 我个人觉得这是一个非常傻逼的行为，因为你的远程库可能会有好几个，比如我同时会有`github`、`gitlab`和`gitee`作为远程库及镜像备份，`remote`这个词指代不清，除了告诉你这个远程库是一个远程库这种显而易见的事，没有任何意义。

至于使用GUI，那就更简单了:

![](/pic/GUIRemoteAdd.jpg)

## 推送本地分支到远程库

我们现在要学习一个极为重要的指令：`git push <remote> <branch>`，可以将本地分支推送到指定的远程库。(推送时可能会需要你输入SSH账密，也就是Github账号和密码)

一个本地分支一旦推送到远程库，它就成为了远程分支。每个远程分支和本地分支都一一对应。

我们心中一定要有一个概念，远程库或者中心库是无比神圣的，我们要尽量避免错误的内容被推送上去，因为一旦成为远程分支，任何人都能访问到这个分支，你之后想要修正在这个分支上犯下的低级错误就不是简单利用`git revert`就能解决的了。

**练习：**

1. 创建一个本地仓库，通过Github新建一个远程仓库，写一个`Hello World`文件，本地提交。
2. 通过`git remote add github <url>` 建立远程联系。
3. 通过`git push github master`提交本地分支`master`到远程库`github`。按`F5`刷新Github仓库的Web页面，观察结果。
4. 如果你愿意，可以到[这里](https://github.com/WhiteRobe/TIC2019GitTrain/issues/1) `https://github.com/WhiteRobe/TIC2019GitTrain/issues/1` 留下你第一个仓库的地址，顺便了解一下什么是Github上的`Issues`。

> PS:如果你不想每次推送或建立远程仓库时都输入密码，你可能需要了解一下SSH公钥。这部分内容我不打算在这里介绍，自行百度"SSH公钥"或"Github免密推送"即可，或者到[此处查看](https://blog.csdn.net/Shenpibaipao/article/details/73369189)。

---

这里我们要介绍一个小技巧，假如刚刚你在新建一个`github`仓库时勾选了生成`.gitignore`或`LICENSE`文件，你此时会发现本地的`master`分支是无法被推送上去的。
你需要带上【-f】参数进行强制推送，洗掉远程库的记录并以本地库的记录取代。(需要仓库所有者权限)

> 注意！这是十分危险的，但作为一个新手你无需太过于担心这个问题，随着日后经验的积累，你会知道应该如何修正这些错误。

## 远程库管理

- `git remote` 可以查看本地库和远程库的关联，加上参数【-v】还能顺便列出地址链接。
- `git remote rm <name>` 可以移除一个远程库。
- `git remote rename <old_name> <new_name>` 可以对远程库进行重命名。

以上操作使用Git GUI做起来更方便，推荐使用GUI。

## 版本同步

现在，我们建立了本地-远程的连接关系，我们假设一个场景：多人开发时，他人也可能随时往中心仓库推送内容，你在开发时该如何知道别人是否进行了更新呢？

`git fetch <remote> <branch>` 就是这样一个指令，它可以拉取服务器上各个分支的变动，并告知你。

在了解了分支变动之后，你需要使用`git merge`指令来把变动合并到本地分支上，以实现版本同步。(可能需要解决冲突)

当然，你还可以直接使用`git pull <remote> <branch>`拉取变动并直接尝试合并操作。

**练习:**

1. 在刚刚新建的Github仓库的Web页面种，直接修改文件并提交，以实现远程库和本地库同一个分支上记录不同。
2. 使用上述方法拉取服务器的变动，观察本地`Hello World`文件的变化。

## 本章回顾

本章内容较多，除了 `git push -f <remote> <branch>` 需要Git Bash才能操作之外，其它指令都能用Git GUI实现。

- `git branch` 可以查看本地分支；
- `git branch -r` 可以查看远程分支；
- `git branch -a` 可以查看本地和远程分支；
- `git branch -m <new_branch_name>` 可以修改当前分支的名字；
- `git branch <new_branch>` 可以从当前分支创建一个新的子分支；
- `git checkout <branch>` 可以切换分支(别忘了该指令还可用于版本回滚)；
- `git merge <branch>` 可以合并一个分支到当前分支；如果有冲突，解决冲突完需要`add`和`commit`操作来进行合并的历史提交。
- 如何在Github上新建一个远程库。
- `git merge --abort`放弃正在进行的合并操作
- `git remote add <name> <url>` 添加一个远程仓库。
- `git remote push <remote> <branch>` 把一个本地分支推送到远程库。
- `git remote` 可以查看本地库和远程库的关联，加上参数【-v】还能顺便列出地址链接。
- `git remote rm <name>` 可以移除一个远程库。
- `git remote rename <old_name> <new_name>` 可以对远程库进行重命名。
- `git fetch <remote> <branch>` 可以拉取服务器上各个分支的变动，并告知你。
- `git pull <remote> <branch>` 拉取变动并直接尝试合并操作。

## 扩展阅读

如果你想更具体地了解什么样的多人协作方式是比较流行和受欢迎的，你可以到此处查看：

- **第三章(进阶)** [了解基于Git的协同工作流](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/knowning_of_git_flow.md)