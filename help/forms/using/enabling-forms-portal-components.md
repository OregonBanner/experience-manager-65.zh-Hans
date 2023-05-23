---
title: 啟用表單入口網站元件
seo-title: Enabling forms portal components
description: 開箱即用的Forms Portal元件已停用。 啟用Document Services和Document Services述詞群組以啟用Forms Portal元件。
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 啟用表單入口網站元件 {#enabling-forms-portal-components}

開箱即用的Forms Portal元件無法使用。 若要讓元件出現在AEM sidekick的可用元件清單中，請執行以下步驟：

1. 登入網站的作者執行個體並開啟AEM Sites頁面。

1. 對於使用靜態範本的頁面，請執行下列步驟：

   1. 在頁首中，點選 ![畫佈下拉式清單](assets/canvas-drop-down.png) > **設計** 以在設計模式中開啟頁面。
   1. 點選任何元件（使用藍色邊框），然後點選 ![欄位層級](assets/field-level.png) 以選取包含目前元件的段落系統。
   1. 在段落系統中，點選 ![settings_icon](assets/settings_icon.png) 開啟段落系統的「編輯」對話方塊。
   1. 從清單 **[!UICONTROL 允許的元件]**，啟用核取方塊 **[!UICONTROL 檔案服務]** 和 **[!UICONTROL 檔案服務述詞]** 元件。 點選 **[!UICONTROL 確定]**.

1. 對於使用動態範本的頁面，請執行下列步驟：

   1. 在頁首中，點選 ![屬性](assets/properties.png) > **編輯範本** 以開啟頁面的範本。
   1. 點選 **配置容器** 並點選 ![摘要管理](/help/forms/using/assets/feedmanagement.png). 在 **允許的元件** 標籤，啟用 **Document Services和Document Services述詞** 選項，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>您也可以選取元件，以啟用這些類別中的特定元件。 如需有關元件及其使用方式的詳細資訊，請參閱 [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md) 和 [將連結元件內嵌在頁面中](/help/forms/using/embedding-link-component-page.md).

現在，元件瀏覽器中提供Document Services和Document Services述詞元件類別。 元件會針對使用相同範本的所有頁面啟用。

## 相关文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API的網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表單的簡介](/help/forms/using/introduction-publishing-forms.md)
