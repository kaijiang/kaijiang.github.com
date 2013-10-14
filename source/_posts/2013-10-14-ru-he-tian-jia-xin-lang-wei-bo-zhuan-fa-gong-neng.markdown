---
layout: post
title: "如何添加新浪微博转发功能"
date: 2013-10-14 02:58
comments: true
categories: blog
---
搭完整个blog的框架后，开始添加一些widget，首当其冲的就是新浪微博的转发功能。

新浪微博提供了开发平台，可以在其提供的接口下添加相应代码完成相应功能。添加微博转发功能到个人网站主要参考了[微博分享按钮](http://open.weibo.com/sharebutton)。

在当前octopress框架下实现主要分以下几步：

* 修改`_config.yml`

添加以下内容：
    # Sina weibo
    weibo_share_button: true
可方便在配置文件中进行功能开启关闭。

<!-- more -->
* 在source/_include/里添加一个html文件weibo.html

添加内容：
    % if site.weibo_share_button %
    <html xmlns:wb="http://open.weibo.com/wb">
    <script src="http://tjs.sjs.sinajs.cn/open/api/js/wb.js" type="text/javascript" charset="utf-8"></script>
    <wb:share-button addition="number" type="button" default_text="来自jiangkai's blog" ralateUid="1639057585"></wb:share-button>
    % endif %
第一行是XML命名空间，第二行为需要添加的js，第三行为WBML代码，定制转发微博相应动作。
需要注意,default_text不能为空，否则点击转发图标后无法生成链接，ralateUid为转发该微博的时候会@的微博用户。

* 修改source/_include/article.html

在该行下
    <div class="entry-content">{{ content }}</div>
添加
    % include weibo.html %

这样在每篇blog的下方增加微博转发按钮。

需要注意的是，在[微博分享按钮](http://open.weibo.com/sharebutton)里的第二步非必须，除非有特定需要在微博中显示转发来源网页或者应用用于推广。

