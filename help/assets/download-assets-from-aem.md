---
title: 下载资源
description: 瞭解如何從下載資產 [!DNL Adobe Experience Manager] 和啟用或停用下載功能。
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 3%

---

# 從下載資產 [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | 本文 |

您可以下載資產，包括靜態和動態轉譯。 或者，您也可以直接透過傳送包含資產連結的電子郵件 [!DNL Adobe Experience Manager Assets]. 下載的資產會整合在ZIP檔案中。 針對匯出作業，壓縮的ZIP檔案檔案大小上限為1 GB。 每個匯出作業最多允許500個總資產。

>[!NOTE]
>
>任何擁有讀取許可權的使用者： `/var/dam/share` 位置可以存取電子郵件訊息中共用的下載連結。
>
>任何擁有讀取許可權的使用者 `/var/dam/jobs/download` 位置可以下載資產。
>
>無法下載資產型別 — 影像集、迴轉集、混合媒體集和轉盤集。

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**若要下載資產，請遵循下列步驟：**

1. 在左上角，按一下標誌。 在左側邊欄中，按一下 **[!UICONTROL 導覽]**.
1. 於 [!UICONTROL 導覽] 頁面，按一下 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 導覽至包含您要下載之資產的資料夾。
1. 選取資料夾或選取資料夾內的一或多個資產。
1. 在工具列上，按一下 **[!UICONTROL 下載]**.
1. 在「下載」對話方塊中，選取您想要的下載選項。

   | 匯出或下載選項 | 描述 |
   |---|---|
   | **[!UICONTROL 为每个资产创建单独的文件夹]** | 選取此選項可將您下載的每個資產（包括巢狀內嵌於資產上層資料夾下的子資料夾中的資產）納入本機電腦上的一個資料夾中。 如果未選取此選項，預設會忽略資料夾階層，並將所有資產下載至本機電腦中的一個資料夾。 |
   | **[!UICONTROL 电子邮件]** | 會傳送電子郵件通知給使用者。 標準電子郵件範本可在下列位置取得：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 您部署期間自訂的範本可在下列位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以將租使用者特定的自訂範本儲存在下列位置：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 资产]** | 選取此選項，即可以原始格式下載資產，而不使用任何轉譯。<br>如果原始資產有子資產，則可以使用子資產選項。 |
   | **[!UICONTROL 演绎版]** | 轉譯是資產的二進位表示法。 資產具有主要代表性 — 上傳檔案的主要代表性。 它們可以有任意數量的表示。 <br> 使用此選項，您可以選取要下載的轉譯。 可用的轉譯取決於您選取的資產。 如果資產有任何轉譯，則可使用選項。 |
   | **[!UICONTROL 智能裁剪]** | 選取此選項，即可從AEM內下載所選資產的所有智慧型裁切轉譯。 已建立包含「智慧型裁切」轉譯的zip檔案，並下載至您的本機電腦。 |
   | **[!UICONTROL 动态演绎版]** | 選取此選項可即時產生一系列替代轉譯。 選取此選項時，您也可以從以下專案選取，以選取要動態建立的轉譯： [影像預設集](image-presets.md) 清單。 <br>此外，您也可以選取大小與測量單位、格式、色域、解析度，以及任何選用的影像修飾元（例如反轉影像）。 只有當您有以下條件時，才可使用選項： [!DNL Dynamic Media] 已啟用。 |

1. 在對話方塊中，按一下 **[!UICONTROL 下載]**.

當您選取要下載的資料夾時，將會下載資料夾下的完整資產階層。 若要將您下載的每個資產（包括父資料夾下巢狀子資料夾中的資產）納入個別資料夾中，請選取 **[!UICONTROL 為每個資產建立個別的資料夾]**.

## 啟用資產下載servlet {#enable-asset-download-servlet}

中的預設servlet [!DNL Experience Manager] 允許已驗證身分的使用者發出任意大型的並行下載請求，以建立對他們可見的資產的ZIP檔案，這會使伺服器和網路過載。 若要降低此功能所導致的潛在DoS風險， `AssetDownloadServlet` 發佈執行個體預設會停用OSGi元件。

若要允許從您的DAM下載資產，例如在使用Asset Share Commons或其他類似入口網站的實作時，請透過OSGi設定手動啟用servlet。 Adobe建議將允許的下載大小設定為儘可能的低，而不影響日常下載需求。 高值可能會影響效能。

1. 以定位發佈執行模式的命名慣例建立資料夾(`config.publish`)： `/apps/<your-app-name>/config.publish`. 若要定義執行模式的組態屬性，請參閱 [執行模式](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode).
1. 在設定資料夾中，建立檔案型別 `nt:file` 已命名 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. 填入 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` ，如下所示。 將下載的大小上限（以位元組為單位）設定為 `asset.download.prezip.maxcontentsize`. 以下範例將ZIP下載的大小上限設定為不超過100 kB。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

預設情況下， `GET` 下載檔案的要求， [!DNL Experience Manager] 對ZIP封存檔的下載大小強制執行50 MB的限制。 透過起始的下載 `POST` 此限制不會影響請求或使用者介面。

## 停用資產下載servlet {#disable-asset-download-servlet}

此 `Asset Download Servlet` 可以在上停用 [!DNL Experience Manager] 更新Dispatcher設定以封鎖任何資產下載請求來發佈執行個體。 也可以直接透過OSGi主控台手動停用servlet。

1. 若要透過Dispatcher設定封鎖資產下載請求，編輯 `dispatcher.any` 設定並將規則新增至 [篩選區段](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter). `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 若要在發佈執行個體上停用OSGi元件，請存取OSGi主控台： `http://[aem_server]:[port]/system/console/components`. 尋找 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` 並按一下 **[!UICONTROL 停用]**.

>[!MORELIKETHIS]
>
>* [使用Brand Portal下載資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)
>* [下載受DRM保護的資產](drm.md).
>* [在Win或Mac案頭上使用Experience Manager案頭應用程式下載資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets).
>* [使用支援的Adobe Creative Cloud應用程式中的Adobe資產連結下載資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html).

