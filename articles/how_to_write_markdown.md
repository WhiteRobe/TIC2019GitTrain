# 第四章(进阶) 如何书写Markdown/README.md
> 深入学习的阅读资料：[Mastering Markdown](https://guides.github.com/features/mastering-markdown/)

我无意于重复已经存在的教程信息，只准备简单列出本次培训中各位所需要知道的精简信息。
如果你有兴趣，请移步阅读资料中的超链接，更加系统性地进行学习。

- 本章你将了解到如何书写Markdown。以及如何在Github上写一份好看的`README.md`文件。

## Markdown语法

Markdown是一种快捷式的标签语言，如果有同学写过HTML，对这玩意应该非常之熟悉。
正因为其本质上基于HTML，因此HTML标签也是可以共存的，例如：`<h1>一级标题</h1>` 与 `# 一级`是完全等价的。

关于Markdown，你们可以找到现成的学习资料：[Mastering Markdown](https://guides.github.com/features/mastering-markdown/)，我就不再次重复这个过程了。

本篇将致力于告诉你如何使用Markdown语言书写一份好看的`README.md`文件

## 什么是 `README.md`

`README.md` 是有关本项目的总览，是其他人首次接触本项目对本项目的第一印象。一份好的`README.md`可以让人对你的项目更感兴趣。

## `README.md`编写技巧 

大部分情况下，你可以按照编写HTML页面的方式来编写`README.md`。但我们今天说点更加有趣的。

> 本小节将随时更新，收集一些编写小技巧。 ![](https://img.shields.io/maintenance/yes/2019.svg)

### 如何插入图片

**练习**：

1. 新建一个仓库，按一下配置构建目录：

- `/pic/pic1.jpg`
-  `/README.md`

2. 在`README.md`文件中书写一行`![](/pic/pic1.jpg)`，提交到github，观察效果。

> 你也可以使用`<img src="/pic/pic1.jpg" width="100%"></img>`来添加该图片，同时还能更加精准的控制尺寸。

这样插入图片似乎还行，但我们之前提过，github是可以拿来当图床的，这样引用显然是没办法作为图床使用的。还是以`/pic/pic1.jpg`图片为例，敲入以下内容：

- `<img src="https://github.com/<你的GithubID>/<库的名字>/raw/master/pic/pic1.jpg"></img>`

也就是：`![](https://github.com/<你的GithubID>/<库的名字>/raw/<分支>/<图片地址>)`，通过这个URL就可以访问到这张图片的真正地址啦。

> 作为参考，你们可以到我编写的[这个项目](https://raw.githubusercontent.com/WhiteRobe/TreasureHunter/master/README.md)里查看此类写法。

### 如何居中显示

居中显示需要用到HTML标签，且内部内容也必须采用HTML标签书写，如：

```
<p align="center">
	<img src="https://github.com/WhiteRobe/TIC2019GitTrain/raw/master/practice/example/logo.png" width="30%">
	</img>
</p>
```

<p align="center">
	<img src="https://github.com/WhiteRobe/TIC2019GitTrain/raw/master/practice/example/logo.png" width="30%">
	</img>
</p>


### 如何挂上好看的徽章

你们一定注意到了本项目的`README.md`页面有一堆好看的徽章，比如：

- 输入：`![License](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)` 可以创建：

![License](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)

- 输入：`![](https://img.shields.io/badge/Windows-7|10-blue.svg)` 可以创建：

![](https://img.shields.io/badge/Windows-7|10-blue.svg)

- 甚至还有图标内容——输入：`![](https://img.shields.io/badge/力扣CN-LeetCode.cn-green.svg?style=for-the-badge&logo=leetcode)
[https://leetcode-cn.com](https://leetcode-cn.com/)`:

![](https://img.shields.io/badge/力扣CN-LeetCode.cn-green.svg?style=for-the-badge&logo=leetcode)

- 也可以使用BASE64自定义图标：

[![](https://img.shields.io/badge/身披白袍-Shenpibaipao-green.svg?style=for-the-badge&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAIAAACQKrqGAAAACXBIWXMAAAsTAAALEwEAmpwYAAAE6WlUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSLvu78iIGlkPSJXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQiPz4gPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iQWRvYmUgWE1QIENvcmUgNS42LWMxNDIgNzkuMTYwOTI0LCAyMDE3LzA3LzEzLTAxOjA2OjM5ICAgICAgICAiPiA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPiA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyIgeG1sbnM6cGhvdG9zaG9wPSJodHRwOi8vbnMuYWRvYmUuY29tL3Bob3Rvc2hvcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RFdnQ9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZUV2ZW50IyIgeG1wOkNyZWF0b3JUb29sPSJBZG9iZSBQaG90b3Nob3AgQ0MgKFdpbmRvd3MpIiB4bXA6Q3JlYXRlRGF0ZT0iMjAxOS0wNi0yM1QxNTo1NTowMSswODowMCIgeG1wOk1vZGlmeURhdGU9IjIwMTktMDYtMjNUMTU6NTU6NTErMDg6MDAiIHhtcDpNZXRhZGF0YURhdGU9IjIwMTktMDYtMjNUMTU6NTU6NTErMDg6MDAiIGRjOmZvcm1hdD0iaW1hZ2UvcG5nIiBwaG90b3Nob3A6Q29sb3JNb2RlPSIzIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOjQ5OTI3M2ZiLWMyMDYtOGQ0OC1iYjllLWRiMTI1MTJiYTc2NiIgeG1wTU06RG9jdW1lbnRJRD0ieG1wLmRpZDo0OTkyNzNmYi1jMjA2LThkNDgtYmI5ZS1kYjEyNTEyYmE3NjYiIHhtcE1NOk9yaWdpbmFsRG9jdW1lbnRJRD0ieG1wLmRpZDo0OTkyNzNmYi1jMjA2LThkNDgtYmI5ZS1kYjEyNTEyYmE3NjYiPiA8eG1wTU06SGlzdG9yeT4gPHJkZjpTZXE+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJjcmVhdGVkIiBzdEV2dDppbnN0YW5jZUlEPSJ4bXAuaWlkOjQ5OTI3M2ZiLWMyMDYtOGQ0OC1iYjllLWRiMTI1MTJiYTc2NiIgc3RFdnQ6d2hlbj0iMjAxOS0wNi0yM1QxNTo1NTowMSswODowMCIgc3RFdnQ6c29mdHdhcmVBZ2VudD0iQWRvYmUgUGhvdG9zaG9wIENDIChXaW5kb3dzKSIvPiA8L3JkZjpTZXE+IDwveG1wTU06SGlzdG9yeT4gPC9yZGY6RGVzY3JpcHRpb24+IDwvcmRmOlJERj4gPC94OnhtcG1ldGE+IDw/eHBhY2tldCBlbmQ9InIiPz45baZ7AAABvElEQVQoz32SzUoCURTHD4iLQOgBctEruAxUcOmqvYK46wl6hZZuWuRGECMXBkWKouUHkZnpZFYoaEb4OXNHtGZyZCZ1pjMfCW06/C/3cM+Pw/8cLnCDAU/ITBT/Ec+yiAFH03h9tNuGWq1Jvc4Wi8zVFZPJkHx+XKtxoxFiMJdlNputWiyUxVIGKAJUAJ62t5s7O027/cVme9jcJIkEYjBXFDadLgHkAKomU39/ny8UZElSfoO/vKSj0dlioaG53DVAw+FYTqd6ebVYCI2G8Pws9XokFBoeHwurlYr2j44erVYDEsVXj6eysXEHUNZ0C6AaUBQQZLl3eDgJh3X0ze/PAiB3r6ms5SSdVtGv+RwzsdPRUcpsxsko9K2potEklVJR9Ds8OZlVq0ZXnw+73miruNFUXnfF0w0EOru765EHBwdNt7vpdLbc7pbLhTaYiwsDZeLxAgD2+6Zp5W/g1nCsYSRioGw+j95xX/Wtrfe9PRIMfiSTn5nMNBbreL0lk4nRN8AR8tntTmq1CUUxqdQgEhlGo/TZGX1+PorFRqenWOL6fcRA/S4sKyyXa+GgM0lSP4ok6S/8eIzYD7RMqg7UJHT/AAAAAElFTkSuQmCC)](https://blog.csdn.net/Shenpibaipao/)

这都归功于一个项目：[https://shields.io/](https://shields.io/) 欢迎各位尝试这个[项目](https://github.com/badges/shields)。

### 超链接附加悬浮标题

- 举例：`[WhiteRobe/TIC2019GitTrain](https://github.com/WhiteRobe/TIC2019GitTrain "悬浮标题")`，显示效果：

[WhiteRobe/TIC2019GitTrain](https://github.com/WhiteRobe/TIC2019GitTrain "悬浮标题")

### 添加项目访问量监控

- 调用插件：`![HitCount](http://hits.dwyl.io/{username}/{project}.svg)`。

如`![HitCount](http://hits.dwyl.io/WhiteRobe/TIC2019GitTrain.svg)`，显示效果：![HitCount](http://hits.dwyl.io/WhiteRobe/TIC2019GitTrain.svg)


## 一份好的`README.md`应该包含哪些内容

1. 首先，你应该在最顶上列出你的项目名称，给人一个记忆点
2. 接着，给出你的LICENSE、项目参数等。(比如上文提到的那一排Badge)
3. 给出项目的样例，例如一个[网站项目](https://github.com/WhiteRobe/Qbook-web)应该给出各个界面的样子，网站的功能。
3. 列出项目的依赖、环境搭建及项目运行指南。
4. 如果你欢迎其他人一同完善这个项目，还要给出contributing guidelines.
5. 贡献者和项目捐赠者。

> 这里有一份参考：[carbon/README.md](https://github.com/dawnlabs/carbon/blob/master/README.md)

## 编写练习

1. 仿照本仓库中的[`/practice/example/README.md`](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/practice/example/README.md)编写一份`README.md`文件；
2. 像上次一样，在你练习`pull request`时创建的文件夹中带上你的作品，然后`pull request`到这个仓库。

---

[返回目录](https://github.com/WhiteRobe/TIC2019GitTrain/blob/master/README.md)