---
title: 使用IMS與Adobe Analytics整合
description: 瞭解如何使用IMS整合AEM與Adobe Analytics
exl-id: 2833a6df-ef32-48ab-8395-0f26816f8443
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 66%

---

# 使用IMS與Adobe Analytics整合 {#integration-with-adobe-analytics-using-ims}

透過Analytics Standard API整合AEM與Adobe Analytics時，需要使用Adobe Developer主控台設定Adobe IMS (Identity Management系統)。

>[!NOTE]
>
>AEM 6.5.12.0新增Adobe Analytics Standard API 2.0支援。此版本的API支援IMS驗證。
>
>在AEM中使用Adobe Analytics Classic API 1.4仍支援回溯相容性。 此 [Analytics Classic API使用使用者認證驗證](/help/sites-administering/adobeanalytics-connect.md).
>
>API 选择由用于 AEM/Analytics 集成的身份验证方法驱动。
>
>[迁移到 2.0 API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/) 下还提供了更多信息。

## 前提条件 {#prerequisites}

开始此过程之前：

* [Adobe 支持部门](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html)必须针对以下项目配置您的帐户：

   * Adobe Console
   * Adobe Developer Console
   * Adobe Analytics 和
   * Adobe IMS (Identity Management System)

* 您組織的系統管理員應使用Admin Console，將您組織中必要的開發人員新增到相關的產品設定檔。

   * 這可讓特定開發人員擁有在Adobe Developer主控台中啟用整合的許可權。
   * 有关更多详细信息，请参阅[管理开发人员](https://helpx.adobe.com/cn/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)。


## 配置 IMS 配置 – 生成公钥 {#configuring-an-ims-configuration-generating-a-public-key}

配置的第一阶段是在 AEM 中创建 IMS 配置并生成公钥。

1. 在 AEM 中，打开&#x200B;**工具**&#x200B;菜单。
1. 在&#x200B;**安全性**&#x200B;部分中，选择 **Adobe IMS 配置**。
1. 选择&#x200B;**创建**，打开 **Adobe IMS 技术帐户配置**。
1. 使用&#x200B;**云配置**&#x200B;下的下拉列表，选择 **Adobe Analytics**。
1. 激活&#x200B;**新建证书**&#x200B;并输入新别名。
1. 选择&#x200B;**创建证书**&#x200B;来确认。

   ![](assets/integrate-analytics-io-01.png)

1. 选择&#x200B;**下载**（或&#x200B;**下载公钥**）将文件下载到本地驱动器，以便在[为 Adobe Analytics 与 AEM 的集成配置 IMS](#configuring-ims-for-adobe-analytics-integration-with-aem) 时方便使用。

   >[!CAUTION]
   >
   >将此配置保持开放状态，供[在 AEM 中完成 IMS 配置](#completing-the-ims-configuration-in-aem)时再次使用。

   ![](assets/integrate-analytics-io-02.png)

## 为 Adobe Analytics 与 AEM 的集成配置 IMS {#configuring-ims-for-adobe-analytics-integration-with-aem}

使用 Adobe Developer Console，您需要使用 Adobe Analytics（供 AEM 使用）创建项目（集成），然后分配所需的权限。

### 创建项目 {#creating-the-project}

打开 Adobe Developer Console 以使用 Adobe Analytics（将由 AEM 使用）创建项目：

1. 为项目打开 Adobe Developer Console：

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 将显示您拥有的任何项目。选择&#x200B;**新建项目** – 位置和使用将取决于：

   * 如果您不具有任何项目，**新建项目**将位于底部中心。
      ![新建项目 – 第一个项目](assets/integration-analytics-io-02.png)
   * 如果您已拥有项目，这些项目将列出，**新建项目**将位于右上方。
      ![新建项目 – 多个项目](assets/integration-analytics-io-03.png)


1. 依次选择 **添加到项目**&#x200B;和 **API**：

   ![开始使用新项目](assets/integration-analytics-io-10.png)

1. 依次选择 **Adobe Analytics** 和&#x200B;**下一步**：

   >[!NOTE]
   >
   >如果您已訂閱Adobe Analytics，但未看到它列出，則應檢視 [先決條件](#prerequisites).

   ![添加 API](assets/integration-analytics-io-12.png)

1. 选择&#x200B;**服务帐户 (JWT)** 作为身份验证类型，然后选择&#x200B;**下一步**：

   ![选择身份验证类型](assets/integration-analytics-io-12a.png)

1. **上传公钥**，完成后，选择&#x200B;**下一步**：

   ![上传公钥](assets/integration-analytics-io-13.png)

1. 查看凭据，然后选择&#x200B;**下一步**：

   ![查看凭据](assets/integration-analytics-io-15.png)

1. 选择所需的产品配置文件，然后选择&#x200B;**保存配置的 API**：

   ![选择所需的产品配置文件](assets/integration-analytics-io-16.png)

1. 这将确认配置。

### 将权限分配给集成 {#assigning-privileges-to-the-integration}

您现在必须将所需权限分配给集成：

1. 打开 Adobe **Admin Console**：

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 导航到&#x200B;**产品**（顶部工具栏），然后选择 **Adobe Analytics – &lt;*your-tenant-id*>**（从左侧面板）。
1. 选择&#x200B;**产品配置文件**，然后从提供的列表中选择所需的工作区。例如，默认工作区。
1. 选择 **API 凭据**，然后选择所需的集成配置。
1. 选择&#x200B;**编辑者**&#x200B;作为&#x200B;**产品角色**；而不是选择&#x200B;**观察者**。

## 为 Adobe Developer Console 集成项目存储的详细信息 {#details-stored-for-the-ims-integration-project}

从“Adobe Developer 项目”控制台中，您可以查看所有集成项目的列表：

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

选择特定项目条目以显示有关配置的更多详细信息。其中包括：

* 项目概述
* 见解
* 凭据
   * 服务帐户 (JWT)
      * 凭据详细信息
      * 生成 JWT
* APIS
   * 例如，Adobe Analytics

您需要其中的一些專案，才能在AEM中完成Adobe Analytics的整合。

## 在 AEM 中完成 IMS 配置 {#completing-the-ims-configuration-in-aem}

返回AEM後，您可以從Analytics的整合專案新增所需值來完成IMS設定：

1. 返回到 [AEM 中打开的 IMS 配置](#configuring-an-ims-configuration-generating-a-public-key)。
1. 选择&#x200B;**下一步**。

1. 您可以在此處使用 [為Adobe Developer主控台整合專案儲存的詳細資訊](#details-stored-for-the-ims-integration-project)：

   * **标题**：您的文本。
   * **授权服务器**：复制并粘贴以下&#x200B;**有效负载**&#x200B;部分的 `aud` 行的内容，例如，下面的示例中的 `https://ims-na1.adobelogin.com`
   * **API 密钥**：从[项目概述](#details-stored-for-the-ims-integration-project)的&#x200B;**凭据**&#x200B;部分中复制此密钥
   * **客户端密码**：在[“服务帐户 (JWT)”部分的“客户端密码”选项卡](#details-stored-for-the-ims-integration-project)生成此密码并进行复制
   * **有效负载**：从[“服务帐户 (JWT)”部分的“生成 JWT”选项卡](#details-stored-for-the-ims-integration-project)复制有效负载

   ![AEM IMS 配置详细信息](assets/integrate-analytics-io-10.png)

1. 选择&#x200B;**创建**&#x200B;来确认。

1. 您的 Adobe Analytics 配置将显示在 AEM 控制台中。

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

## 設定Adobe Analytics Cloud服務 {#configuring-the-adobe-analytics-cloud-service}

此設定現在可供使用Analytics Standard API的Cloud Service參考：

1. 開啟 **工具** 功能表。 然後，在 **Cloud Services** 區段，選取 **舊版Cloud Services**.
1. 向下捲動至 **Adobe Analytics** 並選取 **立即設定**.

   此 **建立設定** 對話方塊將會開啟。

1. 輸入 **標題** 此外，如果您願意，也可以 **名稱** （如果留空，這將從標題產生）。

   您也可以選取所需的範本（如果有多個範本可用）。

1. 选择&#x200B;**创建**&#x200B;来确认。

   此 **編輯元件** 對話方塊將會開啟。

1. 在「 」中輸入詳細資料 **Analytics設定** 標籤：

   * **驗證**： IMS

   * **IMS設定**：選取IMS設定的名稱

1. 按一下 **連線至Analytics** 以初始化與Adobe Analytics的連線。

   如果连接成功，则将显示消息&#x200B;**连接成功**。

1. 選取 **確定** 在訊息上。

1. 視需要填寫其他引數，然後按一下 **確定** ，以確認設定。

1. 您現在可以繼續前往 [新增Analytics框架](/help/sites-administering/adobeanalytics-connect.md) 以設定將傳送至Adobe Analytics的引數。
