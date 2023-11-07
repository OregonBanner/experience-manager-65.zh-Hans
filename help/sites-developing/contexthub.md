---
title: ContextHub
description: ContextHub是一个用于存储、操作和呈现上下文数据的框架
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub是一个用于存储、操作和呈现上下文数据的框架。 通过客户端JavaScript API，可访问数据以使内容个性化。

>[!NOTE]
>
>此 [We.Retail参考实施](/help/sites-developing/we-retail.md) 实施ContextHub，并在将ContextHub集成到您自己的项目中时用作参考。

>[!CAUTION]
>
>包含由使用的示例ContextHub配置的路径 [We.Retail参考实施](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`)只能用作创建您自己的配置的参考。
>
>请勿在项目中使用作为您自己的ContextHub配置。

## 持久性 {#persistence}

ContextHub存储在客户端上保留上下文数据。 通过ContextHub JavaScript API，您可以访问存储，以根据需要创建、更新和删除数据。 因此，ContextHub表示页面上的数据层。

每个ContextHub存储都是预定义存储类型的实例：

* ContextHub提供了多个 [示例存储类型](/help/sites-developing/ch-samplestores.md).
* 使用AEM控制台可以 [创建商店](ch-configuring.md#creating-a-contexthub-store).
* 开发人员可以 [创建自定义商店类型](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* 开发人员可以 [访问存储数据](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) 通过JavaScript。

## 分段 {#segmentation}

ContextHub包括管理区段并确定当前上下文解析哪些区段的分段引擎。 定义了多个区段。 您可以使用JavaScript API执行以下操作 [确定已解析的区段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## 演示文稿 {#presentation}

此 [ContextHub工具栏](/help/sites-authoring/ch-previewing.md) 使营销人员和作者能够查看和处理存储数据，以便在创作页面时模拟用户体验。 工具栏由提供对ContextHub存储的访问权限的UI模块组组成。

每个ContextHub UI模块都是预定义模块类型的实例：

* ContextHub提供了多个 [示例模块类型](/help/sites-developing/ch-samplemodules.md).
* 使用AEM控制台可以 [添加用户界面模块](ch-configuring.md#adding-a-ui-module)、和 [在UI模式下对这些组件进行分组](ch-configuring.md#adding-a-ui-mode).

* 开发人员可以 [创建自定义模块类型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

开发人员需要 [将ContextHub组件添加到页面](/help/sites-developing/ch-adding.md).
