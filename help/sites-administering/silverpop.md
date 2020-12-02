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
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 2%

---


# 与Silverpop Engage集成{#integrating-with-silverpop-engage}

>[!NOTE]
>
>Silverpop集成&#x200B;**不**&#x200B;现成可用。 您必须从“包共享”下载[Silverpop集成包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content)并将其安装在实例上。 安装包后，可以按照本文档中的说明配置它。

通过将AEM与Silverpop Engage集成，您可以通过Silverpop管理和发送在AEM中创建的电子邮件。 它还允许您通过AEM表单在AEM页面上使用Silverpop的潜在客户管理功能。

该集成为您提供以下功能：

* 在AEM中创建电子邮件并将其发布到Silverpop进行分发的功能。
* 设置AEM表单操作以创建Silverpop订阅者的能力。

配置Silverpop Engage后，您可以将新闻稿或电子邮件发布到Silverpop Engage。

## 创建Silverpop配置{#creating-a-silverpop-configuration}

Silverpop配置可通过&#x200B;**Cloudservices**、**Tools**&#x200B;或&#x200B;**API端点**&#x200B;添加。 本节将介绍所有方法。

### 通过Cloudservices配置Silverpop {#configuring-silverpop-via-cloudservices}

要在Cloud Services中创建Silverpop配置：

1. 在AEM中，点按或单击&#x200B;**工具** > **部署** > **Cloud Services**。 （或直接访问`https://<hostname>:<port>/etc/cloudservices.html`。）
1. 在第三方服务下，单击&#x200B;**Silverop Engage**，然后单击&#x200B;**Configure**。 将打开Silverpop配置窗口。

   >[!NOTE]
   >
   >除非您从“包共享”下载包，否则第三方服务下的Silverpop Engage不提供。

1. 输入标题和（可选）名称，然后单击&#x200B;**创建**。 将打开** Silverpop设置**配置窗口。
1. 输入用户名、密码，并从下拉列表中选择API端点。
1. 单击&#x200B;**连接到Silverpop。** 成功连接后，您会看到一个成功对话框。单击&#x200B;**确定**&#x200B;退出窗口。 单击&#x200B;**转至Silverpop Engage**&#x200B;可转至Silverpop。
1. 已配置Silverpop。 单击&#x200B;**编辑**&#x200B;可编辑配置。
1. 此外，Silverpop Engage框架可通过提供标题和名称（可选）配置为个性化操作。 单击创建将成功为已配置的Silverpop连接创建框架。

   导入的数据扩展列稍后可通过AEM组件- **文本和个性化**&#x200B;使用。

### 通过工具{#configuring-silverpop-via-tools}配置Silverpop

要在“工具”中创建Silverpop配置，请执行以下操作：

1. 在AEM中，点按或单击&#x200B;**工具** > **部署** > **Cloud Services**。 或者，通过转到`https://<hostname>:<port>/misadmin#/etc`直接在那里导航。
1. 选择&#x200B;**工具**，然后选择&#x200B;**Cloud Services配置，**，然后选择&#x200B;**Silverpop Engage**。
1. 单击&#x200B;**新建**&#x200B;以打开&#x200B;**创建页面**&#x200B;窗口。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 输入&#x200B;**标题**&#x200B;和（可选）**名称**，然后单击&#x200B;**创建**。
1. 按照上一步中的步骤4中的概述输入配置信息。 按照该过程完成Silverpop的配置。

### 添加多个配置{#adding-multiple-configurations}

要添加多个配置，请执行以下操作：

1. 在欢迎页面上，单击&#x200B;**Cloud Services**&#x200B;并单击&#x200B;**Silverpop Engage**。 单击&#x200B;**显示配置**&#x200B;按钮，如果有一个或多个Silverpop配置可用，则显示该按钮。 列出所有可用配置。
1. 单击“Available configurations（可用配置）”旁边的&#x200B;**+**&#x200B;符号。 这将打开&#x200B;**创建配置**&#x200B;窗口。 按照上面的配置过程创建新配置。

### 配置API端点以连接到Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

目前，AEM有六个不安全的端点（1到6个）。 Silverpop现在提供两个新端点以及现有端点的更改连接端点。

配置API端点：

1. 转到`https://<hostname>:<port>/crxde.`上的`/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node`
1. 右键单击并选择&#x200B;**创建**，然后选择&#x200B;**创建节点**。
1. 输入&#x200B;**名称**&#x200B;作为`sp-e0`，然后选择&#x200B;**类型**&#x200B;作为`cq:Widget`。
1. 向新添加的节点添加两个属性：

   1. **名称**: `text`, **类型**: `String`, **值**:  `Engage 0`
   1. **名称**: `value`, **类型**: `String`, **值**:  `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   单击“全部保存”按钮。

1. 再创建一个&#x200B;**名称**&#x200B;为`sp-e7`的节点，**类型**&#x200B;为`cq:Widget`的节点。

   向新添加的节点添加两个属性：

   1. **名称**: `text`, **类型**: `String`, **值**:  `Pilot`
   1. **名称**: `value`, **类型**: `String`, **值**:  `https://apipilot.silverpop.com/XMLAPI`

1. 要更改现有API端点（参与1到6），请逐个单击其中每个端点，并按如下方式替换这些值：

   | **节点名称** | **现有端点值** | **新端点值** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. 单击&#x200B;**保存全部**。 AEM现在可以通过安全端点连接到Silverpop。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)

