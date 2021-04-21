## git介绍  
git 是一款免费、开源的分布式版本控制系统，可用于高效快捷的管理各种项目文件


### git仓库会分成三个区

 - 工作区：我们书写代码的地方，工作的目录就叫工作区。

- 暂存区：暂时存储的区域，在git中，代码无法直接从工作区提交到仓库区，而是需要先从工作区添加到暂存区，然后才能从暂存区提交到仓库区。暂存区的目的是避免误操作。

- 本地仓库区：将保存在暂存区域的内容永久转储到 Git 仓库中，生成版本号。生成版本号之后，就可以任何的回退到某一个具体的版本。




### git基本命令

- git init   
  作用：初始化git仓库，想要使用git对某个项目进行管理，需要git init进行初始化

   - git初始化注意点

     要对某个项目使用git进行管理，需要使用git init命令初始化git仓库git init会在当前目录生成一个隐藏文件夹 .git 不要去修改这个文件夹下的任意东西。

- git add  
  作用：将文件由 工作区 添加到 暂存区，在git中，文件无法直接从工作区直接添加到仓库区，必须先从工作区添加到暂存区，再从暂存区添加到仓库区。
  - 命令：git add 文件名/目录名    (注意少用 git add . 有时可能会暂存一些我们不想要的东西)
  - git add *.js 将当前目录下所有的js文件添加到暂存区 
  - 添加当前目录下所有的文件  
     git add .  
     git add -A  
     git add --all

- git commit  
  作用：将文件由 暂存区 添加到 仓库区，生成版本号



将文件从暂存区提交到仓库

git commit -m "提交说明"



如果不写提交说明，会进入vi编辑器，没有写提交说明，是提交不成功的。

git commit   # 需要使用vi输入内容



如果是一个已经暂存过的文件，可以快速提交，如果是未追踪的文件，那么命令将不生效。

git commit -a -m '提交说明'
​



修改最近的一次提交说明， 如果提交说明不小心输错了，可以使用这个命令

git commit --amend -m "提交说明"
git config配置
如果是第一次提交，需要配置提交者信息，推荐和github的账号邮箱一致

git config  user.name 你的目标用户名
git config  user.email 你的目标邮箱名
​





使用--global参数，配置全局的用户名和邮箱，只需要配置一次即可。推荐配置github的用户名和密码

git config  --global user.name Jepson
git config  --global user.email jepsonpp@qq.com
​



查看配置信息

git config --list
git status
作用：查看文件的状态



命令：git status


红色表示工作区中的文件需要提交


绿色表示暂存区中的文件需要提交




命令：git stauts -s 简化日志输出格式


命令：git log
作用：查看提交日志


命令：git log 查看提交的日志


命令：git log --oneline 简洁的日志信息


git对比


git diff


git diff可以查看每次提交的内容的不同


查看工作区与暂存区的不同

git diff



查看暂存区与仓库区的不同

git diff --cached



查看工作区与仓库区的不同，HEAD表示最新的那次提交

git diff HEAD



查看两个版本之间的不同

git diff c265262 de4845b





git重置


git reset
作用：版本回退，将代码恢复到已经提交的某一个版本中。


git reset --hard 版本号 将代码回退到某个指定的版本(版本号只要有前几位即可)


git reset --hard head~1将版本回退到上一次提交
~1:上一次提交
~2:上上次提交
~0:当前提交




关于参数 --hard的解释

git reset 的参数可以是以下三个值：
git reset --soft 版本号  ： 只重置仓库区
git reset --mixed 版本号 ： 重置仓库区和暂存区【默认】
git reset --hard  版本号 ： 重置仓库区和暂存区和工作区。
git reset 版本号         : 效果与--mixed一致
当使用了git reset命令后，版本会回退，使用git log只能看到当前版本之前的信息。使用git reflog可以查看所有的版本信息



git忽视文件


在仓库中，有些文件是不想被git管理的，比如数据的配置密码、写代码的一些思路等。git可以通过配置从而达到忽视掉一些文件，这样这些文件就可以不用提交了。


在仓库的根目录创建一个.gitignore的文件，文件名是固定的。


将不需要被git管理的文件路径添加到.gitignore中


忽视idea.txt文件

idea.txt
​



忽视.gitignore文件

.gitignore
​



忽视css下的index.js文件

css/index.js
​



忽视css下的所有的js文件

