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
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# 与ExactTarget集成{#integrating-with-exacttarget}

通过将AEM与Exact Target集成，您可以通过Exact Target管理和发送在AEM中创建的电子邮件。 它还允许您通过AEM页面上的AEM表单来使用Exact Target的潜在客户管理功能。

该集成为您提供以下功能：

* 能够在AEM中创建电子邮件并将其发布到Exact Target以进行分发。
* 能够设置AEM表单操作以创建Exact Target订阅者。

配置ExactTarget后，您可以将Newsletter或电子邮件发布到ExactTarget。 请参阅[将Newsletter发布到电子邮件服务](/help/sites-authoring/personalization.md)。

## 创建ExactTarget配置{#creating-an-exacttarget-configuration}

可以通过Cloudservices或“工具”添加ExactTarget配置。 本节将介绍这两种方法。

### 通过Cloudservices配置ExactTarget {#configuring-exacttarget-via-cloudservices}

要在Cloud Services中创建ExactTarget配置，请执行以下操作：

1. 在欢迎页面上，单击&#x200B;**Cloud Services**。 （或直接访问`https://<hostname>:<port>/etc/cloudservices.html`。）
1. 单击&#x200B;**ExactTarget**，然后单击&#x200B;**配置**。 ExactTarget配置窗口将打开。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 输入标题和名称（可选），然后单击&#x200B;**创建**。 将打开&#x200B;**ExactTarget设置**&#x200B;配置窗口。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 输入用户名、密码并选择API端点(例如，**https://webservice.exacttarget.com/Service.asmx**)。
1. 单击&#x200B;**连接到ExactTarget。** 成功连接后，您会看到一个成功对话框。单击&#x200B;**确定**&#x200B;退出窗口。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 选择一个帐户（如果可用）。 该帐户适用于Enterprise 2.0客户。 单击&#x200B;**确定**。

   已配置ExactTarget。 您可以通过单击&#x200B;**Edit**&#x200B;来编辑配置。 您可以通过单击&#x200B;**转到ExactTarget**&#x200B;来转到ExactTarget。

1. AEM现在提供了数据扩展功能。 您可以导入ExactTarget数据扩展列。 除了成功创建ExactTarget配置外，还可通过单击显示“+”号来配置此配置。 可以从下拉列表中选择任何现有的数据扩展。 有关如何配置数据扩展的更多信息，请参阅[ExactTarget文档](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships)。

   导入的数据扩展列稍后可通过&#x200B;**Text and Personalization**&#x200B;组件使用。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 通过工具{#configuring-exacttarget-via-tools}配置ExactTarget

要在工具中创建ExactTarget配置，请执行以下操作：

1. 在欢迎页面上，单击&#x200B;**工具**。 或直接导航到`https://<hostname>:<port>/misadmin#/etc`。
1. 选择&#x200B;**工具**，然后选择&#x200B;**Cloud Services配置，**，然后选择&#x200B;**ExactTarget**。
1. 单击&#x200B;**New**&#x200B;以打开**创建页面**窗口。

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. 输入&#x200B;**标题**&#x200B;和（可选）**名称**，然后单击&#x200B;**创建**。
1. 按照上一步骤的步骤4中所述输入配置信息。 按照该过程完成ExactTarget的配置。

### 添加多个配置{#adding-multiple-configurations}

要添加多个配置，请执行以下操作：

1. 在欢迎页面上，单击&#x200B;**Cloud Services** ，然后单击&#x200B;**ExactTarget**。 单击&#x200B;**显示配置**&#x200B;按钮，如果有一个或多个ExactTarget配置可用，则会显示该按钮。 列出了所有可用配置。
1. 单击可用配置旁边的&#x200B;**+**&#x200B;符号。 此时将打开&#x200B;**创建配置**&#x200B;窗口。 按照上一配置过程创建新配置。
