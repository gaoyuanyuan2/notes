# GitHub

##  Github 三大套件 

1.Issues 讨论。问题提交 

2.Wiki 手册 说明

3.GitPages 项目网站

##  命令

1.基于索引值操作

* git reset --hard [局部索引值]

*  git reset --hard a6ace91

 使用`^`符号:只能后退

*  git reset --hard HEAD `~` n

注:一个`^`表示后退一步， n个表示后退n步使用 `~`符号:只能后退

*  git reset -hard HEAD~n注:表示后退n步

强制回退到以前的版本

* 第一步: git log 查看之前的commit的id，找到想要还原的版本

* 第二步: git reset --hard 44bd896b   还原到之前的某个版本

* 第三步: git push -f origin master  强制push到远程

2.reset命令的三个参数对比

* soft参数仅仅在本地库移动HEAD指针

* mixed参数在本地库移动HEAD指针、重置暂存

* hard参数在本地库移动HEAD指针、重置暂存区、重置工作区


3.比较文件差异

* git diff[文件名] --git diff apple.txt

* 将工作区中的文件和暂存区进行比较git diff [本地库中历史版本] [文件名]

* 将工作区中的文件和本地库历史记录比较不带文件名比较多个文件


4.git checkout 分支名称

* git checkout -b dev 创建新分支

* git push origin dev_area -u 建立连接

* checkout . 撤销所有更改

* git push origin :dev_area 删除分支 **注意空格**

* git branch -a     查看项目的分支(包括本地和远程) 

* git branch -r  查看远程分支

* git branch -d <BranchName> 删除本地分支 

* git checkout -b 本地分支名x origin/远程分支名x

5.邀请：Settings-Collaborators


6.拉取 pull=fetch+merge

* git fetch [远程库地址别名] [远程分支名]

* git merge [远程库地址别名/远程分支名]

7.推送到远端

* git init

* git remote add origin git@github.com:gaoyuanyuan2/test2.git

* git push -u origin master

8.版本

* git tab 版本

9.忽略.gitignore

* git rm --cached **/BaseTest.java

10.清除账号

git credential-manager uninstall  清除掉缓存在git中的用户名和密码 同时删除用户目录下git 配置.

git config --global credential.helper store 再保存



## 哈希

* 哈希是一个系列的加密算法，各个不同的哈希算法虽然加密强度不同。但是有以下几个共同点:

* 不管输入数据的数据最有多大，输入同一个哈合算法。得到的加密结果长度固定。

* 哈希算法确定，输入数据确定，输出数据能够保证不变

* 哈希算法确定，输入数据有变化，输出数据定有变化。而且通常变化很大④哈看算法不可逆

* Git底层采用的是SHA-1算法。

[鲜为人知的Git命令](https://dzone.com/articles/lesser-known-git-commands)

## ssh 方式

一、配置Git个人信息

* $ git config --global user.name "随意起名字"
 
* $ git config --global user.email "你的GitHub邮箱"

二、使用

* $ ssh-keygen -t rsa

* 生成SSH key，下面三处直接回车就行

三、由上面路径C:\Users\Administrator\.ssh找到id_rsa.pub文件，用文字编辑工具打开，复制

四、到自己的GitHub中，找到Settings进入，点击SSH and GPG keys，再新建一个SSH key，将id_rsa.pub文件中的内容放到key中。

五、测试SSH连接

* $ ssh -T git@github.com

六、使用

* $ git clone git@github.com:JeffLi1993/springboot-learning-example.git


[参考](https://blog.csdn.net/qq_36135928/article/details/78714501)




        
      

      
