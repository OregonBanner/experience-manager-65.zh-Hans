---
title: 为移动设备创作页面
description: 在创作移动设备页面时，页面会模拟移动设备的显示方式。 在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 11%

---

# 为移动设备创作页面{#authoring-a-page-for-mobile-devices}

在创作移动设备页面时，页面会模拟移动设备的显示方式。 在创作页面时，您可以在多个模拟器之间切换，以查看最终用户在访问页面时看到的内容。

根据设备渲染页面的功能，将设备分组为类别功能、智能和触控。 当最终用户访问移动页面时，AEM会检测设备并发送与其设备组对应的呈现形式。

>[!NOTE]
>
>要基于现有标准网站创建移动站点，请创建标准网站的Live Copy。 (请参阅 [为不同渠道创建Live Copy](/help/sites-administering/msm-livecopy.md).)
>
>AEM 开发人员可以创建新设备组。(请参阅 [创建设备组过滤器。](/help/sites-developing/groupfilters.md))

请使用以下过程来创作移动页面：

1. 在您的浏览器中，转到 **Siteadmin** 控制台。
1. 打开 **产品** 下面的页面 **网站** >> **Geometrixx移动演示网站** >> **英语**.

1. 切换到其他模拟器。 为此，您可以：

   * 单击页面顶部的设备图标。
   * 单击 **编辑** 按钮 **Sidekick** 并在下拉菜单中选择设备。

1. 拖放 **文本和图像** 组件。
1. 编辑组件并添加一些文本。 单击 **确定** 以保存更改。

页面外观与以下内容相同：

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>从移动设备中请求创作实例上的页面时，会禁用模拟器。然后，可以使用触屏优化UI完成创作。
