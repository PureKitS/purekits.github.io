---
title: 使用GitHub搭建免费图床
date: 2021-07-11 18:01:27
tags: 
- 教程
- Github
- PicGo
- Hexo
categories: PicGo
---



## 前言

最近经过和同学的聊天中得知到了他利用`Github+Hexo`搭建了一个个人博客，我也试着尝试搭建了一个我自己的个人博客，为社么`GitHub`搭建个人博客

<!-- more -->

？选择这个方案的原因得益于使用`GitHub Page`服务可以免除一些麻烦的同时得益于`Git`强大的版本控制，我可以随时追溯到任何一个版本：后来在实际编写和维护博客的同时我发现了一个巨大的问题：“我的那些诱人的图片该怎么办？！！！”



经过一番搜索🔍和同学推荐得知可以使用`GitHub`搭建免费图床！！免费！！虽然`七牛云`也是免费，但是需要拿出我的`身份证`进行`实名认证`!果断放弃，`Google Photos`也可以用作图床搭建，但在中国是无法使用的。

各方搜索我发现了一个及其实用的工具`PicGo`，使用他是可以非常的便捷的使用`Github`搭建图床

> 附上`PicGo`的链接地址 https://picgo.github.io/PicGo-Doc/



## 配置`Github`仓库

1.首先你的有一个`Github`账号。注册`Github`就不用我多言🐕



2.新建一个仓库，并且记下你取的仓库名

![使用Github搭建免费图床-新建仓库-01](https://raw.githubusercontent.com/PureKitS/hexo_pictures_source/main/%E4%BD%BF%E7%94%A8Github%E6%90%AD%E5%BB%BA%E5%85%8D%E8%B4%B9%E5%9B%BE%E5%BA%8A-%E6%96%B0%E5%BB%BA%E4%BB%93%E5%BA%93-01.png)

3.生成一个`Token`用于`PicGo`操作你的仓库

![使用Github搭建免费图床-创建Token-02](https://raw.githubusercontent.com/PureKitS/hexo_pictures_source/main/%E4%BD%BF%E7%94%A8Github%E6%90%AD%E5%BB%BA%E5%85%8D%E8%B4%B9%E5%9B%BE%E5%BA%8A-%E5%88%9B%E5%BB%BAToken-02.png)

然后点击`Generate new token`。

![使用Github搭建免费图床-创建Token-03](https://raw.githubusercontent.com/PureKitS/hexo_pictures_source/main/%E4%BD%BF%E7%94%A8Github%E6%90%AD%E5%BB%BA%E5%85%8D%E8%B4%B9%E5%9B%BE%E5%BA%8A-%E5%88%9B%E5%BB%BAToken-03.png)

把repo的勾打上即可。然后翻到页面最底部，点击`Generate token`的绿色按钮生成`token`。

**注意：**这个token生成后只会显示一次！你要把这个token复制一下存到其他地方以备以后要用。



## 配置`PicGo`

**注意：**仓库名的格式是`用户名/仓库`，比如我创建了一个叫做`hexo_pictures_source`的仓库，在`PicGo`里我要设定的仓库名就是`PureKitS/hexo_pictures_source`。一般我们选择`main`分支即可。然后记得点击确定以生效，然后可以点击`设为默认图床`来确保上传的图床是GitHub。

**注意：**千万！千万!千万！设定仓库名选项不要有空格！！！🐕



![使用Github搭建免费图床-配置PicGo-04](https://raw.githubusercontent.com/PureKitS/hexo_pictures_source/main/%E4%BD%BF%E7%94%A8Github%E6%90%AD%E5%BB%BA%E5%85%8D%E8%B4%B9%E5%9B%BE%E5%BA%8A-%E9%85%8D%E7%BD%AEPicGo-04.png)

至此配置完毕，已经可以使用了。当你上传的时候，你会发现你的仓库里也会增加新的图片了：

![使用Github搭建免费图床-配置PicGo-05](https://raw.githubusercontent.com/PureKitS/hexo_pictures_source/main/%E4%BD%BF%E7%94%A8Github%E6%90%AD%E5%BB%BA%E5%85%8D%E8%B4%B9%E5%9B%BE%E5%BA%8A-%E9%85%8D%E7%BD%AEPicGo-05.png)

## 图片命名 

> 以保证可以有序保存上传，对每个图片都以规定格式命名

> >  博客文章名称-图片对应标题功能-图片序号



