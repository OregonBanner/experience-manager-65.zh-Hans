---
title: 設定AEM Assets與Experience Cloud的整合
description: 瞭解如何透過Experience Cloud設定AEM Assets整合。
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# 設定AEM Assets與Experience Cloud的整合 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

如果您是Adobe Experience Cloud客戶，則可以將Adobe Experience Manager Assets中的資產與Adobe Creative Cloud同步，反之亦然。 您也可以將資產與Experience Cloud同步，反之亦然。 您可以透過以下方式設定此同步處理 [!DNL Adobe I/O]. 已更新的名稱 [!DNL Adobe Marketing Cloud] 是 [!DNL Adobe Experience Cloud].

設定此整合的工作流程為：

1. 在中建立驗證 [!DNL Adobe I/O] 使用公用閘道並取得應用程式ID。
1. 使用應用程式ID在您的AEM Assets執行個體上建立設定檔。
1. 使用此設定來同步您的資產。

在後端，AEM伺服器會與閘道驗證您的設定檔，然後在資產和Experience Cloud之間同步資料。

>[!NOTE]
>
>此功能已棄用 [!DNL Assets]. 尋找取代 [AEM與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md). 如果您有任何查詢， [聯絡Adobe客戶支援](https://www.adobe.com/cn/account/sign-in.supportportal.html).

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## 创建应用程序 {#create-an-application}

1. 登入，存取Adobe Developer閘道介面 [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >您需要管理員許可權才能建立應用程式ID。

1. 從左窗格，導覽至 **[!UICONTROL 開發人員工具]** > **[!UICONTROL 應用]** 以檢視應用程式清單。
1. 按一下 **[!UICONTROL 新增]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) 以建立應用程式。
1. 從 **[!UICONTROL 使用者端認證]** 清單，選取 **[!UICONTROL 服務帳戶（JWT判斷提示）]**，此元件為伺服器對伺服器的通訊服務，用於伺服器驗證。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定應用程式的名稱和選擇性說明。
1. 從 **[!UICONTROL 組織]** 清單中，選取您要同步資產的組織。
1. 從 **[!UICONTROL 範圍]** 清單，選取 **[!UICONTROL dam-read]**， **[!UICONTROL dam-sync]**， **[!UICONTROL dam-write]**、和 **[!UICONTROL cc-share]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。系統會顯示一則訊息，通知已建立應用程式。

   ![成功建立應用程式以將AEM Assets與Creative Cloud整合的通知](assets/chlimage_1-50.png)

1. 複製 **[!UICONTROL 應用程式ID]** 會為新應用程式產生。

   >[!CAUTION]
   >
   >確保您不會不小心複製 **[!UICONTROL 應用程式密碼]** 而非 **[!UICONTROL 應用程式ID]**.

## 新增設定至Experience Cloud {#add-a-new-configuration}

1. 按一下本機AEM Assets執行個體使用者介面上的AEM標誌，並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 舊版Cloud Services]**.

1. 找到 **[!UICONTROL Adobe Experience Cloud]** 服務。 如果不存在任何設定，請按一下 **[!UICONTROL 立即設定]**. 如果設定存在，請按一下 **[!UICONTROL 顯示設定]** 並按一下 `+` 以新增設定。

   >[!NOTE]
   >
   >使用具有組織管理員許可權的Adobe ID帳戶。

1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定新設定的標題和名稱，然後按一下 **[!UICONTROL 建立]**.

   ![命名新設定以整合AEM Assets和Creative Cloud](assets/aem-ec-integration-config1.png)

1. 在 **[!UICONTROL 租使用者URL]** 欄位中，指定AEM Assets的URL。 在過去，如果URL定義為 `https://<tenant_id>.marketing.adobe.com`，將其變更為 `https://<tenant_id>.experiencecloud.adobe.com`.

   1. 导航到&#x200B;**工具 > 云服务 > 旧版云服务**。在Adobe Experience Cloud底下，按一下 **顯示設定**.
   1. 選取要編輯的現有設定。 編輯設定並取代 `marketing.adobe.com` 至 `experiencecloud.adobe.com`.
   1. 保存配置。測試MAC同步復寫代理。

