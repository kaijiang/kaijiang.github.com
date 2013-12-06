---
layout: post
title: "单链表反转"
date: 2013-12-06 02:31
comments: true
categories: code
---
闲的没事实现了一个单链表反转，不知道还有没有更优雅点的实现，类似[linus:利用二级指针删除单向链表](http://coolshell.cn/articles/8990.html)这种。
{% codeblock lang:c %}
node *list_reverse(node *head)
{
    node *prev = NULL, *next = NULL;
    while(head){
        next = head->next;
        head->next = prev;
        prev = head;
        head = next;
    }
	/*return new head*/
    return prev;
}
{% endcodeblock %}
