---
title: 自适应模板渲染
seo-title: 自适应模板渲染
description: 'null'
seo-description: 'null'
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 自适应模板渲染{#adaptive-template-rendering}

自适应模板渲染提供了一种管理具有变体的页面的方法。 该功能最初可用于为移动设备（例如功能电话与智能电话）提供各种HTML输出，当需要将体验交付到需要不同标记或HTML输出的各种设备时，此功能非常有用。

## 概述 {#overview}

模板通常围绕响应式网格构建，基于这些模板创建的页面完全响应式，自动调整到客户端设备的视口。 使用页面编辑器中的模拟器工具栏，作者可以将布局定向到特定设备。

还可以设置模板以支持自适应渲染。 正确配置设备组后，当在模拟器模式中选择设备时，该页面将在URL中使用其他选择器呈现。 使用选择器，可以通过URL直接调用特定页面呈现。

在设置设备组时，请记住：

* 每个设备必须位于至少一个设备组中。
* 一个设备可以位于多个设备组中。
* 由于设备可以位于多个设备组中，因此可以组合选择器。
* 选择器组合将从上到下评估，因为它们会保留在存储库中。

>[!NOTE]
>
>设备组响 **应式设备** ，永远不会有选择器，因为那些被识别为支持响应式设计的设备假定不需要自适应布局

## 配置 {#configuration}

可以为现有设备组或您自己创建的组 [配置自适应渲染选择器。](/help/sites-developing/mobile.md#device-groups)

在此示例中，我们将配置现有设备组 **Smart Phone****** ，使其具有自适应渲染选择器，作为We.Retail中“体验页面”模板的一部分。

1. 编辑需要自适应选择器的设备组，请参阅 `http://localhost:4502/miscadmin#/etc/mobile/groups`

   设置“禁用模 **拟器** ”选项并保存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 选择器将可用于 **Blackberry** 和 **iPhone 4** ，前提是通过以下步骤将设备组 **Smart Phone** 添加到模板和页面结构。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRX DE Lite，通过将设备组添加到模板结构上的多值字符串属性中，允许在模板 `cq:deviceGroups` 上使用设备组。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果我们希望添加Smart Phone设备组：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRX DE Lite，通过将设备组添加到站点结构上的多值字符串属性中，允许在您的站 `cq:deviceGroups` 点上使用设备组。

   `/content/<your-site>/jcr:content`

   例如，如果我们要允许 **Smart Phone** device group:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

现在，在页 [面编辑器中使用模拟器](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) (例如，修改布局时 [](/help/sites-authoring/responsive-layout.md))并选择所配置设备组的设备时，页面将呈现为URL的一部分，其中包含一个选择器。

在我们的示例中，在基于 **Experience Page模板编辑页面并在模拟器中选择iPhone** 4时，将呈现该页面，其中包括选择器，而 `arctic-surfing-in-lofoten.smart.html` 不是 `arctic-surfing-in-lofoten.html`

也可以使用此选择器直接调用页面。

![chlimage_1-161](assets/chlimage_1-161.png)

