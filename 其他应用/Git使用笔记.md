# Git使用笔记

**Git是目前世界上最先进的分布式版本控制系统**

## 使用Git

安装好git之后需要配置自己的用户信息：

$ git config --global user.name"name"

$ git config --global user.emila "emila"

## Git命令

**官网教程：https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%91%BD%E4%BB%A4%E8%A1%8C**

- 检查配置信息 **git config --list**：

  此命令可以列出所有git当时能找到的配置。如果想单独查询某一项的话可以使用 **git config < key >**来检查git的单独某项配置。

- 获取帮助 **git help < verb >**:

  获取帮助有三种等价方法可以使用：

  ```console
  $ git help <verb>
  $ git <verb> --help
  $ man git-<verb>
  ```

  例如想要获得git config命令的手册，就可以执行  git config --help。这些指令不用联网也可以查看手册。

### git操作指令



- **vi < file >**：通过此命令可以编辑指定文件名的文件内容，如果文件名是不存在的，就会在所在目录下面按照文件名创建新的文件。

  ```
  SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
  $ vi test.txt
  
  ```

- **touch**：创建一个文件

  ```
  
  ```
  
  

- **ll**：查看当前目录下面的所有文件信息。

  ```
  SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
  $ ll
  total 2
  -rw-r--r-- 1 SaoLinSiDaShiXiong 197121 74 Mar 17 10:39 readme.txt
  -rw-r--r-- 1 SaoLinSiDaShiXiong 197121  6 Mar 17 10:44 test.txt
  
  ```

- **cat < file >**：查看指定文件内的内容

  ```
  SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
  $ cat test.txt
  test
  
  
  ```

- **ls,dir:**查看当前文件目录下的文件

  ```
  SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
  $ dir
  file1.txt  readme.txt  s  test.txt
  
  SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
  $ ls
  file1.txt  readme.txt  s/  test.txt
  
  ```

- **ls -ah：**查看当前目录的隐藏目录。

  ```
  SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
  $ ls -ah
  ./  ../  .git/  file1.txt  readme.txt  s/  test.txt
  
  ```

- **git log：**使用此指令可以查看提交历史，以便确定要回退到哪个版本。

  ```
  SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
  $ git log
  commit 6fcf57efec72ba040210ef9428c6d5520ca517d4 (HEAD -> master)
  Author: ShaoLinSiDaShiXiong <lzy2572127614@163.com>
  Date:   Fri Mar 18 12:15:37 2022 +0800
  
      第二次更改
  
  commit 0e46dd4d7d6b617c6f38a56c0409565baec0fcaa
  Author: ShaoLinSiDaShiXiong <lzy2572127614@163.com>
  Date:   Fri Mar 18 12:06:36 2022 +0800
  
      aa
  
  commit 1e2c7fcaf87904c1cebd5bf005815cf453f91e2f
  Author: ShaoLinSiDaShiXiong <lzy2572127614@163.com>
  Date:   Fri Mar 18 12:05:26 2022 +0800
  
      diyici
  
  ```

  git log命令希纳是从浊酒尽到最晕啊的提交日志。

  <font color="#900"> 在git log命令后面也可以加上`--pretty=oneline`参数</font>

  ```
  SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
  $ git log --pretty=oneline
  6fcf57efec72ba040210ef9428c6d5520ca517d4 (HEAD -> master) 第二次更改
  0e46dd4d7d6b617c6f38a56c0409565baec0fcaa aa
  1e2c7fcaf87904c1cebd5bf005815cf453f91e2f diyici
  8b49850e62b15c1227cac4f4d0dfcda977468b7f commit
  8e23eba0633e19be3b5c32855ccffc71c16ea1b4 file3的提交 sdaf 撒地方
  2a774e59a8f9955bd3b252baa28311722ba37edb 提交
  3e641ef87fd0e37c63e3eee859376228aa93ef76 第一次测试
  
  ```

  

## 创建版本库

