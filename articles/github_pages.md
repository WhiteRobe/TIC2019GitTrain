# 第四章(进阶2) 神奇的GitHub Pages
> 深入学习的阅读资料：
> - [将 Jekyll 主题添加到 GitHub 页面站点](https://help.github.com/cn/articles/adding-a-jekyll-theme-to-your-github-pages-site-with-the-jekyll-theme-chooser)
> - [配置 GitHub 页面的发布源](https://help.github.com/cn/articles/configuring-a-publishing-source-for-github-pages)
> - [What is GitHub Pages?](https://pages.github.com/)
> - [Transform your plain text into static websites and blogs](https://jekyllrb.com/)

我无意于重复已经存在的教程信息，只准备简单列出本次培训中各位所需要知道的精简信息。
如果你有兴趣，请移步阅读资料中的超链接，更加系统性地进行学习。

- 本章你将了解到如何使用GitHub Pages来展示你的工程。

## 什么是GitHub Pages

[GitHub Pages](https://pages.github.com/)是利用Github的服务器、基于用户定制内容的静态页面。通俗的来说，你可以把它当成一个免费的在线网站，而它的“数据库”就是你所建立的Github仓库。

## Github Pages可以用来做什么？

你可以在网上搜到很多关于Gtihub Pages的应用，主要用于偏静态的展示页面，例如：

- 私人博客
- 项目展示
- 个人简历

## 利用Github Pages来展示你的项目

如果你是一个前端，你可能需要提供一个可供互动的页面来展示你的项目。例如我所编写的两个单人桌游电子化项目：

- [桌游-星期五@Github](https://github.com/WhiteRobe/BoardGame-Friday)->[在线游玩](https://whiterobe.github.io/BoardGame-Friday/);
- [桌游-乌托邦引擎@Github](https://github.com/WhiteRobe/UBE)->[在线游玩](https://whiterobe.github.io/UBE/);

我没有为它们租用任何服务器，只是依托于Github的服务器，就完成了它们的Web应用搭建。

但此类应用偏硬核，且适用范围较小：如果我的项目不是一个网站项目，比如这个项目就只是一个Git教程，该怎么进行展示呢？

其实毫无问题：例如[https://whiterobe.github.io/TIC2019GitTrain/](https://whiterobe.github.io/TIC2019GitTrain/) 是本"Git速成教程项目"的展示站点，我除了编写了一个开源项目必备的`README.md`之外，并没有为此Code任何一行HTML代码。

这是怎么做到的呢？

## 基于Jekyll的快速工程页面展示

- [Jekyll](https://github.com/jekyll/jekyll) 是快速博客向静态网站搭建项目。

此时，作为萌新的你并不需要知道如何使用这个项目，因为Github已经把它收编了，你只需要在Github网站上点击一两个按钮，泡杯咖啡等Github帮你编译网页，你就可以看到类似[这个页面](https://whiterobe.github.io/TIC2019GitTrain/)的静态工程展示页面了。

具体做法如下：

1. 在Github上进入你的仓库，点击`Settings`-`Options`，找到`GitHub Pages`栏目。
2. 按下图所示配置，点击`Select theme`选择一个你喜欢的默认样式。
3. 泡杯咖啡，等待网站上线。

> 请确保你在选中的分支的根路径下编写了`README.md`，否则无法起效。
> 完成后，你的项目会自动在相应分支上进行一次提交，该分支根目录下会多出一个Jekyll配置文件`_config.yml`，注意拉取这个变动到你的本地库。

![](/pic/GithubPages.jpg)

---

[返回目录](/README.md)