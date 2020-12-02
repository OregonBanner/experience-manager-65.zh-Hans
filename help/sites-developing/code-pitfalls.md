---
title: 代码陷阱
seo-title: 代码陷阱
description: 为AEM开发时应避免的常见编码陷阱
seo-description: 为AEM开发时应避免的常见编码陷阱
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# 代码陷阱{#code-pitfalls}

## 避免Java代码{#avoid-sling-bindings-in-java-code}中的Sling绑定

在90%的情况下，Sling Bindings是访问服务的不恰当方式。 相反，您应使用&#x200B;*@Reference*&#x200B;或&#x200B;*@Incrite*&#x200B;注释。

## 避免Java代码{#avoid-thread-interrupt-in-java-code}中的Thread.interrupt

*线程。* 中断是危险的，因为在错误的时间调用它时，它可以关闭文件，包括Lucene文件和永久缓存文件。

## 避免将Java同步与ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}混用

这会导致代码最终陷入死锁的竞赛条件。