版本库又名仓库名，英文repository，可以简单的理解成为一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除Git都能跟踪，任何时刻都可以追踪历史，或者在将某个时刻可以”还原“

所以在使用git之前最好配置一下版本仓库，配置方法如下：

```
$ cd (电脑中选好的路径位置)
$ pwd	//
e:/git/learngit	//这里是提前选好的电脑路径
$ git inti	//这条指令就是将现在所在的目录变成git可以管理的仓库。
Initialized empty Git repository in e:/git/learngit
```

创建仓库最主要的命令就是git inti 瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令就可以看见。

### 把文件添加到版本库

首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。

因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

使用Windows的童鞋要特别注意：

千万不要使用Windows自带的**记事本**编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。建议你下载[Visual Studio Code](https://code.visualstudio.com/)代替记事本，不但功能强大，而且免费！

**将一个文件添加进Git需要两个步骤：**

1. git add file.txt file2.txt	第一步，用命令`git add`告诉Git，把文件添加到仓库,使用命令`git add <file>`，注意，可反复多次使用，添加多个文件。

2. git commit -m"add 2 file"第二步，用命令`git commit`告诉Git，把文件提交到仓库。`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，`git commit`命令执行成功后会告诉你，`1 file changed`：1个文件被改动（我们新添加的readme.txt文件）；`2 insertions`：插入了两行内容（readme.txt有两行内容），使用命令`git commit -m <message>`，完成。

   ```
   SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
   $ git commit
   [master f5ea04e] 这是一个需要删除的文件
    1 file changed, 1 insertion(+)
    create mode 100644 t.txt
   
   ```

   当我们没有对该文件进行提交备注的时候，git会让我们添加备注，这个时候通过:wq是不能正常保存退出的，需要使用:wq!来强制保存退出

## git 查看文件的几种方法

### 查看版本库状态git status

**git status:**

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/git/learngit (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   file1.txt
        new file:   test.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        readm.txt
        s/


```

<font color="#900">使用status指令来查看仓库状态之后的结构是这样的**Changes not staged for commit：**之后的文件是等待提交的文件，这些文件我们可以通过git commit指令进行提交。</font>

<font color="#900">**Changes not staged for commit:**之后的文件是未提交的修改，这些文件是已经提交过，但是内容又被修改过，需要我们使用git commit指令进行提交。</font>

<font color="#900">**Untracked files:**这些文件是还没有被git添加的文件，我们可以通过git add指令进行添加。</font>

<font color="#900">**使用git commit方法也可以查看可以提交的文件信息。**</font>

****

### 查看当前文件被更改的内容 git diff

**git diff:**此命令可以查看被修改的内容。

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git diff
diff --git a/test.text b/test.text
index a88b954..377d4db 100644
--- a/test.text
+++ b/test.text
@@ -1,6 +1,6 @@

 hello,wolder.
 `"你好世界"
-"提交文件必须要带-m么?
-aaaaaaaa
+"提交文件必须要带-m么?+a
+aaaabababbbaaaa

```

`git diff`顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以从上面的命令输出看到，我们将

`-"提交文件必须要带-m么?`
`-aaaaaaaa。`

修改成了：

`+"提交文件必须要带-m么?+a`
`+aaaabababbbaaaa`

知道了对`test.text`作了什么修改后，再把它提交到仓库就放心多了，提交修改和提交新文件是一样的两步。

****

### 查看版本库中文件更改的状态git log

**git log:**`git log`命令显示从最近到最远的提交日志。

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git log
commit ef9a94d66fcfe539db6003f54d961348aa358d23 (HEAD -> master)
Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.com>
Date:   Thu May 12 08:48:07 2022 +0800

    提交

commit 248f00a39efcd8550124f9f2c337cce2462c6085
Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.com>
Date:   Wed May 11 21:48:49 2022 +0800

    commit test

commit c2ad4f4c21bb5f52817545cfe610eac47a038874
Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.com>
Date:   Wed May 11 21:45:39 2022 +0800

    aaa

commit a740f416f5e6071fa0082de21b74683a499bedf0
Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.:

```

这里可以清楚的看见每一次提交的文件，时间，还有提交的备注。正常情况下，git会显示最近三次的文件提交信息，我们可以通过回车来查看以前的内容。

**在文件内容过多的情况下，我们可以加上`--pretty=oneline`参数：**

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git log --pretty=oneline
ef9a94d66fcfe539db6003f54d961348aa358d23 (HEAD -> master) 提交
248f00a39efcd8550124f9f2c337cce2462c6085 commit test
c2ad4f4c21bb5f52817545cfe610eac47a038874 aaa
a740f416f5e6071fa0082de21b74683a499bedf0 aaaa
484cabaf54a4c9662b0d1f192394b4ac79a1e59e 一次简单的测试

```

这样的话，git就只会返回每次提交的id号和提交的备注。

**需要友情提示的是，你看到的一大串类似`1094adb...`的是`commit id`（版本号），和SVN不一样，Git的`commit id`不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的`commit id`和我的肯定不一样，以你自己的为准。为什么`commit id`需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。**

每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线。

#### 查看最近的提交修改

假如说我们当前版本的代码编译运行出现了一个bug，这个时候我们可以使用`git log --stat`来查看最近的提交修改。

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git log --stat
commit f5ea04e158a5d23a6809e755c136a7e64ea04a05 (HEAD -> master)
Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.com>
Date:   Thu May 12 10:28:29 2022 +0800

    这是一个需要删除的文件

 t.txt | 1 +
 1 file changed, 1 insertion(+)

commit ef9a94d66fcfe539db6003f54d961348aa358d23
Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.com>
Date:   Thu May 12 08:48:07 2022 +0800

    提交

 test.text | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)

