---
title: 在AEM Forms中取得XDP和PDF檔案
seo-title: Getting XDP and PDF documents in AEM Forms
description: AEM Forms可讓您上傳表單和支援的資產，以便搭配最適化表單使用。 您也可以以ZIP檔形式大量上傳表單和相關資源。
seo-description: AEM Forms allows you to upload forms and supported assets to use with adaptive forms. You can also bulk upload forms and related resources as a ZIP.
uuid: cd49b4a8-c282-4059-95a0-c98f6c92ab14
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 28b9f1d6-6a52-458f-a8ed-a206502eda0d
docset: aem65
role: Admin
exl-id: 9ecdc50a-31e3-46ae-948a-d1f6e6085734
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# 在AEM Forms中取得XDP和PDF檔案{#getting-xdp-and-pdf-documents-in-aem-forms}

## 概述 {#overview}

您可以將表單上傳到AEM Forms，將表單從您的本機檔案系統匯入到CRX存放庫。 下列資產型別支援上傳作業：

* 表單範本（XFA表單）
* PDF forms
* 檔案(平面PDF檔案)

您可以個別上傳支援的資產型別，或當作ZIP封存檔上傳。 您可以上傳型別的資產 `Resource`，且僅與ZIP封存中的XFA表單並排。

>[!NOTE]
>
>確定您是 `form-power-users` 群組以上傳XDP檔案。 請聯絡您的管理員以成為群組的成員。

## 正在上傳表單 {#uploading-forms}

1. 透過存取登入AEM Forms使用者介面 `https://'[server]:[port]'/aem/forms.html`.
1. 導覽至您要上傳表單的資料夾或包含表單的資料夾。
1. 在動作工具列中，點選 **建立>檔案上傳**.

   ![「建立」下的「本機儲存體的檔案」選項](assets/step.png)

1. 上傳表單或封裝對話方塊可讓您瀏覽並選擇您要上傳的檔案。 檔案瀏覽器只會顯示支援的檔案格式(ZIP、XDP和PDF)。

   >[!NOTE]
   >
   >檔案名稱只能包含英數字元、連字型大小或底線。

1. 選擇檔案後按一下「上傳」以上傳檔案，或按一下「取消」取消上傳。 快顯視窗會列出在目前位置新增的資產和更新的資產。

   >[!NOTE]
   >
   >對於ZIP檔案，會顯示所有支援資產的相對路徑。 ZIP內不支援的資產會遭忽略，不會列出。 不過，如果ZIP封存僅包含不支援的資產，則會顯示錯誤訊息，而非快顯對話方塊。

   ![上傳XFA表單時顯示上傳對話方塊](assets/upload-scr.png)

1. 如果一或多個資產的檔案名稱無效，則會顯示錯誤。 修正以紅色反白顯示的檔案名稱，然後重新上傳。

   ![上傳XFA表單時出現錯誤訊息](assets/upload-scr-err.png)

上傳完成後，背景工作流程會根據資產的預覽為每個資產產生縮圖。 較新版本的資產（如果上傳）會覆寫現有資產。

### 受保護模式 {#protected-mode}

AEM Forms伺服器可讓您執行JavaScript程式碼。 惡意JavaScript程式碼可能會傷害AEM Forms環境。 保護模式會限制AEM Forms只從受信任的資產和位置執行XDP檔案。 AEM Forms UI中可用的所有XDP都視為受信任的資產。

受保護模式預設為開啟。 如有必要，您可以停用受保護模式：

1. 以管理員身分登入AEM Web Console。 URL為https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr
1. 開啟Mobile Forms設定以進行編輯。
1. 取消選取「受保護模式」選項，然後按一下 **儲存**. 受保護模式已停用。

## 更新參考的XFA表單 {#updating-referenced-xfa-forms}

在AEM Forms中，XFA表單範本可由最適化表單或其他XFA表單範本參照。 此外，範本可以參考資源或其他XFA範本。

引用XFA的最適化表單會有其欄位與XFA中可用的欄位繫結。 更新表單範本時，關聯的調適型表單會嘗試與XFA同步。 如需詳細資訊，請參閱 [將調適型表單與關聯的XFA同步](../../forms/using/synchronizing-adaptive-forms-xfa.md).

移除表單範本會損毀相依的最適化表單或表單範本。 這類最適化表單有時會被非正式地稱為「骯髒表單」。 在AEM Forms使用者介面中，您可以透過以下兩種方式找到已變更的表單。

* 資產清單中的最適化表單縮圖上會顯示警告圖示，而當您將指標停留在警告圖示上時，會顯示下列訊息。\
   `Schema/Form Template for this adaptive form has been updated so please go to Authoring mode and rebase it with new version.`

![更新相關XFA後針對不同步的最適化表單發出警告](assets/dirtyaf.png)

系統會維持旗標，指出最適化表單是否已變更。 此資訊可與表單中繼資料一併顯示在表單屬性頁面上。 僅適用於已修改的最適化表單，中繼資料屬性 `Model Refresh` 顯示 `Recommended` 值。

![最適化表單與XFA模型不同步的指示](assets/model-refresh.png)
