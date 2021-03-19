---
title: We.Retail中的全球化网站结构
seo-title: We.Retail中的全球化网站结构
description: We.Retail中的全球化网站结构
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# 在We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}中尝试全球化网站结构

We.Retail已构建为一个全球化的站点结构，提供可实时复制到特定国家/地区网站的语言主页。 一切都是开箱即用设置，让您能够尝试此结构和内置的翻译功能。

## 正在尝试{#trying-it-out}

1. 从&#x200B;**全局导航 — >站点**&#x200B;打开站点控制台。
1. 切换到列视图（如果尚未处于活动状态），然后选择We.Retail。 请注意瑞士、美国、法国等国在语言硕士课程旁边的国家结构示例。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 选择瑞士，查看该国语言的语言根源。 请注意，这些根下尚未包含任何内容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切换到“列表”视图并查看国家/地区的语言副本均为Live Copy。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回列视图并单击“语言主控”，查看包含内容的语言主控根。 请注意，只有英语包含内容。

   We.Retail不附带任何翻译内容，但已准备好结构和配置，以便您演示翻译服务。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 选择“英语”主控后，打开站点控制台中的&#x200B;**引用**&#x200B;边栏，然后选择&#x200B;**语言副本**。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾选&#x200B;**语言副本**&#x200B;标签旁边的复选框，以选择所有语言副本。 在边栏的&#x200B;**更新语言副本**&#x200B;部分，选择选项&#x200B;**创建新翻译项目**。 为项目提供名称，然后单击&#x200B;**更新**。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 将为每个语言翻译创建一个项目。 将它们视图到&#x200B;**导航 — >项目**&#x200B;下。

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 单击“德语”查看翻译项目的详细信息。 请注意，状态位于&#x200B;**草稿**&#x200B;中。 要将翻译与Microsoft的翻译服务开始，请单击&#x200B;**翻译作业**&#x200B;标题旁的V形标记，然后选择&#x200B;**开始**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻译项目开始。 单击卡底部标有“翻译作业”的省略号可查看详细信息。 状态为&#x200B;**准备审阅**&#x200B;的页面已由翻译服务翻译。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 在列表中选择一个页面，然后在工具栏的站点&#x200B;**中选择**&#x200B;预览，将在页面编辑器中打开已翻译的页面。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>此过程演示了与Microsoft机器翻译的内置集成。 使用[AEM Translation Integration Framework](/help/sites-administering/translation.md)，您可以与许多标准翻译服务集成以安排AEM的翻译。

## 更多信息 {#further-information}

有关详细的技术详细信息，请参阅创作文档[多语言站点内容翻译](/help/sites-administering/translation.md)。
