---
title: 3-hexo使用及写博客说明

date: {{date}}
categories:
- GitHub
tags:
- hexo
- 3-hexo

---
关于如何配置3-hexo，我这里就不写了（其实我也忘记怎么配置了），可以看下3-hexo作者写的
https://github.com/yelog/hexo-theme-3-hexo

[https://yelog.org/2017/03/17/windows-hexo/](https://yelog.org/2017/03/17/windows-hexo/)

配置好后我想大概有两个问题，一是如何将3-hexo的信息改为自己的（刚配置后还是叶落阁），二是怎么写博客

# 一、配置后的情况
这里补充一条，为了能够快速理解hexo和3-hexo的文件夹内容所表示的含义
配置后的图片,有几个文件要重点关注，
> source 博文文件夹，里面存放你写的博客（一般.md文件）
> themes 主题文件夹，下载的3-hexo主题在里面（注意按照叶落阁命令行下载时，命令行最后有个/themes）
> _config.yml 配置，配置hexo的信息（并不是3-hexo哦）
![](http://ww1.sinaimg.cn/large/006YaFIqly1g5ude1jvwyj30l30bat9n.jpg)
## 1.配置hexo
打开_config.yml，里面的#相当于注释，有几个地方需要改一下（有可能遗漏，可以自己看着改）
> title: 秦艽 #标签页上面的
> author: 秦艽 #写成自己的
> url: http://qignshiijao.github.io #改成自己的
> theme: 3-hexo #使用的主题
> highlight: enable: false #使用叶落阁里面的代码高亮的话，填false
> deploy: #这应该是搭建博客时就写好的
>  type: git
>  repository: git@github.com:qingshijiao/qingshijiao.github.io.git
>  branch: master

进入themes->3-hexo,
> .git #本地仓库（这个好像不能提交，但是不能推送的远程仓库，我没有推送成功）
> source #头像和付款码等
> _config.yml 配置，配置3-hexo的信息

![](http://ww1.sinaimg.cn/large/006YaFIqly1g5ude1jtp9j30kt07t0tb.jpg)

# 二 、修改3-hexo信息
## 1.修改头像和付款码 ##
三个图片修改一下（名字也可以换成其他，不过考虑到还要在配置文件中更改，我直接沿用叶落阁）

![](http://ww1.sinaimg.cn/large/006YaFIqly1g5ude1k8wcj30n9065mz9.jpg)
## 2.更改_config.yml
> avatar: /img/avatar.jpg #头像
> favicon: /img/avatar.jpg
> github: https://github.com/qingshijiao #github地址，也是你头像下方的几个小图标（不填，图标就不会出现）
> 左下角定义菜单里面，有关于是否显示（true or false）和跳转链接(比如/about)
> 文末声明可以改
> highlight: on: true #这是3-hexo自己添加的代码高亮形式，上文中的hexo高亮需关闭
> 比如代码高亮的theme: atom-light 后面这个可以改成它注释里面的，换个名字就能自动配置好了
> 友情链接可以添加多个
> comment评论，这部分我使用的是gitment没有尝试成功，[原文链接](https://yelog.org/2017/06/26/gitment/)

**可以直接执行下面的三查看效果（有时候付款码图片会出现错误，我等了一会，它自动好了，不清楚原因）**

# 二、写博客
写博客地址blog/source
一般博客都写在_posts里面
![](http://ww1.sinaimg.cn/large/006YaFIqly1g5udh627azj30g305w3yo.jpg)
## 1.写404界面
可以参考[hexo搭建404界面](https://yelog.org/2017/02/25/hexo-create-404-page/)
需要在hexo文件夹中执行git bash, 输入 hexo new page 404
测试: https://你的github名字.github.io/404
## 2.写关于界面
同搭建404界面差不多，执行hexo new page about
改成permalink: /about
## 3.开始写博客
博文后面有关于写作 https://yelog.org/2017/03/23/3-hexo-instruction/
我讲一下我遇到的问题，比如这篇文章开头
> title: 3-hexo使用及写博客说明
>
> date: {{date}}
> categories:
> -github
> tags:
> -hexo
> -3-hexo

**每一行末尾不要打回车**

**即使你预览的这种形式也没问题，它会自动识别，你打回车它不能识别（说多了都是泪。。。）**
![](http://ww1.sinaimg.cn/large/006YaFIqly1g5udh60ffjj30zi05i74j.jpg)
# 三、生成博客效果
在hexo启动git bash命令行
这是分别是
- hexo clean 清除所有渲染的页面
- hexo g 将markdown渲染成页面
- hexo s 启动hexo

![](http://ww1.sinaimg.cn/large/006YaFIqly1g5udh5zqmuj30gx019744.jpg)
完成之后可以先到 http://localhost:4000 查看效果，再ctrl+c关闭
![](http://ww1.sinaimg.cn/large/006YaFIqly1g5udh5zsduj30jq01o746.jpg)
然后将效果渲染到你的博客
![](http://ww1.sinaimg.cn/large/006YaFIqly1g5udh5zrdcj30kc02oaa0.jpg)
运行完，刷新一下你的博客就好了

**在 http://localhost:4000 能显示而在个人博客上泵显示，应该是没运行hexo d引起的**

# 四、在博客文件夹里面搭建本地版本库
这个主要是为了将博客推从到github上保存，在github新建一个远程仓库或者直接在你的hexokinase仓库（你的github用户名.github.io）上也可以，提交和推从可以看[这篇博客](https://qingshijiao.github.io/2019/08/07/GitHub%E6%9C%80%E5%85%A8%E5%85%A5%E9%97%A8%E6%89%8B%E5%86%8C%EF%BC%88%E5%B0%8F%E7%99%BD%E5%90%91%EF%BC%89/)

建本地仓库,bash命令行输入git init
![](http://ww1.sinaimg.cn/large/006YaFIqly1g5udh608yaj30lc09hjru.jpg)
