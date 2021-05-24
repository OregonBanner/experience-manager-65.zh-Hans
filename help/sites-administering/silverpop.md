---
title: 与Silverpop Engage集成
seo-title: 与Silverpop Engage集成
description: 了解如何将AEM与Silverpop Engage集成
seo-description: 了解如何将AEM与Silverpop Engage集成
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 2%

---

# 与Silverpop Engage集成{#integrating-with-silverpop-engage}

>[!NOTE]
>
>Silverpop集成开箱即用，它&#x200B;**不**。 您必须从Package Share中下载[Silverpop集成包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content)，并将其安装到实例上。 安装包后，可以按照本文档中的说明对其进行配置。

将AEM与Silverpop Engage集成后，您可以通过Silverpop管理和发送在AEM中创建的电子邮件。 它还允许您通过AEM页面上的AEM表单来使用Silverpop的潜在客户管理功能。

该集成为您提供以下功能：

* 在AEM中创建电子邮件并将其发布到Silverpop以进行分发的功能。
* 能够设置AEM表单操作以创建Silverpop订阅者。

配置Silverpop Engage后，您可以将新闻稿或电子邮件发布到Silverpop Engage。

## 创建Silverpop配置{#creating-a-silverpop-configuration}

可以通过&#x200B;**Cloudservices**、**Tools**&#x200B;或&#x200B;**API端点**&#x200B;添加Silverpop配置。 本节将介绍所有方法。

### 通过Cloudservices配置Silverpop {#configuring-silverpop-via-cloudservices}

要在Cloud Services中创建Silverpop配置，请执行以下操作：

1. 在AEM中，点按或单击&#x200B;**工具** > **部署** > **Cloud Services**。 （或直接访问`https://<hostname>:<port>/etc/cloudservices.html`。）
1. 在第三方服务下，单击&#x200B;**Silverop Engage**，然后单击&#x200B;**配置**。 将打开Silverpop配置窗口。

   >[!NOTE]
   >
   >除非从包共享下载包，否则第三方服务下的选项将不提供Silverpop Engage。

1. 输入标题和名称（可选），然后单击&#x200B;**创建**。 将打开** Silverpop设置**配置窗口。
1. 输入用户名、密码，然后从下拉列表中选择一个API端点。
1. 单击&#x200B;**连接到Silverpop。** 成功连接后，您会看到一个成功对话框。单击&#x200B;**确定**&#x200B;退出窗口。 您可以通过单击&#x200B;**转到Silverpop Engage**&#x200B;来转到Silverpop。
1. Silverpop已配置。 您可以通过单击&#x200B;**Edit**&#x200B;来编辑配置。
1. 此外，还可以通过提供标题和名称（可选）为个性化操作配置Silverpop Engage框架。 单击创建将为已配置的Silverpop连接成功创建框架。

   导入的数据扩展列稍后可通过AEM组件 — **Text and Personalization**&#x200B;使用。

### 通过工具{#configuring-silverpop-via-tools}配置Silverpop

要在工具中创建Silverpop配置，请执行以下操作：

1. 在AEM中，点按或单击&#x200B;**工具** > **部署** > **Cloud Services**。 或直接导航到`https://<hostname>:<port>/misadmin#/etc`。
1. 选择&#x200B;**工具**，然后选择&#x200B;**Cloud Services配置，**，然后选择&#x200B;**Silverpop Engage**。
1. 单击&#x200B;**新建**&#x200B;以打开&#x200B;**创建页面**&#x200B;窗口。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 输入&#x200B;**标题**&#x200B;和（可选）**名称**，然后单击&#x200B;**创建**。
1. 按照上一步骤的步骤4中所述输入配置信息。 按照该步骤完成Silverpop的配置。

### 添加多个配置{#adding-multiple-configurations}

要添加多个配置，请执行以下操作：

1. 在欢迎页面上，单击&#x200B;**Cloud Services**，然后单击&#x200B;**Silverpop Engage**。 单击&#x200B;**显示配置**&#x200B;按钮，如果有一个或多个Silverpop配置可用，则会显示该按钮。 列出了所有可用配置。
1. 单击可用配置旁边的&#x200B;**+**&#x200B;符号。 此时将打开&#x200B;**创建配置**&#x200B;窗口。 按照上一配置过程创建新配置。

### 配置API端点以连接到Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

目前，AEM有六个不安全的端点（参与1到6）。 Silverpop现在提供两个新端点以及现有端点的更改连接端点。

要配置API端点，请执行以下操作：

1. 转到`https://<hostname>:<port>/crxde.`上的`/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node`
1. 右键单击并选择&#x200B;**创建**，然后选择&#x200B;**创建节点**。
1. 输入&#x200B;**名称**&#x200B;作为`sp-e0`，然后选择&#x200B;**类型**&#x200B;作为`cq:Widget`。
1. 向新添加的节点添加两个属性：

   1. **名称**: `text`，类 **型**: `String`,  **值**:  `Engage 0`
   1. **名称**: `value`，类 **型**: `String`,  **值**:  `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   单击“全部保存”按钮。

1. 再创建一个节点，其中&#x200B;**名称**&#x200B;为`sp-e7`,**类型**&#x200B;为`cq:Widget`。

   向新添加的节点添加两个属性：

   1. **名称**: `text`，类 **型**: `String`,  **值**:  `Pilot`
   1. **名称**: `value`，类 **型**: `String`,  **值**:  `https://apipilot.silverpop.com/XMLAPI`

1. 要更改现有API端点（参与1到6），请逐一单击每个端点并按如下方式替换值：

   | **节点名称** | **现有端点值** | **新的端点值** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. 单击&#x200B;**Save All**。 AEM现已准备好通过安全端点连接到Silverpop。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