commit 248f00a39efcd8550124f9f2c337cce2462c6085
Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.com> 	
```

我们可以配合`--pretty=oneline`来减少返回的内容

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git log --stat --pretty=oneline
f5ea04e158a5d23a6809e755c136a7e64ea04a05 (HEAD -> master) 这是一个需要删除的文件
 t.txt | 1 +
 1 file changed, 1 insertion(+)
ef9a94d66fcfe539db6003f54d961348aa358d23 提交
 test.text | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
248f00a39efcd8550124f9f2c337cce2462c6085 commit test
 test.text | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
c2ad4f4c21bb5f52817545cfe610eac47a038874 aaa
 test.text | 1 +
 1 file changed, 1 insertion(+)
a740f416f5e6071fa0082de21b74683a499bedf0 aaaa
 test.text | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
484cabaf54a4c9662b0d1f192394b4ac79a1e59e 一次简单的测试
 test.text | 3 +++
 1 file changed, 3 insertions(+)

```



****

## 版本退回 git reset

我们每次向git提交文件的时候，git都会帮我们记录。我们可以将我们编写的文件返回到任意一次我们提交时候的状态。

首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

**git reset --hard HEAD^**

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git reset --hard HEAD^
HEAD is now at 248f00a commit test
```

我们这里执行了退回指令，`HEAD is now at 248f00a commit test`我们可以看到我们现在的文件处于`commit test`状态，还可以看到对应的提交id`248f00a`

****

### 通过版本号(commit id)来进行版本退回

如果我们退回到了以前的版本，但是突然反悔想，又觉得退回操作是多余的，这个时候我们可以通过`commit id`来将我们的文件返回到任意的一次提交状态。

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git reset --hard ef9a9
HEAD is now at ef9a94d 提交
```

**这样使用的条件是，我们知道对应的版本号，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个最新的`commit id`是`ef9a94d...`，于是就可以指定回到未来的某个版本**

版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。

这个时候在查看文件中的内容：**cat test.text**

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ cat test.text

hello,wolder.
`"你好世界"
"提交文件必须要带-m么?+a
aaaabababbbaaaa
```

