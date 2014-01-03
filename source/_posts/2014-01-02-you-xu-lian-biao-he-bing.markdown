---
layout: post
title: "有序链表合并"
date: 2014-01-02 23:21
comments: true
categories: code
---
问题：
两个有序单链表，现在需要实现这两个链表合并，并保证合并后的链表依然有序。
{% codeblock lang:c %}
node *list_emerge(node *head1, node *head2)
{
    node **head = NULL;
    node *dummy = (node *)malloc(sizeof(node));
    node *new = dummy;
    while (head1 && head2 && (head = head1->value < head2->value ? &head1 : &head2)) {
        new->next = *head;
        new = *head;
        *head = (*head)->next;
    }
    new->next = head1 ? head1 : head2;
    new = dummy->next;
    free(dummy);
    return new;
}
{% endcodeblock %}
采用非递归方式实现，dummy的引入是方便确定头节点以及应对head1,head2可能为空的情况
