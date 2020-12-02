---
title: 内容处置筛选器
seo-title: 内容处置筛选器
description: 了解如何使用内容处置过滤器来防止XSS攻击。
seo-description: 了解如何使用内容处置过滤器来防止XSS攻击。
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 内容处置筛选器{#content-disposition-filter}

内容处置过滤器是一种安全功能，可防止SVG文件受到XSS攻击。

安装后，过滤器将阻止访问所有资产。 例如，您无法在线视图pdf。 本节将介绍如何根据需要配置过滤器。

## 配置内容处置筛选器{#configure-content-disposition-filter}

您可以在GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)中视图[Apache Sling Content Disposition过滤器。

“内容处置过滤器”选项提供以下功能：

* 内容处置路径：一列表路径，其中过滤器将应用，后跟一列表mime类型以在该路径上排除。此路径必须是绝对路径，并且最后可能包含通配符(&#39;&amp;ast;&#39;)，以使每个资源路径与给定路径前缀相匹配。 例如：/content/&amp;ast;:image/jpeg,image/svg+xml &quot;将对/content中除jpg和svg图像外的每个节点应用滤镜

* 排除的资源路径：排除资源的列表，必须将每个资源路径指定为绝对和完全限定的路径。 不支持前缀匹配／通配符。

* 为所有资源路径启用：此标志控制是否对所有路径启用此过滤器，排除资源路径定义的排除路径除外。 将此设置为“true”会导致忽略内容处置路径。 将覆盖独立于配置的资源路径，其中包含名为“jcr:data”或“jcr:content jcr:data”的属性。