可以看到文件已经返回到了最新的版本中。

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的`HEAD`指针，当你回退版本的时候，Git仅仅是把HEAD从指向`append GPL`：

```ascii
┌────┐
│HEAD│
└────┘
   │
   └──> ○ 第三次提交
        │
        ○ 第二次提交
        │
        ○ 第一次提交
```

改为指向`add distributed`：

```ascii
┌────┐
│HEAD│
└────┘
   │
   │    ○ 第三次提交
   │    │
   └──> ○ 第二次提交
        │
        ○ 第一次提交
```

然后顺便把工作区的文件更新了。所以你让`HEAD`指向哪个版本号，你就把当前版本定位在哪。

### 查看每次执行的命令

现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的`commit id`怎么办？

在Git中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到`第二版本`时，再想恢复到`第三版本`，就必须找到`第三版本`的commit id。Git提供了一个命令`git reflog`用来记录你的每一次命令：

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git reflog
ef9a94d (HEAD -> master) HEAD@{0}: reset: moving to ef9a9
248f00a HEAD@{1}: reset: moving to HEAD^
ef9a94d (HEAD -> master) HEAD@{2}: commit: 提交
248f00a HEAD@{3}: reset: moving to head~1
806beef HEAD@{4}: reset: moving to 806bee
c2ad4f4 HEAD@{5}: reset: moving to HEAD~1
248f00a HEAD@{6}: reset: moving to head~1
806beef HEAD@{7}: commit: append abcd
248f00a HEAD@{8}: commit: commit test
c2ad4f4 HEAD@{9}: commit: aaa
a740f41 HEAD@{10}: commit: aaaa
484caba HEAD@{11}: commit (initial): 一次简单的测试

```

**这个时候我们就可以看到每次操作的记录了，还有对应的版本号id。**

****

## 工作区和缓存区

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

先来看名词解释。

#### 工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的`git02`文件夹就是一个工作区：

![image-20220512094052810](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220512094052810.png)

#### 版本库（Repository）

工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

![0](C:\Users\SaoLinSiDaShiXiong\Pictures\笔记图片\0.jpg)

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

俗话说，实践出真知。现在，我们再练习一遍，先对`readme.txt`做个修改，比如加上一行内容：

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
```

然后，在工作区新增一个`LICENSE`文本文件（内容随便写）。

先用`git status`查看一下状态：

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	LICENSE

no changes added to commit (use "git add" and/or "git commit -a")
```

Git非常清楚地告诉我们，`readme.txt`被修改了，而`LICENSE`还从来没有被添加过，所以它的状态是`Untracked`。

现在，使用两次命令`git add`，把`readme.txt`和`LICENSE`都添加后，用`git status`再查看一下：

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   LICENSE
	modified:   readme.txt
```

现在，暂存区的状态就变成这样了：

![git-stage](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)

所以，`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。

```
$ git commit -m "understand how stage works"
[master e43a48b] understand how stage works
 2 files changed, 2 insertions(+)
 create mode 100644 LICENSE
```

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git status
On branch master
nothing to commit, working tree clean
```

现在版本库变成了这样，暂存区就没有任何内容了：

![git-stage-after-commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)

****

## 管理修改

**git其实管理的是修改，而不是文件。**

当我们在对一个文件进行内容的编辑之后，再将他add之后，在进行修改，之后在进行commit提交。这个时候提交的只是第一次add时的内容。

我们回顾一下操作过程：

第一次修改 -> `git add` -> 第二次修改 -> `git commit`

