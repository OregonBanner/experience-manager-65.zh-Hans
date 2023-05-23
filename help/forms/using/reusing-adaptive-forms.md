---
title: 重複使用最適化表單
seo-title: Reusing adaptive forms
description: 您可以重複使用現有的最適化表單來建立新的最適化表單。
seo-description: You can reuse an existing adaptive form to create new adaptive forms.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# 重複使用最適化表單 {#reusing-adaptive-forms}

## 简介 {#introduction}

如果您想要使用現有最適化表單的某些屬性來產生新表單，您只需使用複製 — 貼上功能即可。 此外，您還可以在所需的資料夾路徑貼上新的最適化表單。 會複製所有中繼資料屬性，並複製XFA和XSD型調適型表單的XFA和XSD。

>[!NOTE]
>
>不會複製狀態和稽核詳細資料。 例如，如果您的最適化表單已發佈，然後您複製它時，貼上的最適化表單會處於未發佈狀態。 同樣地，如果正在稽核複製的資產，貼上的資產不會處於相同的稽核中。

### 複製最適化表單 {#copy-an-adaptive-form}

使用下列其中一種方法複製調適型表單：

1. 按一下複製 ![aem6forms_copy](assets/aem6forms_copy.png) 圖示加以檢視。

   >[!NOTE]
   >
   >快速動作是在滑鼠懸停時顯示在縮圖上的動作專案。

1. 選取最適化表單。 不同檢視的選取程式不同。

   如果您在卡片檢視中，請按一下選取專案以移至選取模式 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) 圖示並按一下您要複製的所有最適化表單。

   如果您在清單檢視中，請按一下所有最適化表單的核取方塊以選取它們。

   >[!NOTE]
   >
   >所有選取的資產都必須是調適型表單，因為調適型表單僅支援複製貼上功能，而且所有選取的資產都必須存在於相同的資料夾中。

   選取資產後，按一下副本 ![aem6forms_copy](assets/aem6forms_copy.png) 圖示出現在工具列上，用來複製選取的最適化表單。

### 貼上最適化表單 {#paste-an-adaptive-form}

按一下複製動作會自動退出選取模式並進行貼上 ![aem6forms_paste](assets/aem6forms_paste.png) 圖示可見。 現在前往所需的資料夾路徑，然後按一下貼上 ![aem6forms_paste](assets/aem6forms_paste.png) 圖示貼上複製的自適應表單。

如果您貼上同一個資料夾，或是另一個具有相同節點名稱的檔案（儲存於CRX存放庫中）存在於這個目標資料夾中，則會將1附加至尾碼(例如，myaf會變成myaf1，而如果myaf1存在於相同位置，myaf會變成myaf2。 所有其他屬性仍維持與原始的最適化表單相同。

按一下貼上之後 ![aem6forms_paste](assets/aem6forms_paste.png) 圖示中，則會再次隱藏。 您一次只能貼上一次。 若要再次建立相同資產的復本，請再次複製。

### 變更新最適化表單的內容 {#change-contents-of-new-adaptive-form}

已貼上的最適化表單內容可以使用以下方法變更，以與複製的表單不同：

1. **變更中繼資料屬性：**

   您可以變更最適化表單的中繼資料屬性，例如標題和說明。 如需有關中繼資料屬性及其變更方式的詳細資訊，請參閱 [管理表單中繼資料](/help/forms/using/manage-form-metadata.md)

1. **變更XFA/XSD型最適化Forms的XFA/XSD：**

   您可以變更最適化表單中使用的XFA/XSD。 若要瞭解如何變更這些最適化表單，請參閱 [管理表單中繼資料](/help/forms/using/manage-form-metadata.md)

1. **重新发布:**

   貼上的資產與複製的資產不同。 您可以將它發佈為新資產，以供一般使用者使用。 若要瞭解如何發佈資產，請參閱 [發佈和取消發佈表單](/help/forms/using/publishing-unpublishing-forms.md)
