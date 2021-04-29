---
title: 内容处置筛选器
seo-title: 内容处置筛选器
description: 了解如何使用内容处置过滤器防止XSS攻击。
seo-description: 了解如何使用内容处置过滤器防止XSS攻击。
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
translation-type: tm+mt
source-git-commit: cd895fcab5adce600ce230fb6867392e45963c16
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 内容处置筛选器{#content-disposition-filter}

内容处置滤镜是针对SVG文件的XSS攻击的安全功能。

安装后，过滤器将阻止访问所有资产。 例如，您无法在线视图PDF。 本节介绍如何根据您的需要配置过滤器。

## 配置内容处置筛选器{#configure-content-disposition-filter}

您可以在GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)中视图[Apache Sling Content Disposition过滤器。

“内容处置过滤器”选项提供以下功能：

* **内容处置路** 径：列表路径，在路径中，将应用筛选器，然后列表mime类型以在该路径上排除。此路径必须是绝对路径，并且最后可能包含通配符(`*`)，以使每个资源路径与给定路径前缀匹配。例如：`/content/*:image/jpeg,image/svg+xml`将对“/content”中的每个节点应用筛选器？ jpg和svg图像除外

* **排除的资源路** 径：排除的资源的列表，每个资源路径都必须作为绝对和完全限定的路径。不支持前缀匹配/通配符。

* **为所有资源路径启用：此标** 志控制是否为所有路径启用此过滤器，除由排除资源路径定义的排除路径外。将此值设置为“true”会导致忽略内容处置路径。 与配置无关，只覆盖包含名为`jcr:data`或`jcr:content/jcr:data`的属性的资源路径。
