---
title: Dynamic Media限制
description: 了解在创建图像集、旋转集或上传PDF时的最佳实践和强制限制。 另外，了解不支持的Web浏览器和Dynamic Media查看器的操作系统组合。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: d4eae7774cb657713a06261deeef0fd2ad542836
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 4%

---

# Dynamic Media限制

以下各节介绍了Dynamic Media中的限制。

本主题包括以下部分：

* [Dynamic Media对资产类型的最佳实践和强制限制](#best-practice-enforced-limits)
* [Dynamic Media查看器不支持的Web浏览器和操作系统组合](#unsupported-browser-os)

## Dynamic Media对资产类型的最佳实践和强制限制 {#best-practice-enforced-limits}

在您创建旋转集或图像集，或上传PDF以进行页面提取时，Adobe会推荐以下最佳实践并强制实施以下限制：

| 资产 — 限制类型 | 最佳实践 | 规定的限制 | 2022年12月31日的上限变更 |
| --- | --- | --- | --- |
| **图像**  — 每个图像的智能作物数量 | 5 | 100 | 20 |
| **所有集**  — 每个集的重复资产数 | 无重复项 | 20 | 不适用 |
| **所有集**  — 每组资产的最大数量 | 每组5-10张图像 | 1000 | 不适用 |
| **旋转集**  — 每个2D集的最大行/列数 | 每套12-18页图片 | 1000 | 不适用 |
| **PDF**  — 要考虑提取的PDF的最大页面数 |  | 5000（用于新上传） | 100(适用于所有PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Media查看器不支持的Web浏览器和操作系统组合 {#unsupported-browser-os}

Dynamic Media查看器不支持以下Web浏览器和操作系统组合。

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1更新
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9小牛队
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite
