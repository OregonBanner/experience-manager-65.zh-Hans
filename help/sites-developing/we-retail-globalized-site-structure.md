---
title: 试论We.Retail中的全球化网站结构
seo-title: 试论We.Retail中的全球化网站结构
description: 'null'
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 试论We.Retail中的全球化网站结构{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail是使用全球化的站点结构构建的，提供可实时复制到国家／地区特定网站的语言母版。 一切都是开箱即用设置，让您能够尝试此结构和内置的翻译功能。

## 试用 {#trying-it-out}

1. 从全局导航->站 **点中打开站点控制台**。
1. 切换到列视图（如果尚未激活），然后选择“We.Retail”。 请注意与瑞士、美国、法国等国一起沿用语言大师的国家结构示例。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 选择“瑞士”，查看该国语言的语言根源。 请注意，这些根下尚无任何内容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切换到列表视图，查看国家／地区的语言副本是所有Live Copy。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回列视图并单击“语言母版”，查看包含内容的语言母版根。 请注意，只有英语包含内容。

   We.Retail不附带任何翻译内容，但已准备好结构和配置，以便您展示翻译服务。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 选择“英语主页”后，在站点控制台中打 **开“引用** ”边栏，然后选择“语 **言副本”**。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾选“语言副本”标签旁 **的复选框** ，以选择所有语言副本。 在边栏 **的“更新语言副本** ”部分，选择“创建 **新翻译项目”选项**。 为项目提供名称，然后单击“更 **新”**。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 将为每个语言翻译创建一个项目。 在“导航”->“ **项目”下查看它们**。

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 单击“德语”可查看翻译项目的详细信息。 请注意，状态位于“草 **稿”中**。 要使用Microsoft的翻译服务开始翻译，请单击“翻译作业”标题旁的V形 **标记** ，然后选择“开 **始”**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻译项目开始。 单击卡底部标有“翻译作业”的省略号可查看详细信息。 状态为“准 **备审阅** ”的页面已由翻译服务翻译。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 选择列表中的某个页面，然后在工具栏中 **选择“在站点中预览** ”，将在页面编辑器中打开译文页面。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>此过程演示了与Microsoft机器翻译的内置集成。 使用 [AEM Translation Integration Framework](/help/sites-administering/translation.md)，您可以与许多标准翻译服务集成以编排AEM的翻译。

## 更多信息 {#further-information}

有关详细信息，请参阅创作文档多语 [言站点的翻译内容](/help/sites-administering/translation.md) ，以获取完整的技术详细信息。
