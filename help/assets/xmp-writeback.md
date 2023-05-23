---
title: XMP回寫至轉譯
description: 瞭解XMP回寫功能如何將資產的中繼資料變更傳播到資產的所有或特定轉譯。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# XMP回寫至轉譯 {#xmp-writeback-to-renditions}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | 本文 |

中的此XMP回寫功能 [!DNL Adobe Experience Manager Assets] 會將中繼資料變更複製到原始資產的轉譯。 當您從Assets內變更資產的中繼資料或上傳資產時，變更最初會儲存在資產階層中的中繼資料節點中。

XMP回寫功能可讓您將中繼資料變更傳播到資產的所有或特定轉譯。 功能只會回寫那些使用的中繼資料屬性 `jcr` 名稱空間，也就是名為的屬性 `dc:title` 會寫回，但有一個屬性命名為 `mytitle` 不是。

請考量您修改 [!UICONTROL 標題] 標題為的資產屬性 `Classic Leather` 至 `Nylon`.

![元数据](assets/metadata.png)

在此案例中， [!DNL Experience Manager Assets] 將變更儲存至 **[!UICONTROL 標題]** 中的屬性 `dc:title` 資產階層中儲存的資產中繼資料引數。

![metadata_stored](assets/metadata_stored.png)

不過， [!DNL Experience Manager Assets] 不會自動將任何中繼資料變更傳播到資產的轉譯。 另請參閱 [如何啟用XMP回寫](#enable-xmp-writeback).

## 啟用XMP回寫 {#enable-xmp-writeback}

若要讓中繼資料變更在上傳時傳播至資產的轉譯，請修改 **[!UICONTROL Adobe CQ DAM Rendition Maker]** Configuration Manager中的設定。

1. 若要開啟Configuration Manager，存取 `https://[aem_server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL Adobe CQ DAM Rendition Maker]** 設定。
1. 選取 **[!UICONTROL 傳播XMP]** 選項，然後儲存變更。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 啟用特定轉譯的XMP回寫 {#enabling-xmp-writeback-for-specific-renditions}

若要讓XMP回寫功能傳播中繼資料變更以選取轉譯，請將這些轉譯指定至XMP回寫程式工作流程步驟： [!UICONTROL DAM中繼資料回寫] 工作流程。 依預設，此步驟會使用原始轉譯進行設定。

若要讓XMP回寫功能將中繼資料傳播至轉譯縮圖140.100.png和319.319.png，請執行下列步驟。

1. 在Experience Manager介面中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 從「模型」頁面，開啟 **[!UICONTROL DAM中繼資料回寫]** 工作流程模型。
1. 在“ **[!UICONTROL DAM元数据写回]** ”属性页中，打开“ **[!UICONTROL XMP写回进程”步骤]** 。
1. 在 [!UICONTROL 步驟屬性] 對話方塊中，按一下 **[!UICONTROL 程式]** 標籤。
1. 在 **引數** 方塊，新增 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然後按一下 **[!UICONTROL 確定]**.

   ![step_properties](assets/step_properties.png)

1. 保存更改。
1. 若要重新產生金字塔TIFF轉譯 [!DNL Dynamic Media] 使用新屬性的影像，新增 **[!UICONTROL Dynamic Media程式影像資產]** 步驟至 [!UICONTROL DAM中繼資料回寫] 工作流程。

   PTIFF 呈现仅在 Dynamic Media Hybrid 实施中本地创建和存储。

1. 儲存工作流程。

中繼資料變更會傳播至資產的轉譯專案thumbnail.140.100.png和thumbnail.319.319.png，而非其他專案。

>[!NOTE]
>
>如需64位元Linux中的XMP回寫問題，請參閱 [如何在64位元RedHat Linux上啟用XMP回寫](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>如需支援的平台，請參閱 [XMP中繼資料回寫先決條件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## 篩選XMP中繼資料 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 對於從資產二進位檔讀取並在擷取資產時儲存在JCR中的XMP中繼資料，支援屬性/節點的封鎖清單和允許清單篩選。

使用封鎖清單進行篩選可讓您匯入所有XMP中繼資料屬性，但指定要排除的屬性除外。 然而，對於具有大量XMP中繼資料（例如1000個具有10,000個屬性的節點）的資產型別（例如INDD檔案），要篩選的節點名稱並不總是事先知道的。 如果使用封鎖清單進行篩選，可以匯入大量含有許多XMP中繼資料的資產， [!DNL Experience Manager] 部署可能會遇到穩定性問題，例如阻塞的觀察佇列。

透過允許清單篩選XMP中繼資料可讓您定義要匯入的XMP屬性，以解決此問題。 如此一來，任何其他或未知的XMP屬性都會被忽略。 為達到回溯相容性，您可以將其中一些屬性新增至使用封鎖清單的篩選器。

>[!NOTE]
>
>篩選僅適用於從資產二進位檔中的XMP來源衍生的屬性。 對於衍生自非XMP來源（例如EXIF和IPTC格式）的屬性，篩選無法運作。 例如，資產建立日期會儲存在名為的屬性中 `CreateDate` 以EXIFTIFF顯示。 Experience Manager會將此值儲存在名為的中繼資料欄位中 `exif:DateTimeOriginal`. 由於來源是非XMP來源，因此篩選無法在此屬性上運作。

1. 若要開啟Configuration Manager，存取 `https://[aem_server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL Adobe CQ DAM XmpFilter]** 設定。
1. 若要透過允許清單套用篩選，請選取 **[!UICONTROL 將允許清單套用至XMP屬性]**，並指定要匯入到的屬性 **[!UICONTROL 允許用於XMP篩選的XML名稱]** 方塊。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 若要透過允許清單套用篩選後，篩選掉封鎖的XMP屬性，請在 **[!UICONTROL XMP篩選的封鎖XML名稱]** 方塊。

   >[!NOTE]
   >
   >此 **[!UICONTROL 套用封鎖清單至XMP屬性]** 選項預設為選取。 換言之，使用封鎖清單的篩選功能預設為啟用。 若要停用此篩選，請取消選取 **[!UICONTROL 套用封鎖清單至XMP屬性]** 選項。

1. 保存更改。
