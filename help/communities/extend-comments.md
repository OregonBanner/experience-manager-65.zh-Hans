---
title: 扩展注释组件
seo-title: Extend Comments Component
description: 扩展“注释”组件，以针对特定用途更改其外观或行为
seo-description: Extend the Comments component to alter its appearance or behavior for specific uses
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 扩展注释组件  {#extend-comments-component}

意图 [扩展](client-customize.md#extensions) 默认组件是为特定用途更改组件的外观或行为。

组件的路径是唯一的，并将默认组件引用为超级资源类型。 与元件叠加的全局范围相比，其范围是有限的，因此风险较小。

>[!NOTE]
>
>扩展 [覆盖](client-customize.md#overlays) 不支持该组件。

## 示例 {#example}

假设注释组件的标题必须使用替代外观显示在AEM实例的一个网站上，而使用默认外观显示在另一个网站上。 叠加默认注释会更改所有实例的注释组件，更好的解决方案是确保有多个注释组件可在各种网站上使用。

要实施此解决方案，请创建一个扩展（覆盖）现有组件的组件并修改Handlebars脚本。 使用新注释的站点区域可以使用扩展注释区域，而使用默认外观的站点不受影响。

注释组件实际上是组成注释系统的两个组件之一。 因此，需要扩展以下两个部分： *评论* 和 *注释*. 要编辑的脚本位于 *注释* 组件的 `header.hbs` 文件，而父级 *评论* 组件（注释系统）是作者实际添加到页面中的内容。

要扩展注释，您必须：

1. [创建组件](extend-create-components.md)
1. [向示例页面添加注释](extend-sample-page.md)
1. [更改外观](extend-alter-appearance.md)
