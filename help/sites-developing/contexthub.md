---
title: ContextHub
seo-title: ContextHub
description: ContextHub是用于存储、处理和呈现上下文数据的框架
seo-description: ContextHub是用于存储、处理和呈现上下文数据的框架
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub是用于存储、处理和呈现上下文数据的框架。 客户端Javascript API允许您访问用于个性化内容的数据。

>[!NOTE]
>
>[We.Retail引用实施](/help/sites-developing/we-retail.md)可实施ContextHub，并在您将ContextHub集成到您自己的项目时用作引用。

>[!CAUTION]
>
>[We.Retail引用实施](/help/sites-developing/we-retail.md)(`/libs/settings/cloudsettings/legacy`)使用的包含示例ContextHub配置的路径，应仅用作创建您自己配置的引用。
>
>它不应在项目中用作您自己的ContextHub配置。

## 持久性 {#persistence}

ContextHub存储客户端上的持久上下文数据。 ContextHub Javascript API允许您访问存储区，以根据需要创建、更新和删除数据。 因此， ContextHub表示页面上的数据层。

每个ContextHub存储都是预定义存储类型的实例：

* ContextHub提供了多种[示例存储类型](/help/sites-developing/ch-samplestores.md)。
* 使用AEM控制台创建存储](ch-configuring.md#creating-a-contexthub-store)。[
* 开发人员可以[创建自定义存储类型](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。
* 开发人员可以通过Javascript[访问存储数据](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores)。

## 分段 {#segmentation}

ContextHub包括一个分段引擎，用于管理区段并确定哪些区段针对当前上下文进行解析。 定义了多个区段。 您可以使用Javascript API确定[已解析的区段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)。

## 演示文稿 {#presentation}

[ContextHub工具栏](/help/sites-authoring/ch-previewing.md)使营销人员和作者能够查看和处理存储数据，以模拟创作页面时的用户体验。 工具栏由UI模块组成，这些模块提供对ContextHub存储的访问。

每个ContextHub UI模块都是预定义模块类型的实例：

* ContextHub提供了多种[示例模块类型](/help/sites-developing/ch-samplemodules.md)。
* 使用AEM控制台可以[添加UI模块](ch-configuring.md#adding-a-ui-module)，并以UI模式](ch-configuring.md#adding-a-ui-mode)将它们分组到[中。

* 开发人员可以[创建自定义模块类型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

开发人员需要[将ContextHub组件添加到页面](/help/sites-developing/ch-adding.md)。