你看，我们前面讲了，Git管理的是修改，当你用`git add`命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，`git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别：

```
$ git diff HEAD -- readme.txt 
diff --git a/readme.txt b/readme.txt
index 76d770f..a9c5755 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.
-Git tracks changes.
+Git tracks changes of files.
```

可见，第二次修改确实没有被提交。

那怎么提交第二次修改呢？你可以继续`git add`再`git commit`，也可以别着急提交第一次修改，先`git add`第二次修改，再`git commit`，就相当于把两次修改合并后一块提交了：

第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

****

## 撤销修改

在日常工作中，我们很可能会犯一些错误，比如在文件中添加了一些不应该出现的内容，这个时候我们就需要了解git中都有那些撤销操作，具体怎么使用了。

### 丢弃工作区的内容

使用`git checkout -- file`可以丢弃工作区的修改：

```
$ git checkout -- test.txt
$ git restore test.text
```

命令`git checkout -- test.txt`意思就是，把`test.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

**总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。**

**`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令。**



Git同样告诉我们，用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区：

```
$ git reset HEAD readme.txt
Unstaged changes after reset:
M	test.txt
```

`git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。

## 删除文件

在我们可以使用git来删除我们版本库中的文件通过使用`rm`来完成删除操作。

```
$ rm t.txt
```

这里我们已经提前将文件进行了提交，这里执行了删除操作，在工作区中(文件夹内)已经删除了文件。

<font color="#f00">**从来没有被添加到版本库就被删除的文件，是无法恢复的！**</font>

这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，`git status`命令会立刻告诉你哪些文件被删除了：

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    t.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

这个时候我们可以删除版本库中的文件，或者将版本库中的文件恢复到工作区。

**删除版本库中的文件：**

我们可以使用add或rm来删除版本库中的文件

```
SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git rm t.txt
rm 't.txt'

SaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git commit -m"第二次删除"
[master c76dd5e] 第二次删除
 1 file changed, 1 deletion(-)
 delete mode 100644 t.txt
```

**先手动删除文件，然后使用git rm [file]和git add [file]效果是一样的。**

这个时候缓存区和工作区就都是干净的。

**另一种情况是删错了：**

因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

```
$ git checkout -- t.txt
$ git restore -- t.txt
```

这里使用`$ git restore -- t.txt`和使用`$ git checkout -- t.txt`的效果是一样的

`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

****

## 分支

每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

![git-br-initial](https://www.liaoxuefeng.com/files/attachments/919022325462368/0)

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

![git-br-create](https://www.liaoxuefeng.com/files/attachments/919022363210080/l)

你看，Git创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

![git-br-dev-fd](https://www.liaoxuefeng.com/files/attachments/919022387118368/l)

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

![git-br-ff-merge](https://www.liaoxuefeng.com/files/attachments/919022412005504/0)

所以Git合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

![git-br-rm](https://www.liaoxuefeng.com/files/attachments/919022479428512/0)



##### 创建分支

**需要注意的是我们每次创建的新的分支都是在原有分支的基础之上进行创建的，即新的分支包含原本分支内的所有版本内容。**

<font color="#f00">不管在是在那个分支中创建的文件，在文件编辑完成之后使用`git status`指令都可以进行查看其状态</font>

###### **创建分支有一下几种方法：**

- **git branch [name]**:

  通过这种方式我们可以创建一个新的分支

  ```
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
  $ git branch b
  
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
  $ git branch
    b
  * master
  ```

  可以看到我们已经创建了一个新的分支b。

- **git checkout -b [name]**:分支创建并跳转

  ```
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
  $ git checkout -b c
  Switched to a new branch 'c'
  
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (c)
  $ git branch
    a
    b
  * c
    master
  ```

  这里可以看到我们创建了一个新的分支c，跳转到了该分支。

- **git switch -c [name]**:

  这种方式是新的git命令，我可以通过这种方式来进行分支的创建和跳转。

  ```
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
  $ git switch -c a
  Switched to a new branch 'a'
  
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (a)
  
  ```

  可以看到我们运行了指令之后，直接跳转到了a分支之中。

##### 查看分支

查看 分支主要使用`branch`指令：

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (c)
$ git branch
  a
  b
* c
  master
```

通过该指令我们看到我们创建的分支，并且能看到所在的分支，在分支名字前带有`*`的就当前所在的分支

