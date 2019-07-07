# 第二章(进阶2) 世上真有后悔药
> 深入学习的阅读资料：[git-recipes: 2.6-回滚错误的修改](https://github.com/geeeeeeeeek/git-recipes/wiki/2.6-%E5%9B%9E%E6%BB%9A%E9%94%99%E8%AF%AF%E7%9A%84%E4%BF%AE%E6%94%B9)

我无意于重复已经存在的教程信息，只准备简单列出本次培训中各位所需要知道的精简信息。
如果你有兴趣，请移步阅读资料中的超链接，更加系统性地进行学习。

要流畅阅读本章，你应该对 [第二章:Git的基本使用](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/how_to_use_git.md) 和 [第二章(进阶1):让仓库更干净](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/how_to_write_gitignore.md) 有较好的理解。

- 本章你将了解到如何修正错误的仓库历史、如何对不满意的Commit进行修正。

- 本章属于进阶内容，大部分操作将以Git指令进行操作，但是Git GUI依然是可用的，请自行尝试。

## 仓库历史

首先我们要先回顾一下：什么是仓库历史？
当我们键入`git log`，可以得到完整的仓库历史，其中比较重要的是版本号(SHA ID)、提交信息(commit message)和修改分支。

> 如果仓库历史较长，请使用Git GUI或`git log --oneline`指令。

对于`git log`，还有很多小技巧，如已经提过的`git log --oneline`；我们还可以通过过滤模式来过滤`git log`的输出。

- `git log -n` n是一个大于零的整数，用于过滤出最近的n次提交。
- `git log --since="日期"` 可以过滤出从起始日期开始的提交记录，如`git log --since="2019-07-02"`；
- 相应的，还有【--until】【--after】【--before】，可以进行组合输出，如`git log --after="2019-07-02" --before="2019-10-10" `
- `git log --author="作者名"` 可以按照作者名过滤出提交信息。
- ...


令人高兴的是，作为一个Windows开发者，基于GUI可以很容易地过滤出相应的提交记录，比Git Bash输入指令不知道高到哪里去了。

## 撤销提交：revert 和 reset

当我们认为某次的提交是有问题的，想要撤销那一次提交，该如何做呢？（注意，**撤销**和**回滚**的意义并不相同）

我们先介绍`git revert <SHA ID>`指令，该指令可以直接把某一次的提交取消，所有在本次提交中发生变更的文件都会还原回上一次提交的内容，解决冲突后，这些文件进入缓存区，等待提交。

这么说未免有点抽象，我们做个小实验：

1. 新建一个库，新建一个文件`test.txt`，键入内容【1】，提交。假设本次的版本号为"111111"；
2. 修改文件内容为【2】，提交；假设本次的版本号为"222222"；
3. 修改文件内容为【3】，提交；假设本次的版本号为"333333"；
4. 键入命令`git revert 222222`，会发现内容被(或将被修改为【1】)；
5. 解决冲突(如果有的话)，提交。会发现新生成了一个commit记录"4444444"，之前的记录也都存在。

---

相比于`git revert`，`git reset`是一种不安全的撤销方式。当年使用`git reset <SHA ID>`来重置记录时，所有在此之后的记录都将永久消失。如果带上参数【--hard】，还会直接清空工作区里的所有变更，是一种比较暴力的撤销方式。

**练习：**

1. 新建一个库，进行多次提交；
2. 修改工作区某个文件的内容，但不进行提交，使用`git reset <之前某个版本的ID>`；
3. 修改工作区某个文件的内容，但不进行提交，使用`git reset --hard <之前某个版本的ID>`；
4. 比较二者差异、比较其与`git revert`对仓库历史的影响。

## 撤销版本追踪：reset 和 rm

在上面的内容中，我们了解到reset是一种非常暴力的撤销方式。而`reset`不仅仅可以撤销一次commit，还可以撤销Git对缓存区的一次提交。

**练习:**(如何撤销缓存区的记录)

1. 新建一个库，新建一个文件`test.txt`，使用`git add test.txt`将其添加到缓存区。
2. 使用`git status`查看缓存区状态。
3. 使用`git reset test.txt`将其移出缓存区，使用`git status`查看缓存区状态。

> 此处的`git reset test.txt` 可用 `git rm --cached test.txt` 替代。
> 
> - Git GUI中只需要点击缓存区中的文件前的图标即可实现将其从缓存区移除的操作。

而`rm`指令不仅可以通过搭配【--cached】参数移除缓存区中不需要的内容，还可以撤销仓库记录中对某个工作区文件的版本控制/追踪，也就是把这个文件从版本库/工作区中删除。我们会在下一小节提到。

**练习:**(如何用删除的方法撤销对某个文件的追踪)

1. 新建一个库，新建一个文件`test.txt`，将其添加至缓存区，使用`git commit`提交。
2. 使用`git rm test.txt`将其从版本库中删除。(相应的工作区也会移除这个文件，除非使用`git rm --cached <文件>`指令，详见下一小节的练习。)
3. 使用`git status`查看版本库信息。
4. 使用`git commit`提交、确认本次移除操作。

## 禁止版本追踪：.gitignore 与 rm 的区别

- 要流畅阅读本章，你应该对 [第二章(进阶1):让仓库更干净](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/articles/how_to_write_gitignore.md) 有较好的理解。

`git rm <文件名>`也常被用于修正`.gitignore`文件中被错误追踪的文件。

例如，先进行了一次`test.txt`的提交，由于此时`test.txt`已经进入了版本库，在`.gitignore`文件中添加`test.txt`并不能取消对`test.txt`的追踪，所以此时你应当使用`git rm test.txt`来去除这个文件。

由于`git rm <文件名>`也会同时直接移除工作区的相关文件，而如果你只是希望这个文件不被Git追踪和提交到远程库，但在本地需要保留，你应当使用`git rm --cached <文件名>`来移除这个文件。

> 但需要注意的是，这个修改只对你的本地库有效，任何在此之前克隆了这个库的人依然会追踪这个文件。

**练习:**(如何在保留工作区相应文件的情况下，撤销对某个文件的追踪)

1. 新建一个库，新建一个文件`test.txt`，将其添加至缓存区，使用`git commit`提交。
2. 编写`.gitignore`，添加`test.txt`的忽略字段。
3. 修改`test.txt`的文件内容，打开Git GUI，点击`Rescan`，会发现`test.txt`依旧被扫描出发生了变动。
4. 使用`git rm --cached test.txt`移除对其的版本控制，再次进行`Rescan`，观察结果。

## 修改仓库历史：`git commit --amend`

如果你对上一次提交的信息觉得不满意，比如敲错了一个单词，或是忘了提交一个文件。怕被同事笑话，该如何修正呢？

`git commit --amend`指令可以修正上一次commit时所填写的提交信息和所提交的文件。

- 如果想要修正的是前第`n`次的记录，你需要`checkout`到前第`n-1`次提交，再进行`amend` 操作。

- 每次提交实际上改写了一次仓库记录，因此需要小心谨慎。

> 同样，如果该提交已经被推送到远程仓库，我建议你最好将错就错。

**练习:**(我建议使用Git GUI进行练习，较为直观和方便)

![](/pic/GitCommitAmend.jpg)

1. 新建一个库，添加一个文件`test.txt`，使用`git commit`提交，记录本次提交的版本ID。
2. 进行`amend`操作，只修改commit message，提交，查看提交内容、记录本次提交的版本ID。
3. 进行`amend`操作，将`test.txt`移出缓存区，提交，查看提交内容、记录本次提交的版本ID。
4. 对比三次提交的版本ID。

## 本章回顾

- `git log` 的过滤方法；
- `git revert` 和 `git reset`的用法与区别；
- `git rm` 的用法；
- `git commit --amend` 修改仓库历史；

除了 `git rm`之外，所有操作都可以在GUI中完成，可以自行尝试。

---

[返回目录](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/README.md)