1. 在 **[!UICONTROL 使用者端ID]** 欄位，貼上您在程式結尾複製的應用程式ID [建立應用程式](#create-an-application).

   ![提供整合AEM Assets和Creative Cloud所需的應用程式ID值](assets/cloudservices_tenant_info.png)

1. 下 **[!UICONTROL 同步]** 選取 **[!UICONTROL 已啟用]** 啟用同步化並按一下 **[!UICONTROL 確定]**. 如果您選取 **已停用**，同步化會以單一方向運作。

1. 在設定頁面中，按一下 **[!UICONTROL 顯示公開金鑰]** 以顯示針對執行個體產生的公開金鑰。 或者，按一下 **[!UICONTROL 下載OAuth閘道的公開金鑰]** 下載包含公開金鑰的檔案。 然後，開啟檔案以顯示公開金鑰。

## 啟用同步 {#enable-synchronization}

1. 使用程式最後步驟中所述的下列方法之一顯示公開金鑰 [新增設定至Experience Cloud](#add-a-new-configuration). 按一下 **[!UICONTROL 顯示公開金鑰]**.

1. 複製公開金鑰並貼到 **[!UICONTROL 公開金鑰]** 您所建立之應用程式的設定介面欄位 [建立應用程式](#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 单击&#x200B;**[!UICONTROL 更新]**。立即將您的資產與AEM Assets執行個體同步。

## 測試同步 {#test-the-synchronization}

1. 按一下本機AEM Assets執行個體使用者介面上的AEM標誌，並導覽至 **[!UICONTROL 工具]**> **[!UICONTROL 部署]**> **[!UICONTROL 復寫]**尋找為同步處理所建立的復寫設定檔。
1. 於 **[!UICONTROL 復寫]** 頁面，按一下 **[!UICONTROL 作者上的代理]**.
1. 從設定檔清單中，按一下您組織的預設復寫設定檔以開啟它。
1. 在對話方塊中，按一下 **[!UICONTROL 測試連線]**.

   ![測試連線，並為您的組織設定預設復寫設定檔](assets/chlimage_1-54.png)

1. 當復寫回覆完成時，請在測試結果結束時檢查成功訊息。

## 將使用者新增至Experience Cloud {#add-users-to-experience-cloud}

1. 使用管理員認證登入Experience Cloud。
1. 從導軌，前往 **[!UICONTROL 管理]** 然後按一下 **[!UICONTROL 啟動Enterprise Dashboard]**.
1. 在邊欄中，按一下 **[!UICONTROL 使用者]** 以開啟 **[!UICONTROL User Management]** 頁面。
1. 在工具列中按一下 **新增** ![aem_assets_add_icon](assets/aem_assets_add_icon.png).
1. 新增一或多個使用者，讓您提供與Creative Cloud共用資產的能力。

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## 在AEM Assets和Experience Cloud之間交換資產 {#exchange-assets-between-aem-and-experience-cloud}

1. 登入AEM Assets。
1. 在「資產」主控台中，建立資料夾並上傳部分資產至該資料夾。 例如，建立資料夾 **mc-demo** 並將資產上傳至其中。
1. 選取資料夾並按一下 **共用** ![assets_share](assets/do-not-localize/assets_share.png).
1. 從功能表中選取 **[!UICONTROL Adobe Experience Cloud]** 以及按一下 **[!UICONTROL 共用]**. 訊息會通知該資料夾已與Experience Cloud共用。

   >[!NOTE]
   >
   >共用型別的資產資料夾 `sling:OrderedFolder`在Adobe Experience Cloud中共用的內容中不支援。 如果您想要共用資料夾，在AEM Assets中建立資料夾時，請勿選取 **[!UICONTROL 已訂購]** 選項。

1. 重新整理AEM Assets使用者介面。 您在本機AEM Assets執行個體的Assets主控台中建立的資料夾會複製到Experience Cloud使用者介面。 上傳至AEM Assets資料夾的資產會由AEM伺服器處理後，顯示在Experience Cloud資料夾副本中。
1. 您也可以在Experience Cloud中上傳資料夾復寫復本中的資產。 處理之後，資產會顯示在AEM Assets的共用資料夾中。

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and vice versa for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [資產與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)

