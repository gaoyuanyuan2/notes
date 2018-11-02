## GitHub
### 1、Github 三大套件 
<br>1.Issues 讨论。问题提交 
<br><br>2.Wiki 手册 说明
<br><br>3.GitPages 项目网站
### 2、命令
<br>1.基于索引值操作
<br>git reset --hard [局部索引值]
<br>git reset --hard a6ace91
<br>使用`^`符号:只能后退
<br>git reset --hard HEAD `~` n
<br>注:一个`^`表示后退一步， n个表示后退n步使用 `~`符号:只能后退
<br>git reset -hard HEAD~n注:表示后退n步
<br><br>2.reset命令的三个参数对比
<br>soft参数仅仅在本地库移动HEAD指针
<br>mixed参数在本地库移动HEAD指针、重置暂存
<br>hard参数在本地库移动HEAD指针、重置暂存区、重置工作区
<br><br>3.比较文件差异
<br>git diff[文件名] --git diff apple.txt
<br>将工作区中的文件和暂存区进行比较git diff [本地库中历史版本] [文件名]
<br>将工作区中的文件和本地库历史记录比较不带文件名比较多个文件
<br><br>4.git checkout 分支名称
<br><br>5.邀请：Settings-Collaborators
<br><br>6.拉取 pull=fetch+merge
<br>git fetch [远程库地址别名] [远程分支名]
<br>git merge [远程库地址别名/远程分支名]
### 3、哈希
<br>哈希是一个系列的加密算法，各个不同的哈希算法虽然加密强度不同。但是有以下几个共同点:
<br>不管输入数据的数据最有多大，输入同一个哈合算法。得到的加密结果长度固定。
<br>哈希算法确定，输入数据确定，输出数据能够保证不变
<br>哈希算法确定，输入数据有变化，输出数据定有变化。而且通常变化很大④哈看算法不可逆
<br>Git底层采用的是SHA-1算法。





        
      

      