##### 切换分支

****

###### 切换分支的两种方式：

- **git  checkout [name]**:用于切换到指定的分支

  ```
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (c)
  $ git checkout master
  Switched to branch 'master'
  
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
  ```

- **git switch [name]**:用于切换到指定的分支,该方式是新的git命令，比checkout好理解一些

  ```
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
  $ git switch a
  Switched to branch 'a'
  
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (a)
  $ git switch master
  Switched to branch 'master'
  
  ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
  ```

##### 合并分支

**合并分支的意思是将当前分支和指定的分支合并，即将指定分支的内容全部加入当前分支。**

**git merge [name]**:合并某分支到当前分支

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git merge a
Already up to date.
```

当使用完这个命令之后，我们就可以将两个分支内的内容进行合并，a分支的内容就都会在master之内，在这个时候我们就可以删除掉分支a了，因为master内包含了分支a的所有内容。

###### 合并分支冲突

如过我们在分支2中修改了t文件中的内容并且进行提交，这个时候转回到分支1同样修改t文件，这个时候git就无法执行快速合并。

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git merge test
Auto-merging t.txt
CONFLICT (content): Merge conflict in t.txt
Automatic merge failed; fix conflicts and then commit the result.

```

这个时候我们可以查看t文件中的内容。

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1
```

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们需要修改之后在进行保存。

###### 查看分支合并情况

**$ git log --graph**

通过此代码可以查看分支合并的具体情况。

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$  git log --graph
*   commit 8b652405b9d5b3eb79ffdc89edf760d7ceface75 (HEAD -> master)
|\  Merge: 875b7cf 5866fdc
| | Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.com>
| | Date:   Thu May 12 20:46:49 2022 +0800
| |
| |     commit tow
| |
| * commit 5866fdc3b75566cf232e1daf8b24ccf994027e13
| | Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.noreply.github.com>
| | Date:   Thu May 12 20:37:06 2022 +0800
| |
| |     test commit
| |
* | commit 875b7cff87da2fda6c2435e12c406c78ea2452d5
|/  Author: ShaoLinSiDaShiXiong <104408139+ShaoLinSiDaShiXiong@users.norepl:...skipping...
*   commit 8b652405b9d5b3eb79ffdc89edf760d7ceface75 (HEAD -> master)
```



###### 使用--no-ff合并分支

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git merge --no-ff -m"--no--ff test" b
Merge made by the 'ort' strategy.
 t.txt | 1 +
 1 file changed, 1 insertion(+)

```

**查看合并分支过程：**

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git log --graph --pretty=oneline
*   c009aad977a956eb3e41c0e906d8b60c6f0cba81 (HEAD -> master) --no--ff test
|\
| * 21752251ed45530c29b2346a64b6571345b3279c (b) add +a in branch b
|/
*   8b652405b9d5b3eb79ffdc89edf760d7ceface75 commit tow
|\
| * 5866fdc3b75566cf232e1daf8b24ccf994027e13 test commit
* | 875b7cff87da2fda6c2435e12c406c78ea2452d5 masster branchi

```

**如果两个分支中的文件内容不一样那么就不可以通过这种方式进行合并。**

##### 删除分支

**git branch -d  [name]**:删除分支

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (bb)
$ git branch
  asd
  b
* bb
  master

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (bb)
$ git branch -d asd
Deleted branch asd (was 301f0c7).

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (bb)
$ git branch
  b
* bb
  master
```

当使用了该命令git就会删除指定的分支，和分支内的修改记录内容，但是该分支中创建的文件不会被删除。

这个时候我们也可以进入别的分支进行版本库状态的查看，然后进行文件的添加和提交。

**如果一个分支再进行删除的时候没有和其他分支进行合并，那么他的删除代码是这样的：**

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git branch -D b
Deleted branch b (was 7b425d8).
```

我们需要将`-d`换成大写的`-D`来进行强制删除。

##### 不小心删除分支恢复方法

