---
title: 使用IMS与Adobe Analytics集成
description: 了解如何使用IMS将AEM与Adobe Analytics集成
exl-id: 2833a6df-ef32-48ab-8395-0f26816f8443
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 55%

---


# 使用IMS与Adobe Analytics集成 {#integration-with-adobe-analytics-using-ims}

通过Analytics Standard API将AEM与Adobe Analytics集成需要使用Adobe Developer控制台配置Adobe IMS (Identity Management System)。

>[!NOTE]
>
>AEM 6.5.12.0中新增了对Adobe Analytics Standard API 2.0的支持。此版本的API支持IMS身份验证。
>
>为了向后兼容，仍支持在AEM中使用Adobe Analytics Classic API 1.4。 此 [Analytics Classic API使用用户凭据](/help/sites-administering/adobeanalytics-connect.md).
>
>API 选择由用于 AEM/Analytics 集成的身份验证方法驱动。
>
>[迁移到 2.0 API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/) 下还提供了更多信息。

## 前提条件 {#prerequisites}

开始此过程之前：

* [Adobe 支持部门](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)必须针对以下项目配置您的帐户：

   * Adobe Console
   * Adobe Developer Console
   * Adobe Analytics 和
   * Adobe IMS (Identity Management System)

* 您组织的系统管理员应使用 Admin Console 将您组织中所需的开发人员添加到相关的产品配置文件中。

   * 这将为特定开发人员提供在Adobe Developer控制台中启用集成的权限。
   * 请参阅 [管理开发人员](https://helpx.adobe.com/enterprise/using/manage-developers.html).


## 配置 IMS 配置 – 生成公钥 {#configuring-an-ims-configuration-generating-a-public-key}

配置的第一阶段是在 AEM 中创建 IMS 配置并生成公钥。

1. 在 AEM 中，打开&#x200B;**工具**&#x200B;菜单。
1. 在 **安全性** 部分，选择 **Adobe IMS配置**.
1. 选择&#x200B;**创建**，打开 **Adobe IMS 技术帐户配置**。
1. 使用&#x200B;**云配置**&#x200B;下的下拉列表，选择 **Adobe Analytics。**
1. 激活&#x200B;**新建证书**&#x200B;并输入新别名。
1. 选择&#x200B;**创建证书**&#x200B;来确认。

   ![Adobe IMS技术帐户配置向导](assets/integrate-analytics-io-01.png)

1. 选择&#x200B;**下载**（或&#x200B;**下载公钥**）将文件下载到本地驱动器，以便在[为 Adobe Analytics 与 AEM 的集成配置 IMS](#configuring-ims-for-adobe-analytics-integration-with-aem) 时方便使用。

   >[!CAUTION]
   >
   >保持此配置处于打开状态；出现以下情况时再次需要： [在AEM中完成IMS配置](#completing-the-ims-configuration-in-aem).

   ![用于向Adobe I/O添加密钥的信息对话框](assets/integrate-analytics-io-02.png)

## 为 Adobe Analytics 与 AEM 的集成配置 IMS {#configuring-ims-for-adobe-analytics-integration-with-aem}

使用Adobe Developer Console，创建一个与Adobe Analytics(供AEM使用)的项目（集成），然后分配所需的权限。

### 创建项目 {#creating-the-project}

要使用AEM可以使用的Adobe Analytics创建项目，请打开Adobe Developer Console：

>[!CAUTION]
>
>目前，Adobe仅支持Adobe Developer控制台的 **服务帐户(JWT)** 凭据类型。
>
>不要使用 **OAuth 服务器到服务器**&#x200B;凭据类型（以后将支持此类型）。

1. 为项目打开 Adobe Developer Console：

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 您拥有的任何项目都会显示出来。选择 **创建新项目**  — 位置和使用情况取决于以下因素：

   * 如果您不具有任何项目，**新建项目**会位于底部中心。
     ![新建项目 – 第一个项目](assets/integration-analytics-io-02.png)
   * 如果您已经拥有现有项目，则会列出和 **创建新项目** 位于右上角。
     ![新建项目 – 多个项目](assets/integration-analytics-io-03.png)


1. 依次选择 **添加到项目**&#x200B;和 **API**：

   ![开始使用新项目](assets/integration-analytics-io-10.png)

1. 依次选择 **Adobe Analytics** 和&#x200B;**下一步**：

   >[!NOTE]
   >
   >如果您已订阅 Adobe Analytics，但它并未列出，您应查看[先决条件](#prerequisites)。

   ![添加 API](assets/integration-analytics-io-12.png)

1. 选择 **服务帐户(JWT)** 作为身份验证类型，然后继续 **下一个**：

   ![选择身份验证类型](assets/integration-analytics-io-12a.png)

1. **上传公钥**，完成后，选择&#x200B;**下一步**：

   ![上传公钥](assets/integration-analytics-io-13.png)

1. 查看凭据，然后选择&#x200B;**下一步**：

   ![查看凭据](assets/integration-analytics-io-15.png)

1. 选择所需的产品配置文件，然后选择&#x200B;**保存配置的 API**：

   ![选择所需的产品配置文件](assets/integration-analytics-io-16.png)

1. 配置得到确认。

### 将权限分配给集成 {#assigning-privileges-to-the-integration}

现在，将所需权限分配给集成：

1. 打开 Adobe **Admin Console**：

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 导航到&#x200B;**产品**（顶部工具栏），然后选择 **Adobe Analytics – &lt;*your-tenant-id*>**（从左侧面板）。
1. 选择&#x200B;**产品配置文件**，然后从提供的列表中选择所需的工作区。例如，默认工作区。
1. 选择 **API 凭据**，然后选择所需的集成配置。
1. 选择&#x200B;**编辑者**&#x200B;作为&#x200B;**产品角色**；而不是选择&#x200B;**观察者**。

## 为 Adobe Developer Console 集成项目存储的详细信息 {#details-stored-for-the-ims-integration-project}

从“Adobe Developer 项目”控制台中，您可以查看所有集成项目的列表：

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

要显示有关配置的更多详细信息，请选择特定项目条目。 其中包括：

* 项目概述
* 见解
* 凭据
   * 服务帐户 (JWT)
      * 凭据详细信息
      * 生成 JWT
* APIS
   * 例如，Adobe Analytics

其中一些您必须在AEM中完成Adobe Analytics的集成。

## 在 AEM 中完成 IMS 配置 {#completing-the-ims-configuration-in-aem}

通过返回到AEM，您可以添加针对Analytics的集成项目所需的值来完成IMS配置：

1. 返回到 [AEM 中打开的 IMS 配置](#configuring-an-ims-configuration-generating-a-public-key)。
1. 选择&#x200B;**下一步**。

1. 在这里，您可以使用 [为Adobe Developer控制台集成项目存储的详细信息](#details-stored-for-the-ims-integration-project)：

   * **标题**：您的文本。
   * **授权服务器**：复制并粘贴以下&#x200B;**有效负载**&#x200B;分区中 `aud` 行的内容，例如，以下示例中的 `https://ims-na1.adobelogin.com`
   * **API 密钥**：从[项目概述](#details-stored-for-the-ims-integration-project)的&#x200B;**凭据**&#x200B;部分中复制此密钥
   * **客户端密码**：在[“服务帐户 (JWT)”部分的“客户端密码”选项卡](#details-stored-for-the-ims-integration-project)生成此密码并进行复制
   * **有效负载**：从[“服务帐户 (JWT)”部分的“生成 JWT”选项卡](#details-stored-for-the-ims-integration-project)复制有效负载

   ![AEM IMS 配置详细信息](assets/integrate-analytics-io-10.png)

1. 选择&#x200B;**创建**&#x200B;来确认。

1. 您的 Adobe Analytics 配置会显示在 AEM 控制台中。

   ![IMS 配置](assets/integrate-analytics-io-11.png)

## 确认 IMS 配置 {#confirming-the-ims-configuration}

要确认配置是否按预期运行，请执行以下操作：

1. 打开：

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`

1. 选择您的配置。
1. 从工具栏中选择&#x200B;**检查运行状况**，然后选择&#x200B;**查看**。

   ![IMS 配置 – 检查运行状况](assets/integrate-analytics-io-12.png)

1. 如果成功，您将看到一条确认消息。

## 配置Adobe Analytics Cloud服务 {#configuring-the-adobe-analytics-cloud-service}

现在可为Cloud Service引用配置以使用Analytics Standard API：

1. 打开 **工具** 菜单。 然后，在 **Cloud Service** 部分，选择 **旧版Cloud Service**.
1. 向下滚动到 **Adobe Analytics** 并选择 **立即配置**.

   此 **创建配置** 对话框打开。

1. 输入 **标题** 如果你愿意，还有 **名称** （如果留空，则从标题生成）。

   您还可以选择所需的模板（如果有多个模板可用）。

1. 选择&#x200B;**创建**&#x200B;来确认。

   此 **编辑组件** 对话框打开。

1. 请在以下位置输入详细信息 **Analytics设置** 选项卡：

   * **身份验证**： IMS

   * **IMS配置**：选择IMS配置的名称

1. 要初始化与Adobe Analytics的连接，请单击 **连接到Analytics**.

   如果连接成功，则将显示消息&#x200B;**连接成功**。

1. 选择 **确定** 在消息上。

1. 根据需要完成其他参数，然后 **确定** ，以便您确认配置。

1. 您现在可以继续访问 [添加Analytics框架](/help/sites-administering/adobeanalytics-connect.md) 以配置发送到Adobe Analytics的参数。
