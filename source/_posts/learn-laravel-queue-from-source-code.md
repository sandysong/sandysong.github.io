---
title: Laravel Queue 源码分析
date: 2017-04-05 11:00:23
tags: Laravel 源码分析
---
#Overview
Laravel 队列为不同的后台队列服务提供统一的 API ， 例如 Beanstalk，Amazon SQS， Redis，甚至其他基于关系型数据库的队列。 队列的目的是将耗时的任务延时处理，比如发送邮件，从而大幅度缩短Web请求和相应的时间。

{% asset_img Laravel-Queue.svg [Laravel Queue] %}