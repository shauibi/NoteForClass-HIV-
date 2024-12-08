## 小万的Git笔记

git help 求助

#### 配置信息

git config  --global user.name '王皓'

git config -- global config--list  //列举出全部的配置信息。

git config --unset --global user.name //给user.name重新配置

git config --global user.email '邮箱名'

cat ~/.gitconfig  //查询主目录下的配置文件。

git config --global color.ui true  // 调节color.Ui 视觉库。

#### 初始化项目

git init  //初始化项目

创建了一个.git仓库，进行版本控制的功能实现。![image-20230331173226633](C:\Users\000\AppData\Roaming\Typora\typora-user-images\image-20230331173226633.png)

通过ls命令进行  文件的l列举。

#### 提交项目

git status   //查看当前的状态

![image-20230331173913515](C:\Users\000\AppData\Roaming\Typora\typora-user-images\image-20230331173913515.png)

查看发现并没有可递交的文件。

![image-20230331174622438](C:\Users\000\AppData\Roaming\Typora\typora-user-images\image-20230331174622438.png)

发现在与.git同级的文件夹下插入一个新的文件的时候会产生未被递交的文件错误。

git add <文件名> //加入这个文件到预提交。

git commit -m '添加 什么什么文件'//加入文件。

git log //查看以往的提交。

#### 修改项目的提交。

![image-20230331184042464](C:\Users\000\AppData\Roaming\Typora\typora-user-images\image-20230331184042464.png)

git diff <文件的名称>//会查看出进入库的版本和修改后版本的区别。 此处查看到的是未入库的版本。

git commit -am //不用add可以直接去提交。

#### 重命名工作文件

git rm style.css // 告诉Git，已经删除了style.css 这个文件。

然后再把改名后的工作文件

git add theme.css //添加到暂存区

git commit -m ''//把暂存区的工作调配到库中。 

#### 重命名，移动文件

git mv theme.css ninhao-theme.css//将文件重命名为ninghao-theme.css

然后要提交这个修改。

![image-20230331191814677](C:\Users\000\AppData\Roaming\Typora\typora-user-images\image-20230331191814677.png)

重命名的情况下，去让这个文件位于  css  文件夹之下。

将ninghao-theme.css 移动到css目录下

#### 删除文件

git rm <文件名称>

这个修改需要提交，才能删除这个文件

#### 恢复被删除的文件，HEAD指针。

git checkout HEAD --index.html   //把将要删除的文件从暂存区中拿出来，恢复到最近一次操作该文件的工作目录。

git checkout HEAD^ --index.html //把删除过的文件，在上一次提交的结果中恢复过来。

#### 回滚到版本之前。

git revert  <提交的id号>

恢复了提交。

#### Reset 回盖某次提交。

在默认情况下，每次提交以后，头部指针都会指向最后一次提交。

在reset情况下，指向之前的某次提交。

git reset --soft  <某次提交的id>///暂存区的指令还是存在的。

git reset --hard  <某次提交的id>

git reset --mixed <某次提交的id>//暂存区的指令不存在了、

#### 分支命令

git branch //查看所有分支

git branch <分支名>//创建分支

git checkout  <分支 名称> //切换到指定分支上。

在指定分支对文件进行修改后，轮换到另一个分支后，会回滚到HEAD指针最后一次指向的当前指针指向的revert。

git log --oneline --decorate //带有描述的日志

git log --oneline --decorate --all//带有全部分支的日志

#### 查看两个分支的区别

git diff <分支1>..<分支2>

#### 合并分支功能fast-forward

git merge <要合并的分支>//当前分支与要合并的分支合并，操作一致。

合并分支以后， 不用再提供新的提交。  

整体合并

#### 合并时冲突的解决

先解决冲突，再去进行合并。

产生了conflict冲突。

![image-20230331224322057](C:\Users\000\AppData\Roaming\Typora\typora-user-images\image-20230331224322057.png)

箭号和等号中间的是冲突产生的位置。

#### 重命名分支

git branch -m <想要重命名的分支>  <重命名之后的分支名字>

#### 删除分支

git branch -d bugfix-1

#### stash任务缓存机制。

如果想进行某一项任务，又不想与其他任务同时提交，就可以使用这种stash机制。

git stash  save '描述信息'

查看保存的任务的话，

git stash list

想要查看工作进度和现在分支进度的区别

git stash show -p <显示工作进度的代号>

想要应用工作进度，把保存的工作进度恢复过来。

git stash apply <显示工作进度的代号>

删除工作进度。

git stash drop  <表示工作进度的代号>

在apply了工作进度之后，我们发现，在stash列表之中，依旧存在工作进度，这时候我们使用下列语句将其删除。

git stash pop <表示工作进度的代号>

#### 查看提交日志

默认出现日期，作者，id和提交描述。

git log --oneline//可显示一个简单的日志和描述。

git log -<数字> //可显示 数字对应的条数的日志。

git log --author="<所查的作者的名称>"//可显示对应作者的日志更改情况。

想去寻找所有包含 index.html的提交的日志

git log --oneline --grep='index.html'

想去查找在某个日期之前提交的日志

git log --oneline --before='2023-04-01'

想去寻找三天前，一个礼拜前的提交

#### 给经常使用的git命令添加别名

git config --global alias.co checkout//把checkout设置成别名为co。

可以在系统上面去设置命令的别名。

vim ~/.bash_profile

在里面加入 alias  gco='git checkout'

source ~/.bash_profile

输入上面这行命令之后，设置就会生效了。

#### 不想让项目去跟踪某些文件

 git config  --global core.excludesfile ~/.gitignore _global

在全局范围内忽略这些文件。

编辑一下.gitignore_global //在全局范围内，将文件里面的文件名列表忽略。

vim ~/.gitignore_global

touch <文件名>  //创建文件。

#### 给单独的一个项目去创建忽略文件

在项目的根目录上去创建一个目录

vim  gitignore

在文件内部写入

*<文件名>  

然后add

接着commit

#### remote命令

我们可以在远程创建一个版本库，然后可以在本地把版本推送到版本库上面。

git remote add <远程惯例>  <远程的url>

git remote -v //查看创建的远程的版本库。

#### Push推送远程版本

git push -u <远程惯例>  <本地分支>

移除远程惯例

git remote remove origin

![image-20230401164140080](C:\Users\000\AppData\Roaming\Typora\typora-user-images\image-20230401164140080.png)

最后一行代表着，github上的分支会自动跟随本地上的分支。

查看所有分支：

git branch -a

查看远程分支

git branch -r

使用远程版本库。

clone //克隆版本库。

fork //基于项目开发自己的版本

pull request //如果他觉得我们也需要这些东西的话，申请一个pull request、

添加贡献者contributors共同开发。

写入到版本库的权限。

#### Clone别人的版本库

git clone <远程url> <项目名称>

#### 提取版本库的更新

git fetch//提取更新

然后使用 git merge 去合并更新

![image-20230401170644325](C:\Users\000\AppData\Roaming\Typora\typora-user-images\image-20230401170644325.png)

在本项目下进行相关的配置。

#### pull request

在github中，自己的版本库更新之后，跟原本他人的版本库进行pull request

#### 共同开发项目

Collaborators

添加贡献者，克隆一份版本库到自己的版本库。

git clone <远程版本库的url> <目录名称>

git config user.name '小雪'

git config user.email '<邮箱名称>'

####  Git的图形化工具

