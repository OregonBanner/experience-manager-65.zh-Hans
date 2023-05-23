---
title: 設定Dynamic Media - Scene7模式
description: 瞭解如何設定Dynamic Media - Scene7模式。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
source-git-commit: a8db862b4a90ee6679de44df9508caf75a4c3eec
workflow-type: tm+mt
source-wordcount: '6489'
ht-degree: 3%

---

# 設定Dynamic Media - Scene7模式{#configuring-dynamic-media-scene-mode}

如果您針對不同環境（例如開發、測試和生產）使用Adobe Experience Manager設定，請為每個環境設定Dynamic MediaCloud Services。

## Dynamic Media - Scene7模式的架構圖 {#architecture-diagram-of-dynamic-media-scene-mode}

下列架構圖說明Dynamic Media - Scene7模式的運作方式。

透過新架構，Experience Manager負責主要來源資產，並與Dynamic Media同步，以處理及發佈資產：

1. 主要來源資產上傳至Experience Manager後，會複製到Dynamic Media。 此時，Dynamic Media會處理所有資產處理和轉譯產生作業，例如視訊編碼和影像的動態變體。
(在Dynamic Media - Scene7模式中，預設上傳檔案大小為2 GB以下。 若要啟用2 GB到15 GB的上傳檔案大小，請參閱 [（可選）設定Dynamic Media - Scene7模式以上傳大於2 GB的資產](#optional-config-dms7-assets-larger-than-2gb).)
1. 產生轉譯後，Experience Manager可以安全地存取和預覽遠端Dynamic Media轉譯(不會將二進位檔案傳回Experience Manager執行個體)。
1. 內容準備好發佈並核准後，就會觸發Dynamic Media服務，將內容推送至傳遞伺服器，並在CDN （內容傳遞網路）快取內容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>下列功能清單會要求您使用Adobe Experience Manager - Dynamic Media隨附的現成可用CDN。 這些功能不支援任何其他自訂CDN。
>
>* [智能图像处理](/help/assets/imaging-faq.md)
>* [快取失效](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [直接連結保護](/help/assets/hotlink-protection.md)
>* [HTTP/2 内容交付](/help/assets/http2.md)
>* cdn層級的URL重新導向
>* Akamai ChinaCDN （用於在中國提供最佳傳遞）


## 在Scene7模式下啟用Dynamic Media {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 預設為停用。 若要使用Dynamic Media功能，您必須啟用它。

>[!WARNING]
>
>Dynamic Media - Scene7模式適用於 *僅限Experience Manager作者執行個體*. 因此，您必須設定 `runmode=dynamicmedia_scene7` 在Experience Manager作者執行個體上， *not* Experience Manager發佈執行個體。

若要啟用Dynamic Media，請使用啟動Experience Manager `dynamicmedia_scene7` 在終端機視窗中輸入下列內容，從命令列執行模式（使用的範例連線埠為4502）：

```shell {.line-numbers}
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （可選）將Dynamic Media預設集和設定從6.3移轉至6.5 （零停機時間） {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

將Experience ManagerDynamic Media從6.3升級至6.4或6.5時，現在包含零停機部署的功能。 若要移轉您的所有預設集和設定，請從 `/etc` 至 `/conf` 在CRXDE Lite中，請確定您執行下列curl命令。

>[!NOTE]
>
>如果您以相容性模式執行Experience Manager執行個體（即已安裝相容性套件），則不需要執行這些命令。

對於所有升級（無論是否包含相容性套件），您可以執行下列Linux® curl命令，複製最初隨Dynamic Media提供的預設現成檢視器預設集：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

移轉您建立的任何自訂檢視器預設集和設定 `/etc` 至 `/conf`，執行下列Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 安裝Feature Pack 18912以進行大量資產移轉 {#installing-feature-pack-for-bulk-asset-migration}

Feature Pack 18912的安裝為 *可選*.

Feature Pack 18912可讓您透過FTP大量擷取資產，或在Experience Manager時從Dynamic Media — 混合模式或Dynamic Media Classic移轉至Dynamic Media - Scene7模式。 可從以下網址取得： [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

另請參閱 [安裝Feature Pack 18912以進行大量資產移轉](/help/assets/bulk-ingest-migrate.md) 以取得詳細資訊。

## 在Cloud Services中建立Dynamic Media設定 {#configuring-dynamic-media-cloud-services}

<!-- **Before you configure Dynamic Media** - After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials.

   ![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**To create a Dynamic Media Configuration in Cloud Services:** -->

1. 在Experience Manager作者模式中，選取Experience Manager標誌以存取全域導覽主控台，並選取「工具」圖示，然後前往 **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media設定]**.
1. 在Dynamic Media設定瀏覽器頁面的左側窗格中，選取 **[!UICONTROL 全域]** (請勿選取左側的資料夾圖示 **[!UICONTROL 全域]**)，然後選取 **[!UICONTROL 建立]**.
1. 於 **[!UICONTROL 建立Dynamic Media設定]** 頁面，輸入標題、Dynamic Media帳戶電子郵件地址、密碼，然後選取您的地區。 此資訊是透過在布建電子郵件中Adobe而提供給您的。 如果您沒有收到電子郵件，請聯絡Adobe客戶支援。

   選取 **[!UICONTROL 連線至Dynamic Media]**.

1. 在 **[!UICONTROL 變更密碼]** 對話方塊，在 **[!UICONTROL 新密碼]** 欄位中，輸入包含8-25個字元的新密碼。 密碼至少必須包含下列其中一項：

   * 大寫字母
   * 小寫字母
   * 数字
   * 特殊字元： `# $ & . - _ : { }`

   此 **[!UICONTROL 目前密碼]** 欄位會刻意預先填入並在互動中隱藏。

   如有必要，您可以選取密碼眼睛圖示以顯示密碼，以檢查您輸入或重新輸入的密碼的拼字。 再次選取圖示以隱藏密碼。

1. 在 **[!UICONTROL 重複密碼]** 欄位，重新輸入新密碼，然後選取 **[!UICONTROL 完成]**.

   新密碼會在您選取時儲存 **[!UICONTROL 儲存]** 右上角的 **[!UICONTROL 建立Dynamic Media設定]** 頁面。

   如果您已選取 **[!UICONTROL 取消]** 在 **[!UICONTROL 變更密碼]** 對話方塊，您仍必須在儲存新建立的Dynamic Media設定時輸入新密碼。

   另請參閱 [變更Dynamic Media的密碼](#change-dm-password).

1. 連線成功後，請設定下列專案。 含有星號(*)的標題為必填：

   * **[!UICONTROL 公司]** - Dynamic Media帳戶的名稱。
      >[!IMPORTANT]
      一個Experience Manager執行個體僅支援Cloud Services中的一個Dynamic Media設定；請勿新增多個設定。 一個Experience Manager執行個體上的多個Dynamic Media設定為 _not_ 受Adobe支援或建議。

      <!-- CQDOC-19579 and CQDOC-19612 -->

      另請參閱 [設定Dynamic Media公司別名帳戶](/help/assets/dm-alias-account.md).

   * **[!UICONTROL 公司根文件夹路径]**

   * **[!UICONTROL 發佈資產]**  — 您可從下列三個選項中選擇：
      * **[!UICONTROL 立即]** 這表示上傳資產時，系統會擷取資產並立即提供URL/內嵌。 發佈資產不需要使用者介入。
      * **[!UICONTROL 啟動時]** 這表示在提供URL/內嵌連結之前，您必須先明確發佈資產。<br><!-- CQDOC-17478, Added March 9, 2021-->從Experience Manager6.5.8開始，Experience Manager發佈例項會反映正確的Dynamic Media中繼資料值，例如 `dam:scene7Domain` 和 `dam:scene7FileStatus` 在 **[!UICONTROL 啟動時]** 僅發佈模式。 若要啟用此功能，請安裝Service Pack 8，然後重新啟動Experience Manager。 前往Sling設定管理員。 尋找的設定 `Scene7ActivationJobConsumer Component` 或建立新檔案)。 選取核取方塊 **[!UICONTROL 在Dynamic Media發佈後復寫中繼資料]**，然後選取 **[!UICONTROL 儲存]**.

         ![「Dynamic Media發佈後復寫中繼資料」核取方塊](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 選擇性發佈]** 此選項可讓您控制在Dynamic Media中發佈哪些資料夾。 它可讓您使用智慧型裁切或動態轉譯等功能，或決定哪些資料夾僅以Experience Manager發佈以供預覽。 這些相同的資產為 *not* 在Dynamic Media中發佈，以便在公共網域中傳送。<br>您可以在這裡設定此選項 **[!UICONTROL Dynamic Media雲端設定]** 或者，您也可以選擇在檔案夾的檔案夾層級中設定此選項 **[!UICONTROL 屬性]**.<br>另請參閱 [在Dynamic Media中使用選擇性發佈](/help/assets/selective-publishing.md).<br>如果您稍後變更此設定，或稍後在檔案夾層級變更此設定，則這些變更只會影響您從此時間點之後上傳的新資產。 資料夾中現有資產的發佈狀態將維持不變，直到您從以下任一位置手動變更資產為止 **[!UICONTROL 快速發佈]** 或 **[!UICONTROL 管理發布]** 對話方塊。
   * **[!UICONTROL 安全預覽伺服器]**  — 可讓您指定安全轉譯預覽伺服器的URL路徑。 也就是說，產生轉譯後，Experience Manager可以安全地存取和預覽遠端Dynamic Media轉譯(不會將二進位檔傳回Experience Manager執行個體)。
除非您有特殊安排要使用您自己公司的伺服器或特殊伺服器，否則Adobe建議您保留此設定。

   * **[!UICONTROL 同步所有內容]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->預設為選取。 如果您想要選擇性地在同步至Dynamic Media時包含或排除資產，請取消選取此選項。 取消選取此選項可讓您從下列兩種Dynamic Media同步模式中選擇：

   * **[!UICONTROL Dynamic Media 同步模式]**
      * **[!UICONTROL 預設為啟用]**  — 除非您特別將資料夾標籤為排除，否則預設情況下，設定會套用至所有資料夾。 <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL 預設為停用]**  — 除非您明確標籤選取的資料夾以同步至Dynamic Media，否則此設定不會套用至任何資料夾。
若要將選取的資料夾標示為同步至Dynamic Media，請選取資產資料夾，然後在工具列上選取 **[!UICONTROL 屬性]**. 於 **[!UICONTROL 詳細資料]** 標籤，在 **[!UICONTROL Dynamic Media同步模式]** 從下拉式清單中選擇下列三個選項。 完成後，選取 **[!UICONTROL 儲存]**. *請記住：如果您選取「 」，則以下三個選項不可用&#x200B;**[!UICONTROL 同步所有內容]**較早。* 另請參閱 [在Dynamic Media中使用資料夾層級的選擇性發佈](/help/assets/selective-publishing.md).
         * **[!UICONTROL 已繼承]**  — 資料夾上沒有明確的同步值；相反地，資料夾繼承其上級資料夾之一或雲端設定中的預設模式的同步值。 繼承的詳細狀態會透過工具提示顯示。
         * **[!UICONTROL 為子資料夾啟用]**  — 包含此子樹狀結構中的所有專案，以便同步至Dynamic Media。 資料夾特定的設定會覆寫雲端設定中的預設模式。
         * **[!UICONTROL 已針對子資料夾停用]**  — 將此子樹狀結構中的所有專案從同步到Dynamic Media中排除。

   >[!NOTE]
   Dynamic Media - Scene7模式中不支援版本設定。 此外，仅当“编辑 Dynamic Media 配置”页面中的&#x200B;**[!UICONTROL 发布资产]**&#x200B;设置为&#x200B;**[!UICONTROL 激活时]**&#x200B;时，并且直到首次激活资产时延迟激活才适用。
   資產啟動後，所有更新都會立即即時發佈到S7傳送。

1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 為了在發佈Dynamic Media內容之前安全地預覽內容，Experience Manager Author會使用權杖型驗證，因此Experience Manager Author預設會預覽Dynamic Media內容。 不過，您可以「允許列出」更多IP，讓使用者存取安全地預覽內容。 若要在Experience Manager中設定此動作，請參閱 [設定影像伺服器的Dynamic Media發佈設定 — 安全性索引標籤](/help/assets/dm-publish-settings.md#security-tab).

如果您想進一步自訂您的設定，例如啟用ACL （存取控制清單）許可權，您可以選擇完成以下任何工作 [（可選）在Dynamic Media - Scene7模式中設定進階設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

<!-- 1. To securely preview Dynamic Media content before it gets published, Experience Manager uses token-based validation and hence Experience Manager Author previews Dynamic Media content by default. However, you can *allowlist* more IPs to provide users access to securely preview content. To set up this action in Experience Manager, see [Configure Dynamic Media Publish Setup for Image Server - Security tab](/help/assets/dm-publish-settings.md#security-tab).     * In Experience Manager Author mode, select the Experience Manager logo to access the global navigation console.
    * In the left rail, select the **[!UICONTROL Tools]** icon, then go to **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
    * On the Dynamic Media Image Server page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * Select the **[!UICONTROL Security]** tab.
    * For the **[!UICONTROL Client address]**, select **[!UICONTROL Add]**.
    * Enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * In the upper-right corner of the page, select **[!UICONTROL Save]**. -->

您現在已完成基本設定；您已準備好使用Dynamic Media - Scene7模式。

### 變更Dynamic Media的密碼 {#change-dm-password}

Dynamic Media中的密碼到期日設定為從目前系統日期算起100年。

密碼至少必須包含下列其中一項：

* 大寫字母
* 小寫字母
* 数字
* 特殊字元： `# $ & . - _ : { }`

如有必要，您可以選取密碼眼睛圖示以顯示密碼，以檢查您輸入或重新輸入的密碼的拼字。 再次選取圖示以隱藏密碼。

當您選取時，已變更的密碼會儲存 **[!UICONTROL 儲存]** 右上角的 **[!UICONTROL 編輯Dynamic Media設定]** 頁面。

**若要變更Dynamic Media的密碼：**

1. 在Experience Manager作者模式中，選取Experience Manager標誌以存取全域導覽主控台。
1. 在主控台左側，選取「工具」圖示，然後前往 **[!UICONTROL Cloud Services] > [!UICONTROL Dynamic Media設定]**.
1. 在Dynamic Media設定瀏覽器頁面的左側窗格中，選取 **[!UICONTROL 全域]**. 請勿選取左側的資料夾圖示 **[!UICONTROL 全域]**. 然後，選取 **[!UICONTROL 編輯]**.
1. 於 **[!UICONTROL 編輯Dynamic Media設定]** 頁面，緊接在 **[!UICONTROL 密碼]** 欄位，選取 **[!UICONTROL 變更密碼]**.
1. 在 **[!UICONTROL 變更密碼]** 對話方塊中，執行下列動作：

   * 在 **[!UICONTROL 新密碼]** 欄位，輸入新密碼。

      此 **[!UICONTROL 目前密碼]** 欄位會刻意預先填入並在互動中隱藏。

   * 在 **[!UICONTROL 重複密碼]** 欄位，重新輸入新密碼，然後選取 **[!UICONTROL 完成]**.

1. 在的右上角 **[!UICONTROL 編輯Dynamic Media設定]** 頁面，選取 **[!UICONTROL 儲存]**，然後選取 **[!UICONTROL 確定]**.

## （可選）在Dynamic Media - Scene7模式中設定進階設定 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

如果您想要進一步自訂Dynamic Media - Scene7模式的設定和設定，或最佳化其效能，您可以完成下列一或多個作業 *可選* 任務：

* [（選用）在Dynamic Media - Scene7模式中啟用ACL許可權](#optional-enable-acl)

* [（可選）設定Dynamic Media - Scene7模式以上傳大於2 GB的資產](#optional-config-dms7-assets-larger-than-2gb)

* [（可選） Dynamic Media的設定和設定 — Scene7模式設定](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [（可選）調整Dynamic Media - Scene7模式的效能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [（選用）篩選資產以進行復寫](#optional-filtering-assets-for-replication)

### （選用）在Dynamic Media - Scene7模式中啟用存取控制清單許可權 {#optional-enable-acl}

當您在AEM上執行Dynamic Media - Scene7模式時，它目前會轉送 `/is/image` 要求在不檢查PlatformServerServlet上的ACL （存取控制清單）許可權的情況下保護預覽影像伺服。 不過，您可以： *啟用* acl許可權。 這樣做會轉寄授權的 `/is/image` 要求。 如果使用者無權存取資產，則會顯示「403 — 禁止」錯誤。

**若要在Dynamic Media - Scene7模式中啟用ACL許可權：**

1. 在Experience Manager中導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 隨即開啟新的瀏覽器索引標籤，其中包含 **[!UICONTROL Adobe Experience Manager Web主控台設定]** 頁面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在頁面上，捲動至名稱 *Adobe CQ Scene7平台伺服器*.

1. 在名稱的右側，選取鉛筆圖示(**[!UICONTROL 編輯設定值]**)。

1. 於 **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** 頁面中，選取下列兩個設定的核取方塊：

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name`  — 啟用時，此設定會快取許可權結果兩分鐘（預設）以儲存。
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name`  — 啟用時，此設定會在使用者透過Dynamic Media Image Server預覽資產時驗證使用者的存取權。

   ![在Dynamic Media - Scene7模式中啟用存取控制清單設定](/help/assets/assets-dm/acl.png)

1. 在頁面的右下角附近，選取 **[!UICONTROL 儲存]**.

### （可選）設定Dynamic Media - Scene7模式以上傳大於2 GB的資產 {#optional-config-dms7-assets-larger-than-2gb}

在Dynamic Media - Scene7模式中，預設的資產上傳檔案大小為2 GB以下。 不過，您可以選擇設定大於2 GB和最大15 GB的資產上傳。

如果您打算使用此功能，請注意下列必要條件和要點：

* 您必須以Dynamic Media - Scene7模式執行Experience Manager6.5搭配Service Pack 6.5.4.0或更新版本。
* 僅支援此大型上傳功能 [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) 客戶。
* 請確定您的Experience Manager執行個體已設定為Amazon S3或Microsoft® Azure Blob儲存體。

   >[!NOTE]
   使用存取金鑰和秘密金鑰設定Azure Blob儲存體，因為Blob儲存體設定中的AzureSas不支援此大型上傳功能。

* Oak&#39;s [直接二進位存取下載](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) 已啟用(Oak) *直接二進位存取上傳* 非必要)。

   若要啟用直接二進位存取下載，請設定屬性 `presignedHttpDownloadURIExpirySeconds > 0` 在資料存放區設定中。 值應該足夠長，以便下載較大的二進位檔，並且可能重試。

* 不會上傳大於15 GB的資產。 （大小限制是在下方的步驟8中設定。）
* 當 **[!UICONTROL Dynamic Media重新處理]** 資產工作流程會在資料夾上觸發，重新處理任何已與Dynamic Media公司同步的大型資產。 不過，如果資料夾中尚未同步任何大型資產，則不會上傳資產。 因此，若要同步Dynamic Media中現有的大型資產，您可以執行 **[!UICONTROL Dynamic Media重新處理]** 資產對個別資產的工作流程。

**若要設定Dynamic Media - Scene7模式以上傳大於2 GB的資產：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.

1. 在CRXDE Lite視窗中，執行下列任一項作業：

   * 在左側邊欄中，導覽至下列路徑：

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 將上方路徑複製並貼到工具列下方的CRXDE Lite路徑欄位中，然後按下 `Enter`.

1. 在左側欄中，以滑鼠右鍵按一下 `fileupload`，然後從彈出式選單中選取 **[!UICONTROL 覆蓋節點]**.

   ![覆蓋節點選項](/help/assets/assets-dm/uploadassets15gb_a.png)

1. 在「覆蓋節點」對話方塊中，選取 **[!UICONTROL 符合節點型別]** 核取方塊以啟用（開啟）選項，然後選取 **[!UICONTROL 確定]**.

   ![覆蓋節點對話方塊](/help/assets/assets-dm/uploadassets15gb_b.png)

1. 從「CRXDE Lite」視窗，執行下列任一項作業：

   * 在左側邊欄中，導覽至下列覆蓋節點路徑：

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 將上方路徑複製並貼到工具列下方的CRXDE Lite路徑欄位中，然後按下 `Enter`.

1. 在 **[!UICONTROL 屬性]** 標籤，在 **[!UICONTROL 名稱]** 欄，找出 `sizeLimit`.
1. 右側 `sizeLimit` 名稱，在 **[!UICONTROL 值]** 欄中，連按兩下「值」欄位。
1. 輸入適當的值（位元組），以便將大小限制增加到所需的最大上傳大小。 例如，若要將上傳資產大小限制增加到10 GB，請輸入 `10737418240` 在值欄位中。
您可以輸入最多15 GB的值(`2013265920` 位元組)。 在此情況下，不會上傳大於15 GB的已上傳資產。

   ![大小限制值](/help/assets/assets-dm/uploadassets15gb_c.png)

1. 在CRXDE Lite視窗的左上角附近，選取 **[!UICONTROL 全部儲存]**.

   *現在，執行下列動作，設定AdobeGranite工作流程外部程式作業處理常式的逾時：*

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。
1. 執行下列任一項作業：

   * 導覽至下列URL路徑：

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 將上方路徑複製並貼到瀏覽器的URL欄位中。 請務必取代 `localhost:4502` 使用您自己的Experience Manager執行個體。

1. 在 **[!UICONTROL AdobeGranite工作流程外部程式工作處理常式]** 對話方塊，在 **[!UICONTROL 最大逾時]** 欄位，將值設為 `18000` 分鐘（5小時）。 預設為10800分鐘（三個小時）。

   ![逾時值上限](/help/assets/assets-dm/uploadassets15gb_d.png)

1. 在對話方塊的右下角，選取 **[!UICONTROL 儲存]**.

   *現在，請執行下列動作，設定Scene7直接二進位上傳程式步驟的逾時：*

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。
1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 在「工作流程模型」頁面上，選擇 **[!UICONTROL Dynamic Media編碼影片]**.
1. 在工具列上，選取 **[!UICONTROL 編輯]**.
1. 在工作流程頁面上，按兩下 **[!UICONTROL Scene7直接二進位上傳]** 程式步驟。
1. 在 **[!UICONTROL 步驟屬性]** 對話方塊，在 **[!UICONTROL 通用]** 標籤，在 **[!UICONTROL 進階設定]** 標題，在 **[!UICONTROL 逾時]** 欄位，輸入值 `18000` 分鐘（5小時）。 預設值為 `3600` 分鐘（一小時）。
1. 選取 **[!UICONTROL 確定]**.
1. 選取 **[!UICONTROL 同步]**.
1. 對重複步驟14到21 **[!UICONTROL DAM更新資產]** 工作流程模型和 **[!UICONTROL Dynamic Media重新處理]** 工作流程模型。

### （可選） Dynamic Media的設定和設定 — Scene7模式設定 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [設定影像伺服器的Dynamic Media發佈設定](/help/assets/dm-publish-settings.md)
* [設定Dynamic Media一般設定](/help/assets/dm-general-settings.md)
* [設定色彩管理](#configuring-color-management)
* [編輯支援格式的MIME型別](#editing-mime-types-for-supported-formats)
* [針對不支援的格式新增MIME型別](#adding-mime-types-for-unsupported-formats)
* [建立批次集預設集以自動生成影像集和迴轉集](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) (在Dynamic Media Classic使用者介面中完成)

#### 設定影像伺服器的Dynamic Media發佈設定 {#publishing-setup-for-image-server}

「Dynamic Media發佈設定」頁面會建立預設設定，以判斷如何將資產從Adobe Dynamic Media伺服器傳送至網站或應用程式。

另請參閱 [設定影像伺服器的Dynamic Media發佈設定](/help/assets/dm-publish-settings.md).

#### 設定Dynamic Media一般設定 {#configuring-application-general-settings}

設定Dynamic Media **[!UICONTROL 發佈伺服器名稱]** URL和 **[!UICONTROL 原始伺服器名稱]** URL。 您也可以指定 **[!UICONTROL 上傳至應用程式]** 設定和 **[!UICONTROL 預設上傳選項]** 全都是根據您的特定使用案例。

另請參閱 [設定Dynamic Media一般設定](/help/assets/dm-general-settings.md).

#### 設定色彩管理 {#configuring-color-management}

Dynamic Media色彩管理可讓您校正資產的色彩。 透過色彩校正，擷取的資產可保留其色彩空間(RGB、CMYK、灰色)和內嵌色彩設定檔。 當您請求動態轉譯時，會使用CMYK、RGB或灰階輸出將影像色彩校正到目標色彩空間。

另請參閱 [設定影像預設集](/help/assets/managing-image-presets.md).

>[!NOTE]
依預設，當您選取時，系統會顯示15個轉譯 **[!UICONTROL 轉譯]** 和15個檢視器預設集 **[!UICONTROL 檢視者]** 在資產的「詳細資訊」檢視中。 您可以提高此限制。另請參閱 [增加顯示的影像預設集數目](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 或 [增加顯示的檢視器預設集數目](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### 編輯支援格式的MIME型別 {#editing-mime-types-for-supported-formats}

您可以定義Dynamic Media要處理的資產型別，並自訂進階資產處理引數。 例如，您可以指定資產處理引數，以執行下列作業：

* 將Adobe PDF轉換為eCatalog資產。
* 將Adobe Photoshop檔案(.PSD)轉換為橫幅範本資產以進行個人化。
* 點陣化Adobe Illustrator檔案(.AI)或Adobe Photoshop封裝PostScript®檔案(.EPS)。
* [視訊設定檔](/help/assets/video-profiles.md) 和 [影像設定檔](/help/assets/image-profiles.md) 分別可用來定義視訊和影像的處理方式。

另請參閱 [正在上傳資產](/help/assets/manage-assets.md#uploading-assets).

**若要編輯支援格式的MIME型別：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 在左側邊欄中，導覽至下列專案：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME型別](assets/mimetypes.png)

1. 在mimeTypes資料夾下，選取mime型別。
1. 在CRXDE Lite頁面的右側，下半部：

   * 連按兩下 **[!UICONTROL 已啟用]** 欄位。 預設會啟用所有資產MIME型別(設為 **[!UICONTROL true]**)，這表示資產會同步至Dynamic Media以進行處理。 如果您想從處理中排除此資產MIME型別，請將此設定變更為 **[!UICONTROL false]**.

   * 點兩下 **[!UICONTROL jobParam]** 以開啟其關聯的文字欄位。 另請參閱 [支援的Mime型別](/help/assets/assets-formats.md#supported-mime-types) 取得可用於指定mime型別的允許處理引數值清單。

1. 执行下列操作之一：

   * 重複步驟3-4以編輯更多MIME型別。
   * 在CRXDE Lite頁面的功能表列上，選取 **[!UICONTROL 全部儲存]**.

1. 在頁面的左上角，選取 **[!UICONTROL CRXDE Lite]** 以返回Experience Manager。

#### 針對不支援的格式新增MIME型別 {#adding-mime-types-for-unsupported-formats}

您可以針對Experience Manager Assets中不支援的格式新增自訂MIME型別。 透過將MIME型別移到之前，確保Experience Manager不會刪除您在CRXDE Lite中新增的任何新節點 `image_`. 此外，請確定其啟用值設為 **[!UICONTROL false]**.

**若要針對不支援的格式新增MIME型別：**

1. 在Experience Manager中導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 隨即開啟新的瀏覽器索引標籤，其中包含 **[!UICONTROL Adobe Experience Manager Web主控台設定]** 頁面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，向下滚动到名称 *Adobe CQ Scene7 Asset MIME 类型服务*，如下面的屏幕截图所示。在名稱的右側，選取 **[!UICONTROL 編輯設定值]** （鉛筆圖示）。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 於 **Adobe CQ Scene7資產MIME型別服務** 頁面，選取任何加號圖示&lt;+>。 在表格中選取加號以新增新MIME型別的位置並不重要。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 型別 `DWG=image/vnd.dwg` 在空白文字欄位中新增。

   範例 `DWG=image/vnd.dwg` 僅供示範之用。 您在這裡新增的MIME型別可以是任何其他不受支援的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在頁面的右下角，選取 **[!UICONTROL 儲存]**.

   此時，您可以關閉已開啟Adobe Experience Manager Web主控台設定頁面的瀏覽器索引標籤。

1. 返回具有已開啟Experience Manager主控台的瀏覽器標籤。
1. 在Experience Manager中導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左側邊欄中，導覽至下列專案：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖曳MIME型別 `image_vnd.dwg` 並將其直接拖曳到上方 `image_` 在樹狀結構中，如下列熒幕擷圖所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 使用MIME型別 `image_vnd.dwg` 仍然選取，從 **[!UICONTROL 屬性]** 標籤，在 **[!UICONTROL 已啟用]** 列，在 **[!UICONTROL 值]** 欄標題，點兩下值以開啟 **[!UICONTROL 值]** 下拉式清單。
1. 型別 `false` 在欄位中(或選取 **[!UICONTROL false]** （從下拉式清單中選取）。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite頁面的左上角附近，選取 **[!UICONTROL 全部儲存]**.

#### 建立批次集預設集以自動生成影像集和迴轉集 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

資產上傳至Dynamic Media時，使用批次集預設集可自動建立影像集或迴轉集。

首先，定義資產在集合中分組的命名慣例。 然後建立批次集預設集，這是唯一命名的、獨立的一組指示。 它必須定義如何使用符合預設集中定義的命名約定的影像來建構集合。

上傳檔案時，Dynamic Media會自動建立一個集合，其中包含與作用中預設集中定義的命名慣例相符的所有檔案。

##### 設定預設命名

建立用於任何批次集預設集配方中的預設命名慣例。 在批次集預設集定義中選取的預設命名慣例可能是貴公司批次產生集所需的一切。 會建立批次集預設集，以使用您定義的預設命名慣例。 當公司定義的預設命名有例外情況時，您可以針對特定內容集建立所需數量的批次集預設集，並採用替代的自訂命名慣例。

雖然設定預設命名慣例並非使用批次集預設集功能所必需，但最佳實務建議您使用預設命名慣例。 它可讓您定義命名慣例的元素，並將這些元素分組到一個集中，以便簡化批次集的建立。

另外，您也可以使用 **[!UICONTROL 檢視程式碼]** 沒有可用的表單欄位。 在此檢視中，您完全使用規則運算式來建立命名慣例定義。

定義、比對和基底名稱有兩個元素可用。 這些欄位可讓您定義命名慣例的所有元素，並識別用來命名包含這些元素的集的慣例部分。 公司的個別命名慣例通常會對每個元素使用一或多行定義。 您可以針對唯一的定義使用儘可能多的線條，並將其群組為不同的元素，例如針對「主要影像」、「顏色」元素、「替代檢視」元素和「色票」元素。

**設定預設命名：**

1. 開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   Adobe在布建時已提供您的認證和登入詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在靠近頁面頂端的導覽列上，導覽至 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 批次集預設集]** > **[!UICONTROL 預設命名]**.
1. 选择&#x200B;**[!UICONTROL 查看表单]**&#x200B;或&#x200B;**[!UICONTROL 查看代码]**，以指定要查看的方式并输入有关每个元素的信息。

   您可以選取 **[!UICONTROL 檢視程式碼]** 核取方塊，以檢視表單選取專案旁的規則運算式值建置。 如果表單檢視因任何原因限制您，您可以輸入或變更這些值，以協助定義命名慣例的元素。 如果無法在表單檢視中剖析您的值，則表單欄位會變成非作用中。

   >[!NOTE]
   停用的表單欄位不會驗證規則運算式是否正確。 您會看到針對「結果」行之後的每個元素所建置的規則運算式結果。 完整的規則運算式會顯示在頁面底部。

1. 視需要展開每個元素，並輸入您要使用的命名慣例。
1. 視需要執行下列任一項作業：

   * 選取 **[!UICONTROL 新增]** 為元素新增其他命名慣例。
   * 選取 **[!UICONTROL 移除]** 刪除元素的命名慣例。

1. 执行下列操作之一：

   * 選取 **[!UICONTROL 另存為]** 並輸入預設集的名稱。
   * 選取 **[!UICONTROL 儲存]** 如果您正在編輯現有的預設集。

##### 建立批次集預設集

Dynamic Media使用批次集預設集將資產組織成影像集（替代影像、顏色選項、360度迴轉），以便在檢視器中顯示。 批次集預設集會自動與資產上傳程式一起在Dynamic Media中執行。

您可以建立、編輯和管理批次集預設集。 批次集預設集定義有兩種形式：一種是可供設定的預設命名慣例，另一種是您即時建立的自訂命名慣例。

您可以使用表單欄位方法來定義批次集預設集，或使用程式碼方法來讓您使用規則運算式。 如同在「預設命名」中一樣，您可以在表單檢視中定義的同時選擇檢視程式碼，並使用規則運算式來建置定義。 或者，您也可以取消勾選任一檢視，以僅使用其中一個檢視。

**若要建立批次集預設集：**

1. 開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   Adobe在布建時已提供您的認證和登入詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在靠近頁面頂端的導覽列上，導覽至 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 批次集預設集]** > **[!UICONTROL 批次集預設集]**.

   **[!UICONTROL 檢視表單]**&#x200B;如「詳細資訊」頁面右上角所設定，是預設檢視。

1. 在「預設集清單」面板中，選取 **[!UICONTROL 新增]** 以啟動畫面右側「詳細資訊」面板中的定義欄位。
1. 在「詳細資訊」面板的「預設集名稱」欄位中，輸入預設集的名稱。
1. 在「批次集型別」下拉式選單中，選取預設集型別。
1. 执行下列操作之一：

   * 如果您使用先前在下設定的預設命名慣例 **[!UICONTROL 應用程式設定]** > **[!UICONTROL 批次集預設集]** > **[!UICONTROL 預設命名]**，展開 **[!UICONTROL 資產命名慣例]**，然後在「檔案命名」下拉式清單中，選取 **[!UICONTROL 預設]**.

   * 若要在設定預設集時定義新的命名慣例，請展開 **[!UICONTROL 資產命名慣例]**，然後在「檔案命名」下拉式清單中，選取 **[!UICONTROL 自訂]**.

1. 在「序列順序」中，定義影像集在Dynamic Media中分組後的顯示順序。

   依預設，您的資產會依字母數字排序。 不過，您可以使用逗號分隔的規則運算式清單來定義順序。

1. 在「設定命名和建立慣例」中，請為您在「資產命名慣例」中定義的基本名稱指定字尾或首碼。 此外，定義在Dynamic Media資料夾結構中建立資料集的位置。

   如果您定義大量集合，請將這些集合與包含資產本身的資料夾分開。 例如，建立「影像集」資料夾，並將產生的影像集放在此處。

1. 在「詳細資訊」面板中，選取 **[!UICONTROL 儲存]**.
1. 選取 **[!UICONTROL 作用中]** 新預設集名稱旁邊。

   啟用預設集可確保當您上傳資產至Dynamic Media時，批次集預設集會套用以產生該集合。

##### 建立批次集預設集以自動產生2D迴轉集

您可以使用「批次集型別」 **[!UICONTROL 多軸旋轉集]** 以建立可自動產生2D迴轉集的配方。 影像群組會使用Row和Column規則運算式，好讓影像資產在多維陣列的對應位置中正確對齊。 多軸旋轉集中沒有最小或最大列數或欄數。

例如，假設您要建立名為的多軸旋轉集 `spin-2dspin`. 您有一組包含三列的迴轉集影像，每列有12個影像。 這些影像的命名方式如下：

```xml {.line-numbers}
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

您可以使用此資訊，建立「批次集型態」配方，如下所示：

![chlimage_1-560](assets/chlimage_1-560.png)

迴轉集之共用資產名稱部分的分組會新增至 **[!UICONTROL 符合]** 欄位（反白顯示）。 资产名称中包含行和列的变量部分将分别添加到 **[!UICONTROL 行]** 和 **[!UICONTROL 列字段]** 。

上传和发布旋转集后，您可以激活&#x200B;**[!UICONTROL 上传作业选项]**&#x200B;对话框中&#x200B;**[!UICONTROL 批集预设]**&#x200B;下方 2D 旋转集方法的名称。

**若要建立批次集預設集以自動產生2D迴轉集：**

1. 開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的帳戶。

   Adobe在布建時已提供您的認證和登入詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在靠近頁面頂端的導覽列上，導覽至 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 批次集預設集]** > **[!UICONTROL 批次集預設集]**.

   **[!UICONTROL 檢視表單]**&#x200B;如「詳細資訊」頁面右上角所設定，是預設檢視。

1. 在「預設集清單」面板中，選取 **[!UICONTROL 新增]** 以啟動畫面右側「詳細資訊」面板中的定義欄位。
1. 在「詳細資訊」面板的「預設集名稱」欄位中，輸入預設集的名稱。
1. 在“批集类型”下拉菜单中，选择&#x200B;**[!UICONTROL 资产集]**。
1. 在「子型別」下拉式清單中，選取 **[!UICONTROL 多軸旋轉集]**.
1. 展開 **[!UICONTROL 資產命名慣例]**，然後在「檔案命名」下拉式清單中，選取 **[!UICONTROL 自訂]**.
1. 使用&#x200B;**[!UICONTROL 匹配]**&#x200B;和（可选）**[!UICONTROL 基本名称]**&#x200B;属性定义组成分组的图像资产命名的正则表达式。

   例如，您的常值Match規則運算式可能如下所示：

   `(w+)-w+-w+`

1. 展開 **[!UICONTROL 列欄位置]**，然後定義2D迴轉集陣列中影像資產位置的名稱格式。

   使用括弧括住檔案名稱中的列或欄位置。

   例如，對於列規則運算式，它看起來可能像這樣：

   `\w+-R([0-9]+)-\w+`

   或

   `\w+-(\d+)-\w+`

   對於欄規則運算式，它看起來可能像這樣：

   `\w+-\w+-C([0-9]+)`

   或

   `\w+-\w+-C(\d+)`

   上述範例僅供示範之用。 您可以視需要建立規則運算式。

   >[!NOTE]
   如果列和欄規則運算式的組合無法判斷資產在多維迴轉集陣列中的位置，則資產不會新增到集合中。 也會記錄錯誤。

1. 在「設定命名和建立慣例」中，請為您在「資產命名慣例」中定義的基本名稱指定字尾或首碼。

   此外，定義在Dynamic Media Classic資料夾結構中建立迴轉集的位置。

   如果您定義大量集合，請將這些集合與包含資產本身的資料夾分開。 例如，建立「迴轉集」資料夾，將產生的迴轉集放在此處。

1. 在「詳細資訊」面板中，選取 **[!UICONTROL 儲存]**.
1. 選取 **[!UICONTROL 作用中]** 新預設集名稱旁邊。

   啟用預設集可確保當您上傳資產至Dynamic Media時，批次集預設集會套用以產生該集合。

### （可選）調整Dynamic Media - Scene7模式的效能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

為了保持Dynamic Media - Scene7模式順暢運作，Adobe建議下列同步效能/可擴充性微調秘訣：

* 更新預先定義的「工作」引數以處理不同的檔案格式。
* 更新預先定義的Granite工作流程（視訊資產）佇列工作者執行緒。
* 更新預先定義的Granite暫時性工作流程（影像和非視訊資產）佇列工作者執行緒。
* 正在更新與Dynamic Media Classic伺服器的最大上傳連線。

#### 更新預先定義的作業引數以處理不同的檔案格式

您可以調整工作引數，以便在上傳檔案時更快處理。 例如，如果您上傳PSD檔案，但不想將其當成範本處理，您可以將圖層擷取設定為false （關閉）。 在這種情況下，調整的工作引數會如下所示： `process=None&createTemplate=false`.

如果您確實要開啟範本建立，請使用下列引數： `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建議針對PDF、PostScript®和PSD檔案使用下列「調整」工作引數：

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| 檔案型別 | 建議的工作引數 |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

若要更新任何這些引數，請遵循中的步驟 [啟用MIME型別型資產/Dynamic Media Classic上傳工作引數支援](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### 更新Granite暫時性工作流程佇列 {#updating-the-granite-transient-workflow-queue}

Granite傳輸工作流程佇列用於 **[!UICONTROL DAM更新資產]** 工作流程。 在Dynamic Media中，它用於影像擷取和處理。

**若要更新Granite暫時性工作流程佇列：**

1. 導覽至 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 並搜尋 **佇列： Granite暫時性工作流程佇列**.

   >[!NOTE]
   必須進行文字搜尋，而非直接URL，因為OSGi PID會動態產生。

1. 在 **[!UICONTROL 最大平行作業數]** 欄位中，將數字變更為所需的值。

   您可以增加 **[!UICONTROL 最大平行作業數]** 以充分支援將大量檔案上傳至Dynamic Media。 確切的值視硬體容量而定。 在某些情況下（即初始移轉或一次性大量上傳），您可以使用較大的值。 但是請注意，使用較大的值（例如兩倍的核心數量）可能會對其他並行活動產生負面影響。 因此，請根據您的特定使用案例測試並調整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新Granite工作流程佇列 {#updating-the-granite-workflow-queue}

Granite工作流程佇列用於非暫時性工作流程。 在Dynamic Media中，它過去是使用 **[!UICONTROL Dynamic Media編碼影片]** 工作流程。

**若要更新Granite工作流程佇列：**

1. 導覽至 `https://<server>/system/console/configMgr` 並搜尋 **佇列： Granite工作流程佇列**.

   >[!NOTE]
   必須進行文字搜尋，而非直接URL，因為OSGi PID會動態產生。

1. 在 **[!UICONTROL 最大平行作業數]** 欄位中，將數字變更為所需的值。

   您可以增加最大平行工作數量，以充分支援將大量檔案上傳至Dynamic Media。 確切的值視硬體容量而定。 在某些情況下（即初始移轉或一次性大量上傳），您可以使用較大的值。 但是請注意，使用較大的值（例如兩倍的核心數量）可能會對其他並行活動產生負面影響。 因此，請根據您的特定使用案例測試並調整值。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新Dynamic Media Classic上傳連線 {#updating-the-scene-upload-connection}

Scene7上傳連線設定會將Experience Manager資產同步至Dynamic Media Classic伺服器。

**若要更新Dynamic Media Classic上傳連線：**

1. 导航至 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在 **[!UICONTROL 連線數目]** 欄位和/或 **[!UICONTROL 作用中工作逾時]** 欄位，視需要變更數字。

   此 **[!UICONTROL 連線數目]** 設定可控制Experience Manager至Dynamic Media上傳所允許的HTTP連線數目上限；通常預先定義的10個連線值即足夠。

   此 **[!UICONTROL 作用中工作逾時]** 設定會決定已上傳Dynamic Media資產在傳遞伺服器上發佈的等待時間。 此值預設為2100秒或35分鐘。

   對於大多數使用案例，設定2100就足夠了。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

### （選用）篩選資產以進行復寫 {#optional-filtering-assets-for-replication}

在非Dynamic Media部署中，您需進行復寫 *全部* 資產（包括影像和視訊）從Experience Manager製作環境移至Experience Manager發佈節點。 此工作流程是必要的，因為Experience Manager Publish伺服器也會傳送資產。

不過，在Dynamic Media部署中，由於資產是透過Cloud Service傳送，因此不需要將這些相同的資產復寫至Experience Manager發佈節點。 這種「混合式發佈」工作流程可避免額外的儲存成本及較長的複製資產處理時間。 其他內容（例如網站頁面）會繼續從Experience Manager發佈節點提供。

這些篩選器可讓您 *排除* 資產無法復寫至Experience Manager發佈節點。

#### 使用預設的資產篩選器進行復寫 {#using-default-asset-filters-for-replication}

如果您使用Dynamic Media進行影像處理、製作視訊或兩者，則可以使用Adobe依現狀提供的預設濾鏡。 下列篩選器預設為作用中：

|  | 过滤器 | Mime型別 | 演绎版 |
| --- | --- | --- | --- |
| Dynamic Media影像傳送 | filter-image<br>篩選集 | 開頭為 **image/**<br>&#x200B;包含 **應用程式/** 結尾為 **set**. | 現成可用的「濾鏡影像」（適用於單一影像資產，包括互動式影像）和「濾鏡集」（適用於迴轉集、影像集、混合媒體集和轉盤集）將：<br>·從復寫中排除原始影像和靜態影像轉譯。 |
| Dynamic Media視訊傳送 | 濾鏡 — 視訊 | 開頭為 **video/** | 現成可用的「篩選視訊」將：<br>·從復寫中排除原始視訊和靜態縮圖轉譯。 |

>[!NOTE]
篩選器套用至MIME型別，且不能為路徑專用。

#### 自訂資產篩選器以進行復寫 {#customizing-asset-filters-for-replication}

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 在左側資料夾樹狀結構中，導覽至 `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` 以檢閱篩選器。

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. 若要定義篩選器的MIME型別，您可以依照以下步驟找到「MIME型別」：

   在左側邊欄中，展開 `content > dam > <locate_your_asset> > jcr:content > metadata`，然後在表格中，找出 `dc:format`.

   下圖為資產路徑至的範例： `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   請注意 `dc:format` 資產的 `Fiji Red.jpg` 是 `image/jpeg`.

   若要將此篩選套用至所有影像，無論其格式為何，請將此值設為 `image/*` 位置 `*` 是套用至任何格式之所有影像的規則運算式。

   若要讓篩選器僅套用至型別JPEG的影像，請輸入值 `image/jpeg`.

1. 定義您要在復寫中包含或排除的轉譯。

   您可以用來篩選復寫字元的字元包括：

   | 要使用的字元 | 如何篩選資產以進行復寫 |
   | --- | --- |
   | * | 通配符 |
   | + | 包含用於復寫的資產 |
   | - | 從復寫中排除資產 |

   导航到 `content/dam/<locate your asset>/jcr:content/renditions`。

   下圖是資產的轉譯範例。

   ![chlimage_1-4](assets/chlimage_1-4.png)

   如果您只想複製原始檔案，您可以輸入 `+original`.
