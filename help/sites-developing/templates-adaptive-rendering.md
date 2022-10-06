---
title: 自适应模板渲染
seo-title: Adaptive Template Rendering
description: 自适应模板渲染
seo-description: null
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 自适应模板渲染{#adaptive-template-rendering}

自适应模板渲染提供了一种管理页面及其变体的方法。 此功能最初可用于为移动设备（例如功能电话和智能电话）交付各种HTML输出，但当需要将体验交付到需要不同标记或HTML输出的各种设备时，此功能非常有用。

## 概述 {#overview}

模板通常围绕响应式网格构建，并且基于这些模板创建的页面是完全响应的，可根据客户端设备的视区自动调整。 使用页面编辑器中的模拟器工具栏，作者可以将布局定位到特定设备。

还可以设置模板以支持自适应渲染。 正确配置设备组后，当在模拟器模式下选择设备时，页面将在URL中以不同的选择器呈现。 使用选择器，可以通过URL直接调用特定页面渲染。

在设置设备组时请记住：

* 每个设备必须至少位于一个设备组中。
* 设备可以位于多个设备组中。
* 由于设备可以位于多个设备组中，因此可以组合选择器。
* 选择器组合会从上到下进行评估，因为它们会保留在存储库中。

>[!NOTE]
>
>设备组 **响应式设备** 将永远没有选择器，因为被识别为支持响应式设计的设备假定不需要自适应布局

## 配置 {#configuration}

可以为现有设备组配置自适应渲染选择器，或者 [您自己创建的组。](/help/sites-developing/mobile.md#device-groups)

在本例中，我们将配置现有设备组 **智能手机** 以在 **体验页面** 模板。

1. 在中编辑需要自适应选择器的设备组 `http://localhost:4502/miscadmin#/etc/mobile/groups`

   设置选项 **禁用模拟器** 并保存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 选择器将可用于 **Blackberry** 和 **iPhone 4** 提供了设备组 **智能手机** 将添加到模板和页面结构中。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRX DE Lite，通过将设备组添加到多值字符串属性中，来允许在模板上使用设备组 `cq:deviceGroups` 在模板的结构中。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果我们想添加智能电话设备组：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRX DE Lite，通过将设备组添加到多值字符串属性中来允许在您的网站上使用设备组 `cq:deviceGroups` 在您网站的结构中。

   `/content/<your-site>/jcr:content`

   例如，如果我们希望允许 **智能手机** 设备组：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

现在，当使用 [模拟器](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) (例如， [修改布局](/help/sites-authoring/responsive-layout.md))后，您将选择已配置设备组的设备，页面将会呈现为URL的一部分并带有一个选择器。

在本例中，根据 **体验页面** 模板，并在模拟器中选择iPhone 4，此时将呈现页面，其中包括选择器作为 `arctic-surfing-in-lofoten.smart.html` 而不是 `arctic-surfing-in-lofoten.html`

也可以使用此选择器直接调用页面。

![chlimage_1-161](assets/chlimage_1-161.png)
