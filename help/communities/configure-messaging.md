---
title: 傳訊功能
seo-title: Messaging Feature
description: 設定傳訊元件
seo-description: Configuring Messaging components
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 3%

---

# 傳訊功能 {#messaging-feature}

除了在論壇和評論中公開可見的互動以外，AEM Communities的傳訊功能也可讓社群成員更私密地互動。

此功能可在 [社群網站](/help/communities/overview.md#communitiessites) 「 」已建立。

傳訊功能提供以下功能：

**A**  — 傳送訊息給一或多個社群成員

**B**  — 傳送直接訊息於 [大量傳送至社群成員群組](/help/communities/messaging.md#group-messaging)

**C**  — 傳送包含附件的郵件

**D**  — 轉寄訊息

**E**  — 回複訊息

**F**  — 刪除訊息

**G**  — 還原已刪除的郵件

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

若要啟用及修改傳訊功能，請參閱：

* [設定傳訊](/help/communities/messaging.md) 適用於管理員
* [傳訊要點](/help/communities/essentials-messaging.md) 適用於開發人員

>[!NOTE]
>
>不支援新增 `Compose Message, Message, or Message List` 元件(可在 `Communities`元件群組)至處於作者編輯模式的頁面。

## 設定傳訊元件 {#configure-messaging-components}

為社群網站啟用傳訊功能時，其設定無需進一步設定。 如果需要變更預設設定，則會提供資訊。

### 設定訊息清單（訊息方塊） {#configure-message-list-message-box}

修改訊息清單的設定 **收件匣**， **已傳送專案**、和 **垃圾桶** 訊息功能頁面，開啟網站於 [作者編輯模式](/help/communities/sites-console.md#authoring-site-content).

1. 在 `Preview` 模式，選取 **訊息** 開啟主要傳訊頁面的連結。 然後選取 **收件匣**， **已傳送專案** 或 **垃圾桶** 以設定該訊息清單的元件。

1. 在 `Edit` 模式，選取頁面上的元件。
1. 若要存取設定對話方塊，請選取 `link` 圖示。
取消繼承後，可以選取設定圖示以開啟設定對話方塊。

1. 設定完成後，必須選取 `broken link` 圖示。

![configure-message-list](assets/configure-message-list.png)

#### “基本”选项卡 {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服务选择器**

   (*必填*)將此設定為屬性的值 **`serviceSelector.name`** 從 [AEM Communities傳訊操作服務](/help/communities/messaging.md#messaging-operations-service).

* **撰寫頁面**

   (*必填*)成員按一下「 」時開啟的頁面 **`Reply`** 按鈕。 目標頁面應包含 **撰寫訊息** 表單。

* **回覆/以資源檢視**

   如果勾選，回覆URL和檢視URL會參照資源，否則資料會在URL中傳遞為查詢引數。

* **設定檔顯示表單**

   用來顯示寄件者設定檔的設定檔表單。

* **垃圾桶資料夾**

   如果勾選，此訊息清單元件只會顯示標示為已刪除（垃圾桶）的訊息。

* **資料夾路徑**

   (*必填*)參考為設定的值 **inbox.path.name** 和 **sentitems.path.name** 在 [AEM Communities傳訊操作服務](/help/communities/messaging.md#messaging-operations-service). 為設定時 `Inbox`，使用以下專案的值新增一個專案： **inbox.path.name**. 為設定時 `Outbox`，使用以下專案的值新增一個專案： **sentitems.path.name**. 設定時 `Trash`，新增兩個同時含有兩個值的專案。

#### 顯示標籤 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **標示讀取按鈕**

   如果勾選，會顯示 `Read`允許將訊息標示為已讀取的按鈕。

* **標示為未讀取按鈕**

   如果勾選，會顯示 `Mark Unread` 允許將訊息標示為已讀取的按鈕。

* **刪除按鈕**

   如果勾選，會顯示 `Delete` 允許將訊息標示為已讀取的按鈕。 將複製刪除功能，如果 **`Message Options`** 也會勾選。

* **消息选项**

   如果勾選，則會顯示 **`Reply`**， **`Reply All`**， **`Forward`** 和 **`Delete`** 允許重新傳送或刪除訊息的按鈕。 將複製刪除功能，如果 **`Delete Button`** 也會勾選。

* **每个页面的消息数**

   指定的數字是分頁配置中每頁顯示的最大訊息數。 如果未指定數字（保留為空白），則會顯示所有訊息且沒有分頁。

* **时间戳模式**

   提供一種或多種語言的時間戳記模式。 en、de、fr、it、es、ja、zh_CN、ko_KR的預設為。

* **显示用户**

   選擇 **`Sender`** 或 **`Recipients`** 以判斷是否要顯示寄件者或收件者。

### 設定撰寫訊息 {#configure-compose-message}

若要修改撰寫訊息頁面的設定，請開啟網站於 [作者編輯模式](/help/communities/sites-console.md#authoring-site-content).

* 在 `Preview` 模式，選取 **訊息** 開啟主要傳訊頁面的連結。 然後選取「新增訊息」按鈕以開啟 `Compose Message` 頁面。

* 在 `Edit` 模式，在包含訊息內文的頁面上選取主要元件。
* 若要存取設定對話方塊，請選取 `link` 圖示。
取消繼承後，可以選取設定圖示以開啟設定對話方塊。

* 設定完成後，必須選取 `broken link` 圖示。

![config-compose-message](assets/config-compose-message.png)

#### “基本”选项卡 {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **重新導向URL**

   輸入傳送訊息後所顯示頁面的URL。 例如：`../messaging.html`。

* **取消 URL**

   輸入寄件者取消郵件時顯示之頁面的URL。 例如：`../messaging.html`。

* **訊息主旨的長度上限**

   主旨欄位中允許的最大字元數。 例如，500。 預設為無限制。

* **訊息內文的最大長度**

   「內容」欄位中允許的最大字元數。 例如，10000。 預設為無限制。

* **服务选择器**

   (*必填*)將此設定為屬性的值 **`serviceSelector.name`** 從 [AEM Communities傳訊操作服務](/help/communities/messaging.md#messaging-operations-service).

#### 顯示標籤 {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **顯示主題欄位**

   如果勾選，則顯示 `Subject` 欄位並啟用在訊息中新增主旨。 未勾選預設值。

* **主旨標籤**

   輸入要顯示在旁邊的文字 `Subject` 欄位。 預設為 `Subject`.

* **显示附加文件字段**

   如果勾選，則顯示 `Attachment` 欄位並啟用新增檔案附件至訊息。 未勾選預設值。

* **附加文件标签**

   輸入要顯示在旁邊的文字 `Attachment` 欄位。 預設為 **`Attach File`**.

* **顯示內容欄位**

   如果勾選，則顯示 `Content` 欄位並啟用新增訊息內文。 未勾選預設值。

* **內容標籤**

   輸入要顯示在旁邊的文字 `Content` 欄位。 預設為 **`Body`**.

* **使用富文本编辑器**

   如果勾選，表示使用具有自己RTF編輯器的自訂「內容」文字方塊。 未勾選預設值。

* **时间戳模式**

   提供一種或多種語言的時間戳記模式。 en、de、fr、it、es、ja、zh_CN、ko_KR的預設為。
