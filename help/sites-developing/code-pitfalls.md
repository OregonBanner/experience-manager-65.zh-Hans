---
title: 代码陷阱
description: 为AEM开发时要避免的常见编码陷阱
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 代码陷阱{#code-pitfalls}

## 避免Java代码中的Sling绑定 {#avoid-sling-bindings-in-java-code}

在90%的情况下，使用Sling绑定是不合适访问服务的方式。 您应该改用 *@Reference* 或 *@Inject* 注释。

## 避免Java代码中的Thread.interrupt {#avoid-thread-interrupt-in-java-code}

*线程。中断* 之所以危险，是因为当在错误时间调用时，它可能会关闭文件，包括Lucene文件和永久缓存文件。

## 避免将Java同步与ReadWriteLocks混合使用 {#avoid-mixing-java-synchronization-with-readwritelocks}

这可能导致争用情况，在这种情况下，代码将最终死锁。
