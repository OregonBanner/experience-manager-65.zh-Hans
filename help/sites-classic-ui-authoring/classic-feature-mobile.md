---
title: 创作适用于移动设备的页面
seo-title: Authoring a Page for Mobile Devices
description: 在创作移动页面时，页面会以模拟移动设备的方式显示。在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。
seo-description: When authoring a mobile page, the page is displayed in a way that emulates the mobile device. When authoring the page, you can switch between several emulators to see what the end-user sees when accessing the page.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 82%

---

# 创作适用于移动设备的页面{#authoring-a-page-for-mobile-devices}

在创作移动页面时，页面会以模拟移动设备的方式显示。在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。

根据设备呈现页面的功能，设备分为功能、智能和触控三个类别。当最终用户访问移动页面时，AEM 会检测设备并发送与其设备组对应的演绎版。

>[!NOTE]
>
>要创建基于现有标准站点的移动站点，请创建标准站点的 Live Copy。(请参阅 [为不同渠道创建Live Copy](/help/sites-administering/msm-livecopy.md).)
>
>AEM 开发人员可以创建新设备组。(请参阅 [创建设备组过滤器。](/help/sites-developing/groupfilters.md))

请使用以下过程来创作移动页面：

1. 在您的浏览器中，转到 **Siteadmin** 控制台。
1. 打开 **产品** 下面的页面 **网站** >> **Geometrixx移动演示网站** >> **英语**.

1. 切换到其他模拟器。要实现此操作，您可以：

   * 单击页面顶部的设备图标。
   * 单击 **Sidekick** 中的&#x200B;**编辑**&#x200B;按钮并从下拉菜单中选择设备。

1. 拖放 **文本和图像** 组件。
1. 编辑组件并添加一些文本。单击&#x200B;**确定**&#x200B;以保存更改。

页面外观如下所示：

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>从移动设备中请求创作实例上的页面时，会禁用模拟器。然后，可以使用触屏优化UI完成创作。
