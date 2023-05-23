---
title: 列印管道和網頁管道
seo-title: Print channel and web channel
description: 匯入列印管道範本並建立及啟用Web管道範本
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 列印管道和網頁管道{#print-channel-and-web-channel}

互動式通訊可透過兩種管道提供：列印與網路。 列印管道用於建立PDF和紙張通訊，例如作為保險費付款提醒的列印信函，而網路管道用於提供線上體驗，例如網站上的信用卡對帳單。

互動式通訊作者可重複使用檔案片段和影像等資產，以建立互動式通訊的列印版和網頁版。

的先決條件之一 [建立互動式通訊](../../forms/using/create-interactive-communication.md) 是讓伺服器上有可供列印和/或web channel使用的範本。 範本作者在AEM中建立網路管道範本時，列印管道範本XDP是在Forms DesignerAdobe中建立並上傳至伺服器。

## 列印頻道 {#printchannel}

互動式通訊的列印頻道使用XFA表單範本XDP。 XDP是在AdobeForms Designer中設計。 如需建立列印管道範本的詳細資訊，請參閱 [版面設計](../../forms/using/layout-design-details.md). 若要在互動式通訊中使用列印管道範本，您必須將範本上傳至AEM Forms伺服器。

### 上傳互動式通訊列印頻道範本 {#upload-interactive-communication-print-channel-template}

若要上傳範本，您必須是表單 — 使用者群組的成員。 使用下列步驟將列印管道範本(XDP)上傳至AEM Forms：

1. 選取 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.

1. 點選 **[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**.

   導覽並選取適當的列印管道範本(XDP)並點選 **[!UICONTROL 開啟]**.

## 網路頻道 {#web-channel}

範本作者和管理員可以建立、編輯和啟用Web範本。 若要允許其他使用者編寫網頁範本，您需要授予他們許可權。 如需詳細資訊，請參閱 [使用者、群組和存取許可權管理](/help/sites-administering/user-group-ac-admin.md).

### 編寫Web Channel範本 {#authoring-web-channel-template}

若要建立Web Channel範本，您必須先建立範本資料夾。 在範本資料夾中建立Web範本後，您需要啟用範本以允許表單使用者根據範本建立互動式通訊的Web通道。

若要編寫Web Channel範本，請完成以下步驟：

1. 建立範本資料夾以保留互動式通訊Web範本（如果尚未建立）。 如需詳細資訊，請參閱範本資料夾： [頁面範本 — 可編輯](/help/sites-developing/page-templates-editable.md).

   1. 點選 **[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 設定瀏覽器]**.
      * 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。
   1. 在「設定瀏覽器」頁面中，點選 **[!UICONTROL 建立]**.
   1. 在建立設定對話方塊中，指定資料夾的標題，核取 **[!UICONTROL 可編輯的範本]**，然後點選 **[!UICONTROL 建立]**.

      資料夾隨即建立並列在「設定瀏覽器」頁面中。

1. 導覽至適當的範本資料夾，並建立網站範本。

   1. 選取「 」，導覽至適當的範本資料夾 **[!UICONTROL 工具]** > **[!UICONTROL 範本]** > **`[Folder]`**.
   1. 點選 **[!UICONTROL 建立]**.
   1. 選取 **[!UICONTROL 互動式通訊 — Web Channel]** 並點選 **[!UICONTROL 下一個]**.
   1. 輸入範本標題和說明，然後點選 **[!UICONTROL 建立]**.

      範本隨即建立，並出現一個對話方塊。

   1. 點選 **[!UICONTROL 開啟]** 以開啟您在範本編輯器中建立的範本。

      「範本編輯器」隨即出現。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      建立或編輯範本時，範本作者可以定義多個方面。 建立或編輯範本類似於頁面製作。 如需詳細資訊，請參閱編輯範本 — 範本作者，位置在： [建立頁面範本](/help/sites-authoring/templates.md).

1. 若要允許此範本用於建立互動式通訊，請啟用此範本。

   1. 點選 **[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 範本]**.
   1. 導覽至適當的範本，選取該範本，然後點選 **[!UICONTROL 啟用]** 在警報訊息中，點選 **[!UICONTROL 啟用]**.

      範本已啟用，其狀態會顯示為「已啟用」。 現在您可以繼續建立互動式通訊，在其中使用新建立的Web Channel範本。

### 列印頻道作為Web Channel的主版 {#print-channel-as-master-for-web-channel}

在製作互動式通訊時，作者可以選取此選項，以建立與列印頻道同步的Web頻道。 使用print channel作為web channel的主版，可確保從print channel衍生出web channel的內容、繼承和資料繫結，並且在print channel中所做的變更可以反映在web channel中。 不過，互動式通訊作者可視需要中斷Web Channel中特定元件的繼承。

![將頻道列印為主版](assets/create_ic_print_master_new.png) ![以print channel為主的Web channel](assets/create_ic_print_master_web_new.png)
