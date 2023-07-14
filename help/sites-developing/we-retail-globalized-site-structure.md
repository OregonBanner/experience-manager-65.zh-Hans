---
title: 在We.Retail中尝试全局化网站结构
description: 在We.Retail中尝试全局化网站结构
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 在We.Retail中尝试全局化网站结构{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail构建时采用了全球化网站结构，所提供的语言主控可以实时复制到国家/地区特定的网站。 所有这一切都是现成设置的，允许您试验此结构和内置的翻译功能。

## 正在尝试 {#trying-it-out}

1. 从打开站点控制台 **全局导航 — >站点**.
1. 切换到列视图（如果尚未激活）并选择We.Retail。 请注意示例国家/地区结构（瑞士、美国、法国等）以及主控语言。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 选择“瑞士”并查看该国家/地区的语言的语言根。 这些根目录下还没有任何内容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切换到列表视图，查看国家/地区的语言副本都是活动副本。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回列视图，单击语言主控，然后查看包含内容的语言主控根。 只有英语才有内容。

   We.Retail不提供任何翻译的内容，但已建立结构和配置以允许您演示翻译服务。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 选择“英语主控”后，打开 **引用** 站点控制台中的边栏并选择 **语言副本**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾选“ ”旁边的复选框 **语言副本** 标签以选择所有语言副本。 在 **更新语言副本** 部分，选择选项以 **创建新翻译项目**. 提供项目的名称，然后单击 **更新**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 将为每个语言翻译创建一个项目。 在下查看它们 **导航 — >项目**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 单击德语可查看翻译项目的详细信息。 状态为 **草稿**. 要使用Microsoft®的翻译服务开始翻译，请单击 **翻译作业** 标题并选择 **开始**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻译项目随即开始。 单击标有翻译作业的卡片底部的省略号可查看详细信息。 具有状态的页面 **准备审查** 已由翻译服务翻译。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 选择列表中的页面之一，然后 **在站点中预览** 在工具栏中，在页面编辑器中打开已翻译页面。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>此过程演示了与Microsoft®机器翻译的内置集成。 使用 [AEM翻译集成框架](/help/sites-administering/translation.md)，您可以将它与许多标准翻译服务集成以编排AEM的翻译。

## 更多信息 {#further-information}

有关更多信息，请参阅创作文档 [翻译多语言站点的内容](/help/sites-administering/translation.md) 了解完整的技术详细信息。
