---
title: Dynamic Media 限制
description: 了解创建图像集、旋转集或上传PDF时的最佳实践和强制限制。 还了解不支持的Dynamic Media Web浏览器和操作系统组合。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: 9247a81a518b1bd6e037c234a6c67f95209bfde8
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 3%

---

# Dynamic Media限制

以下部分介绍了Dynamic Media中的限制。

本主题包含以下部分：

* [Dynamic Media对资源类型的最佳实践和强制限制](#best-practice-enforced-limits)
* [Dynamic Media不支持的Web浏览器和操作系统组合](#unsupported-browser-os)

## Dynamic Media对资源类型的最佳实践和强制限制 {#best-practice-enforced-limits}

在创建旋转集或图像集，或者上传PDF以进行页面提取时，Adobe建议以下最佳实践并强制实施以下限制：

| 资源 — 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| **图像**  — 每个图像的智能裁剪数 | 5 | 100 |
| **所有集**  — 每集的重复资产数 | 无重复项 | 20 |
| **所有集**  — 每组最大资源数 | 每组5-10个图像 | 1000 |
| **旋转集**  — 每个2D集的最大行数/列数 | 每组12-18个图像 | 1000 |
| **PDF**  — 要考虑进行提取的PDF的最大页数 |  | 100(适用于所有PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Media不支持的Web浏览器和操作系统组合 {#unsupported-browser-os}

Dynamic Media不支持以下Web浏览器和操作系统的组合。

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1更新
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9小牛
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

<!-- ## End of support for TLS 1.0 and 1.1 {#tls}

CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)

Effective September 30, 2022, Adobe Dynamic Media will end support for the following:

* TLS (Transport Layer Security) 1.0 and 1.1
* The following weak ciphers in TLS 1.2:
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_RSA_WITH_AES_256_GCM_SHA384`
  * `TLS_RSA_WITH_AES_256_CBC_SHA256`
  * `TLS_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_AES_128_GCM_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA` -->

