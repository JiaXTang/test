## 本地仓库上传到GitHub上的具体步骤
![image](https://user-images.githubusercontent.com/110010605/187809650-c56c6d3e-b035-4ca9-ad87-a320a26439dd.png)

## git 和 GitHub 之间怎么合作？

**git是一个代码版本控制工具。运行在本地，帮你控制版本。**

**github是一个程序员用程序交流网站。** 

他俩的关系：可以借助git工具把本地代码上传到GitHub这个网站上，一方面可以帮你在线管理代码，另一方面可以开源代码来合作开发。

## 1、创建新仓库

创建一个新文件夹，打开，然后执行：

~~~C++
git init
~~~

可以创建一个新的git仓库

## 2、和远程仓库互通

执行以下命令可以创建一个远程仓库的本地的克隆版：

~~~C++
git clone /path/to/repository
~~~

如果是远程服务器上的仓库，使用以下命令：

~~~C++
git clone username@host:/path/to/repository
~~~

使用命令：

~~~C++
git clone https://github.com/JiaXTang/test.git/
~~~

会报以下错误：

~~~C++
fatal: unable to access 'https://github.com/JiaXTang/test.git/': Failed to connect to github.com port 443: Timed out
或者
fatal: unable to access 'https://github.com/JiaXTang/test.git/': OpenSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443
~~~

那是因为git在拉取代码或者提交项目的时候，中间会有git的http和https代理，但是我们本地环境本身就有SSL协议了，所以取消git的https和http代理就行.

解决办法:取消git的https代理，使用本机的代理，命令是:

~~~C++
git config --global --unset http.proxy
git config --global --unset https.proxy
~~~



## 3、补充概念：工作流

本地仓库由git维护的三棵树组成。第一个是本地的**工作目录**，它是实际文件。第二个是**暂存区**，像是个临时暂存区，用来缓存你的改动。第三个是**HEAD**，它就是你最后提交的结果。

## 4、添加和提交

你可以把改动的文件先放进暂存区，命令：

~~~C++
git add <filename>
//例如
git add *  //提交所有改动文件
~~~

在使用以下命令进行提交：

~~~C++
git commit -m "提示信息，帮助你了解你本次提交了啥"
~~~

现在文件就被提交到了HEAD，但还没到远程仓库

## 5、替换本地的改动

如果你发现你操作失误，可以用以下命令进行替换本地改动：

~~~C++
git checkout -- <filename>
~~~

这个命令会使用HEAD中最新的内容替换掉你的本地工作目录中的文件。已经添加到缓存区的改动和新文件都不会受到影响。

如果你想放弃本地的所有改动和提交，可以到服务器上获取最新的版本，并将你的本地主分支指向它

~~~C++
git fetch origin
git reset --hard origin/master
~~~

## 6、推送改动到远程服务器

本地的HEAD中的改动，通过以下命令可以提交到远程服务器仓库：

~~~C++
git push origin master
~~~

可以把master换成你想要推送的任何分支

origin是一个代名词，

如果你没克隆现有的仓库，并想把你的仓库连接到某个远程服务器，你可以用以下命令：

~~~C++
git remote add origin <server>
~~~

这样就可以把改动推送到服务器上了

## 7、关于分支

远程服务器可以有很多个分支。在创建仓库时，master是默认分支。如果在其他分支进行开发，完成以后再把他们合并到主分支去。

创建一个feature_x的分支，并切换过去

~~~C++
git checkout -b feature_x
//切换分支
git checkout master
//删除分支
git branch -d feature_x
//推送到服务器
git push origin <branch>
~~~

## 8、更新与合并

要更新你本地仓库到最新的改动，用以下命令：

~~~C++
 git pull
~~~

在现在这个工作目录里获取并合并其他分支的改动到当前的分支，执行:

~~~C++
git merge <branch>
~~~



