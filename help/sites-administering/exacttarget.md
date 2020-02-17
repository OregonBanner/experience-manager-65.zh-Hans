---
title: 与ExactTarget集成
seo-title: 与ExactTarget集成
description: 了解如何将AEM与ExactTarget集成。
seo-description: 了解如何将AEM与ExactTarget集成。
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2

---


# 与ExactTarget集成{#integrating-with-exacttarget}

将AEM与Exact target集成后，您可以通过Exact target管理和发送在AEM中创建的电子邮件。 它还允许您通过AEM页面上的AEM表单使用ExactTarget的潜在客户管理功能。

该集成为您提供以下功能：

* 在AEM中创建电子邮件并将其发布到ExactTarget进行分发的功能。
* 设置AEM表单操作以创建ExactTarget订阅者的功能。

配置ExactTarget后，您可以将Newsletter或电子邮件发布到ExactTarget。 请参 [阅将新闻稿发布到电子邮件服务](/help/sites-authoring/personalization.md)。

## 创建ExactTarget配置 {#creating-an-exacttarget-configuration}

ExactTarget配置可通过Cloudservices或工具添加。 本节将介绍这两种方法。

### 通过Cloudservices配置ExactTarget {#configuring-exacttarget-via-cloudservices}

在云服务中创建ExactTarget配置：

1. 在欢迎页面上，单击“ **云服务”**。 (或直接访问 `https://<hostname>:<port>/etc/cloudservices.html`。)
1. 单击 **ExactTarget** ，然后单 **击配置**。 ExactTarget配置窗口将打开。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Enter a title and optionally, a name and click **Create**. ExactTarget **设置配置窗口** 即会打开。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 输入用户名、密码并选择API端点(例如， **https://webservice.exacttarget.com/Service.asmx**)。
1. 单击 **“连接到ExactTarget”。** 成功连接后，您会看到一个成功对话框。 单击 **确定** ，以退出窗口。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 选择帐户（如果有）。 此帐户适用于Enterprise 2.0客户。 单击&#x200B;**确定**。

   ExactTarget已配置。 您可以通过单击编辑来编辑 **配置**。 单击转到ExactTarget，即可转 **到ExactTarget**。

1. AEM现在提供数据扩展功能。 您可以导入ExactTarget数据扩展列。 可通过单击“+”符号进行配置，该符号除成功创建ExactTarget配置外，还显示。 可以从下拉列表中选择任何现有的数据扩展。 有关如何配置数据扩展的详细信息，请参阅 [ExactTarget文档](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships)。

   导入的数据扩展列稍后可以通过文本和个 **性化组件使用** 。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 通过工具配置ExactTarget {#configuring-exacttarget-via-tools}

要在工具中创建ExactTarget配置，请执行以下操作：

1. 在欢迎页面上，单击“工 **具”**。 或者，通过转到直接导航到该位置 `https://<hostname>:<port>/misadmin#/etc`。
1. 依次选择 **工具**、云服 **务配置、** ExactTarget **和Cloud Services Configurations**。
1. Click **New** to open the **Create Page **window.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Enter the **Title** and optionally the **Name**, and click **Create**.
1. 按照上一步骤中的步骤4中所述输入配置信息。 按照该过程完成ExactTarget的配置。

### 添加多个配置 {#adding-multiple-configurations}

要添加多个配置：

1. 在欢迎页面上，单击“云 **服务”** ，然后单 **击ExactTarget**。 单击“显 **示配置** ”按钮，如果有一个或多个ExactTarget配置可用，则显示该按钮。 将列出所有可用配置。
1. 单击“ **可用** ”配置旁的+符号。 这将打开“创 **建配置** ”窗口。 请按照之前的配置过程创建新配置。