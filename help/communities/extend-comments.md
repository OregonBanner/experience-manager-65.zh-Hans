---
title: 扩展注释组件
seo-title: 扩展注释组件
description: 扩展“注释”组件以更改其外观或行为以用于特定用途
seo-description: 扩展“注释”组件以更改其外观或行为以用于特定用途
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: 230c700d87d82d248b7d0bbc45c69c5c2b0e3ff8
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 扩展注释组件  {#extend-comments-component}

扩展默 [认组](client-customize.md#extensions) 件的目的是为特定用途更改组件的外观或行为。

组件的路径是唯一的，并将默认组件作为超级资源类型引用。 与组件叠加的全局范围相比，该范围有限，因此风险更小。

>[!NOTE]
>
>不支持 [扩展](client-customize.md#overlays) 叠加的组件。


## 示例 {#example}

假定注释组件的标题必须在AEM实例的一个站点上显示具有替代外观，而在另一个站点上显示带有默认显示。 更好的解决方案是，确保有多个注释组件可供不同站点使用，而不是覆盖默认注释（更改所有实例的注释组件）。

要实现此解决方案，请创建一个新组件，它扩展（覆盖）现有组件并修改Handlebars脚本。 使用新注释的站点的区域可以使用扩展的注释，而使用默认外观的站点则不受影响。

该注释组件实际上是构成该注释系统的两个组件之一。 因此，有两个组件要扩展： *注释* 和 *注释*。 要编辑的脚本位于 *注释* 组件的 `header.hbs` 文件中 *，而父注释组* 件（注释系统）是作者实际添加到页面的内容。

要扩展注释，您需要：

1. [创建组件](extend-create-components.md)
1. [向示例页面添加注释](extend-sample-page.md)
1. [改变外观](extend-alter-appearance.md)

