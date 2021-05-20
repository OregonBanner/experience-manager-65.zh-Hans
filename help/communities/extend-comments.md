---
title: 扩展注释组件
seo-title: 扩展注释组件
description: 扩展“注释”组件，以更改其外观或行为以供特定用途使用
seo-description: 扩展“注释”组件，以更改其外观或行为以供特定用途使用
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 扩展注释组件{#extend-comments-component}

[扩展](client-customize.md#extensions)默认组件的意图是为特定用途更改组件的外观或行为。

组件的路径是唯一的，并将默认组件作为超级资源类型引用。 与组件叠加的全局范围相比，风险较小，因为范围有限。

>[!NOTE]
>
>不支持扩展[覆盖的](client-customize.md#overlays)组件。

## 示例 {#example}

假设评论组件的标题必须在AEM实例的一个站点上显示，并且具有替代外观，而在另一个站点上显示时却具有默认显示。 最好的解决方案是确保有多个注释组件可供在各种网站上使用，而不是覆盖默认注释（更改所有实例的注释组件）。

要实施此解决方案，请创建一个新组件，以扩展（覆盖）现有组件并修改Handlebars脚本。 使用新注释的网站区域可以使用扩展的注释，而使用默认外观的网站则不受影响。

评论组件实际上是构成评论系统的两个组件之一。 因此，需要扩展两个组件：*注释*&#x200B;和&#x200B;*注释*。 要编辑的脚本位于&#x200B;*注释*&#x200B;组件的`header.hbs`文件中，而父&#x200B;*注释*&#x200B;组件（注释系统）是作者实际添加到页面的内容。

要扩展评论，您需要：

1. [创建组件](extend-create-components.md)
1. [将注释添加到示例页面](extend-sample-page.md)
1. [更改外观](extend-alter-appearance.md)
