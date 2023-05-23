---
title: 建立新資料夾以將表單分類
seo-title: Create new folders to categorize forms
description: 使用資料夾來組織您的表單範本、PDF、資源和調適型表單。
seo-description: Use folders to organize your form templates, PDFs, resources, and adaptive forms.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# 建立新資料夾以將表單分類 {#create-new-folders-to-categorize-forms}

您可以使用資料夾更妥善地組織您的資產。 由於AEM Forms支援多種型別的資產(表單範本、PDF、檔案、資源和調適型表單)以及各種中繼資料，因此您可以使用資料夾根據所需的條件將表單分類。

AEM Forms可讓您變更資料夾的標題。 標題與存放庫中儲存資料夾的節點名稱不同。 而是保留標題作為資料夾的中繼資料。 如果您變更資料夾的標題，資料夾中存在的任何資產的路徑都不會受到影響。

## 建立資料夾 {#create-a-folder}

您可以透過下列其中一種方式，在AEM Forms中建立資料夾：

* 上傳包含所需資料夾結構中的資產的ZIP檔案(請參閱 [在AEM Forms中取得XDP和PDF檔案](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 建立新的空白資料夾

1. 登入AEM Forms使用者介面，網址為 `https://<server>:<port>/aem/forms.html`.
1. 導覽至您要建立資料夾的位置。
1. 按一下 ![aem6forms_add](assets/aem6forms_add.png) 圖示並選取「 」 **[!UICONTROL 建立資料夾]**.

1. 輸入下列詳細資料：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（必要）* 要在存放庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >依預設，名稱欄位的值會自動從標題中填入。 名稱只能包含英數字元，或連字型大小(-)和底線(_)特殊字元。 在標題中輸入的任何其他特殊字元都會自動取代為連字型大小，並提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯。

1. 按一下 **[!UICONTROL 提交].**

   具有您定義標題的新資料夾會顯示在資產清單中的目前位置。

   如果存在具有指定名稱的資料夾，提交會失敗並出現錯誤。 您可以將滑鼠懸停在錯誤上，檢視錯誤訊息 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 圖示顯示在名稱欄位旁。

### 編輯資料夾標題 {#edit-the-folder-title-br}

1. 選取您要編輯其標題的資料夾。
1. 按一下編輯 ![aem6forms_edit](assets/aem6forms_edit.png) 圖示加以檢視。
1. 輸入新標題。 文字欄位會預先填入資料夾標題的目前值。 您可以將其變更為新值。
1. 按一下 **[!UICONTROL 提交].**
