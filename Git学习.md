１、简介

​	版本控制系统	集中式SVN/分布式git

​	<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-15 11.02.37.png" alt="截屏2024-07-15 11.02.37" style="zoom: 33%;" /><img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-15 11.03.57.png" alt="截屏2024-07-15 11.03.57" style="zoom:33%;" />

​	git的使用方式

​		命令行

​		图形化界面(GUI)

​		IDE插件/扩展

​	配置用户和邮箱

​	**git config --global user.name "Jasper Yang"**

​	--local:本地配置，只对本地仓库有效

​	--gobal:全局配置，所有仓库生效

​	--system:系统配置，对所有用户生效

​	保存用户名和密码	**git config --global credential.helper store** 

​	查看git配置信息	**git config --global --list**

２、新建仓库

​	**git init/git clone**	

３、工作区域和文件状态

​	工作区 Working Directory	

​	暂存区 Staging Area/Index：临时存储区域，用于保存即将提交到Git仓库的修改内容

​	本地仓库 Local Repository：通过git init命令创建的仓库



​	git文件的三种状态：<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-15 11.38.09.png" alt="截屏2024-07-15 11.38.09" style="zoom:50%;" />

４、添加和提交文件

​	**git init**	创建仓库

​	**git status**	查看仓库状态

​	**git add**	添加到暂存区

​	**git commit**	提交

​	git log	查看提交记录	**git log --oneline**	查看简介提交记录

​	git log --oneline --graph --decorate --all 查看分支

​	alias graph = "git log --oneline --graph --decorate --all" 通过别名简易查询

​	cp -rf branch-demo rebase1 复制文件夹

5、git reset回退版本

<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-15 16.07.08.png" alt="截屏2024-07-15 16.07.08" style="zoom:67%;" />

​	查看文件	**cat file.txt**

​	查看暂存区内容	**git ls-files**

​	回退到上一个版本	**git reset --hard HEAD^**

​	 查看操作的历史记录	**git reflog**



６、使用git diff查看差异

​	查看工作去，暂存区，本地仓库之间的差异 **git diff --chached**

​	查看不同版本之间的差异  **git diff HEAD~ HEAD**

​	查看不同分支之间的差异 



７、git rm 删除文件

​	**rm file1.txt**

​	**git rm file2.txt**	把文件从工作区和暂存区同时删除

​	**git rm --cached<file>**  把文件从暂存区删除，但保留在当前工作区中

​	**git rm -r*** 递归删除某个目录下的所有子目录和文件

​	**git ls-files** 查看暂存区的内容

​	**删除后不要忘记提交commit**



８、gitgnore忽略文件

​	系统或者软件自动生成的文件

​	编译产生的中间文件和结果文件

​	运行时生成日志文件，缓存文件，临时文件

​	设计身份，密码，口令，密钥等敏感信息文件

​	**.gitgnore文件的匹配规则：从上到下逐行匹配，每一行表示一个忽略模式**

<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-16 20.33.13.png" alt="截屏2024-07-16 20.33.13" style="zoom: 50%;" /><img src="/Users/fulina/Desktop/截屏2024-07-16 20.34.18.png" alt="截屏2024-07-16 20.34.18" style="zoom:50%;" />

9、SSH配置和克隆仓库

​	**ssh-keygen -t rsa -b 4096** 生成SSH密钥

​	如果设置过了需要设置新的文件名

<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-16 20.57.58.png" alt="截屏2024-07-16 20.57.58" style="zoom:50%;" />

​	.pub为公钥文件	vi id_rsa.pub

​	**git clone** git@github.com:anteisuba/learn-git.git

​	同步本地仓库和远程仓库：

​			**git pull / git fetch 拉取**

​			**git push 提交**



10、关联本地仓库和远程仓库

​		添加远程仓库：**git remote add <远程仓库别名><远程仓库地址>**

​					 **git push -u <远程仓库别名><远程仓库地址>**

​		查看远程仓库：**git remote -v**

​		拉取远程仓库内容：**git pull <远程仓库名><远程分支名>:<本地分支名>**



11、在VS中使用Git

​	打开命令面板：**c t r l + shift + ^**

​	配置文件：settings.json

​	打开终端：ctrl + shift + ^



12、分支

​	查看分支列表： **git branch**

​	创建分支：	**git branch branch-name**

​	切换分支：	git checkout branch-name

​				 **git switch branch-name**

​	合并分支：	**git merge branch-name**

​	删除分支：	**git branch -d branch-name **

​				 **git branch -D branch-name** 



13、解决合并冲突

​	两个分支未修改同一个文件的同一处位置：Git自动合并

​	两个分支修改了同一个文件的同一处位置：产生冲突

​	解决方法：	

​		手工修改冲突文件，合并冲突内容 **vi main1.txt**

​		添加暂存区	**git add file**

​		提交修改	**git commit -m "message"**

​	中止合并：当不想继续执行合并操作时可以使用下面的命令来中止合并过程	**git merge --abort**	

14、回退和rebase(变基)

​		git switch dev							git switch main

​		git rebase main						     git rebase dev

<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-17 11.14.56.png" alt="截屏2024-07-17 11.14.56" style="zoom:67%;" />

15、分支管理和工作流模型

​	工作流模型：比较好的规范和流程

​	Git flow模型：	

​	版本号规则：<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-17 11.35.48.png" alt="截屏2024-07-17 11.35.48" style="zoom:50%;" />

​	Github Flow模型：<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-17 11.47.47.png" alt="截屏2024-07-17 11.47.47" style="zoom:67%;" />

​	分支命名：

​		版本发布分支/Tag示例：v.1.0.0

​		 功能分支示例：feature-login-page

​		修复分支示例：hotfix-#issueid-desc

​	分支管理：

​		定期合并已经成功验证的分支，及时删除已经合并的分支

​		保持合适的分支数量

​		为分支设置合适的管理权限







