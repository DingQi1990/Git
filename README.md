# Git
* 什么是Git
* 什么是GitHub
* Git的由来
* 分布式和集中式
* Git和GitHub的使用





##### 什么是Git?

分布式版本控制工具



##### 什么是GitHub?

网站, GitHub是代码托管服务器

国内类似的网站:git.oschina.net   coding.net 等



##### Git的由来

很多人都知道，Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。

Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？

事实是，在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！

你也许会想，为什么Linus不把Linux代码放到版本控制系统里呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。

不过，到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使用权。

Linus可以向BitMover公司道个歉，保证以后严格管教弟兄们，嗯，这是不可能的。实际情况是这样的：

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。

Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

历史就是这么偶然，如果不是当年BitMover公司威胁Linux社区，可能现在我们就没有免费而超级好用的Git了。



##### 集中式和分布式









##### Git和GitHub的使用

工作区->暂存区->本地分支->远程分支master->组织的源仓库

期间还可以通过 ``git status``  去查看状态

1. 添加

```
git add./-A
```

2. 提交

```
git commit -m '修改了XXXX'
```



3.推送

```
git push
```



4.网页pull request  提交代码到源仓库

如果pull request 没有通过,你下次push依旧会保存在该push request 中





##### 版本回退

1.在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容，不然要版本控制系统干什么。版本控制系统肯定有某个命令可以告诉我们历史记录，在Git中，我们用`git log`命令查看：

```
commit b09a2d4780f048c0f1de35951c782a457ded9460
Author: dllo <dllo@dingqi.local>
Date:   Mon Apr 17 17:21:40 2017 +0800

    再一次修改le

commit 5ede58054e0db6fbea4192fbd3852bfd45502da2
Author: dllo <dllo@dingqi.local>
Date:   Mon Apr 17 16:52:42 2017 +0800

    修改了README

commit d74e0c332e5dc0faf002c83e60d87f069c24df0f
Author: dllo <dllo@dingqi.local>
Date:   Mon Apr 17 16:01:19 2017 +0800

    修改了README.md

commit 90e71a145c94df249cb77b118b1de7b159bbd0e7
Author: QC-L <liqichang_4869@163.com>
Date:   Mon Apr 17 15:27:00 2017 +0800

    Initial commit

```

`git log`命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是`append GPL`，上一次是`add distributed`，最早的一次是`wrote a readme file`。
如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：

```
dingqi:Git dllo$ git log --pretty=oneline
b09a2d4780f048c0f1de35951c782a457ded9460 再一次修改le
5ede58054e0db6fbea4192fbd3852bfd45502da2 修改了README
d74e0c332e5dc0faf002c83e60d87f069c24df0f 修改了README.md
90e71a145c94df249cb77b118b1de7b159bbd0e7 Initial commit
```



需要友情提示的是，你看到的一大串类似`3628164...882e1e0`的是`commit id`（版本号），和SVN不一样，Git的`commit id`不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的`commit id`和我的肯定不一样，以你自己的为准。为什么`commit id`需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。

每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线：



首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`3628164...882e1e0`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

```
dingqi:Git dllo$ git reset --hard 5ede58054
HEAD is now at 5ede580 修改了README
dingqi:Git dllo$ git log --pretty=oneline
5ede58054e0db6fbea4192fbd3852bfd45502da2 修改了README
d74e0c332e5dc0faf002c83e60d87f069c24df0f 修改了README.md
90e71a145c94df249cb77b118b1de7b159bbd0e7 Initial commit

```

只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个`append GPL`的`commit id`是`3628164...`，于是就可以指定回到未来的某个版本：

```
dingqi:Git dllo$ git reflog
5ede580 HEAD@{0}: reset: moving to 5ede58054
b09a2d4 HEAD@{1}: commit: 再一次修改le
5ede580 HEAD@{2}: commit: 修改了README
d74e0c3 HEAD@{3}: commit: 修改了README.md
```

从git reflog 就能看到你历史修改的id  想恢复哪个就可以找到相应的id.

```
dingqi:Git dllo$ git reset --hard b09a2d4
HEAD is now at b09a2d4 再一次修改le
dingqi:Git dllo$ git log --pretty=online
fatal: invalid --pretty format: online
dingqi:Git dllo$ git log --pretty=oneline
b09a2d4780f048c0f1de35951c782a457ded9460 再一次修改le
5ede58054e0db6fbea4192fbd3852bfd45502da2 修改了README
d74e0c332e5dc0faf002c83e60d87f069c24df0f 修改了README.md
90e71a145c94df249cb77b118b1de7b159bbd0e7 Initial commit
```

我又将之间休改的版本找了回来~是不是很神奇啊~

然后就是讲这几个新的命令重新git push.