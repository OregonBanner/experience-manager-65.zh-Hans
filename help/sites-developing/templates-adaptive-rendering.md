---
title: 自适应模板渲染
description: 自适应模板渲染
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 自适应模板渲染{#adaptive-template-rendering}

自适应模板渲染提供了一种管理具有变体的页面的方法。 这项功能最初对于为移动设备提供各种HTML输出很有用（例如，功能手机和智能手机），当需要将体验交付到需要不同标记或HTML输出的各种设备时，这项功能会很有用。

## 概述 {#overview}

模板是围绕响应式网格构建的，基于这些模板创建的页面具有完全响应式，可自动根据客户端设备的视区进行调整。 使用页面编辑器中的模拟器工具栏，作者可以将布局定位到特定设备。

也可以设置模板以支持自适应渲染。 正确配置设备组后，在模拟器模式下选择设备时，页面将通过URL中的其他选择器呈现。 使用选择器，可通过URL直接调用特定页面渲染。

设置设备组时请记住：

* 每个设备必须至少位于一个设备组中。
* 一个设备可以位于多个设备组中。
* 由于设备可以位于多个设备组中，因此可以组合选择器。
* 选择器组合在存储库中保留时会自上而下评估。

>[!NOTE]
>
>设备组**响应式设备从不具有选择器，因为假定被识别为支持响应式设计的设备不需要自适应布局

## 配置 {#configuration}

自适应渲染选择器可以为现有设备组配置，也可以配置为 [您自己创建的组。](/help/sites-developing/mobile.md#device-groups)

在本例中，您将配置现有的设备组 **智能手机** 将自适应渲染选择器作为 **体验页面** We.Retail中的模板。

1. 在中编辑需要自适应选择器的设备组 `http://localhost:4502/miscadmin#/etc/mobile/groups`

   设置选项 **禁用模拟器** 并保存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 选择器可用于 **BlackBerry®** 和 **IPHONE 4** 已提供设备组 **智能手机** 会添加到模板和页面结构中。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRXDE Lite，通过将设备组添加到多值字符串属性，允许在模板上使用设备组 `cq:deviceGroups` 模板的结构中。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果要添加Smartphone设备组：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRXDE Lite，通过将设备组添加到多值字符串属性，允许该设备组在您的网站上使用 `cq:deviceGroups` 网站结构的信息。

   `/content/<your-site>/jcr:content`

   例如，如果要允许 **智能手机** 设备组：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

现在，使用 [模拟器](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) 在页面编辑器中(例如 [修改布局](/help/sites-authoring/responsive-layout.md))，并且您选择了所配置设备组中的设备，则页面将在URL中通过选择器呈现。

在本例中，当编辑基于 **体验页面** 模板，并在模拟器中选择iPhone 4，则会呈现页面，其中包括选择器，如 `arctic-surfing-in-lofoten.smart.html` 而不是 `arctic-surfing-in-lofoten.html`

也可以使用此选择器直接调用该页面。

![chlimage_1-161](assets/chlimage_1-161.png)
