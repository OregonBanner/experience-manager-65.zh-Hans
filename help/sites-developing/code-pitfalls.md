---
title: 程式碼陷阱
seo-title: Code pitfalls
description: 針對AEM開發時應避免的常見編碼陷阱
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

# 程式碼陷阱{#code-pitfalls}

## 避免Java程式碼中的Sling繫結 {#avoid-sling-bindings-in-java-code}

在90%的情況下，使用Sling繫結是不合適存取服務的方式。 您應該改用 *@Reference* 或 *@Inject* 註解。

## 避免Java程式碼中的Thread.interrupt {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* 很危險，因為如果在錯誤的時間呼叫，可能會關閉檔案，包括Lucene檔案和永久性快取檔案。

## 避免混用Java同步與ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

這可能會導致程式碼最終死鎖的競爭條件。
