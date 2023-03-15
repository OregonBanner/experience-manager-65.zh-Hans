---
title: 与ExactTarget集成
seo-title: Integrating with ExactTarget
description: 了解如何将AEM与ExactTarget集成。
seo-description: Learn how to integrate AEM with ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 与ExactTarget集成{#integrating-with-exacttarget}

将AEM与Exact Target集成后，您可以通过Exact Target管理和发送在AEM中创建的电子邮件。 它还允许您通过AEM页面上的AEM Forms使用Exact Target的潜在客户管理功能。

该集成为您提供了以下功能：

* 能够在AEM中创建电子邮件并将其发布到Exact Target以供分发。
* 能够设置AEM表单的操作以创建Exact Target订阅服务器。

配置ExactTarget后，您可以将新闻稿或电子邮件发布到ExactTarget。 参见 [将新闻稿发布到电子邮件服务](/help/sites-authoring/personalization.md).

## 创建ExactTarget配置 {#creating-an-exacttarget-configuration}

可以通过Cloudservices或工具添加ExactTarget配置。 本节将介绍这两种方法。

### 通过Cloudservices配置ExactTarget {#configuring-exacttarget-via-cloudservices}

要在Cloud Services中创建ExactTarget配置，请执行以下操作：

1. 在欢迎页面上，单击 **Cloud Services**. (或直接访问 `https://<hostname>:<port>/etc/cloudservices.html`.)
1. 单击 **ExactTarget** 然后 **配置**. 将打开ExactTarget配置窗口。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 输入标题和（可选）名称，然后单击 **创建**. 此 **ExactTarget设置** 配置窗口打开。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 输入用户名、密码并选择API端点(例如， **https://webservice.exacttarget.com/Service.asmx**)。
1. 单击 **连接到ExactTarget。** 成功连接后，您将看到成功对话框。 单击 **确定** 以退出窗口。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 选择一个帐户（如果可用）。 该帐户适用于Enterprise 2.0客户。 单击&#x200B;**确定**。

   已配置ExactTarget。 您可以通过单击来编辑配置 **编辑**. 您可以通过单击转到ExactTarget **转到ExactTarget**.

1. AEM现在提供数据扩展功能。 您可以导入ExactTarget数据扩展列。 可以通过在成功创建的ExactTarget配置之外单击“+”号来配置此设置。 可以从下拉列表中选择任何现有数据扩展。 有关如何配置数据扩展的更多信息，请参阅 [ExactTarget文档](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships).

   导入的数据扩展列以后可以通过 **文本和个性化** 组件。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 通过工具配置ExactTarget {#configuring-exacttarget-via-tools}

要在工具中创建ExactTarget配置，请执行以下操作：

1. 在欢迎页面上，单击 **工具**. 或直接导航到此处，转到 `https://<hostname>:<port>/misadmin#/etc`.
1. 选择 **工具**，则 **Cloud Services配置、** 则 **ExactTarget**.
1. 单击 **新** 打开**创建页面**窗口。

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. 输入 **标题** 以及（可选） **名称**，然后单击 **创建**.
1. 按照上一过程中的步骤4输入配置信息。 按照该过程完成配置ExactTarget。

### 添加多个配置 {#adding-multiple-configurations}

要添加多个配置，请执行以下操作：

1. 在欢迎页面上，单击 **Cloud Services** 并单击 **ExactTarget**. 单击 **显示配置** 一个或多个ExactTarget配置可用时显示的按钮。 列出了所有可用的配置。
1. 单击 **+** 在“Available configurations（可用配置）”旁边签名。 这将打开 **创建配置** 窗口。 按照之前的配置过程创建新配置。
