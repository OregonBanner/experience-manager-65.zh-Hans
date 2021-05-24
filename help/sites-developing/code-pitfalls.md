---
title: 代码缺陷
seo-title: 代码缺陷
description: 为AEM开发时需要避免的常见编码陷阱
seo-description: 为AEM开发时需要避免的常见编码陷阱
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 代码缺陷{#code-pitfalls}

## 避免Java代码{#avoid-sling-bindings-in-java-code}中的Sling绑定

在90%的情况下，Sling绑定是获取服务访问权限的不适当方式。 您而是应该使用&#x200B;*@Reference*&#x200B;或&#x200B;*@Inject*&#x200B;注释。

## 避免Java代码{#avoid-thread-interrupt-in-java-code}中的线程。中断

*Thread.* 中断是危险的，因为当在错误的时间调用时，它可能会关闭文件，包括Lucene文件和永久缓存文件。

## 避免将Java同步与ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}混合

这可能会导致代码最终会陷入死锁的争用情况。
