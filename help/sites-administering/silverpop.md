---
title: 与Silverpop Engage集成
seo-title: Integrating with Silverpop Engage
description: 了解如何将AEM与Silverpop Engage集成
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# 与Silverpop Engage集成{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

通过将AEM与Silverpop Engage集成，您可以通过Silverpop管理和发送在AEM中创建的电子邮件。 它还允许您通过AEM页面上的AEM Forms使用Silverpop的销售线索管理功能。

该集成为您提供了以下功能：

* 能够在AEM中创建电子邮件并将其发布到Silverpop以供分发。
* 能够设置AEM表单的操作以创建Silverpop订阅服务器。

配置Silverpop Engage后，您可以将新闻稿或电子邮件发布到Silverpop Engage。

## 创建Silverpop配置 {#creating-a-silverpop-configuration}

Silverpop配置可以通过以下方式添加 **Cloud Services**， **工具**，或 **API端点**. 本节介绍了所有方法。

### 通过Cloud Services配置Silverpop {#configuring-silverpop-via-cloudservices}

要在Cloud Services中创建Silverpop配置，请执行以下操作：

1. 在AEM中，点按或单击 **工具** > **部署** > **Cloud Services**. (或直接访问 `https://<hostname>:<port>/etc/cloudservices.html`.)
1. 在第三方服务下，单击 **Silverop Engage** 然后 **配置**. 将打开Silverpop配置窗口。

   >[!NOTE]
   >
   >除非从包共享下载包，否则Silverpop Engage不作为第三方服务下的选项提供。

1. 输入标题和（可选）名称，然后单击 **创建**. 将打开** Silverpop设置**配置窗口。
1. 输入用户名、密码，然后从下拉列表中选择API端点。
1. 单击 **连接到Silverpop。** 成功连接后，您将看到成功对话框。 单击 **确定** 所以你离开窗口。 您可以通过单击转到Silverpop **转到Silverpop Engage**.
1. Silverpop已配置。 您可以通过单击来编辑配置 **编辑**.
1. 此外，还可以通过提供标题和名称（可选）为个性化操作配置Silverpop Engage框架。 单击“创建”为已配置的Silverpop连接成功创建框架。

   导入的数据扩展列以后可以通过AEM组件使用 —  **文本和个性化**.

### 通过工具配置Silverpop {#configuring-silverpop-via-tools}

要在工具中创建Silverpop配置，请执行以下操作：

1. 在AEM中，点按或单击 **工具** > **部署** > **Cloud Services**. 或直接导航到此处，转到 `https://<hostname>:<port>/misadmin#/etc`.
1. 选择 **工具**，则 **Cloud Services配置、** 则 **Silverpop Engage**.
1. 单击 **新**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 在 **创建页面** 窗口中，输入 **标题** 以及（可选） **名称**，然后单击 **创建**.
1. 按照上一过程中的步骤4输入配置信息。 请按照该过程操作，以便您能够完成Silverpop的配置。

### 添加多个配置 {#adding-multiple-configurations}

要添加多个配置，请执行以下操作：

1. 在欢迎页面上，单击 **Cloud Services** 并单击 **Silverpop Engage**. 单击 **显示配置** 一个或多个Silverpop配置可用时显示的按钮。 列出了所有可用的配置。
1. 单击 **+** 在“Available configurations（可用配置）”旁边签名。 它会打开 **创建配置** 窗口。 按照之前的配置过程操作，以便创建配置。

### 配置用于连接到Silverpop的API端点 {#configuring-api-end-points-for-connecting-to-silverpop}

目前，AEM有六个不安全的端点（参与1 - 6 ）。 Silverpop现在为现有端点提供两个新端点和已更改的连接端点。

要配置API端点，请执行以下操作：

1. 转到 `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` 日期 `https://<hostname>:<port>/crxde.`
1. 右键单击并选择 **创建**，则 **创建节点**.
1. 输入 **名称** 作为 `sp-e0` 并选择 **类型** 作为 `cq:Widget`.
1. 向新添加的节点添加两个属性：

   1. **名称**： `text`， **类型**： `String`， **值**： `Engage 0`
   1. **名称**： `value`， **类型**： `String`， **值**： `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   单击“全部保存”。

1. 使用以下方式创建另一个节点 **名称** 作为 `sp-e7` 和 **类型** 作为 `cq:Widget`.

   向新添加的节点添加两个属性：

   1. **名称**： `text`， **类型**： `String`， **值**： `Pilot`
   1. **名称**： `value`， **类型**： `String`， **值**： `https://apipilot.silverpop.com/XMLAPI`

1. 要更改现有API端点（参与1 - 6），请逐一单击每个端点，然后按以下方式替换值：

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
