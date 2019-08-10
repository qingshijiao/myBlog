---
title: 在GitHub上设置远程仓库

date: {{date}}
categories:
- GitHub
tags:
- github

---
# 一、创建一个GitHub账号
这里不过多介绍
# 二、创建一个仓库
点击您的仓库，我这里有个汉化插件，你们的应该是英文，位置相同。
![](https://img-blog.csdnimg.cn/20190804131623180.PNG)
点击新建
![](https://img-blog.csdnimg.cn/20190804131714694.PNG)
输入仓库名称即可，使用README.md初始化仓库可选可不选，视频上说的是不选
![](https://img-blog.csdnimg.cn/20190804131733320.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
下面有三个分别表示没有本地仓库的建造一个本地仓库然后command，有本地仓库的直接command，导入代码从另一个仓库
两种方式：HTTPS 和 SSH（密钥）
![](https://img-blog.csdnimg.cn/20190804131934629.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
# 三、创建ssh密钥并配置
随便在哪里使用右键菜单中的git bash here 
输入命令  ssh -keygen -t rsa
会自动在你账户目录（C:\Users\你的用户名\\.ssh）下生成ssh文件夹，里面有私钥（私钥自己一定要保护好）和公钥（public）
用文本打开公钥并复制
![](https://img-blog.csdnimg.cn/20190804133044634.PNG)
在github主页上点头像->设置
![](https://img-blog.csdnimg.cn/20190804133300556.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
点击后选择new  ![](https://img-blog.csdnimg.cn/20190804133451732.PNG)
Title随便写（比如key1），下面的就是刚才复制的公钥，然后添加。![](https://img-blog.csdnimg.cn/20190804133509366.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
# 四、将本地仓库同步到远程仓库
## 1.使用ssh推送
### 使用命令行
在你的工作目录中使用git bash here ，我的工作目录是test1
命令行输入下面的两个，**分开输入，https后面的写成你自己的**
![](https://img-blog.csdnimg.cn/20190804134036922.PNG)
### 使用乌龟
**如果没有使用命令行的可以直接看这个，使用过的可以另创建一个仓库重新练习**
右键你的工作目录，选择Git 同步
![](https://img-blog.csdnimg.cn/20190804134615116.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
点击管理后，先点击网络看是否为ssh客户端，不是的话换一下
![](https://img-blog.csdnimg.cn/20190804134936732.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
然后点击Git-远端，按照下面输入，一般为origin
Putty密钥就是你的私钥，没有的话查看所有文件
![](https://img-blog.csdnimg.cn/20190804135139604.PNG)
![](https://img-blog.csdnimg.cn/20190804135428357.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20190804135714165.PNG)
点击确定后，出来点推送，**弹出来个对话框选择“是”**
![](https://img-blog.csdnimg.cn/20190804135856497.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
刷新一下你的github，就可以看到推送成功了。
## 2.使用https推送
上面推送完成的，为了更好的查看效果，可以另外再建一个仓库，我没有新建，只演示一下，
只用填写URL，点是（远端不是origin都会报错，不影响）
![](https://img-blog.csdnimg.cn/20190804140717640.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
会让你输入用户名和密码，显示推送成功
![](https://img-blog.csdnimg.cn/20190804141041193.PNG)
# 五、克隆远程仓库到本地
新建一个clone文件夹
![](https://img-blog.csdnimg.cn/20190804141304335.PNG)
### 使用命令行
先打开你要克隆到的文件夹，使用git bash here 输入命令
git clone https://github.com/qingshijiao/test1.git
https和ssh都行
![](https://img-blog.csdnimg.cn/20190804141544912.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
### 使用乌龟
右键git 克隆，URL中输入https或者ssh，两种方式都行
![](https://img-blog.csdnimg.cn/20190804141854387.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
你还可以看版本库浏览器和显示日志，里面的内容和你本地仓库的都一样
![](https://img-blog.csdnimg.cn/20190804142013176.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMjc5MTUx,size_16,color_FFFFFF,t_70)
# 六、推送文件冲突
这个比较琐碎，还是看视频吧
https://www.bilibili.com/video/av53325547/?p=15
推送不成功，选择乌龟拉取，然后手动修改冲突文件，右键该文件选择乌龟解决冲突，确定。
出现您正在进行特殊的提交（冲突已经解决的话点确定），确定，推送成功。