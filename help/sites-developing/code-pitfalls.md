---
title: 代码陷阱
seo-title: Code pitfalls
description: 为AEM开发时要避免的常见编码陷阱
seo-description: Common coding pitfalls to avoid when developing for AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 代码陷阱{#code-pitfalls}

## 避免Java代码中的Sling绑定 {#avoid-sling-bindings-in-java-code}

在90%的情况下，使用Sling绑定访问服务是不合适的方法。 您应该改用 *@Reference* 或 *@Inject* 注释。

## 避免Java代码中的Thread.interrupt {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* 很危险，因为它可能会在错误时间调用时关闭文件，包括Lucene文件和永久缓存文件。

## 避免将Java同步与ReadWriteLocks混合 {#avoid-mixing-java-synchronization-with-readwritelocks}

这可能导致争用情况，在这种情况下，代码将最终死锁。
