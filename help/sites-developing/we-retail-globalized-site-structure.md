---
title: 在We.Retail中尝试全球化网站结构
seo-title: 在We.Retail中尝试全球化网站结构
description: 在We.Retail中尝试全球化网站结构
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 在We.Retail中尝试全球化站点结构{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail是通过全球化的站点结构构建的，其中提供了语言母版，可以实时复制到特定于国家/地区的网站。 所有内容都设置为开箱即用，让您能够尝试使用此结构和内置翻译功能。

## 尝试{#trying-it-out}

1. 从&#x200B;**全局导航 — >站点**&#x200B;中打开站点控制台。
1. 切换到列视图（如果尚未处于活动状态），然后选择We.Retail。 请注意与瑞士、美国、法国等国一起在语言硕士课程旁边的国家结构示例。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 选择瑞士，查看该国语言的语言根源。 请注意，这些根下尚未有任何内容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切换到列表视图，然后查看国家/地区的语言副本是所有Live Copy。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回到列视图并单击“语言主控”，并查看包含内容的语言主控根。 请注意，只有英语包含内容。

   We.Retail不提供任何翻译内容，但已设置结构和配置，以便您演示翻译服务。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 选择“英语”主控后，打开站点控制台中的&#x200B;**References**&#x200B;边栏，然后选择&#x200B;**语言副本**。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾选&#x200B;**语言副本**&#x200B;标签旁边的复选框以选择所有语言副本。 在边栏的&#x200B;**更新语言副本**&#x200B;部分中，选择选项&#x200B;**创建新的翻译项目**。 为项目提供名称，然后单击&#x200B;**更新**。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 将为每个语言翻译创建一个项目。 在&#x200B;**导航 — >项目**&#x200B;下查看它们。

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 单击德语可查看翻译项目的详细信息。 请注意，状态为&#x200B;**Draft**。 要使用Microsoft的翻译服务开始翻译，请单击&#x200B;**翻译作业**&#x200B;标题旁边的V形标记，然后选择&#x200B;**开始**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 将启动翻译项目。 单击卡片底部标有“翻译作业”的省略号可查看详细信息。 状态为&#x200B;**准备审阅**&#x200B;的页面已被翻译服务翻译。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 选择列表中的其中一个页面，然后在工具栏中选择&#x200B;**在站点中预览** ，会在页面编辑器中打开翻译的页面。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>此过程演示了与Microsoft机器翻译的内置集成。 使用[AEM翻译集成框架](/help/sites-administering/translation.md)，您可以与许多标准翻译服务集成以编排AEM的翻译。

## 更多信息 {#further-information}

有关更多信息，请参阅创作文档[多语言站点的翻译内容](/help/sites-administering/translation.md) ，以获取完整的技术详细信息。
