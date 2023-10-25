---
title: 在We.Retail中尝试全局化网站结构
description: 了解如何使用We.Retail在Adobe Experience Manager中尝试全局化网站结构。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 在We.Retail中尝试全局化网站结构{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail构建时采用了全球化网站结构，该结构提供了语言母版，可实时复制到特定于国家/地区的网站。 所有开箱即用的设置允许您试验此结构和内置翻译功能。

## 正在尝试 {#trying-it-out}

1. 从打开站点控制台 **全局导航 — >站点**.
1. 切换到列视图（如果尚未激活）并选择We.Retail。 请注意示例国家/地区结构（瑞士、美国、法国等）以及语言母版。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 选择瑞士，查看该国家/地区的语言的语言根。 这些根目录下还没有任何内容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切换到列表视图，查看国家/地区的语言副本是所有活动副本。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回到列视图，单击语言母版并查看包含内容的语言母版根。 只有英语才有内容。

   We.Retail不提供任何已翻译的内容，但其结构和配置已准备就绪，可让您演示翻译服务。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 选择英语母版后，打开 **引用** 站点控制台中的边栏并选择 **语言副本**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾选“ ”旁边的复选框 **语言副本** 标签以选择所有语言副本。 在 **更新语言副本** 部分，选择选项以 **创建新翻译项目**. 提供项目的名称，然后单击 **更新**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 为每个语言翻译创建一个项目。 在下查看它们 **导航 — >项目**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 单击德语以查看翻译项目的详细信息。 状态为 **草稿**. 要使用Microsoft®的翻译服务开始翻译，请单击 **翻译作业** 标题并选择 **开始**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻译项目随即开始。 单击标记为翻译作业的卡片底部的省略号可查看详细信息。 具有状态的页面 **准备好审查** 已由翻译服务翻译。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 选择列表中的某个页面，然后 **在站点中预览** 在工具栏中，在页面编辑器中打开已翻译页面。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>此过程演示了与Microsoft®机器翻译的内置集成。 使用 [AEM翻译集成框架](/help/sites-administering/translation.md)中，您可以将它与许多标准翻译服务集成以编排AEM的翻译。

## 更多信息 {#further-information}

有关详细信息，请参阅创作文档 [翻译多语言站点的内容](/help/sites-administering/translation.md) 以了解完整的技术详细信息。
