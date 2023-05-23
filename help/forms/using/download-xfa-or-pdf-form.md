---
title: 下載XFA或PDF表單範本
seo-title: Download an XFA or a PDF form template
description: 您可以將表單從存放庫匯出至本機系統，然後將下載的表單移轉至新的存放庫。
seo-description: You can export forms from the repository to the local system and migrate the downloaded forms to new repository.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Admin
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 下載XFA或PDF表單範本 {#download-an-xfa-or-a-pdf-form-template}

如名稱所示，下載作業可讓您將表單從存放庫匯出至本機系統。 結合上傳操作，此操作可幫助您將表單從一個存放庫移轉至另一個存放庫。

在AEM Forms中，下列資產型別支援下載操作：

* 表單範本(XFA Forms)
* PDF forms
* 檔案(平面PDF檔案)

AEM Forms支援個別下載這些表單型別，或是以包含一或多個受支援表單的資料夾下載。

除了這些資產外，您也可以下載 `Resource` 資產型別（如果存在於資料夾中）。 提供此功能是為了讓您下載XFA表單與表單一起引用的資源。

## 下載一或多個表單 {#download-one-or-more-forms}

1. 登入AEM Forms使用者介面，網址為 `https://<server>:<port>/aem/forms.html`.

1. 導覽至您要下載的資產位置。

1. 選取資產。 按一下 **[!UICONTROL 下載]** ![aem6forms_download](assets/aem6forms_download.png) 圖示加以檢視。

   >[!NOTE]
   >
   >您只能選取一個表單進行下載。 如果您想要下載多個表單，則必須將它們下載為資料夾。

1. 在出現的對話方塊中，按一下 **[!UICONTROL 下載]**.

   AEM Forms會產生一個包含所選檔案或所選資料夾的ZIP檔案。

   如果您正在下載資料夾，資料夾中支援的資產會以現有的階層下載。

   ZIP檔案會儲存至 `Downloads` 資料夾。

## 上傳作業的相關考量事項 {#related-considerations-for-the-upload-operation}

* 您可以將ZIP檔案上傳至相同存放庫或其他存放庫中的任何其他位置
* 上傳作業期間會保留資料夾中資產的階層
* 上傳時會反映下載前對已下載資產所做的任何中繼資料變更
