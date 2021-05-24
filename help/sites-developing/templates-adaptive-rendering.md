---
title: 自适应模板渲染
seo-title: 自适应模板渲染
description: 自适应模板渲染
seo-description: 'null'
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# 自适应模板渲染{#adaptive-template-rendering}

自适应模板渲染提供了一种管理页面及其变体的方法。 此功能最初对于为移动设备（例如功能手机和智能手机）交付各种HTML输出非常有用，但当需要将体验交付到需要不同标记或HTML输出的各种设备时，此功能非常有用。

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
>设备组&#x200B;**响应式设备**&#x200B;将永远没有选择器，因为被识别为支持响应式设计的设备假定不需要自适应布局

## 配置 {#configuration}

可以为现有设备组或您自己创建的[组配置自适应呈现选择器。](/help/sites-developing/mobile.md#device-groups)

对于此示例，我们将将现有设备组&#x200B;**智能手机**&#x200B;配置为在We.Retail的&#x200B;**体验页面**&#x200B;模板中具有自适应呈现选择器。

1. 编辑`http://localhost:4502/miscadmin#/etc/mobile/groups`中需要自适应选择器的设备组

   设置选项&#x200B;**禁用模拟器**&#x200B;并保存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 如果在以下步骤中将设备组&#x200B;**智能手机**&#x200B;添加到模板和页面结构中，则此选择器将可用于&#x200B;**Blackberry**&#x200B;和&#x200B;**iPhone 4**。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRX DE Lite，允许设备组在模板结构的多值字符串属性`cq:deviceGroups`中添加，以在模板上使用。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果我们想添加智能电话设备组：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRX DE Lite，允许设备组在您的站点上使用，方法是将设备组添加到站点结构上的多值字符串属性`cq:deviceGroups`。

   `/content/<your-site>/jcr:content`

   例如，如果我们要允许&#x200B;**智能电话**&#x200B;设备组：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

现在，当在页面编辑器中使用[emulator](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)时（例如在[修改布局](/help/sites-authoring/responsive-layout.md)时），并选择已配置设备组的设备时，页面将呈现为URL的一部分，并提供一个选择器。

在我们的示例中，当基于&#x200B;**体验页面**&#x200B;模板编辑页面并在模拟器中选择iPhone 4时，将呈现该页面，其中包括选择器`arctic-surfing-in-lofoten.smart.html`，而不是`arctic-surfing-in-lofoten.html`

也可以使用此选择器直接调用页面。

![chlimage_1-161](assets/chlimage_1-161.png)
