---
layout: post
title: "比较geek的strcmp实现"
date: 2013-12-06 03:47
comments: true
categories: code
---

自己好玩实现了个strcmp，和string.h里面的strcmp返回值一致。

比较geek的地方在类似my_strcmp("com","computer")的时候程序的执行流程还有最后返回值那块。

{% codeblock lang:c %}
int my_strcmp(const char *str1, const char*str2)
{
    int ret;
    assert(str1 && str2);
    while(!(ret = *str1 - *str2) && *str1++ && *str2++);
    return (ret < 0) ? -1 : !!ret;
}
{% endcodeblock %}
