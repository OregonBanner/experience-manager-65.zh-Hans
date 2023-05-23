---
title: 使用 Brand Portal 配置 AEM Assets
seo-title: Configure AEM Assets with Brand Portal
description: 瞭解如何使用Brand Portal設定AEM Assets，以將資產和集合發佈到Brand Portal。
seo-description: Learn how to configure AEM Assets with Brand Portal for publishing assets and Collections to Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2076'
ht-degree: 8%

---

# 使用 Brand Portal 配置 AEM Assets {#configure-integration-65}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

Adobe Experience Manager Assets Brand Portal可讓您將核准的品牌資產從Adobe Experience Manager Assets發佈到Brand Portal，並分發給Brand Portal使用者。

AEM Assets是透過Adobe Developer主控台使用Brand Portal設定的，可取得AdobeIdentity Management服務(IMS)帳戶權杖以授權Brand Portal租使用者。

>[!NOTE]
>
>AEM 6.5.4.0及更高版本支援透過AEM Assets主控台使用Brand Portal設定Adobe Developer。
>
>之前，Brand Portal是透過舊版OAuth閘道進行設定，該閘道會使用JSON Web權杖(JWT)交換取得IMS存取權杖以取得授權。
>
>自2020年4月6日起，系統不再支援透過舊版OAuth閘道進行設定，且將變更為Adobe Developer主控台。

>[!TIP]
>
>***僅適用於現有客戶***
>
>建議繼續使用現有的舊版OAuth閘道設定。 如果您遇到舊版OAuth閘道設定問題，請刪除現有設定，並透過Adobe Developer主控台建立新設定。

本說明說明說明下列兩個使用案例：

