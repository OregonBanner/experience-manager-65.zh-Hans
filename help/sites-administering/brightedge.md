---
title: 与BrightEdge Content Optimizer集成
seo-title: 与BrightEdge Content Optimizer集成
description: 了解如何将AEM与BrightEdge Content Optimizer集成。
seo-description: 了解如何将AEM与BrightEdge Content Optimizer集成。
uuid: 7075dd3c-2fd6-4050-af1c-9b16ad4366ec
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: cf25c9a8-0555-4c67-8aa5-55984fd8d301
exl-id: f14cc5fd-aeab-4619-b926-b6f1df7e50e5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 与BrightEdge Content Optimizer集成{#integrating-with-brightedge-content-optimizer}

创建BrightEdge云配置，以便AEM可以使用您BrightEdge帐户的凭据进行连接。 如果您使用多个帐户，则可以创建多个配置。

创建配置时，需指定标题。 标题应当具有描述性，以便用户可以将配置与BrightEdge帐户关联。 当页面作者或管理员将网页与BrightEdge帐户关联时，此标题会显示在下拉列表中。

1. 在边栏中，单击工具>操作>云>Cloud Services。
1. 单击BrightEdge Content Optimizer部分中显示的链接。 是否已创建BrightEdge配置确定链接文本：

   * 立即配置：未创建配置时，将显示此链接。
   * 显示配置：创建一个或多个配置后，将显示此链接。

   ![chlimage_1-4](assets/chlimage_1-4a.png)

1. 如果单击显示配置，请单击可用配置旁边的+链接。
1. 键入配置的标题。 （可选）键入用于在存储库中存储配置的节点名称。 单击创建。
1. 在BrightEdge Content Optimizer的“配置”对话框中，键入BrightEdge帐户的用户名和密码，然后单击“确定”。

## 编辑BrightEdge配置{#editing-a-brightedge-configuration}

根据需要修改BrightEdge配置的用户名和密码。 修改会影响使用配置的所有页面。

1. 在边栏中，单击工具>操作>云>Cloud Services。
1. 在BrightEdge Content Optimizer部分中，单击显示配置。

   ![chlimage_1-5](assets/chlimage_1-5a.png)

1. 单击要编辑的配置的名称。
1. 单击编辑，修改属性值，然后单击确定。

## 将页面与BrightEdge配置{#associating-pages-with-a-brightedge-configuration}关联

将页面与BrightEdge配置关联，以将页面数据发送到BrightEdge服务进行分析。 将页面与配置关联后，子页面将继承关联。 通常，您会关联网站的主页，以便将所有页面的数据发送到BrightEdge。

1. 打开经典的网站控制台。 ([http://localhost:4502/siteadmin#/content](http://localhost:4502/siteadmin#/content))
1. 在“网站”树中，选择包含要与BrightEdge配置关联的页面的文件夹或页面。
1. 在页面列表中，右键单击要配置的页面，然后单击属性。
1. 在“Cloud Services”选项卡上，单击“添加服务”按钮，然后在“Cloud Services”对话框中选择“BrightEdge Content Optimizer”，然后单击“确定”。
1. 在BrightEdge Content Optimizer列表中，选择要与页面关联的BrightEdge配置，然后单击“确定”。

   ![chlimage_1-6](assets/chlimage_1-6a.png)

## 激活BrightEdge配置{#activating-a-brightedge-configuration}

激活BrightEdge配置以在发布实例上复制该配置，并使已发布的页面能够与BrightEdge服务进行交互。

1. 在边栏中，单击站点，然后浏览到与BrightEdge配置关联的页面并将其选中。
1. 单击或点按发布图标，然后单击或点按发布。

   ![chlimage_1-7](assets/chlimage_1-7a.png)

1. 在显示的配置列表中，确保选择您的BrightEdge配置，然后单击“发布”。

   ![chlimage_1-8](assets/chlimage_1-8a.png)
