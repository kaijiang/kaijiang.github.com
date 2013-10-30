---
layout: post
title: "如何在宏定义中计算柔性数组元素大小"
date: 2013-10-25 11:28
comments: true
categories: code
---
{% codeblock lang:c %}
#include <stdio.h>
#include <inttypes.h>
#include <string.h>
#include <netinet/in.h>

typedef struct _id_list{
    uint16_t n;
    uint16_t uid;
    uint16_t elts[0];
} id_list_t;
    
#define MAX_ELEM 10
#define MAX_LEN sizeof(id_list_t) + MAX_ELEM * sizeof(((id_list_t *)0)->elts[0])
    
int main(void){
    uint8_t id_list_buf[MAX_LEN];
    memset(id_list_buf, 0, MAX_LEN);
    uint16_t i;
    id_list_t * p_id_list = (id_list_t *)id_list_buf;
    
    p_id_list->n = MAX_ELEM;
    p_id_list->uid = 257;
        for (i = 0; i < MAX_ELEM; i++){
        p_id_list->elts[i] = i;
    }
    
    printf("MAX_LEN = %u\n", MAX_LEN);
    for (i = 0; i < MAX_LEN; i += 2){
        printf("%u\n", *(uint16_t *)&id_list_buf[i]);
    }
    return 0;
}
{% endcodeblock %}

