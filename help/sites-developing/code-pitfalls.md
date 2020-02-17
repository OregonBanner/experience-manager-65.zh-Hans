---
title: 代码缺陷
seo-title: 代码缺陷
description: 为AEM进行开发时避免的常见编码缺陷
seo-description: 为AEM进行开发时避免的常见编码缺陷
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 代码缺陷{#code-pitfalls}

## 避免Java代码中的Sling绑定 {#avoid-sling-bindings-in-java-code}

在90%的情况下，Sling绑定是访问服务的不恰当方式。 您应该使用@Reference ** 或@Incrite注释 ** 。

## 避免Java代码中的Thread.interrupt {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* 是危险的，因为在调用错误的时间时，它可能关闭文件，包括Lucene文件和永久缓存文件。

## 避免将Java同步与ReadWriteLocks混合 {#avoid-mixing-java-synchronization-with-readwritelocks}

这会导致代码最终陷入死锁的竞赛条件。