* [新設定](#configure-new-integration-65)：如果您是新的Brand Portal使用者，並且想要使用Brand Portal設定您的AEM Assets編寫執行個體，您可以透過Adobe Developer主控台建立設定。
* [升級設定](#upgrade-integration-65)：如果您是擁有舊版OAuth閘道設定的現有Brand Portal使用者，請刪除現有設定，並透過Adobe Developer主控台建立新設定。

所提供的資訊是根據以下假設，即任何閱讀本「說明」的人員都熟悉以下技術：

* 安裝、設定和管理Adobe Experience Manager和AEM套件。

* 使用Linux和Microsoft Windows作業系統。

## 前提条件 {#prerequisites}

您需要以下各项才能使用 Brand Portal 配置 AEM Assets：

* 使用最新Service Pack且正在執行中的AEM Assets作者執行個體
* Brand Portal租使用者URL
* 對Brand Portal租使用者的IMS組織具有系統管理員許可權的使用者

[下載並安裝AEM 6.5](#aemquickstart)

[下載並安裝最新的AEM Service Pack](#servicepack)

### 下載並安裝AEM 6.5 {#aemquickstart}

建議使用AEM 6.5設定AEM編寫執行個體。 如果您尚未啟動並執行AEM，請從下列位置下載：

* 如果您是現有AEM客戶，請從下載AEM 6.5 [Adobe授權網站](https://licensing.adobe.com).

* 如果您是Adobe合作夥伴，請使用 [Adobe合作夥伴訓練計畫](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) 以請求AEM 6.5。

下載AEM後，如需設定AEM編寫執行個體的指示，請參閱 [部署和維護](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### 下載並安裝AEM最新Service Pack {#servicepack}

如需詳細指示，請參閱

* [AEM 6.5 Service Pack發行說明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**聯絡支援人員** 如果您找不到最新的AEM套件或Service Pack。

## 创建配置 {#configure-new-integration-65}

使用Brand Portal設定AEM Assets需要在AEM Assets作者執行個體和Adobe Developer Console中進行設定。

1. 在AEM Assets中，建立IMS帳戶並產生公開憑證（公開金鑰）。
1. 在Adobe Developer主控台中，為您的Brand Portal租使用者（組織）建立專案。
1. 在專案下，使用公開金鑰設定API以建立服務帳戶(JWT)連線。
1. 取得服務帳戶憑證和JWT裝載資訊。
1. 在AEM Assets中，使用服務帳戶憑證和JWT裝載設定IMS帳戶。
1. 在AEM Assets中，使用IMS帳戶和Brand Portal端點（組織URL）設定Brand Portal雲端服務。
1. 將資產從AEM Assets發佈到Brand Portal以測試設定。

>[!NOTE]
>
>AEM Assets作者執行個體只能設定為一個Brand Portal租使用者。

如果您是第一次使用Brand Portal設定AEM Assets，請依照列出的順序執行下列步驟：
1. [获取公共证书](#public-certificate)
1. [建立服務帳戶(JWT)連線](#createnewintegration)
1. [設定IMS帳戶](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-integration)

### 创建 IMS 配置 {#create-ims-configuration}

IMS設定會向Brand Portal租使用者驗證您的AEM Assets作者執行個體。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [設定IMS帳戶](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公開金鑰（憑證）會在Adobe Developer Console上驗證您的設定檔。

1. 登入您的AEM Assets作者執行個體。 預設URL為 `http://localhost:4502/aem/start.html`.

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導覽至 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS設定]**.

1. 在Adobe IMS設定頁面中，按一下 **[!UICONTROL 建立]**. 它會重新導向至 **[!UICONTROL Adobe IMS技術帳戶設定]** 頁面。 根據預設， **憑證** 標籤開啟。

1. 選取 **[!UICONTROL AdobeBrand Portal]** 在 **[!UICONTROL 雲端解決方案]** 下拉式清單。

1. 選取 **[!UICONTROL 建立新憑證]** 核取方塊並指定 **別名** 以取得公開金鑰。 別名會作為公開金鑰的名稱。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。然後，按一下 **[!UICONTROL 確定]** 以產生公開金鑰。

   ![创建证书](assets/ims-config2.png)

1. 按一下 **[!UICONTROL 下載公開金鑰]** 圖示並將公開金鑰(.crt)檔案儲存在電腦上。

   公開金鑰稍後將用於設定Brand Portal租使用者的API，以及在Adobe Developer主控台中產生服務帳戶認證。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在 **帳戶** 索引標籤中，會建立Adobe IMS帳戶，而這需要在Adobe Developer Console中產生的服務帳戶認證。 暂时保持此页面打开。

   開啟新標籤並 [在Adobe Developer主控台中建立服務帳戶(JWT)連線](#createnewintegration) 以取得用於設定IMS帳戶的認證和JWT裝載。

### 建立服務帳戶(JWT)連線 {#createnewintegration}

在Adobe Developer主控台中，專案和API是在Brand Portal租使用者（組織）層級設定。 設定API會建立服務帳戶(JWT)連線。 有兩種設定API的方法，透過產生金鑰組（私密金鑰和公開金鑰）或透過上傳公開金鑰。 若要使用Brand Portal設定AEM Assets，您必須在AEM Assets中產生公開金鑰（憑證），並透過上傳公開金鑰在Adobe Developer Console中建立憑證。 在AEM Assets中設定IMS帳戶需要這些認證。 設定IMS帳戶後，您可以在AEM Assets中設定Brand Portal雲端服務。

執行以下步驟來產生服務帳戶憑證和JWT裝載：

1. 以IMS組織(Adobe Developer租使用者)的系統管理員許可權登入Brand Portal主控台。 預設URL為 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >確保您已從右上角的下拉式清單（組織）中選取正確的IMS組織(Brand Portal租使用者)。

1. 按一下 **[!UICONTROL 建立新專案]**. 系統會為您的組織建立名稱由系統產生的空白專案。

   按一下 **[!UICONTROL 編輯專案]** 更新 **[!UICONTROL 專案標題]** 和 **[!UICONTROL 說明]**，然後按一下 **[!UICONTROL 儲存]**.

1. 在 **[!UICONTROL 專案概述]** 標籤，按一下 **[!UICONTROL 新增API]**.

1. 在 **[!UICONTROL 新增API視窗]**，選取 **[!UICONTROL AEM Brand Portal]** 並按一下 **[!UICONTROL 下一個]**.

   確保您有權存取AEM Brand Portal服務。

1. 在 **[!UICONTROL 設定API]** 視窗，按一下 **[!UICONTROL 上傳您的公開金鑰]**. 然後，按一下 **[!UICONTROL 選取檔案]** 並上傳您在中下載的公開金鑰（.crt檔案） [取得公開憑證](#public-certificate) 區段。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![上傳公開金鑰](assets/service-account3.png)

1. 驗證公開金鑰並按一下 **[!UICONTROL 下一個]**.

1. 選取 **[!UICONTROL Assets Brand Portal]** ，然後按一下 **[!UICONTROL 儲存已設定的API]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![選取產品設定檔](assets/service-account4.png)

1. 設定API後，您會重新導向至API概觀頁面。 從左側導覽列於 **[!UICONTROL 認證]**，按一下 **[!UICONTROL 服務帳戶(JWT)]** 選項。

   >[!NOTE]
   >
   >您可以檢視認證並執行產生JWT權杖、複製認證詳細資料、擷取使用者端密碼等動作。

1. 從 **[!UICONTROL 使用者端認證]** 標籤，複製 **[!UICONTROL 使用者端ID]**.

   按一下 **[!UICONTROL 擷取使用者端密碼]** 並複製 **[!UICONTROL 使用者端密碼]**.

   ![服務帳戶認證](assets/service-account5.png)

1. 導覽至 **[!UICONTROL 產生JWT]** 標籤並複製 **[!UICONTROL JWT裝載]** 資訊。

您現在可以將使用者端ID （API金鑰）、使用者端密碼和JWT裝載使用至 [設定IMS帳戶](#create-ims-account-configuration) 在AEM Assets中。

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe I/O Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.
-->

### 設定IMS帳戶 {#create-ims-account-configuration}

确保您已执行以下步骤：

* [获取公共证书](#public-certificate)
* [建立服務帳戶(JWT)連線](#createnewintegration)

執行以下步驟來設定IMS帳戶。

1. 開啟IMS設定並導覽至 **[!UICONTROL 帳戶]** 標籤。 您保持頁面開啟的時間 [取得公開憑證](#public-certificate).

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在 **[!UICONTROL 授權伺服器]** 欄位中指定URL： [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   在中指定使用者端ID **[!UICONTROL API金鑰]** 欄位， **[!UICONTROL 使用者端密碼]**、和 **[!UICONTROL 裝載]** （JWT裝載）您複製的時間 [建立服務帳戶(JWT)連線](#createnewintegration).

   单击&#x200B;**[!UICONTROL 创建]**。

   IMS帳戶已設定。

   ![IMS 帐户配置](assets/create-new-integration6.png)

1. 選取IMS帳戶設定並按一下 **[!UICONTROL 檢查健康狀態]**.

   按一下 **[!UICONTROL Check]** （在對話方塊中）。 在成功設定時，會出現一則訊息， *已成功擷取權杖*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您必須只有一個IMS設定。
>
>確保IMS設定通過健康狀態檢查。 如果設定未通過健康狀態檢查，則為無效。 您必須刪除它並建立新的有效設定。

### 配置云服务 {#configure-the-cloud-service}

執行以下步驟來設定Brand Portal雲端服務：

1. 登入您的AEM Assets作者執行個體。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導覽至 **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. 在Brand Portal設定頁面中，按一下 **[!UICONTROL 建立]**.

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   選取您建立的IMS設定，同時 [設定IMS帳戶](#create-ims-account-configuration).

   在 **[!UICONTROL 服務URL]** 欄位中，指定您的Brand Portal租使用者（組織） URL。

   ![](assets/create-cloud-service.png)

1. 单击“**[!UICONTROL 保存并关闭]**”。将创建云配置。

   您的AEM Assets作者執行個體現在已透過Brand Portal租使用者完成設定。

### 测试配置 {#test-integration}

執行以下步驟來驗證設定：

1. 登入您的AEM Assets雲端例項。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導覽至 **[!UICONTROL 部署]** > **[!UICONTROL 復寫]**.

   ![](assets/test-integration1.png)

1. 在「復寫」頁面中，按一下 **[!UICONTROL 作者上的代理]**.

   ![](assets/test-integration2.png)

   您可以看到為您的Brand Portal租使用者建立的四個復寫代理。

   找到Brand Portal租使用者的復寫代理，然後按一下復寫代理URL。

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >復寫代理程式會平行運作並平均共用工作分佈，因此將發佈速度提升至原始速度的四倍。 設定Cloud Service後，無需進行其他設定即可啟用復寫代理（預設會啟動以啟用多個資產的平行發佈）。

1. 若要驗證AEM Assets與Brand Portal之間的連線，請按一下 **[!UICONTROL 測試連線]** 圖示。

   ![](assets/test-integration4.png)

   系統會顯示訊息，指出 *測試封裝已成功傳遞*.

   ![](assets/test-integration5.png)

1. 驗證全部四個復寫代理的測試結果。


   >[!NOTE]
   >
   >請避免停用任何復寫代理程式，因為這可能會導致資產（在佇列中執行）復寫失敗。
   >
   >請確定四個復寫代理均已設定為避免逾時錯誤。 另請參閱 [疑難排解平行發佈至Brand Portal的問題](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).
   >
   >請勿修改任何自動產生的設定。

您現在可以：

* [将资产从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-assets.md)
* [從Brand Portal發佈資產到AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-Hans) - Brand Portal中的Asset Sourcing
* [将文件夹从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-folder.md)
* [将收藏集从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-collection.md)
* [将预设、架构和 Facet 发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

另請參閱 [Brand Portal檔案](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 以取得詳細資訊。


## 升級設定 {#upgrade-integration-65}

按照列出的順序執行以下步驟，將現有設定升級至Adobe Developer Console：
1. [驗證執行中的工作](#verify-jobs)
1. [刪除現有設定](#delete-existing-configuration)
1. [创建配置](#configure-new-integration-65)

### 驗證執行中的工作 {#verify-jobs}

在進行任何修改前，請確保您的AEM Assets作者執行個體上沒有執行發佈工作。 為此，您可以驗證所有四個復寫代理程式上作用中工作的狀態，並確保佇列處於閒置狀態。

1. 登入您的AEM Assets作者執行個體。

1. 從 **工具** ![工具](assets/do-not-localize/tools.png) 面板，導覽至 **[!UICONTROL 部署]** > **[!UICONTROL 部署復寫]**.

1. 在「復寫」頁面中，按一下 **[!UICONTROL 作者上的代理]**.

   ![](assets/test-integration2.png)

1. 找到Brand Portal租使用者的復寫代理。

   確保 **佇列閒置** 對於所有復寫代理程式，沒有作用中的發佈工作。

   ![](assets/test-integration3.png)

### 刪除現有設定 {#delete-existing-configuration}

刪除現有設定時，您必須執行下列檢查清單：
* 刪除全部四個復寫代理
* 刪除Brand Portal雲端服務
* 刪除MAC使用者

1. 登入您的AEM Assets作者執行個體並以管理員身分開啟CRX Lite。 預設URL為 `http://localhost:4502/crx/de/index.jsp`.

1. 導覽至 `/etc/replications/agents.author` 並刪除Brand Portal租使用者的全部四個復寫代理。

   ![](assets/delete-replication-agent.png)

1. 導覽至 `/etc/cloudservices/mediaportal` 並刪除Brand Portal雲端服務設定。

   ![](assets/delete-cloud-service.png)

1. 導覽至 `/home/users/mac` 並刪除 **Mac使用者** 您的Brand Portal租使用者。

   ![](assets/delete-mac-user.png)


您現在可以 [建立設定](#configure-new-integration-65) 透過您AEM 6.5編寫執行個體上的Adobe Developer主控台。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
