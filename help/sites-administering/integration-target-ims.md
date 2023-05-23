---
title: 使用IMS與Adobe Target整合
description: 瞭解如何使用IMS整合AEM與Adobe Target
exl-id: 8ddd86d5-a5a9-4907-b07b-b6552d7afdc8
source-git-commit: 5c3de9c272030b3e258aea95899a58553c3b33db
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 55%

---

# 使用IMS與Adobe Target整合{#integration-with-adobe-target-using-ims}

透過Target Standard API整合AEM與Adobe Target時，需要使用Adobe Developer主控台設定Adobe IMS (Identity Management系統)。

>[!NOTE]
>
>AEM 6.5新增了對Adobe Target Standard API的支援。Target Standard API使用IMS驗證。
>
>在AEM中使用Adobe Target Classic API仍支援回溯相容性。 此 [Target Classic API使用使用者認證驗證](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>API 选择由用于 AEM/Target 集成的身份验证方法驱动。
>另請參閱 [租使用者ID和使用者端代碼](#tenant-client) 區段。

## 前提条件 {#prerequisites}

开始此过程之前：

* [Adobe 支持部门](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html)必须针对以下项目配置您的帐户：

   * Adobe Console
   * Adobe Developer Console
   * Adobe Target 和
   * Adobe IMS (Identity Management System)

* 您組織的系統管理員應使用Admin Console，將您組織中必要的開發人員新增到相關的產品設定檔。

   * 這可讓特定開發人員擁有在Adobe Developer主控台中啟用整合的許可權。
   * 有关更多详细信息，请参阅[管理开发人员](https://helpx.adobe.com/cn/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)。


## 配置 IMS 配置 – 生成公钥 {#configuring-an-ims-configuration-generating-a-public-key}

配置的第一阶段是在 AEM 中创建 IMS 配置并生成公钥。

1. 在 AEM 中，打开&#x200B;**工具**&#x200B;菜单。
1. 在&#x200B;**安全性**&#x200B;部分中，选择 **Adobe IMS 配置**。
1. 选择&#x200B;**创建**，打开 **Adobe IMS 技术帐户配置**。
1. 使用&#x200B;**云配置**&#x200B;下的下拉列表，选择 **Adobe Target**。
1. 激活&#x200B;**新建证书**&#x200B;并输入新别名。
1. 选择&#x200B;**创建证书**&#x200B;来确认。

   ![](assets/integrate-target-io-01.png)

1. 选择&#x200B;**下载**（或&#x200B;**下载公钥**）以将文件下载到本地驱动器，以便在[为 Adobe Target 与 AEM 的集成配置 IMS](#configuring-ims-for-adobe-target-integration-with-aem) 时方便使用。

   >[!CAUTION]
   >
   >将此配置保持开放状态，供[在 AEM 中完成 IMS 配置](#completing-the-ims-configuration-in-aem)时再次使用。

   ![](assets/integrate-target-io-02.png)

## 为 Adobe Target 与 AEM 的集成配置 IMS {#configuring-ims-for-adobe-target-integration-with-aem}

使用Adobe Developer Console時，您需要使用AEM將使用的Adobe Target建立專案（整合），然後指派所需的許可權。

### 创建项目 {#creating-the-project}

打开 Adobe Developer Console 以使用 Adobe Target（将由 AEM 使用）创建项目：

1. 为项目打开 Adobe Developer Console：

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 将显示您拥有的任何项目。选择&#x200B;**新建项目** – 位置和使用将取决于：

   * 如果您不具有任何项目，**新建项目**将位于底部中心。
      ![新建项目 – 第一个项目](assets/integration-target-io-02.png)
   * 如果您已拥有项目，这些项目将列出，**新建项目**将位于右上方。
      ![新建项目 – 多个项目](assets/integration-target-io-03.png)


1. 依次选择 **添加到项目**&#x200B;和 **API**：

   ![](assets/integration-target-io-10.png)

1. 依次选择 **Adobe Target** 和&#x200B;**下一步**：

   >[!NOTE]
   >
   >如果您已訂閱Adobe Target，但未看到它列出，則應檢視 [先決條件](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **上传公钥**，完成后，选择&#x200B;**下一步**：

   ![](assets/integration-target-io-13.png)

1. 查看凭据，然后选择&#x200B;**下一步**：

   ![](assets/integration-target-io-15.png)

1. 选择所需的产品配置文件，然后选择&#x200B;**保存配置的 API**：

   >[!NOTE]
   >
   >显示的产品配置文件取决于您是否拥有：
   >
   >* Adobe Target Standard – 仅&#x200B;**默认工作区**&#x200B;可用
   >* Adobe Target Premium – 列出了所有可用的工作区，如下所示


   ![](assets/integration-target-io-16.png)

1. 这将确认创建。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 将权限分配给集成 {#assigning-privileges-to-the-integration}

您现在必须将所需权限分配给集成：

1. 打开 Adobe **Admin Console**：

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 导航到&#x200B;**产品**（顶部工具栏），然后选择 **Adobe Target – &lt;*your-tenant-id*>**（从左侧面板）。
1. 选择&#x200B;**产品配置文件**，然后从提供的列表中选择所需的工作区。例如，默认工作区。
1. 选择 **API 凭据**，然后选择所需的集成配置。
1. 选择&#x200B;**编辑者**&#x200B;作为&#x200B;**产品角色**；而不是选择&#x200B;**观察者**。

## 为 Adobe Developer Console 集成项目存储的详细信息 {#details-stored-for-the-ims-integration-project}

从“Adobe Developer Console – 项目”中，您可以查看所有集成项目的列表：

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

选择&#x200B;**查看**（特定项目条目右侧）以显示有关配置的更多详细信息。其中包括：

* 项目概述
* 见解
* 凭据
   * 服务帐户 (JWT)
      * 凭据详细信息
      * 生成 JWT
* APIS
   * 例如，Adobe Target

要在基于 IMS 的 AEM 中完成 Adobe Target 的集成，您需要其中的一些项。

## 在 AEM 中完成 IMS 配置 {#completing-the-ims-configuration-in-aem}

返回AEM後，您可以從Target的Adobe Developer主控台整合中新增所需值，以完成IMS設定：

1. 返回到 [AEM 中打开的 IMS 配置](#configuring-an-ims-configuration-generating-a-public-key)。
1. 选择&#x200B;**下一步**。

1. 在这里，您可以使用 [Adobe Developer Console 中项目配置的详细信息](#details-stored-for-the-ims-integration-project)：

   * **标题**：您的文本。
   * **授权服务器**：复制并粘贴以下&#x200B;**有效负载**&#x200B;部分的 `aud` 行的内容，例如，下面的示例中的 `https://ims-na1.adobelogin.com`
   * **API金鑰**：從以下位置複製此專案： [概觀](#details-stored-for-the-ims-integration-project) 區段
   * **使用者端密碼**：在中產生此專案 [概觀](#details-stored-for-the-ims-integration-project) 區段和副本
   * **有效负载**：从[生成 JWT](#details-stored-for-the-ims-integration-project) 部分中复制此有效负载

   ![技術帳戶設定](assets/integrate-target-io-10.png)

1. 选择&#x200B;**创建**&#x200B;来确认。

1. 您的 Adobe Target 配置将显示在 AEM 控制台中。

   ![](assets/integrate-target-io-11.png)

## 确认 IMS 配置 {#confirming-the-ims-configuration}

要确认配置是否按预期运行，请执行以下操作：

1. 打开：

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 选择您的配置。
1. 从工具栏中选择&#x200B;**检查运行状况**，然后选择&#x200B;**查看**。

   ![](assets/integrate-target-io-12.png)

1. 如果成功，您會看到訊息：

   ![](assets/integrate-target-io-13.png)

## 設定Adobe TargetCloud Service {#configuring-the-adobe-target-cloud-service}

此設定現在可供使用Target Standard API的Cloud Service參考：

1. 開啟 **工具** 功能表。 然後，在 **Cloud Services** 區段，選取 **舊版Cloud Services**.
1. 向下捲動至 **Adobe Target** 並選取 **立即設定**.

   此 **建立設定** 對話方塊將會開啟。

1. 輸入 **標題** 此外，如果您願意，也可以 **名稱** （如果留空，這將從標題產生）。

   您也可以選取所需的範本（如果有多個範本可用）。

1. 选择&#x200B;**创建**&#x200B;来确认。

   此 **編輯元件** 對話方塊將會開啟。

1. 在「 」中輸入詳細資料 **Adobe Target設定** 標籤：

   * **驗證**： IMS

   * **租使用者ID**：Adobe IMS租使用者ID。 另請參閱 [租使用者ID和使用者端代碼](#tenant-client) 區段。

      >[!NOTE]
      >
      >IMS需要從Target本身取得此值。 您可以登入Target，並從URL擷取租使用者ID。
      >
      >例如，如果URL為：
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >然後您會使用 `yourtenantid`.

   * **使用者端代碼**：請參閱 [租使用者ID和使用者端代碼](#tenant-client) 區段。

   * **IMS設定**：選取IMS設定的名稱

   * **API型別**：REST

   * **A4T Analytics Cloud 配置**：选择用于 Target 活动目标和量度的 Analytics Cloud 配置。如果您在定位内容时使用 Adobe Analytics 作为报告源，则需要此项。如果您沒有看到雲端設定，請參閱中的注意事項 [設定A4T Analytics Cloud設定](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **使用準確定位**：預設會選取此核取方塊。 如果选中，云服务配置将等到上下文加载完后，再加载内容。请参阅以下注释。

   * **從Adobe Target同步區段**：選取此選項可下載Target中定義的區段，以便在AEM中使用它們。 当“API 类型”属性为 REST 时，您必须选择此选项，因为内联分段不受支持，并且您始终需要从 Target 使用分段。（请注意，AEM 术语“分段”等同于 Target“受众”。）

   * **使用者端資源庫**：選取您想要使用AT.js使用者端程式庫，還是mbox.js （已棄用）。

   * **使用Tag Management系統來提供使用者端資源庫**：使用DTM （已棄用）、AdobeLaunch或任何其他標籤管理系統。

   * **自訂AT.js**：如果您勾選Tag Management方塊或使用預設的AT.js，請保留空白。 或者，您也可以上傳自訂AT.js。 僅當您已選取AT.js時顯示。
   >[!NOTE]
   >
   >[使用Target Classic API的Cloud Service設定](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) 已棄用(使用Adobe Recommendations設定索引標籤)。

1. 按一下 **連線到目標** 以初始化與Adobe Target的連線。

   如果连接成功，则将显示消息&#x200B;**连接成功**。

1. 選取 **確定** 在訊息上，後面接著 **確定** ，以確認設定。

1. 您現在可以繼續前往 [新增目標框架](/help/sites-administering/target-configuring.md#adding-a-target-framework) 以設定將傳送至Target的ContextHub或ClientContext引數。 請注意，這可能不是將AEM體驗片段匯出至Target的必要專案。

### 租使用者ID和使用者端代碼 {#tenant-client}

替換為 [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md)，則「使用者端代碼」欄位已新增至Target設定視窗。

設定租使用者ID和使用者端代碼欄位時，請注意下列事項：

1. 对于大多数客户来说，租户 ID 和客户代码是相同的。这意味着，这两个字段包含相同的信息并且是相同的。确保在这两个字段中输入租户 ID。
2. 对于遗留问题，您还可以在“租户 ID”和“客户端代码”字段中输入不同的值。

在这两种情况下，请注意：

* 根據預設，使用者端代碼（如果先新增）也會自動複製到「租使用者ID」欄位中。
* 您可以选择更改默认租户 ID 集。
* 因此，对 Target 进行的后端调用将基于租户 ID，而对 Target 进行的客户端调用将基于客户端代码。

如前所述，第一個案例最常用於AEM 6.5。無論是哪一種方式，請確定 **兩者** 欄位包含正確的資訊，具體取決於您的需求。

>[!NOTE]
>
>如果要更改现有 Target 配置，请：
>
>1. 重新输入租户 ID。
>2. 重新连接到 Target。
>3. 保存配置。

