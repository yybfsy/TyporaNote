## 第一章 Git 概述



### 1.1 版本控制系统简介

版本系统控制，是一种记录一个或若干个文件内容的变化，以便将来查询特定版本修改   的系统。版本控制系统不仅可以应用于软件源代码的文本文件，而且可以对任何类型的  文件进行版本控制。用的比较多的是svn，git等。

### 1.2 工作模式

版本控制系统的工作模式分为两种：集中式工作和分布式工作模式。

#### 1.2.1 集中式工作模式

![image-20211028191805782](https://gitee.com/yybovo/note-images/raw/master/Typora/git001.png)

为了让不同系统上的开发者能够协同工作，集中化的版本控制系统应运而生。这类系统都有一个单一的集中管理的服务器，保存所有的修订版本。而协同工作的人们都得通过客户端连接到这台服务，获取最新的文件或者提交更新。

集中式版本控制系统存在以下几个问题:

- 一 且服务器出现问题，所有的客户机将无法更新到最新版本,并且无法恢复到指定的版本。因为所有版本信息都在中央版本库中。
- 必须具有网络环境，单机无法实现版本控制。
- 客户机之间无法直接进行联系，无论中央版本服务器是否出现问题。CVS、SVN 都是集中式版本控制系统。

#### 1.2.2 分布式工作模式

![image-20211028192744288](https://gitee.com/yybovo/note-images/raw/master/Typora/git002.png)

分布式版本控制系统中无需集中版本库服务器,每台客户机都具有独立的版本控制功能，多台客户机之间相连就可以实现文件共享及版本管理。分布式工作模式的好处:无需网络环境也可以进行版本控制，在网络环境下可以实现协同工作。Git就是采用的分布式工作模式。

### 1.3 Git工作模式

Git工作模式包含：集中式工作模式、开源社区工作。

#### 1.3.1 集中式工作模式

![image-20211028191805782](https://gitee.com/yybovo/note-images/raw/master/Typora/git001.png)

Git为了便于客户机之间的协同工作，Git版本控制系统一 般会设置一 个中央版本库服务器，目的是让所有客户机都从该主机更新版本，提交最新版本。该工作模式下的客户机地位都平等。

#### 1.3.2 开源社区工作模式

![image-20211028195652149](https://gitee.com/yybovo/note-images/raw/master/Typora/git003.png)

对于开源软件开源社区的协作开发模式，不可能让所有人都具有修改中央版本库的限，让不同的客户机对中央版本库的不同操作权限，将有利于维护开源软件的安全性。

### 1.4 Git的工作流程

> - 初始化一个本地版本库，每个版本库仅需要执行一次。
> - 将中央版本库内容克隆到本地版本库，每个客户机仅需要执行一次。
> - 添加指定文件到版本控制管理(只是添加到暂存区)
> - 将修改操作操作到本地版本库(将暂存区的内容提交到本地版本库)
> - 将本地版本库中的修改内容“推送”到中央版本库，客户机需要在一阶段性工作完后或在某些时间点(下班，周五)将修改过的内容备份到中央版本库，方便他人更新最新的代码。
> - 将中央版本库中的变化内容“拉取”本地版本库，客户机需要不时的更新才可以获取最新的内容。

### 1.5 工作区和版本区

Git 存在两个特别重要的区域：工作区与版本区。而版本区又存在两个很重要的区域：暂存区与分支区。

![image-20211028202029827](https://gitee.com/yybovo/note-images/raw/master/Typora/git004.png)

工作区:存放着用户可编辑的文件本身。
暂存区:也称为stage或index,存放着对文件的快照。
分支区:该区域中可以包含很多分支，而每个分支都可以记录当前工作区中文件的快照。

### 1.6 Git的安装

- Git的下载

  需要去 Git 官网下载对应系统的软件了，下载地址为 [git-scm.com](https://git-scm.com/)或者[gitforwindows.org](http://gitforwindows.org/)
  `上面的 git-scm 是 Git 的官方，里面有不同系统不同平台的安装包和源代码，而 gitforwindows.org 里只有 windows 系统的安装包`

- Git的安装

  参考 https://blog.csdn.net/mukes/article/details/115693833?spm=1001.2014.3001.5506

### 1.7 注意事项

版本控制文件类型:对于版本控制系统，无论是cvs, SVN，GIT,都只 能控制文本文件，对二进行制文件是无法控制。不幸的是，微软的office文件都属于二进行制文件，不能使用版本系统进行控制。字符编码与记事本:建议使用编码UTF-8。

 C:\User\家蹲阿企 在Git Bash 中表示--> /c/Users/家蹲阿企

*一般推荐Notepad++ 和 EditPlus编辑（格式要改为UTF-8）*

### 1.8 Git初始化-创建本地版仓库

每个Git版本控制系统中的主机都可以包含若干个本地版本库，一般情况下一个本地版本库对应一个项目，用于对某个特定项目中的本地文件进行版本管理。其实，版本库就是一个目录，这个目录里的所有文件都可被Git管理起来，并且可以随时追踪和返回文件的特定历史。
本例首先在D:\Git Program下新建一个git目录，然后在其中再创建一个repositories 目录，其下将来可能会存在很多项目目录，每一个项目目录就是-一个本地版本库。例如，有一个P2P项目录。

<font color=red>目录中文件名最好不要有空格，如果有，命令使用该目录名时要用引号包括起来</font>

![](https://gitee.com/yybovo/note-images/raw/master/Typora/git005.png)

### 1.9 初始化版本库

- 首先进入本地版本库目录:D:\Git_Program\git\repositories\P2P, 打开Git Bash命令行窗口，然后通过Linux命令进入到本地版本库目录（先切换到d盘）

  -- `reset`或者`clear` 清屏

![image-20211029110924210](https://gitee.com/yybovo/note-images/raw/master/Typora/git006.png)

- 执行初始化命令：git init

  ![image-20211029111259114](https://gitee.com/yybovo/note-images/raw/master/Typora/git007.png)

​        后面显示（master）表示默认创建了master主分支。

### 1.10 .git隐藏目录

.git目录的作用

  初始化后的版本库增加了一个.git的隐藏目录（以点开头的是隐藏文件）

![image-20211029111707896](https://gitee.com/yybovo/note-images/raw/master/Typora/git008.png)



![image-20211029112504710](https://gitee.com/yybovo/note-images/raw/master/Typora/git009.png)

这个目录下包含了当前版本库正常工作所需要的所有内容:暂存区文件、版本记录文件、配置文件等。换句话说，如果你想从项目中删除Git 的版本控制，但又要保留项目原文件，那么只需要删除这个.git目录就可以了。这样，这个项目就与Git没有了任何关系。

### 1.11 创建用户

作为版本控制系统的客户端,每台客户机对版本库的所有提交操作都需要注明操作者身份，所以客户机首先需要进行自我身份的注册，即创建用户。Git 要求“用户名与Emai"这两样信息是必不可少的。
Git具有三种不同的创建方式，会产生三种不同作用域的用户。这三种创建方式的用户信息会写到三个不同的配置文件中。这三种用户的创建均要使用git config 命令，只不过使用的选项不同。
这三种创建方式的创建的用户作用域由大到小依次是:系统用户、全局用户与本地库用户。在多种用户都进行了创建的前提下，小范围的用户会覆盖大范围用户，即默认会以小范围用户操作Git。
系统用户:当前主机系统中所有用户均可使用的Git用户。
全局用户:当前主机系统的当前登录用户可以使用的Git用户。
本地库用户:只能对当前的本地版本库进行提交的Git用户。

- 系统用户 git config --system

  `git config --system user.name "kirito"`

  `git config --system user.email "kirito@163.com"`

  可以在任意目录下运行该创建命令。本例创建系统用户 kirito

![image-20211029115921501](https://gitee.com/yybovo/note-images/raw/master/Typora/git010.png)

​        用户注册信息会写到/mingw64/etc/gitconfig文件中（新版本转到了C:\Users\家蹲阿企）

​        cat：显示文件内容（-n 显示行号）

​        `cat /mingw64/etc/gitconfig`

> .gitconfig文件具体位置时的解决方法(我的是在C:\Users\家蹲阿企、.gitconfig)

>   直接在终端输入命令进入vim编辑：

>   git config --global --edit

>   使用强制保存命令:wq!即可解决权限不够的问题

​       `cat ./.gitconfig`

![image-20211029125820818](https://gitee.com/yybovo/note-images/raw/master/Typora/git012.png)

​        也可以通过

​        `git config --system --list`

![image-20211029122307366](https://gitee.com/yybovo/note-images/raw/master/Typora/git011.png)



- 全局用户 git config --global

  `git config --global user.name "yui"`

  `git config --global user.email "yui@163.com"`

  可以在任意目录下运行该创建命令。本例创建系统用户 yui

  ![image-20211029130433976](https://gitee.com/yybovo/note-images/raw/master/Typora/git013.png)

​        用户注册信息会写到当前用户目录下的.gitconfig文件中

​        `cat ./.gitconfig`

![image-20211029131006598](https://gitee.com/yybovo/note-images/raw/master/Typora/git014.png)

​        也可以通过命令查看配置信息

​        `git config --global --list`

![image-20211029131452026](https://gitee.com/yybovo/note-images/raw/master/Typora/git015.png)

- 本地用户

  <font color=red>只能在当前的本地库目录下运行该命令。</font>本例创建本地用户sakula

  `git config user.name "sakula"`

  `git config user.email "sakula@163.com"`

  ![image-20211029165750072](https://gitee.com/yybovo/note-images/raw/master/Typora/git016.png)

​        用户注册信息会写到当前版本目录下的.git目录的config文件中。

​        ![image-20211029170127141](https://gitee.com/yybovo/note-images/raw/master/Typora/git017.png)

​        通过以下命令可查看配置信息。通过显示的信息可以看到，user.name与user.email有三组值，**但后面的值会将前面的值覆盖，即起作用的将是最后一组值**。

​        `git config --list`

![image-20211029170633290](https://gitee.com/yybovo/note-images/raw/master/Typora/git018.png)

### 1.12 基本操作

- 新建文件夹

  在本地仓库中新建一个hello.html文件，文件内容为Hello Git World

  `echo "Hello Git World" > hello.html`

  ![image-20211029171544510](https://gitee.com/yybovo/note-images/raw/master/Typora/git019.png)

- 查看状态

  用于查看当前版本库的Git状态。

  `git status`

![image-20211029172515800](https://gitee.com/yybovo/note-images/raw/master/Typora/git020.png)

​        最后提示，没有任何文件被添加到提交，没有被跟踪的文件出现(使用git add 进行跟踪)。
​        该命令的作用是告诉Git系统，将指定文件的当前快照写入到版本库暂存区。即，将文件交给Git进行版本管理。

- 添加一个文件(暂存区)

  `git add`    `文件名`

  ![image-20211029173132605](https://gitee.com/yybovo/note-images/raw/master/Typora/git021.png)

​        警告:在hello.html文件中，LF 将被替换为CRLF。在工作目录中，文件将使用原始的行结束符。LF为Linux 下的换行符，而CRLF为Windows下的换行符。由于              文件创建于Linux 下，保存在Windows中，所以文件的行结束符使用的是Windowps下的CRLF.
​        此时再次查看Git状态，提示，尚未提交。

![image-20211029173441854](https://gitee.com/yybovo/note-images/raw/master/Typora/git022.png)

- 添加多个文件(暂存区)

  `git add`    `添加多个文件，文件之间使用空格分隔`

  ![image-20211029174442315](https://gitee.com/yybovo/note-images/raw/master/Typora/git023.png)

​        `git add`   `使用通配符*指定多个文件`

![image-20211029174835938](https://gitee.com/yybovo/note-images/raw/master/Typora/git024.png)

- 提交操作

  `git commint`

  提交操作通过命令将Git暂存区中的文件快照永久性的写入到本地仓库之中。

![image-20211029175717636](https://gitee.com/yybovo/note-images/raw/master/Typora/git025.png)

​        在提交时必须要通过选项 -m 给出一个操作提示信息
​        再来查看一个Git状态，提交是将暂存区的快照文件提交到本地仓库中

![image-20211029175852383](https://gitee.com/yybovo/note-images/raw/master/Typora/git026.png)

### 1.13 忽略文件



一般情况下工作区中的文件都是要交给Git管理的，但有些文件并不想交给Git管理。但是又由于该文件处于工作区，所以我们在执行git status 命令的时候会给出xx文件Untracked (未被跟踪)。我们想通过一 些设置让Git忽略这些文件，再运行git status 命令时不对其进行检测。只要在工作区创建一个文件，名称为.gitignore,把要被忽略的文件名写入到其中，然后将.gitignore文件add添加并提交commit到本地版本库即可。

- 新建一个要被忽略的文件

  在工作区随意新建一个文件，info.txt

  ![image-20211029180854873](https://gitee.com/yybovo/note-images/raw/master/Typora/git027.png)

- 查看Git状态

  通过命令 git status 查看Git状态 ，可以看到提示info.txt信息：该文件没有被跟踪

  ![image-20211029181203810](https://gitee.com/yybovo/note-images/raw/master/Typora/git028.png)

- 新建并提交.gitignore文件

  在工作目录下新建.gitignore文件，并将要被忽略的info.txt 文件名写入到其中，然后将.gitignore文件添加add并提交commit到本地版本库。

  ![image-20211029181706743](https://gitee.com/yybovo/note-images/raw/master/Typora/git029.png)

![image-20211029181921552](https://gitee.com/yybovo/note-images/raw/master/Typora/git030.png)

- 再次查看Git状态

  再次查看Git状态，可以看到已经没有info.txt 文件未被跟踪提示了，说明Git将该文件已经忽略了

  ![image-20211029182222464](https://gitee.com/yybovo/note-images/raw/master/Typora/git031.png)

### 1.14 查看区别：git diff

- 比较工作区与暂存区

  `git diff`

  查看工作区与缓存区内容的区别，使用无选项的git diff命令

  首先向hello.html文件中添加一行新的内容: one line，然后再查看区别: git diff hello.html

  *`>>`   表示在末尾追加*

  ![image-20211029201501022](https://gitee.com/yybovo/note-images/raw/master/Typora/git032.png)

​        其中 +one line 表示工作区中的内容比暂存区中的内容多出一行 one line
​        此时将hello.html文件添加到add到暂存区，再次来查看区别:没有任何输出，这就说明此时工作区中hello.html文件的内容与暂存区中hello.html文件的内容没有区别。

- 比较暂存区与本地库

  `git diff --cached`

  查看暂存区与本地库中的内容的区别，使用一个--cached选项的git diff命令。

  ![image-20211029202307649](https://gitee.com/yybovo/note-images/raw/master/Typora/git033.png)

​        其中 +one line 表示工作区中的内容比暂存区中的内容多出一行 one line
​        提交hello.html文件，再次查看暂存区中hello.html与本地库中hello.html中的内容的区别:发现没有任何内容的输出，说明暂存区与本地库内容一致。



### 1.15 撤销修改

对于己修改过的文件内容需要进行撤销，根据修改内容已经出现的位置可以分为三种情况:
1. 仅仅是工作区中内容进行了修改，还未添加add到暂存区。

2. 已经add添加到暂存区，但是还未commit提交到本地版本库。

3. 已经提交commit到本地版本库

  不同的情况具有不同的撒销方式。

- 仅在工作区中修改

  Git命令：`git checkout --` `文件名`

  如果仅在工作区中进行了修改，可以在文件中将内容直接复原即可。
  但是有时候修改内容较多，已经记不清修改过哪些地方，此时可以使用命令进行撤销。
  首先修改工作区中的文件内容，在hello.html文件中添加一行新内容: two line
  使用命令方式撤销之前的修改，然后再查看文件的内容，还原到之前

  ![image-20211029211115352](https://gitee.com/yybovo/note-images/raw/master/Typora/git034.png)

- 已在暂存区修改（只是退回到工作区）

  Git命令：`git reset HEAD` `文件名`

  如果对文件修改过的内容已经被add添加到暂存区，则有必要通过命令方式进行撤销。
  首先要在工作区中修改hello.html文件内容，新增一行内容: two line， 并将hello.html
  文件添加add到暂存区。再次查看git状态,然后使用git reset HEAD命令撤销(删除)指定文件在暂存区中
  的内容.

  ![image-20211029212336092](https://gitee.com/yybovo/note-images/raw/master/Typora/git035.png)

![image-20211029212617925](https://gitee.com/yybovo/note-images/raw/master/Typora/git036.png)

​        再次查看状态,提示:可以使用gitadd命令将修改过的内容添加到暂存区，也可以`git checkout --`命令将工作区中的文件修改撤销

![image-20211029212831798](https://gitee.com/yybovo/note-images/raw/master/Typora/git037.png)



### 1.16 回退到之前的版本

若修改过的文件，不仅add到了暂存区,还commit到了本地版本库,还能撤销吗?
已经是无法撤销修改了，但是可以回退到修改前的版本。

- 查看历史版本 

  `git log`

  如果要回退到之前的版本，首先我们得会查看版本库的历史版本。
  通过gitlog命令可以查看详细的历史版本信息。

  ![image-20211029214151642](https://gitee.com/yybovo/note-images/raw/master/Typora/git038.png)

​        每一个记录单元均由五行构成:
​        第1行: commit的id，由于Git是分布式版本控制系统，整个系统中存在有多个版本库,为了保证各个版本库中commit的id不重复，所有Git中的commit的id不是顺序递增的，而是与版本库主机的IP，版本库，提交者，提交时间相关的内容计算出来的一个值。
​        第2行:提交者的信息
​        第3行:提交的时间
​        第4行:分隔行，即空行。将前面所述基本信息与后面的修改日志内容进行分隔。
​        第5行:提交日志信息。

- 查看简单形式的日志

  `git log --pretty=oneline`

  通过命令，以单行形式简单展示历史记录信息

![image-20211029214628175](https://gitee.com/yybovo/note-images/raw/master/Typora/git039.png)

- 上面的commit-id显示的是全长度的id， 可以简写commit-id方式来显示，只需要添加--abbrev-commit选项即可。abbrev: 缩写，简写。

  `git log --pretty=oneilne --abbrev-commit`

![image-20211029215805315](https://gitee.com/yybovo/note-images/raw/master/Typora/git040.png)

- 翻页与退出
  当gitlog日志命令显示的内容太多，无法在一页内显示完毕所有内容时，其最后一行出现一个冒号，让输入命令。

  常用的命令有:
  回车:显示下一行
  空格:显示下一页
  q:退出git log命令

- HEAD指针

  Git会默认创建一个master分支，即主分支。这是Git对版本进行管理的唯一的一条时间线。在这条master时间线上有很多版本的时间节点，而HEAD指针则指向的是当前刚刚提交的版本时间节点。

  它可以通过`^`的数量来表示当前版本之前的版本，例如，HEAD`^`表示当前版本的前一个版本，HEAD`^^`表示前两个版本，但是之前的版本较多的时候，`^`的数量将不好数，此时可以使用`~`加数字表示当前版本之前的第几个版本。

![image-20211029220357377](https://gitee.com/yybovo/note-images/raw/master/Typora/git041.png)

- 查看可引用历史版本

  使用`git log`俞令只可以查看到HEAD指针及其之前的版本信息，如果版本发生回退，则可能会出现HEAD指针之后仍存在版本的情况，而这些版本信息通过`git log`命令是看不到的。所以我们就得使用`git reflog`可查看到所有历史版本信息。
  由于查看所有历史版本信息的目的大多是为了进行版本回退或恢复使用`commit-id`，所有该命令被命名为`reflog`,即引用`log`.

  ![image-20211030114858818](https://gitee.com/yybovo/note-images/raw/master/Typora/git042.png)

  查看所有历史版本，第一列为commit-id,但发现该`commit-id`并不完整，比`git log`查看的commit-id要短很多。这是commit-id的短格式，仅仅是长格式中的前七位。只要可以区分开commit-id,Git允许使用短格式。

  ![image-20211030114759280](https://gitee.com/yybovo/note-images/raw/master/Typora/git043.png)

### 1.17 版本回退

git reset命令可以实现版本回退，其有三个选项，可以完成三种不同效果的回退，
回退三种不同的Git状态。

- `git reset --soft` `回退的版本（例如HEAD^）`

  回退到指定版本。但仅仅修改分支中的HEAD指针的位置，不会改变工作区与暂存区中的文件的版本。实现上是改变了暂存区commit之前的状态。

  - 回退前
    首先在版本库中的hello.html 文件中添加“three line”的内容，并提交该内容。我们的目的就是要再回退到该版本。

    ![image-20211030121155647](https://gitee.com/yybovo/note-images/raw/master/Typora/git044.png)

​              对比工作区与缓存区、缓存区与版本区 发现内容相同并无差异。

- + 发生回退

    回退到前一个版本

    `git reset --soft` `回退的版本（例如HEAD^）`

    ![image-20211030122119093](https://gitee.com/yybovo/note-images/raw/master/Typora/git045.png)

    

  + 回退后

    再次对比工作区与暂存区、暂存区与本地库中版本的差异，发现工作区与暂存区内容没有差异，但是暂存区与本地库中的版本出现了差异:暂存区中的内容没有回退，但是本地库中的版本却回退到了之前的版本。

    ![image-20211030123428262](https://gitee.com/yybovo/note-images/raw/master/Typora/git046.png)

    既当前的Git状态为暂存区中的版本尚未提交状态。

    查看历史版本信息，可以发现已经看不到添加“three line”这个版本了。不过，“three line”这个版本仍然存在，通过`git reflog`可以查看到

    ![image-20211030123903255](https://gitee.com/yybovo/note-images/raw/master/Typora/git047.png)

  + 恢复到回退版本

    若要恢复到回退之前的版本，可以直接将暂存区中的数据commit提交即可。

- `git rest --mixed`  `回退的版本（例如HEAD^）`

  回退到指定版本。它不仅修改了分支中HEAD指针的位置，还将暂存区中数据也回退到了指定版本。但是工作区中的版本仍是回退前的版本。

  `--mixed`是`git reset`命令的默认选项

  - 首先添加一行“five line”到hello.html。现在要回退该版本

    ![image-20211030134318371](https://gitee.com/yybovo/note-images/raw/master/Typora/git048.png)

    对比工作区与缓存区、缓存区与版本区 发现内容相同并无差异。

  - 发生回退

    `git rest --mixed` `回退的版本（例如HEAD^）`

    ![image-20211030135438080](https://gitee.com/yybovo/note-images/raw/master/Typora/git049.png)

  - 回退后

    对工作区与暂存区，发现工作区与暂存区内容出现差异:工作区中的内容没有回退，但是暂存区中的版本回退到了之前的版本。再看看暂存区与本地库中的版本，发现内容没有差异，说明本地库中的版本也回退到了之前的版本。即当前的Git状态为工作区中的文件文件修改过后尚未进行add时的操作。

    ![image-20211030140220835](https://gitee.com/yybovo/note-images/raw/master/Typora/git050.png)

    不过，“five line”这个版本仍然存在，通过`git reflog`可以查看到

    ![image-20211030140510778](https://gitee.com/yybovo/note-images/raw/master/Typora/git051.png)

  - 恢复回退前的版本

    就本例而言，虽然可以通过先add再提交commit的方式就可以恢复回退前的版本，但若回退的版本是很多版本之前的版本，最好不要使用该方式，而是使用版本跳转命令的方式。首先要通过git reflog命令查看到要恢复的提交标识commit-id，<font color=red>cd61f77</font>.

- `git reset --hard` `回退的版本（例如HEAD^）`

  回退到指定版本。 该命令不仅修改了分支中HEAD指针的位置，还将工作区、暂存区和本地库中数据也回退到了指定的版本。

  - 回退前
    通过查看历史版本可以看出，前面刚刚向hello.html 文件中添加了一个新行，内容为“six line” 。现在要回退该版本。

    ![image-20211030141621672](https://gitee.com/yybovo/note-images/raw/master/Typora/git052.png)

    对比工作区与缓存区、缓存区与版本区 发现内容相同并无差异。

  - 发生回退

    `git reset --hard`  `回退的版本（例如HEAD^）`

    回退到前一个版本

    ![image-20211030142230357](https://gitee.com/yybovo/note-images/raw/master/Typora/git098.png)

  - 回退后

    对比工作区与缓存区、缓存区与版本区 发现内容相同并无差异。再查看:工作区中hello.html 文件的内容:发现之前的“6 Line” 内容消失了，工作区中的hello.html文件内容回退到之前的版本。

    ![image-20211030142840544](https://gitee.com/yybovo/note-images/raw/master/Typora/git053.png)

    不过，"six line”这个版本仍然是存在的，我们可以通过`git reflog`查看到。

    ![image-20211030143117094](https://gitee.com/yybovo/note-images/raw/master/Typora/git054.png)

  - 恢复到回退版本

    首先要通过`git reflog`命令查看要恢复的版本commit-id，本例为：<font color=red>47a180c</font>

    `git reset --hard` `cimmit-id`

    恢复后再查看历史版本

    ![image-20211030143610042](https://gitee.com/yybovo/note-images/raw/master/Typora/git055.png)

    查看工作区hello.html内容：已经完全恢复

### 1.18 删除文件

要删除文件，首先要清楚该文件所处的git状态。若要是该文件未被Git管理，在工作区直接进行删除即可。但是，若该文件已经经过多次add与commit操作后要文件要被删除，则我们就需要通过Git命令来操作。


- 搭建环境
  首先新创建一个文件test.html,然后将该文件add添加到暂存区，再commit提交到本地库。

  ![image-20211030144827225](https://gitee.com/yybovo/note-images/raw/master/Typora/git056.png)

- 查看暂存区文件列表 `git ls-files`

  ![image-20211030145210990](https://gitee.com/yybovo/note-images/raw/master/Typora/git057.png)

- 查看本地库文件列表 `git ls-files --with-tree=HEAD`

  <font color=red>该命令实际上查看的是主分支上当前`HEAD`指针所指向的时间点的文件列表。若查看上一时间点的文件列表，则可将`HEAD`替换为`HEAD^`。当前，也可以使用`HEAD~n.`</font>

  ![image-20211030145551649](https://gitee.com/yybovo/note-images/raw/master/Typora/git058.png)

- <font color=red>仅</font>删除暂存区中的指定文件(工作区和本地仓库都还存在) `git rm-cached` `文件名`

  文件命令*仅* 可以删除暂存区中的指定文件。

  ![image-20211030150016881](https://gitee.com/yybovo/note-images/raw/master/Typora/git059.png)

- 恢复被删除文件 `git reset HEAD` `文件名`

  此时，通过`git commit`命令可以将本地库中的文件文件也删除。暂存区与本地库中的指定文件均被删除后要恢复,最简单的方式就是再对该文件进行add和commit操作，该操作不再演示。这里主要演示的是如何恢复在暂存区删除的文件。

  ![image-20211030150634789](https://gitee.com/yybovo/note-images/raw/master/Typora/git060.png)

- 完全删除 `git rm` `文件名`

  所谓完全删除，指的是将工作区、暂存区和本地库中的指定文一次性均删除。

  查看工作区:该文件已经消失 查看暂存区:该文件已经消失查看本地库:该文件仍然存在。

  ![image-20211030151006424](https://gitee.com/yybovo/note-images/raw/master/Typora/git061.png)

​       若要将本地库中也删除，直接提交commit即可

![image-20211030151539152](https://gitee.com/yybovo/note-images/raw/master/Typora/git099.png)

- 恢复被删除的文件 `git reset --haed` `commitid`

  使用版本回退命令，将版本回退到删除之前的版本即可。
  首先要查看要恢复的版本的commit-id.

  ![image-20211030151942202](https://gitee.com/yybovo/note-images/raw/master/Typora/git062.png)

  回退到该版本：<font color=red>e098a86</font>

  再次查看工作区、暂存区和本地库：均已恢复了文件

  ![image-20211030152341909](https://gitee.com/yybovo/note-images/raw/master/Typora/git063.png)


### 1.19 Git 分支理论

#### 1.19.1 Git 主干

![image-20211030154722001](https://gitee.com/yybovo/note-images/raw/master/Typora/git064.png)

Git是以时间为主线对版本进行管理的，而这条时间主线就是Git主干。主干上的每一个节点就是一个版本，即一次commit提交。在主干上可以定义多个指针，指向不同的节点。Git默认会创建一个名称为master的指针。默认情况下用户操作的是master指针，但用户通过命令对操作的指针进行切换。用户每次提交一次， 就会形成一个新的节点，当前操作的指针就会向前移动一次。

#### 1.19.2 Git 分支

![image-20211030160346688](https://gitee.com/yybovo/note-images/raw/master/Typora/git065.png)

为了更加形象的描述指针的移动轨迹，我们称某一个指针的移动轨迹为一个分支。这样的话，一个指针就代表了一个分支，可以使用不同的指针操作不同的分支。Master指针的移动轨迹与Git 的主干是重合，所以称为master主分支。

Git中还有一个特殊的指针叫HEAD,代表当前版本。其总是指向当前分支的当前版本，即总是指向当前分支指针所指向的节点(版本)。Git创建一个分支是很快， 例如，创建一个新的分支dev，就是创建一个 dev指针。而分支的切换就是修改HEAD指针的指向。一旦切换到另外一个分支dev，那再往向的
提交commit都是提交到新分支dev上了，即dev指针向后移动，但是master指针是不动的。
当前，在多分支下，可以在各个分支间任意切换，切换后均可进行各自的提交，而各自的提交与其它分支是无关的。

#### 1.19.3 分支合并

![image-20211030161831796](https://gitee.com/yybovo/note-images/raw/master/Typora/git066.png)

当前dev分支上的工作完成后，需要将其合并到主分支master上。合并过程其实很快，只需要将master指针指向dev指针指向的节点,然后再将HEAD指针指向maste指针指向的节点即可。即分支的合并就是修改了两个指针的指向而己。
对于合并的较形象的理解是，合并就是将原来在dev 分支上的节点，全部投射到master分支上，即全部合并到master分支上。

#### 1.19.4 合并后的删除

![image-20211030163051753](https://gitee.com/yybovo/note-images/raw/master/Typora/git067.png)

将dev分支合并到master分支修改的仅仅是master与HEAD指针，而dev指针并未修改。即仅仅是将dev上的节点投射到master分支上，并未将master分支上的节点投射到dev分支上。所以合并后，dev 分支中的节点会少于master分支上的节点，即dev分支上的文件版本低于master分支的。
例如上 图中的最后一个紫色的节点，其为master分支上的节点，表示master分支修改并提交了某文件，但dev分支上并未修改该文件，所以合并后dev分支的该文件版本低于master分支上该文件的版本。合并后的dev分支不仅无用，它的存在还会引起不必要的麻烦，所有合并后一般会将dev分支删除，即将dex指针删除。

### 1.20 分支基本操作

- 创建并切换分支 `git checkout -b` `分支名称`

  命令：创建并切换到dev分支：`git checkout -b dev`

  ![image-20211030200212620](https://gitee.com/yybovo/note-images/raw/master/Typora/git068.png)

  该命令等价于两条命令: 
  `git branch dev` `分支名称`:新建分支dev
  `git checkout dev` `分支名称`:切换到分支dev

  ![image-20211030200458454](https://gitee.com/yybovo/note-images/raw/master/Typora/git069.png)

- 查看系统分支

  `git branch`

  ![image-20211030200717609](https://gitee.com/yybovo/note-images/raw/master/Typora/git070.png)

  该命令会列出当前系统中存在的所有分支，且当前分支前会显示*。

- 切换分支

  `git checkout 分支名称`

  ![image-20211030201033734](https://gitee.com/yybovo/note-images/raw/master/Typora/git071.png)

- 删除分支

  `git branch -d 分支名称`

  <font color=red>若要删除某分支，必须保证当前分支不能是要被删除的分支</font>

  ![image-20211030201637075](https://gitee.com/yybovo/note-images/raw/master/Typora/git072.png)

- 合并分支

  `git merge 要被合并的分支名称`

  对于分支的合并需要注意，如果要将分支B合并到分支A上，首先要将当前分支切换到A分支上，然后再运行合并命令。
  下面演示合并过程:
  当前处理dev分支，在该分支下为hello.html文件添加一行新内容7Line.然后add添加并commit提交，此时commit到的是dev分支，而非master分支。
  查看dev和master分支中的hello.html文件内容

  ![image-20211030202647063](https://gitee.com/yybovo/note-images/raw/master/Typora/git073.png)

  将dev分支合并到master分支。必须确保当前是master分支。

  ![image-20211030203504437](https://gitee.com/yybovo/note-images/raw/master/Typora/git074.png)

### 1.21 分支合并与冲突

Git的冲突检测单位是文件，即当不同分支对同一个文件进行修改后进行合并，就会产生冲突。

这是与SVN不同的。SVN检测冲突是文件中的列，什么意思?
若两个分支修改的不是同一个文件，合并时肯定不会产生冲突;但若修改的是同一个文件上的不同行的内容，合并时也不会产生冲突:若修改的是同一个文件上同一行上的不同列，在合并的时候也不会产生冲突。只有两个分支修改的是同一个文件同一行中同列数据的时候，在合并时才会产生冲突。

- 产生冲突的合并

  - 查看master 与 dev 分支下的hello.html文件内容：两文件内容一致

    ![image-20211030204536512](https://gitee.com/yybovo/note-images/raw/master/Typora/git075.png)

  - 修改dev分支下的文件

    在dev分支下使用vim编辑器修改hello.html文件,将第二行的"two line”改为“222line然后添加add并提交commit.

    vim 基本命令语法

    `i`--修改

    `esc` --退出修改

    `:wq!` --保存并退出

    ![image-20211030205643441](https://gitee.com/yybovo/note-images/raw/master/Typora/git076.png)

  - 修改master分支下的文件

    在master分支下使用vim编辑器修改hello.html文件，将第三行“three line""改为“333line然后添加add并提交commit。

    ![image-20211031123904589](https://gitee.com/yybovo/note-images/raw/master/Typora/git100.png)

  - 合并后出现冲突

    由于dev分支下修改的结果是，第二行内容为“222 line”,第三行内容为“three Line”。Master分支修改结果是，第二行内容为“two Line”,第三行内容为“333 line” 。

    合并后到底第二行和第三行内容应该是什么?
    这就是冲突。冲突将导致合并失败。

    ![image-20211030210632871](https://gitee.com/yybovo/note-images/raw/master/Typora/git077.png)

    hello.html中的合并冲突自动合并失败；修复冲突，然后提交结果

  - 查看git状态：给出合并没成功的提示

    ![image-20211030211216463](https://gitee.com/yybovo/note-images/raw/master/Typora/git078.png)

    =======  为冲突内容分隔线
    <<<<<< HEAD  到分隔线的内容表示 : 当前分支中的内容
    分隔线到>>>>>  dev 的内容表示 : 合并来的dev分支的内容

  - 解决冲突

    解决冲突的方法就是手工修改冲突内容，然后 add 添加并 commit 提交。内容可以任意修改，例如本例是将修改内容合了一行。

    ![image-20211030212406352](https://gitee.com/yybovo/note-images/raw/master/Typora/git079.png)

  - 查看冲突解决后两分支文件内容

    需要注意，冲突解决后提交的最终版本，即合并后的版本，仅仅是master分支中的版本，dev分支中的版本仍然是合并前的版本。即对于解决冲突后的master中的版本要超前dev中的版本。
    由于合并的本意是将dev分支上完成或阶段性完成的工作提交到master 分支中，分支的工作就暂告一个段落。后面dev分支上的工作再开始时，要与master分支的内容保持一致，从master 分支内容开始，所以一般在合并后，会立即将dev分支删除。再开始重新创建dev分支。
    查看master分支中的版本，为解决冲突后合并的最终版本。

    切换到dev分支，查看hello.html文件内容：查看到的版本为合并前的版本。

    ![image-20211030213907590](https://gitee.com/yybovo/note-images/raw/master/Typora/git080.png)

  - 查看历史版本中的合并显示

    以最普通的方式查看历史版本，并体现不出合并的发生

    ![image-20211030214424509](https://gitee.com/yybovo/note-images/raw/master/Typora/git081.png)

    可以在命令后添加`- -graph`选项，以图形化的形式显示出合并的出现。可以看出该文件发生过两次合并。

    ![image-20211030214646218](https://gitee.com/yybovo/note-images/raw/master/Typora/git082.png)

  - 删除dev分支

    首先切换到master分支，再删除dev分支

    ![image-20211030214834099](https://gitee.com/yybovo/note-images/raw/master/Typora/git083.png)



## 第二章 Git远程版本库概述



为了方便团队协作，Git 一般会使用中央版本库。相对于本地版本库而言，中央版本库都在其它主机上，我们一般称中央版本库为远程版本库。常用的远程版本库有：GitHub，码云Gitee。

### 2.1 Github简介

GitHub是一个面向开源及私有软件项目的托管平台，因为平台只支持Git作为唯一的版本库格式进行托管，故名为GitHub。Hub：中心，所以Git Hub，即Git中心。

### 2.2 Github 的注册与登录

参考：https://blog.csdn.net/caoli201314/article/details/106970408

### 2.3 免密登录原理

Git的本地仓库要不时的从GitHub上接取数据及向GitHub推送数据，但每次都要通过帐号与密码的身份验证才可访问，非常麻烦。所以我们要设置免密登录，使用Git 的本地版本库可以免密登录并访问GitHub。

#### 2.3.1 免密登录机制

Git主机间的通信采用的是SSH协议，即Sercure Shell 协议。该协议的免密登录机制要求主机之间采用SSH-key即SSH密钥进行身份验证。SSH密钥包含“公钥与私钥”，所以我们首先要了解什么是“公钥与私钥”，然后还要理解“公钥与私钥”在免密登录中的作用，即免密登录的工作原理。

- 公钥与私钥 
  对与公钥与私钥要了解以下三点:
  “公钥与私钥加密”是一种“不对称的加密文式”，是传统的“对称加密方式”的功能的增强。最常见的对称加密方式是:用户名密码方式。
  公钥与私钥是成对的，即一个公钥对应一个私钥。使用公钥加密后，只能使用私钥进行解密。
  公钥与私钥的关系:就好比“锁与钥匙”的关系。公钥相当于“锁”，锁是可以被他人看到的，是要发送给别人的，所以称为公钥:私钥相当于“钥匙”，它是不能公开的，只能有公钥发出者保存。

- 免密码登录的工作原理
  免密登录在Master/Slave主从集群中使用较多，且多用于Master主机免密登录访问slave主机，所以对于免密登录原理的分析就以Master/Slave为例。
  对于免密登录的机制，主要由两部分构成：构建与验证。

  ![image-20211030223923069](https://gitee.com/yybovo/note-images/raw/master/Typora/git084.png)

  免密登录构建:
  Master生成一对密钥: 公钥与私钥，保存到Master本地。
  Master将公然及用户信息(用户名，密码等)发送给Slave,并将公钥及用户信息保存到slave本地。

  免密登录验证:
  Master向Slave发送连接请求，包含Master的用户信息。
  Slave从本地文件中查找是否存在连接中包含的用户信息。若不存在：则拒绝访问，若存在：可以访问。
  Slave将加密后的随机字符串发送给Master。
  Master将加密后的附页字符串使用私钥进行解密。
  Master将解密后的字符串给发送给slave。
  Slave将接收到的字符串与本地未加密的字符串进行比较，相同则可以访 问，不同则被拒绝。

### 2.4 设置本地库对GitHub的免密登录

此时我们要设置本地库免密登录GitHub， 即这里的本地版本库相当于前面的Master,而GitHub则相当于slave。所以，密钥对应由本地版本版本库生成，而GitHub
中只需要保存公钥即可。

#### 2.4.1 本地库主机的设置

- 查看密钥文件
  由于生成的密钥存放在本地版本库主机的当前用户主目录下的隐藏目录.ssh下面两个隐藏文件中，这两个文件分别是 id_sra 与  id_sra.pub。 其中 id_sra 中存放的是私钥，id_sra.pub 中存放的是公钥。所以生成密钥前首先要看本地版本库主机的当前用户主目录，确认有没有.ssh目录。

  ![image-20211030225509288](https://gitee.com/yybovo/note-images/raw/master/Typora/git085.png)

- 本地库生成密钥

  在本地版本库主机运行 `ssh-keygen`命令，生成SSH密钥

  ![image-20211030225933677](https://gitee.com/yybovo/note-images/raw/master/Typora/git086.png)

- 再次查看密钥文件

  再次查看本地版本库主机的当前用户主目录时，发现已经生成了.ssh目录，查看该目录其下也生成了 id_rsa 与 id_rsa.pub 文件。说明SSH密钥生成成功。

  ![image-20211030230125139](https://gitee.com/yybovo/note-images/raw/master/Typora/git087.png)

#### 2.4.2 GitHub设置

登录GitHub官网，打开setting设置页面

- 打开公钥填写界面

  ![image-20211030230543516](https://gitee.com/yybovo/note-images/raw/master/Typora/git088.png)

  ![image-20211030230742549](https://gitee.com/yybovo/note-images/raw/master/Typora/git089.png)

  ![image-20211030230855097](https://gitee.com/yybovo/note-images/raw/master/Typora/git090.png)

- 复制公钥

  在本地库打开当前用户目录下的 .ssh/.id_rsa.pub 文件，将公钥进行复制。

  ![image-20211030231159456](https://gitee.com/yybovo/note-images/raw/master/Typora/git091.png)

- 填写公钥

  ![image-20211030231529785](https://gitee.com/yybovo/note-images/raw/master/Typora/git092.png)

  在Title 中要填入该key的名称，可以随意定义。例如，这是我使用主机上的Git要连接该GitHub,所以可以命名为Y7000P2019。将复制好的公钥粘贴到key文本框中。点击Add SSH key后，即可看到GitHub中存放到手公钥信息。

  ![image-20211030231801013](https://gitee.com/yybovo/note-images/raw/master/Typora/git093.png)


### 2.5 创建GitHub远程空的版本库

- 打开创建库页面

  登录GitHub官网，打开New repository页面

  ![image-20211030232216605](https://gitee.com/yybovo/note-images/raw/master/Typora/git094.png)

- 填写创建库的表单

  仅填入远程版本库名称即可Create repository， 其它保持默认。为了便于记忆，一般情况下远程版本库名称与本地版本库名称设置相同。

  ![image-20211030232759159](https://gitee.com/yybovo/note-images/raw/master/Typora/git095.png)

- 进入空版本库页面

  点击 create repository 后，即可进入远程版本库页面。远程版本库创建好之后，默认Git间的连接采用的是Https协议。较之SSH 协议，HTTPS 协议数据传输速度慢，且无法实现免密登录,即每次连接均需要输入用户名和密码，所以生产环境下一般采用的是SSH协议。所以首先要点击SSH,其后显示的就是远程版本库的访问地址。

  ![image-20211030233046494](https://gitee.com/yybovo/note-images/raw/master/Typora/git096.png)

  远程版本库创建好之后，由于版本库仍然为空的，所以GitHub给出了三条建议:
  1.使用命令行创建一个新的仓库。即删除这个空的版本库再创建一个新的版本库。
  2.使用命令行推送一个新的仓库。即将本地版本库的内容push到远程版本库。
  3.从其它版本库中导入代码。

  ![image-20211030233453257](https://gitee.com/yybovo/note-images/raw/master/Typora/git097.png)

  

### 2.6 本地仓库内容push到远程仓库

#### 2.6.1 命令解析

我们使用上面第二点建议，从本地库中推送己存在的版本库内容。
只需要本地库中运行给出的两条命令即可。

> ```
> git remote add origin git@github.com:yybfsy/P2P.git
> //git branch -M main  //修改master分支名为main（与黑人有关）
> git push -u origin master //main
> ```

- `git remote add`命令的意思是：为指定一个远程版本库命名一个本地名称。 这里的远程版本库为`git@github.com:yybfsy/P2P.git`，为其起的本地名称为origin，即起源。其中远程版本库的`git@`表示以git用户访问，而仓库的具体地址为`github.com`主机中的`yybfsy`目录下的`P2P.git`. 远程版本库目录一般以`.git`结尾。
- `git push`命令用法:
  - `git push origin master`：将本地版本库中master分支推送到origin远程库。
  - `git push origin`：将本地版本库中当前分支推送到origin远程版本库。
  - `git push -u origin`：将本地版本库master 分支推送到origin 远程版本库，并将origin设置为默认的远程库，即以后所有git push就不用再指定远程版本库了。
  - `git push`：将本地版本库中当前分支推送到默认远程片库。

#### 2.6.2 命令执行

在 Git Bash 的本地版本库目录中远程输入以上两条命令。在第一次连接GitHub时本地库的 Git 系统会给出提示，GitHub 站点主机的真实性不能确定，RSA 密钥指纹是 xxx,你确定要连接吗?输入 yes。 然后再给出一个警告，永久性的添加GitHub站点到已知主机列表。以后再连接就不会出现该警告。

![image-20211031151008051](https://gitee.com/yybovo/note-images/raw/master/Typora/git101.png)

#### 2.6.3 查看结果

![image-20211031151241094](https://gitee.com/yybovo/note-images/raw/master/Typora/git102.png)

### 2.7 从远程库clone到本地库

- 创建本地存放目录

  在要克隆远程版本库的本地库主机中创建要存放本地库的目录。本例在D盘的Git_Program目录下创建git2/repositories目录，将来用于克隆远程版本库的P2P版本库。注意，P2P版本库目录不用创建，它分从远程库中克隆出来。

- 复制远程库地址

  打开并登录到GitHub，在登录之后可以看到远程仓库，选择我们要克隆的仓库，选中之后:

  ![image-20211031152850302](https://gitee.com/yybovo/note-images/raw/master/Typora/git103.png)

- 运行克隆命令

  在本地库主机运行 Git Bash 命令，首先进入到将要存放的本地库的D:\Git_Program\git2\repositories目录，然后运行克隆命令。

  `git clone` `远程版本库地址`

  ![image-20211031153355007](https://gitee.com/yybovo/note-images/raw/master/Typora/git104.png)

  命令运行完毕，在当前目录下就会出现克隆自GitHub版本库，即本地库。

### 2.8 从远程库pull内容到本地库

- git2 修改内容后commit

  首先要进入到Git的本库版本库目录中，然后插入一行新的内容在hello.html，最后再将修改的内容add与commit提交到本地版本库。

  ![image-20211031154359596](https://gitee.com/yybovo/note-images/raw/master/Typora/git105.png)

- git 将修改的内容 push 到远程库

  git 直接运行 `git push` 命令

  ![image-20211031154625447](https://gitee.com/yybovo/note-images/raw/master/Typora/git106.png)

  但是，需要注意的是：git2 与 git 不是同一台主机，这里运行的命令应该是以下两条命令。
  `git remote add origin git@ github.com:yybfsy/P2P.git`
  `git push -u origin master`
  由于 git2 与 git 是同一台主机模拟的，无需也不能再为该远程版本库再指定本地名称了，也无需再指定git push命令的默认远程库了。

- git2 从远程库 pull 到本地库

  首先进入到 git2 的本地版本库目录，然后直接运行`git pull`命令。

  ![image-20211031155607118](https://gitee.com/yybovo/note-images/raw/master/Typora/git107.png)

  运行该命令的前提同样是前面指定过默认远程库。本例指定的默认的远程库为origin该命令等价于`git pull origin master`
  `git pull`命令常见的用法:

  - `git pull origin master`：将远程库origin的master分支拉取到本地库与本库库的master分支合并。
  - `git pull origin dev`：将远程库origin的master分支拉取到本地并与本的dev分支合并。
  - `git pull`：从默认远程库的拉取本地库当前分支内容，并与本地库当前分支合并。

### 2.9 查看本地的远程库信息

`git reomote`：该命令可列举出当前本地版本库可操作的远程版本库名称

![image-20211031160343081](https://gitee.com/yybovo/note-images/raw/master/Typora/git108.png)

`git remote -v`：该命令可以显示出更为详细的信息，远程库地址及本地库可执行的操作权限。

![image-20211031160523652](https://gitee.com/yybovo/note-images/raw/master/Typora/git109.png)

### 2.10 删除本地的远程库信息

`git remote rm` `远程库名称`

![image-20211031160727120](https://gitee.com/yybovo/note-images/raw/master/Typora/git110.png)

### 2.11 Git Hub删除已有库

首先登录GitHub，进入到当前要删除的库页面，点击setting选项卡

![image-20211031161838113](https://gitee.com/yybovo/note-images/raw/master/Typora/git111.png)

在该选项卡页面最下有删除

![image-20211031162033714](https://gitee.com/yybovo/note-images/raw/master/Typora/git112.png)

为了确定没有删错，系统让再删入要删除库的名称

![image-20211031162213344](https://gitee.com/yybovo/note-images/raw/master/Typora/git113.png)

### 2.12 版本发行

现代的开发多采用敏捷开发模式，该开发模式可以应需求的快速变化，可以频繁交付新的软件版本，其采用迭代方式逐步完善软件功能。当开发出新的版本生如何进行发布? 
Git 中软件的发行，是通过标签完成的。

- 什么是标签

  一个软件的某个发行版本对应的其实就是软件开发过程中其一阶段的最后一 次`git commit`提交。我们知道每-一个 git 提交，对应的都会有一个 commit-id ,而标签就是与某一个 commit-id 绑定的名称。一个标签一旦与某一个 commit-id 绑定，那么该标签就不能修改绑定到其它commit-id了，除非将该标签删除后才可以与其它commit-id绑定。

- 定义标签

  Git中的标签分为两种：轻量标签与附注标签。

  - 定义轻量标签
    修改hello.html文件，添加一行内容“8Line”，然后add操作，再commit提交。

    ![image-20211031163531925](https://gitee.com/yybovo/note-images/raw/master/Typora/git114.png)

    定义轻量标签刚刚提交的版本为5.0。

    `git tag` `版本` `commit-id`

    ![image-20211031163712778](https://gitee.com/yybovo/note-images/raw/master/Typora/git115.png)

  - 定义附注标签

    轻量标签只有标签名称，而使用附注标签，还可以为标签添加说明。

    ![image-20211031163948524](https://gitee.com/yybovo/note-images/raw/master/Typora/git116.png)

    `-a` 选项：指定标签名称

    `-m` 选项：设置标签说明

- 查看标签

  查看标签命令有两个,一个是查看当前系统下的所有标签，一个是查看指定标签的详情。

  - 查看所有标签 `git tag`

    该命令是查看当前系统下的所有标签，标签的输出顺序不是时间顺序，而是字母顺序。

    ![image-20211031164311814](https://gitee.com/yybovo/note-images/raw/master/Typora/git117.png)

  - 查看标签的详情 `git show` `标签名称`

    具有说明的标签，同时也会将说明显示，没有说明的，无显示。

    ![image-20211031164634529](https://gitee.com/yybovo/note-images/raw/master/Typora/git118.png)

- 修改指定版本的代码

  软件版本一旦被指定， 即标签一旦与某一 commit-id 绑定，那么这个版本的代码还能修改吗?
  若将 master 回退到该 commit-id ，然后再修改代码，修改完成后再 commit ,我们会发现代码修改过了，但该标签绑定的 commit id 并没有发生变化，即该软件版本的代码仍未修改。当然，此时我们可以将该标签删除，然后再定义一个同名标签与修改过代码的 commit-id 绑定。这样也是可以的。
  但是这里存在一个巨大的风险，我们修改过的代码是 master 主分支上的，一且修改过的代码出现问题，将可以导致整个代码出问题。所以，我们一般不会修改master主分支上的代码。
  那应该怎么办? 
  Git 将标签定义为了与分支同级别的概念，它不仅驻是一个 commit-id 的别名。Git 允许程序员使用分支切换命令`git checkout`将代码转向标签所指定的版本。

  ![image-20211031165814403](https://gitee.com/yybovo/note-images/raw/master/Typora/git119.png)

  命令执行完毕，系统给出了很多的提示，该提示的总体意思为:当前处于“游离”状态，在该状态下用户的任何修改与提交对任何的分支都没有影响(言外之意是：其修改将不会被保留)。若保留修改，则可以通过git checkout-b命令创建一个 新的分支。

  ![image-20211031165936301](https://gitee.com/yybovo/note-images/raw/master/Typora/git120.png)

  在该新分支上再进行修改提交，然后再合并到master分支，最后再将该分支删除。此时创建的分支名称可以随意。当前，合并到master 分支后，仍需要删除原标签，然后再与新的 commit-id 绑定。不过，生产环境下，一旦标签定义完成就不会与删除再绑定了。而是会再定义一个新的标签与新的 commit-id 绑定。

- 推送标签到远程库

  前面定义的版本仅仅是定义在本地库，其最终需要推送到远程版本库作为一个发行版本出现。可以通过以下两种方式:

  - 推荐指定标签 `git push origin v4.0`

    ![image-20211031170605072](https://gitee.com/yybovo/note-images/raw/master/Typora/git121.png)

  - 推送所有标签 `git push origin --tags`

    ![image-20211031170807594](https://gitee.com/yybovo/note-images/raw/master/Typora/git122.png)

  - GitHub查看推送结果

    登录GitHub并打开远程版本库页面，在 release 中可以看到推送到远程库中的标签，即发行版本。

    ![image-20211031171047741](https://gitee.com/yybovo/note-images/raw/master/Typora/git123.png)

    ![image-20211031171158143](https://gitee.com/yybovo/note-images/raw/master/Typora/git124.png)

    其他用户在更新本地版本库时，会将标签一并更新， 然后可以指定标签版本作为一个新的分支进行编辑，编辑完成后再合并到master，最后将该分支删除。

- 删除标签

  - 删除本地标签：`git tag -d v4.0`

    ![image-20211031171736562](https://gitee.com/yybovo/note-images/raw/master/Typora/git125.png)

  - 删除远程标签：`git push origin:refs/tags/v4.0`

    <font color=red>若要删除远程库中的标签，首先要删除本地库中的该标签，然后再运行如下命令</font>

    ![image-20211031172105032](https://gitee.com/yybovo/note-images/raw/master/Typora/git126.png)

    ![image-20211031172151841](https://gitee.com/yybovo/note-images/raw/master/Typora/git127.png)

## 第三章 码云 Gitee 远程版本库



码云官网 ：htpp://gitee.com

### 3.1 免密登录设置

登录后，点击页面右上角的头像，在淡出的下拉菜单中点击"设置"

![image-20211031205016343](https://gitee.com/yybovo/note-images/raw/master/Typora/git128.png)

在“设置”页面中左侧栏目中点击“SSH 公钥”，即可看到填写公钥的表单。
与GitHub中的设置相似，在“标题”中要填入该Key的名称，可以随意定义，例如，这是张三在公司使用主机上的Git要连接该Gitee,所以可以命名为zhangsanCompany.
公钥同样来自于本地版本版本库主机的当前用户目录下的 .ssh/id_ rsa.pub 文件。把它的内容复制到公钥文本框中。

![image-20211031205526940](https://gitee.com/yybovo/note-images/raw/master/Typora/git130.png)

点击"确定"后，又弹出权限验证对话框，只需要输入当前用户登录时的密码即可。

![image-20211031205801453](https://gitee.com/yybovo/note-images/raw/master/Typora/git131.png)

点击验证即可

### 3.2 创建码云空版本库

登录之后，点击页面右上角的+号，在弹出的菜单项目中点击“新建仓库”。

在“新建仓库”页面，只需要填写名称及完成项目的路径，其他保持默认设置。然后点击“创建”按键。

其它push、pull、clone 操作，与使用GitHub完全相同。

如果是最新版的git的话，是因为git官方目前取消了ssh旧版本协议支持。大家用http协议就能用了（克隆仓库中选择http的）同时给项目所在的仓库换成http源的就解决了
