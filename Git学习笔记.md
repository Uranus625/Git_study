# Git分布式版本控制工具

> 参考视频：[Git学习-哔哩哔哩](https://www.bilibili.com/video/BV1MU4y1Y7h5?p=1&vd_source=d13fed8345cf3fc82c8c32365f9b43ef)
>
> 参考文档：[Git 教程 | 菜鸟教程](https://www.runoob.com/git/git-tutorial.html)

## 简介

### 版本控制器方式

* **集中式版本控制工具**，如SVN、CVS

  ​		版本库是集中存放在中央服务器的，team里每个人work时从中央服务器下载代码，时必须联网才能工作，局域网或互联网。个人修改然后提交到中央管理库。

* **分布式版本控制工具**，如Git

  ​		分布式版本控制系统没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样工作的时候，无需联网了。多人协作只需要各自的修改推送给对方，就能互相看到对方的修改了。

### Git工作流程图

![Git工作流程图](Git学习笔记.assets/Git工作流程图.png)

```powershell
1. clone（克隆）：从远程仓库中克隆代码到本地仓库
2. checkout（检出）：从本地仓库中检出一个仓库分支然后进行修订
3. add（添加）：在提交前先将代码提交到暂存区
4. commit（提交）：提交到本地仓库。本地仓库中保存修改的各个历史版本
5. fetch（抓取）：从远程库抓取到本地仓库，不进行任何的合并动作，一般操作比较少
6. pull（拉取）：从远程库拉到本地库，自动进行合并（merge），然后放到工作区，相当于fetch+merge
7. push（推送）：修改完成后，需要和团队成员共享代码时，将代码推送到远程仓库
```

## 安装配置

### 安装

> 官网链接：[Git - Downloads (git-scm.com)](https://git-scm.com/downloads)

### 配置用户信息

```shell
git config --global user.name "Uranus625"
git config --blobal user.email "3132249802@qq.com"
```

### 查看配置信息

```shell
git config --blobal user.name
git config --blobal user.email
```

### 解决中文乱码问题

> 参考链接：[git 显示中文和解决中文乱码 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/133706032)

1. 打开Git Bash执行下面命令

```shell
git config --global core.quotepath false
```

2. 菜单中修改

​		在`git bash`的界面中右击空白处，弹出菜单，选择`选项->文本->本地Locale`，设置为`zh_CN`，而旁边的字符集选框选为`UTF-8`。

## 文件状态

![Git文件状态](Git学习笔记.assets/Git文件状态.png)

## 常用操作指令

* 创建仓库命令

  ```shell
  git init			   	   #初始化git本地仓库
  git clone			    #拷贝一份远程仓库，也就是下载一个项目。
  ```

* 提交与修改

  ```shell
  git add					#添加文件到暂存区
  git status			   #查看仓库当前的状态，显示有变更的文件。
  git diff				 #比较文件的不同，即暂存区和工作区的差异。
  git commit 			#提交暂存区到本地仓库。
  git reset 			   #回退版本。
  git rm				   #将文件从暂存区和工作区中删除。
  git mv				  #移动或重命名工作区文件。
  ```

* 提交日志

  ```shell
  git log						#查看历史提交记录
  git blame <file>	 #以列表形式查看指定文件的历史修改记录
  ```

* 远程操作

  ```shell
  git remote				#远程仓库操作
  git fetch 				  #从远程获取代码库
  git pull				   #下载远程代码并合并
  git push				 #	上传远程代码并合并
  ```

## 建立本地仓库

* 本地建立

  ```shell
  git init
  ```

* 远程克隆

  ```shell
  git clone [URL]
  ```

## 本地仓库提交回退

* 提交本地仓库

  ```shell
  git add <file>
  #git rm [-r] --cached <file>将文件从暂存区移除，-r用来移除文件夹
  git add commit -m "注释说明"
  ```

* 查看提交日志

  ```shell
  git log [option]
  			options:
  						--all	#显示所有分支
  						--pretty=oneline	#将提交信息显示为一行
  						--abbrev-commit		#使得输出的commitid更简短
  						--graph				#以图的形式显示
  git reflog   #显示所有操作日志
  ```

* 版本回退

  ```shell
  git reset --hard [commitid]
  ```

* 忽略特定文件

  1. 工作目录下建立`.gitignore`文件
  2. `.gitignore`中加入忽略的文件

## 分支

* 查看分支

  ```shell
  git branch
  ```

* 新建分支

  ```shell
  git branch [分支名]
  ```

* 删除分支

  ```shell
  git branch -d [分支名]				#需要做各种检查
  git branch -D [分支名]				#强制删除
  ```

* 切换分支

  ```shell
  git checkout [分支名]
  git checkout -b [分支名] 		#创建并切换到
  ```

* 合并分支

  ```shell
  git merge [dev01]			#把dev01分支合并到当前分支
  ```

## SSH密钥

1. 生成SSH公钥

   1. `ssh-keygen -t rsa`
   2. 不断回车选择默认设置
      * 如果公钥已近存在，则自动覆盖

2. 在`~/.ssh`下生成3各文件

   ```shell
   id_rsa						#本地密钥
   id_rsa.pub				#公钥
   known_hosts
   ```

3. 将id_rsa.pub中的内容全选复制，并粘贴远端

## 远程仓库

* 关联远程仓库

  ```shell
  git remote add origin [URL]		#origin为给远程仓库取的名字，规范为origin
  ```

* 查看远程仓库

  ```shell
  git remote
  ```

* 将本地仓库同步到远程仓库

  ```shell
  git push origin main
  #完整指令如下：
  git push [-f] [--set-upstream] [远端名称 [本地分支名 : 远端分支名]]
  					-f							  #强制
  					-set--upstream		#推送到远端的同时建立起和远端分支的关联关系
  					#远端名称一般为 origin
  					#当本地分支名与远端分支名相同时，可省去冒号，只写一个分支名
  ```

* 将远程仓库同步到本地

  ```shell
  git fetch					#将远程分支拉到本地，此时会出现origin/main的分支
  git merge origin/main			#合并分支
  ```

  ```shell
  git pull					#等价于上面两条指令
  ```

  ```shell
  git fetch/pull [远端名称(origin)] [远端分支名(不指定则抓取所有分支)]
  ```