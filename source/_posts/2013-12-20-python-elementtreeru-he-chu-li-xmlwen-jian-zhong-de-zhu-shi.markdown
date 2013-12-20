---
layout: post
title: "python ElementTree如何处理xml文件中的注释"
date: 2013-12-20 02:25
comments: true
categories: code
---

在用python的ElementTree处理xml文件的时候，有一个问题比较烦人：    
当你的xml文件里有注释的时候，调用ElementTree.write()的时候会把注释去掉后保存，对于这种情况，需要加入以下代码进行处理：

{% codeblock lang:python %}

import xml.etree.ElementTree as ET

class CommentParser(ET.XMLTreeBuilder):
    def __init__(self):
        ET.XMLTreeBuilder.__init__(self)
        # assumes ElementTree 1.2.X
        self._parser.CommentHandler = self.handle_comment

    def handle_comment(self, data):
        self._target.start(ET.Comment, {})
        self._target.data(data)
        self._target.end(ET.Comment)

def parse(source):
    return ET.parse(source, CommentParser())
	
{% endcodeblock %}

本质上就是在调用ElementTree.parser()的时候，传入处理comment的handler，方法其实就是ElementTree.Comment()，不知道什么时候ElementTree的版本能自己加入啊。
