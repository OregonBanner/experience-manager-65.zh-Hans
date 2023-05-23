---
title: 在HTML Workspace中使用最適化表單
seo-title: Using an adaptive form in HTML Workspace
description: 在HTML Workspace中使用最適化表單
seo-description: Using an adaptive form in HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# 在HTML Workspace中使用最適化表單{#using-an-adaptive-form-in-html-workspace}

AEM Forms on JEE提供在HTML Workspace中使用最適化表單的功能。

由於可以在流程設計期間選擇XDP，因此新增了從現有的最適化表單AEM存放庫瀏覽的功能。 此功能讓流程設計人員能夠在「起點」和「任務」中設定最適化表單。

## 流程設計體驗 {#process-design-experience}

執行下列動作，讓最適化表單用於程式設計：

* 在指派任務和起點中，將表單資產指派給任務時，您可以瀏覽至CRX存放庫中的最適化表單資產。
* 在「指派任務/起點維護作業」特性表中，您可以隱藏最適化表單的頂層/全域工具列。
* 您可以在調適型表單中使用新的動作設定檔來轉譯和提交動作。

### LiveCycle應用程式匯出和匯入 {#livecycle-application-export-and-import}

由於調適型表單位於AEM存放庫中，因此LiveCycle應用程式匯出僅包含所使用調適型表單的參考。 因此，匯出和匯入LiveCycle應用程式是兩個步驟的過程。 LiveCycle應用程式包括流程定義等。 包含最適化表單的個別套件會從AEM匯出為ZIP檔案。 匯入時，會透過Workbench匯入LiveCycle應用程式，並透過AEM匯入調適型表單。

## HTML Workspace中最適化表單的使用者體驗 {#user-experience-of-adaptive-form-in-html-workspace}

除了可用於行動表單的控制項外，HTML Workspace還提供一些最適化表單特定控制項。 當使用者開啟任務或起點時，使用者可以在HTML工作區中新增附件、儲存、簽署、提交和導覽最適化表單。 具體情況如下：

1. 若要附加檔案，請使用「工作」附件，如行動Forms中的情況。 任何最適化表單的「檔案附件」型別按鈕都會隱藏。

1. 若要儲存最適化表單，請按一下 **儲存**，就像行動Forms一樣。 最適化表單的任何「儲存型別」按鈕都會隱藏。

1. 若要提交最適化表單，請使用 **提交** 按鈕或路由動作可供使用，就像行動Forms中的情況。 最適化表單的任何提交型別按鈕都會隱藏。

1. **最適化表單全域工具列可見性**：如果流程設計工具隱藏全域/頂層工具列，則工具列和按鈕不會出現在調適型表單上。

1. **最適化Forms的工作區導覽控制項**：下一個/上一個按鈕與HTML Workspace中適用性表單的儲存、提交和路由動作按鈕一起提供。 按一下「下一個/上一個」按鈕，在HTML Workspace中導覽最適化表單的面板。 「下一個/上一個」按鈕提供深層導覽，類似於最適化表單行動檢視中的導覽控制項。

1. **Adaptive Form的eSign Services和摘要元件**：摘要元件在HTML Workspace中無法運作。 換言之，如果最適化表單有摘要元件，則不會在工作區中顯示。 工作區使用者按一下「HTML工作區」中的「提交」或「路由」動作，而非「設計」元件中的「自動提交」。 簽署檔案後，它會顯示為平面簽署的檔案。 按一下 **提交** 或路由動作來關閉/完成任務或「起點」。\
   已簽署的檔案會從eSign服務伺服器收集，而資料xml檔案會轉送至程式中的下一個步驟。

## 在流程設計中使用調適型表單的步驟 {#steps-to-use-adaptive-forms-in-process-design}

1. 開啟Adobe Experience Manager Forms Workbench

1. 前往 **檔案>新增>應用程式** 或使用現有的應用程式來建立應用程式。

   ![建立新應用程式](assets/create_new_appl.png)

   建立新應用程式

1. 建立程式，或使用應用程式中的現有程式。

   ![建立新程式](assets/create_new_process.png)

   建立新程式

1. 建立「起始點」或「指派任務」，然後按兩下它。
1. 在 **[!UICONTROL 簡報與資料]** 區段，選取 **[!UICONTROL 使用CRX資產]** 並按一下資產前的省略符號。

   ![使用CRX資產](assets/use_crx_asset.png)

   使用CRX資產

1. 選取透過「管理資產」UI建立的最適化表單，然後按一下 **[!UICONTROL 確定]**.

   ![選取最適化表單](assets/selecting_form.png)

   選取最適化表單

   >[!NOTE]
   >
   >如需建立最適化表單的詳細資訊，請參閱 [建立最適化表單](../../forms/using/creating-adaptive-form.md).
   >
   >
   >如需建立流程的詳細資訊，請參閱 [建立和管理流程](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
