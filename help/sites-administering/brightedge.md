---
title: 与BrightEdge Content Optimizer集成
description: 了解如何将AEM与BrightEdge Content Optimizer集成。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f14cc5fd-aeab-4619-b926-b6f1df7e50e5
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# 与BrightEdge Content Optimizer集成{#integrating-with-brightedge-content-optimizer}

创建BrightEdge云配置，以便AEM可以使用您的BrightEdge帐户的凭据进行连接。 如果使用多个帐户，可以创建多个配置。

在创建配置时，需要指定标题。 标题应为描述性的，以便用户能够将配置与BrightEdge帐户关联。 当页面作者或管理员将网页与BrightEdge帐户关联时，此标题将显示在下拉列表中。

1. 在边栏中，单击“工具” > “操作” > “云” > “Cloud Service” 。
1. 单击BrightEdge Content Optimizer部分中显示的链接。 是否已创建BrightEdge配置将决定链接文本：

   * 立即配置：当尚未创建任何配置时，将显示此链接。
   * 显示配置：创建一个或多个配置后，将显示此链接。

   ![chlimage_1-4](assets/chlimage_1-4a.png)

1. 如果单击显示配置，则单击可用配置旁边的+链接。
1. 键入配置的标题。 （可选）键入用于将配置存储在存储库中的节点的名称。 单击“创建”。
1. 在“BrightEdge Content Optimizer配置”对话框中，键入BrightEdge帐户的用户名和密码，然后单击“确定”。

## 编辑BrightEdge配置 {#editing-a-brightedge-configuration}

根据需要修改BrightEdge配置的用户名和密码。 修改将影响使用该配置的所有页面。

1. 在边栏中，单击“工具” > “操作” > “云” > “Cloud Service” 。
1. 在BrightEdge Content Optimizer部分中，单击显示配置。

   ![chlimage_1-5](assets/chlimage_1-5a.png)

1. 单击要编辑的配置名称。
1. 单击“编辑”，修改属性值，然后单击“确定”。

## 将页面与BrightEdge配置关联 {#associating-pages-with-a-brightedge-configuration}

将页面与BrightEdge配置关联以将页面数据发送到BrightEdge服务进行分析。 将页面与配置关联时，子页面将继承关联。 通常，您需要关联网站的主页，以便将所有页面中的数据发送到BrightEdge。

1. 打开经典“网站”控制台。 ([http://localhost:4502/siteadmin#/content](http://localhost:4502/siteadmin#/content))
1. 在网站树中，选择包含要与BrightEdge配置关联的页面的文件夹或页面。
1. 在页面列表中，右键单击要配置的页面，然后单击“属性”。
1. 在“Cloud Service”选项卡上，单击“添加服务”按钮，在“Cloud Service”对话框中，选择BrightEdge Content Optimizer ，然后单击“确定”。
1. 在BrightEdge Content Optimizer列表中，选择要与页面关联的BrightEdge配置，然后单击“确定”。

   ![chlimage_1-6](assets/chlimage_1-6a.png)

## 激活BrightEdge配置 {#activating-a-brightedge-configuration}

激活BrightEdge配置以将其复制到发布实例上，并使已发布的页面能够与BrightEdge服务交互。

1. 在边栏上，单击站点，然后浏览并选择与BrightEdge配置关联的页面。
1. 单击“发布”图标，然后单击“发布”。

   ![chlimage_1-7](assets/chlimage_1-7a.png)

1. 在显示的配置列表中，确保已选择BrightEdge配置，然后单击“发布”。

   ![chlimage_1-8](assets/chlimage_1-8a.png)
