---
title: 与Silverpop Engage集成
description: 了解如何将Adobe Experience Manager与Silverpop Engage集成。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# 与Silverpop Engage集成{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. Download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

将AEM与Silverpop Engage集成后，您可以通过Silverpop管理和发送在AEM中创建的电子邮件。 它还允许您通过AEM页面上的AEM表单使用Silverpop的潜在客户管理功能。

该集成提供了以下功能：

* 能够在AEM中创建电子邮件并将其发布到Silverpop以供分发。
* 能够设置AEM表单的操作以创建Silverpop订阅服务器。

配置Silverpop Engage后，您可以将新闻稿或电子邮件发布到Silverpop Engage。

## 创建Silverpop配置 {#creating-a-silverpop-configuration}

Silverpop配置可以通过以下方式添加 **Cloud Service**， **工具**，或 **API端点**. 本节介绍了所有方法。

### 通过Cloud Service配置Silverpop {#configuring-silverpop-via-cloudservices}

要在Cloud Service中创建Silverpop配置，请执行以下操作：

1. 在AEM中，单击 **工具** > **部署** > **Cloud Service**. (或直接访问 `https://<hostname>:<port>/etc/cloudservices.html`.)
1. 在第三方服务下，单击 **Silverop Engage** 然后 **配置**. 将打开Silverpop配置窗口。

   >[!NOTE]
   >
   >除非从包共享下载包，否则Silverpop Engage在第三方服务下不可用。

1. 输入标题和（可选）名称，然后单击 **创建**. 将打开** Silverpop设置**配置窗口。
1. 输入用户名、密码，然后从下拉列表中选择一个API端点。
1. 单击 **连接到Silverpop。** 成功连接后，您会看到一个成功对话框。 单击 **确定** 所以你离开窗户。 您可以通过单击转到Silverpop **转到Silverpop Engage**.
1. Silverpop已配置。 您可以通过单击来编辑配置 **编辑**.
1. 此外，还可以通过提供标题和名称（可选）为个性化操作配置Silverpop Engage框架。 单击“创建”为已配置的Silverpop连接成功创建框架。

   导入的数据扩展列以后可以通过AEM组件使用 —  **文本和个性化**.

### 通过工具配置Silverpop {#configuring-silverpop-via-tools}

在工具中创建Silverpop配置：

1. 在AEM中，单击 **工具** > **部署** > **Cloud Service**. 或直接导航到此处，转到 `https://<hostname>:<port>/misadmin#/etc`.
1. 选择 **工具**，则 **Cloud Service配置，** 则 **Silverpop Engage**.
1. 单击 **新建**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 在 **创建页面** 窗口，输入 **标题** 和（可选） **名称**，然后单击 **创建**.
1. 按照上一过程中的步骤4输入配置信息。 请按照该过程操作，以便完成Silverpop的配置。

### 添加多个配置 {#adding-multiple-configurations}

要添加多个配置，请执行以下操作：

1. 在欢迎页面上，单击 **Cloud Service** 并单击 **Silverpop Engage**. 单击 **显示配置** 当一个或多个Silverpop配置可用时显示的按钮。 列出了所有可用的配置。
1. 单击 **+** 在“Available configurations（可用配置）”旁边签名。 它会打开 **创建配置** 窗口。 按照之前的配置过程操作，以便创建配置。

### 配置用于连接到Silverpop的API端点 {#configuring-api-end-points-for-connecting-to-silverpop}

目前，AEM有六个不安全的端点（参与1 - 6）。 Silverpop现在为现有端点提供两个新的端点并更改连接端点。

要配置API端点，请执行以下操作：

1. 转到 `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` 日期 `https://<hostname>:<port>/crxde.`
1. 右键单击并选择 **创建**，则 **创建节点**.
1. 输入 **名称** 作为 `sp-e0` 并选择 **类型** 作为 `cq:Widget`.
1. 向新添加的节点添加两个属性：

   1. **名称**： `text`， **类型**： `String`， **值**： `Engage 0`
   1. **名称**： `value`， **类型**： `String`， **值**： `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   单击“全部保存”。

1. 创建另一个节点，使用 **名称** 作为 `sp-e7` 和 **类型** 作为 `cq:Widget`.

   向新添加的节点添加两个属性：

   1. **名称**： `text`， **类型**： `String`， **值**： `Pilot`
   1. **名称**： `value`， **类型**： `String`， **值**： `https://apipilot.silverpop.com/XMLAPI`

1. 要更改现有API端点（参与1 - 6），请逐一单击每个端点，然后替换相应值，如下所示：

   | **节点名称** | **现有端点值** | **新端点值** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. 单击 **全部保存**. AEM现在已准备好通过安全的端点连接到Silverpop。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
