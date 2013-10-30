---
layout: post
title: "如何加速emacs cscope查询速度"
date: 2013-10-29 02:51
comments: true
categories: emacs
---

emacs + cscope对于小项目来说速度还不错，但是对于动不动几百兆甚至上G的源代码，速度明显超出忍受范围，由于工作原因，项目代码较多，在emacs下用cscope C-s s s搜索symbol速度慢得几乎无法忍受，需要100s以上，后来搜索下了资料并且观察了下cscope命令行参数以及cscope-indexer脚本，发现可以采用两个步骤就能加速上百倍搜索性能:

###1.不要让emacs边搜索边更新    
cscope默认在每次进行查找时更新cscope.out。当工程十分庞大时，建议关闭该选项以提高查找速度。方法是在~/.emacs文件中加入
    (setq cscope-do-not-update-database t)    
###2.cscope建立反向索引   
cscope参数中-q可以建立反向索引来加速搜索，但是默认的cscope-indexer没有开启这个功能，因此需要修改默认的cscope-indexer脚本，把
    cscope -b -i $LIST_FILE -f $DATABASE_FILE
替换为
    cscope -q -b -i $LIST_FILE -f $DATABASE_FILE
然后删掉cscope相关文件，重新生成，再试一次，搜索时间基本上就稳定在1s以内了！
