---
title: 製作巢狀群組
seo-title: Authoring Nested Groups
description: 建立巢狀群組
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 4%

---

# 製作巢狀群組{#authoring-nested-groups}

## 建立作者群組 {#creating-groups-on-author}

在AEM Author例項上，從全域導覽：

* 選取 **[!UICONTROL Communities]** > **[!UICONTROL 網站]**.
* 選取 **[!UICONTROL engage資料夾]** 以開啟。
* 選取的卡 **[!UICONTROL 快速入門教學課程]** 英文網站。

   * 選取卡片影像。
   * 執行 *not* 選取圖示。

結果是達到 [群組主控台](/help/communities/groups.md)：

![create-group](assets/create-group.png)

群組功能將顯示為資料夾，在其中建立群組的例項。 選取「群組」資料夾以將其開啟。 發佈時建立的群組是可見的。

![create-new-group](assets/create-new-group.png)

## 建立主要藝術群組 {#create-main-arts-group}

可以建立此群組，因為engage的網站結構包含群組功能。 網站中的函式設定 `Reference Template` 預設為允許選取任何已啟用的群組範本。 因此，為此新群組選擇的範本為 `Reference Group`.

這些主控台與Communities Sites主控台類似。

* 選取 **[!UICONTROL 建立群組]**

* **社区组模板**:

   * **[!UICONTROL 社群群組標題]**：藝術
   * **[!UICONTROL 社群群組說明]**：各種藝術團體的父級群組
   * **[!UICONTROL 社群群組根目錄]**： *保留為預設值*
   * **[!UICONTROL 其他可用的社群群組語言]**：使用下拉式選單來選取可用的社群群組語言。 功能表會顯示建立上層社群網站的所有語言。 使用者可以選取這些語言之一，以在此單一步驟中建立多個地區設定的群組。 在個別社群網站的「群組」主控台中，會以多種指定語言建立相同的群組。
   * **[!UICONTROL 社群群組名稱]**：藝術
   * **[!UICONTROL 範本]**：下拉式選單以選取 `Reference Group`
   * 選取 **[!UICONTROL 下一個]**

![巢狀社群群組](assets/parent-to-nestedgroup.png)

使用這些設定繼續瀏覽其他面板：

* **[!UICONTROL Design]**

   * 變更設計或允許預設父網站的設計。
   * 选择&#x200B;**[!UICONTROL 下一步]**。

* **[!UICONTROL 设置]**

   * **[!UICONTROL 审核]**

      * 留空（繼承自父網站）。
   * **[!UICONTROL 成员资格]**

      * 使用預設值 `Optional Membership.`

      * **[!UICONTROL 缩略图]**
         * `optional.*`
      * **[!UICONTROL 选择下一步]**。



* 选择&#x200B;**[!UICONTROL 创建]**。

### Arts Group中的巢狀群組 {#nesting-groups-within-arts-group}

此 `groups` 資料夾現在包含兩個群組（重新整理頁面）。

![巢狀化群組](assets/create-community-group.png)

#### 发布组 {#publish-group}

建立巢狀內嵌群組之前 `arts` 群組，將游標暫留在 `arts` 卡片並選取發佈圖示以進行發佈。

![publish-site](assets/publish-site.png)

等候確認群組已發佈。

![group-published](assets/group-published.png)

此 `arts` 群組也應包含 `groups` 資料夾，但是空的資料夾，可以在其中建立新群組。 導覽至「藝術群組」資料夾，建立3個巢狀群組，每個群組都有不同的成員資格設定：

1. **[!UICONTROL 視覺]**

   * 标题: `Visual Arts`
   * 名称: `visual`
   * 模板: `Reference Group`
   * 成員資格：選取 `Optional Membership`，公開群組，對所有成員開放。

1. **[!UICONTROL 聽覺]**

   * 标题: `Auditory Arts`
   * 名称: `auditory`
   * 模板: `Reference Group`
   * 成員資格：選取 `Required Membership`，開放群組，可供成員加入。

1. **[!UICONTROL 历史]**

   * 标题: `Art History`
   * 名称: `history`
   * 模板: `Reference Group`
   * 成員資格：選取 `Restricted Membership`，機密群組，僅對受邀成員可見。 例如，邀請 [示範使用者](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

重新整理頁面以檢視所有三個巢狀群組（子社群）。

若要從Communities Sites主控台導覽至巢狀群組：

* 選取 **[!UICONTROL engage資料夾]**
* 選取 **[!UICONTROL 快速入門教學課程卡片]**
* 選取 **[!UICONTROL 群組]** 資料夾
* 選取 **[!UICONTROL 藝術卡]**
* 選取 **[!UICONTROL 群組]** 資料夾

![create-new-group2](assets/create-new-group2.png)

## 發佈群組 {#publishing-groups}

![publish-site](assets/publish-site.png)

發佈主要社群網站後：

* 個別發佈每個群組：

   * 正在等候確認群組已發佈。

* 發佈巢狀內嵌的任何群組之前，請先發佈父群組：

   * 所有群組必須以由上而下的方式發佈。

![group-published](assets/group-published.png)

## 發佈體驗 {#experience-on-publish}

可以在登入時體驗不同的群組，例如使用 [示範使用者](/help/communities/tutorials.md#demo-users) 用於：

* 藝術/歷程記錄群組成員：emily.andrews@mailinator.com/password
   * 受限制的（秘密）群組（藝術/歷史）是可見的：
   * 可以看見選用（公用）群組。
   * 可以加入受限制（開放）的群組。

* 群組管理員： aaron.mcdonald@mailinator.com/password

   * 可以看見選用（公用）群組。
   * 可以加入受限制（開放）的群組。
   * 無法看見受限制的（秘密）群組。

存取社群 [成員和群組主控台](/help/communities/members.md) 將其他使用者新增至與社群群組相對應的各種成員群組。
