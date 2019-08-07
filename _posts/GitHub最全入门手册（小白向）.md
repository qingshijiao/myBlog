---
title: GitHub最全入门手册（小白向）

date: {{date}}
categories:
- github
tags:
- github

---
**本博客仅用于记录自己学习GitHub的过程，如有侵权，可联系删帖。**
**原文链接：https://www.bilibili.com/video/av53325547/?p=3**

# 一、下载GitHub
安装过程就不写了，直接看**原文链接**中，非常地详细。（东西不要都装C盘）
里面还有TortoiseGit（一个git辅助工具）的安装教程及汉化。
链接：https://pan.baidu.com/s/1Z1evzqDp8b4OGtyET1Vw2w 提取码：rh3e
备用  链接：https://pan.baidu.com/s/13mMPAyC7sMRC2e-JLFq-2A  提取码：xtab 

# 二、创建本地仓库
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804093141239.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
新建一个文件夹repositories，方便管理多个本地库，再建一个文件夹test1（你也可以按照视频中建立repo1）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804094349834.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
点开test1，有三种方式建立本地版本库(三选一)
 - 使用Git GUI Here（选择Create New Repository，后选择Browse，Create后会出现一个对话框，是查看每次代码提交的不同之处）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804094848650.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
 - 使用Git Bash Here（命令为git init）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804095149346.PNG)
 - 使用乌龟工具Git 在这里建立本地版本库（直接点确定，**不要打勾**）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804095310713.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
三种方式都会生成一个隐藏文件夹  **.git  这就是本地仓库**(没有的话，点击查看，在隐藏的项目前打勾)
**包含 .git 的文件夹，如我的是test1，这个是工作目录**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804095656610.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
# 三、向本地仓库中添加文件
现在工作目录test1中创建一个文本hello.txt，里面输入11111。（问号表示未添加到本地仓库.git）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804100251604.PNG)
右键hello.txt，选择乌龟工具，点击添加（由于截不了图，只放结果图，文件出现一个加号，没有的也影响不大，只要出现如下对话框即可）
**这一步是将文件添加到暂存区**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804100725747.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
工作区，添加是添加到暂存区，还需提交到一个分支中（分支概念后面讲）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804100950396.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
在文件夹空白处右键，然后点击git提交->"master"，一定要写日志信息，不然不能提交。
提交后出现成功，关闭对话框即可。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804101650239.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
提交成功后，hello.txt文件上会出现一个对号
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804101820336.PNG)
# 四、修改文件内容并且提交

> 问：如何查看自己本地仓库中的文件
> 答：文件夹空白处右键，然后点击乌龟(TortoiseGit)，找到版本库浏览器（R）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804102319355.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)

点击hello.txt，修改文本内容，在文本末尾添加22222（第一次添加的是11111），保存并退出
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804102537101.PNG)
hello.txt会出现一个感叹号，说明此文件已经被修改，然后右键点击提交（因为已经添加过暂存区，所以这次不需要添加），输入日志信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019080410302216.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
**这里可以自己多次尝试修改并提交**

> 问：修改了好几次，如何查看都进行了哪些修改和提交
> 答：空白处或hello.txt文件上右键点击乌龟，显示日志L，上面的可以查看提交日志，选择其中一个然后点击下面的文件，可以查看这一次和上一次修改内容的变化（橙色背景为上次，黄色背景为这次）
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804103708829.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
# 五、删除本地仓库中的文件
可以再新建一个hello1.txt文件，添加内容，右键添加到暂存区，然后提交到master分支
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804104330289.PNG)
直接点击hello1.txt文件，然后点击键盘上的Delete键（或者采用右键删除，或者使用乌龟的删除），然后再次提交（**这一步谨慎操作**）即可。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804105247353.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
> 问：如果我误删除，但是还没有提交，怎么恢复？
> 答：一是使用快捷键**crtl+z**，二是空白处右键乌龟，里面找个还原V

> 问：如何查看我是否删除该文件，本地仓库中真的删除了吗？
> 答：可以再空白处右键，选择乌龟的版本浏览器R查看
> 未提交时，版本库浏览器中还有![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804105402505.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
> 提交后，版本库浏览器中没有![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804105510123.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)

> 问：我只想再本地仓库中删除，但是我的工作区里想保留文件（即回到未添加未提交状态）
> 答：使用乌龟删除时，有一个删除但是保留本地副本，选择它
> 比如我版本库里面有hello2.txt，我只想保留本地副本（只在我的工作区test1里面有，.git里面没有），右键hello2.txt文件然后选择删除并保留本地副本，然后提交，输入日志信息，再次查看版本库浏览器，可以看到里面的hello2.txt文件已经被删除，但是本地副本有。
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804110122859.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804110533475.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
>![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804110717293.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
# 六、将Java工程添加到本地版本库中
从下载的资料中找HelloProject，然后复制到工作目录（包含.git的文件夹，如我的是test1），**然后添加到暂存区**，出现一个叹号
由于Java工程中的一些文件不是必要的，我们可以考虑不将它们添加到版本库中(比如.idea out)
按住ctrl选中两个文件夹，右键点击乌龟，然后找到添加到忽略列表->按照名称忽略，**推荐选择递归忽略，将.gitignore放在文件/文件夹所在的目录**，选择保留本地文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804112244228.PNG)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804112550887.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804112601142.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
然后将生成的.gitignore也添加到暂存区，方便其他人也忽略相同的文件（右键文件，然后选择乌龟），然后将HelloProjiect工程提交到master分支，写日志文件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804113106947.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
可以在版本库浏览器中查看
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190804113307879.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
# 七、在GitHub上设置远程仓库
[在GitHub上设置远程仓库](https://qingshijiao.github.io/2019/08/07/%E5%9C%A8GitHub%E4%B8%8A%E8%AE%BE%E7%BD%AE%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93/)
# 八、分支
[https://www.bilibili.com/video/av53325547/?p=18](https://www.bilibili.com/video/av53325547/?p=18 "https://www.bilibili.com/video/av53325547/?p=18")
# 九、IDEA中使用GitHub
[https://www.bilibili.com/video/av53325547/?p=20](https://www.bilibili.com/video/av53325547/?p=20 "https://www.bilibili.com/video/av53325547/?p=20")