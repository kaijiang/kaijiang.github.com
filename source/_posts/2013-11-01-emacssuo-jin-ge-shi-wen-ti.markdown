---
layout: post
title: "emacs缩进格式问题"
date: 2013-11-01 01:16
comments: true
categories: emacs
---

各个编辑器之间最大的问题就是格式不统一，经常这边格式改的挺好，在另外一个编辑器里打开就又不对齐了，归结到最重要的一个问题就是TAB的不统一，有的编辑器默认TAB是4，有的是8，有的是6....    
解决这个问题的方法就是强制用空格来替代TAB，这样就解决了编辑器之间不统一的问题，只要同一种格式在各种编辑器打开都是统一风格了。    
emacs解决这个问题的方法就是将`indent-tabs-mode`这个变量设置为无效就行。正确的设置方式如下:
    (defconst mystyle
      '(......)
      "mystyle" )
    (c-add-style "mystyle" mystyle)
    (defun myhook()
      (setq indent-tabs-mode nil)
      (c-set-style "mystyle"))
    (add-hook 'c++-mode-hook 'myhook
改完后世界终于清净了！