css/*.js
​



忽视css下的所有文件

css/.



忽视css文件夹

css



git分支操作

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个平行宇宙里努力学习SVN。

如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了Git又学会了SVN！


为什么要有分支？
》如果你要开发一个新的功能，需要2周时间，第一周你只能写50%代码，如果此时立即提交，代码没写完，不完整的代码会影响到别人无法工作。如果等代码写完再提交，代码很容易丢失，风险很大。
有了分支，你就可以创建一个属于自己的分支，别人看不到，也不影响别人，你在自己的分支上工作，提交到自己的分支上，等到功能开发完毕，一次性的合并到原来的分支。这样既安全，又不影响他人工作。
在工作过程中，经常会碰到多任务并行开发 的情况，使用分支就能很好的避免任务之间的影响。


其他版本工具比如svn，cvs中也有分支这个概念，但是这些工具中的分支操作非常的慢，形同摆设。


git分支命令


在git中，分支实质上仅仅是一个指针，每次代码提交后，这个分支指针就会向后移动，保证一直指向最后一次提交的的版本。git中使用HEAD指向当前分支


创建分支

git branch 分支名称创建分支，分支中的代码，在创建时与当前分支的内容完全相同。



git在第一次提交时，就有了一个叫master的主分支。


git branch dev，创建了一个叫做dev的分支


查看分支


git branch可以查看所有的分支，


在当前分支的前面会有一个*


在git中，有一个特殊指针HEAD,永远会指向当前分支




切换分支


git checkout 分支名称切换分支 HEAD指针指向了另一个分支


在当前分支的任何操作，都不会影响到其他的分支，除非进行了分支合并。


提交代码时，会生产版本号，当前分支会指向最新的版本号。




创建并切换分支


git checkout -b 分支名称 创建并切换分支


切换分支会做两件事情


创建一个新分支


把head指针指向当前的分支




删除分支

git branch -d 分支名称 可以删除分支





注意：不能在当前分支删除当前分支，需要切换到其他分支才能删除。
注意：master分支是可以删除的，但是不推荐那么做。

合并分支


git merge 分支名称 将其他分支的内容合并到当前分支。


在master分支中执行git merge dev 将dev分支中的代码合并到master分支


git合并冲突


对于同一个文件，如果有多个分支需要合并时，容易出现冲突。


合并分支时，如果出现冲突，只能手动处理，再次提交，一般的作法，把自己的代码放到冲突代码的后面即可。






git远程仓库


github与git


git与github没有直接的关系。


git是一个版本控制工具。


github是一个代码托管平台，开源社区，是git的一个远程代码仓库。

gitHub是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。
github免费，代码所有人都能看到，但是只有你自己能修改。付费的可以隐藏。
创建git项目时，不能有中文。





git clone


作用：克隆远程仓库的代码到本地


git clone [远程仓库地址]


git clone git://github.com/jepsongithub/test.git会在本地新建一个test文件夹，在test中包含了一个.git目录，用于保存所有的版本记录，同时test文件中还有最新的代码，你可以直接进行后续的开发和使用。


git克隆默认会使用远程仓库的项目名字，也可以自己指定。需要是使用以下命令：git clone [远程仓库地址] [本地项目名]




git push


作用：将本地仓库中代码提交到远程仓库


git push 仓库地址 master 在代码提交到远程仓库，注意master分支必须写，不能省略


例子：git push XXX master 如果第一次使用，需要填写github的用户名和密码




git pull

作用：将远程的代码下载到本地



注意：通常在push前，需要先pull一次。


获取远程仓库的更新，并且与本地的分支进行合并

git pull
git remote
每次push操作都需要带上远程仓库的地址，非常的麻烦，我们可以给仓库地址设置一个别名



给远程仓库设置一个别名

git remote add 仓库别名 仓库地址
git remote add why git@github.com:XXX/test.git
​



删除why这个别名

git remote remove why
​



git clone的仓库默认有一个origin的别名


SSH免密码登陆


git支持多种数据传输协议：


https协议：github.com/jepsongithu… 需要输入用户名和密码


ssh协议：git@github.com:jepsongithub/test.git 可以配置免密码登录




每次push或者pull代码，如果使用https协议，那么都需要输入用户名和密码进行身份的确认，非常麻烦。
github为了账户的安全，需要对每一次push请求都要验证用户的身份，只有合法的用户才可以push
使用ssh协议，配置ssh免密码，可以做到免密码往github推送代码


SSH免密码登录配置


注意：这些命令需要在bash中敲


创建SSH Key：ssh-keygen -t rsa


在文件路径 C:\用户\当前用户名\ 找到 .ssh 文件夹


文件夹中有两个文件：


私钥：id_rsa


公钥：id_rsa.pub




在 github -> settings -> SSH and GPG keys页面中，新创建SSH key


粘贴 公钥 id_rsa.pub 内容到对应文本框中


在github中新建仓库或者使用现在仓库，拿到git@github.com:用户名/仓库名.git


此后，再次SSH方式与github“通信”，不用输入密码确认身份了   


## git与github的操作  
---
### github创建仓库后需要添加公钥  

Secure Shell (SSH) 是一个允许两台电脑之间通过安全的连接进行数据交换的网络协议。通过加密保证了数据的保密性和完整性。SSH采用公钥加密技术来验证远程主机，以及(必要时)允许远程主机验证用户  

### 生成ssh key的方法
- 1、下载本地git工具（git.exe）
- 2、 配置git基本信息   
   
      git config --global user.name "your name"  
      git config --global user.email "your eamil"
      可以通过 git config --list 来查看配置信息

- 3 输入命令  ssh-keygen -t rsa -C "your_email@xxx.com"
- 4 根据生成的位置，复制公钥  
    ![gitpub.png](gitpub.png)  
- 到github官网首页  
    
   ![setting.png](setting.png)  
   找到个人头像，找到setting点进去  
    
   ![newkey.png](newkey.png)  
   找到SSH and GPG keys 然后点击 new SSH key  

   ![sshdone](sshdone.png)  
   最后将刚生成的公钥粘贴进去就完成了  

关联了github后，有时git pull 或者 git push会报如下错误  
![error](error.png)  
```
错误关键字是 OpenSSL SSL_read: Connection was reset, errno 10054
```
错误原因可能是网络不稳定，连接超时造成的，如果你试了多次还是报这个错误，建议你执行下面的命令
```
git config --global http.sslVerify "false"
```