如果不小心删除了分支，且分支内有些内容很重要且没有进行保存，想要进行恢复，首先需要需要查看最后一次提交内容的提交id。然后通过`git branch [new_branch_name] [commit_id]`来恢复分支

**具体操作如下：**

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 ~/Desktop/新建文件夹 (master)
$ ls
README.en.md  README.md  new.txt  test02.txt

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 ~/Desktop/新建文件夹 (master)
$ git branch
* master

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 ~/Desktop/新建文件夹 (master)
$ git reflog
efa41f6 (HEAD -> master, a/master) HEAD@{0}: checkout: moving from recover_branch_a to master
96a3d69 HEAD@{1}: commit: aasfsa
88cd9cf HEAD@{2}: checkout: moving from master to recover_branch_a
efa41f6 (HEAD -> master, a/master) HEAD@{3}: reset: moving to efa41f6
efa41f6 (HEAD -> master, a/master) HEAD@{4}: checkout: moving from a to master
7760d6b HEAD@{5}: reset: moving to HEAd^
88cd9cf HEAD@{6}: commit: a
7760d6b HEAD@{7}: merge v: Fast-forward
efa41f6 (HEAD -> master, a/master) HEAD@{8}: checkout: moving from v to a
7760d6b HEAD@{9}: checkout: moving from a to v
efa41f6 (HEAD -> master, a/master) HEAD@{10}: checkout: moving from v to a
7760d6b HEAD@{11}: commit: v
efa41f6 (HEAD -> master, a/master) HEAD@{12}: checkout: moving from a to v
efa41f6 (HEAD -> master, a/master) HEAD@{13}: checkout: moving from master to a
efa41f6 (HEAD -> master, a/master) HEAD@{14}: pull a master --allow-unrelated-histories: Merge made by the 'ort' strategy.
d357f15 HEAD@{15}: commit (initial): test02

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 ~/Desktop/新建文件夹 (master)
$ git branch a 96a3

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 ~/Desktop/新建文件夹 (master)
$ git branch
  a
* master

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 ~/Desktop/新建文件夹 (master)
$ git switch a
Switched to branch 'a'
g
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 ~/Desktop/新建文件夹 (a)
$ ls
README.en.md  README.md  aa  new.txt  test02.txt  v

```

可以看到我们的分支已经恢复了，且里面的内容也都在



****

##### bug分支

当我们在当前分支没有将工作做完时，突然又有一个额外的任务需要我们来进行处理，这个时候我们就可以将已经add的文件隐藏起来，然后创建新的分支来处理需要处理的文件。

**stash**

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   t.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   t.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        v


ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git stash
Saved working directory and index state WIP on master: 0a36cce test commit test
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git stash
Saved working directory and index state WIP on master: 0a36cce test commit test

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        v

nothing added to commit but untracked files present (use "git add" to track)

```

这个时候可以看到，没有提交的他。t.txt文件已经被隐藏起来了。

我们可以通过**`stash list`**指令来查看隐藏的内容。

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git stash list
stash@{0}: WIP on master: 0a36cce test commit test
g

```

当我们处理完了其他问题，想要将隐藏的内容拿出来也很简单。

一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；

另一种方式是用`git stash pop`，恢复的同时把stash内容也删了：

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git stash pop
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   t.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        v

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (1787c71eb5c33c2a3bd7adcc906b6b14dfbf482c)

```

###### 复制分支修改

很多时候我们并不需要将整个分支进行复制，我们可能只需要将一次提交操作进行复制。

为了方便操作，Git专门提供了一个`cherry-pick`命令，让我们能复制一个特定的提交到当前分支：

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ ls
t.txt
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ git cherry-pick 2aac8
[master 8e2ec9c]  branch c commit bug demo to demo
 Date: Fri May 13 10:00:09 2022 +0800
 1 file changed, 1 insertion(+)
 create mode 100644 demo.txt

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/get02 (master)
$ ls
demo.txt  t.txt
```

## 关联gitee仓库

通过`git remote add orgini`指令来关联gitee仓库

```
git remote add orgini [远程仓库地址]
```

##### 关联多个远程仓库

这里的orgini是我们设置的远程仓库的名，只要不重名，我们就可以自定义。

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/gitTest/aaa (c)
$ git remote add giteetest01 https://gitee.com/shaolinsidashixiong/test01

ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/gitTest/aaa (c)
$ git remote -v
giteetest01     https://gitee.com/shaolinsidashixiong/test01 (fetch)
giteetest01     https://gitee.com/shaolinsidashixiong/test01 (push)
origin  https://gitee.com/shaolinsidashixiong/aaa.git (fetch)
origin  https://gitee.com/shaolinsidashixiong/aaa.git (push)

```

这里可以看到我们关联了两个远程仓库分别是：

origin：https://gitee.com/shaolinsidashixiong/aaa.git 

giteetest01：https://gitee.com/shaolinsidashixiong/test01

两个仓库。

**需要注意的是，当我们连接了多个远程仓库的时候，使用push上传就变成了这样：**

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/gitTest/aaa (c)
$ git push giteetest01 c
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 391 bytes | 391.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Powered by GITEE.COM [GNK-6.3]
To https://gitee.com/shaolinsidashixiong/test01
   746468a..29f10ed  c -> c
```

**我们需要指定，究竟要上传到那个远程仓库的那个分支。**

###### 查看所有关联的远程仓库

需要查看所有关联的远程仓库需要使用`remote`+参数 `-v`：

```
ShaoLinSiDaShiXiong@DESKTOP-K8QB8FV MINGW64 /e/gitTest/aaa (c)
$ git remote -v
giteetest01     https://gitee.com/shaolinsidashixiong/test01 (fetch)
giteetest01     https://gitee.com/shaolinsidashixiong/test01 (push)
origin  https://gitee.com/shaolinsidashixiong/aaa.git (fetch)
origin  https://gitee.com/shaolinsidashixiong/aaa.git (push)

```

### 将本地仓库的分支内容添加到远程仓库

想要将本地仓库的分支内容关联到远程仓库，首先要将本地仓库和远程仓库进行连接。

之后使用 **`git push --set-upstream origin branch`**指令来进行上传。

- **origin：**指的是远程仓库的连接名。
- **branch：**是分支名，如果远程仓库中没有该分支，则会自动生成该分支。



## Eclipse使用git

一般新版的eclipse都集成自带git。

eclipse使用git首先需要进行最基本的配置。

![image-20220515210843296](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220515210843296.png)

这里的name可以自定义，邮箱填入自己的邮箱，通过 AddEntry...按钮进行添加。

### clone项目

从Gitee上或GitHub上clone项目很简单，首先需要调出git窗口。

![image-20220515213506278](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220515213506278.png)

![image-20220515213528533](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220515213528533.png)

将 Git Repositories Open之后，点击clone按钮。输入对应库的链接。                                                                                                                                                                                                                                               

****

## 将项目上传到远程仓库

新疆项目=》创建本地git仓库=》链接远程仓库=》通过pull将项目一致=》push

## git常用指令

| 指令                 | 作用                                                     |
| -------------------- | -------------------------------------------------------- |
| git status           | 查看当前版本库状态                                       |
| git diff [file]      | 查看文件都做出了那些修改                                 |
| git show [file]      | 查看文件都做出了那些修改                                 |
| git add [file]       | 将文件添加到缓存区                                       |
| git commit -m"  "    | 将文件提交到版本库中                                     |
| git push             | 将文件上传到远程版本库中                                 |
| git remote -v        | 查看当前版本库连接的所有远程仓库                         |
| git remote add       | 为当前版本库关联一个远程仓库，需要指定连接名和连接地址。 |
| git remote rm origin | 通过连接名来删除一个远程连接                             |
|                      |                                                          |

