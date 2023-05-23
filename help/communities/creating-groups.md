---
title: 社区组
seo-title: Community Groups
description: 建立社群群組
seo-description: Creating community groups
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 3%

---

# 社区组 {#community-groups}

社群群組功能可讓發佈和作者環境中的授權使用者（社群成員和作者）在社群網站中動態建立子社群。

此功能出現於 [群組功能](/help/communities/functions.md#groups-function) 中存在於 [社群網站](/help/communities/sites-console.md) 結構。

A [社群群組範本](/help/communities/tools-groups.md) 動態建立社群群組時，會提供社群群組頁面的設計。

將功能新增至社群網站的結構或社群網站範本時，會為群組功能選取一或多個群組範本。 此群組範本清單會呈現給從社群網站動態建立新群組的成員或作者。

## 建立新群組 {#creating-a-new-group}

建立新社群群組的能力取決於社群網站的存在，其中包含群組功能，例如從 [引用網站範本](/help/communities/sites.md).

以下範例使用根據以下範例建立的社群網站： `Reference Site Template` 如 [AEM Communities快速入門](/help/communities/getting-started.md) 教學課程。

這是發佈時載入的頁面，當 **群組** 已選取功能表專案：

![new-group](assets/new-group.png)

當您選取 **新增群組** 圖示時，編輯對話方塊開啟。

在 **設定** 標籤中，您會提供群組的基本功能：

![群組設定](assets/group-settings.png)

* **组名称**

   要在社群網站上顯示的群組標題。 請避免在群組名稱中使用底線字元(_)和關鍵字（例如資源和設定）。

* **描述**

   要顯示在社群網站上的群組說明。

* **邀请**

   邀請加入群組的成員清單。 預先輸入搜尋將提供社群成員邀請的建議。

* **组 URL 名称**

   成為URL一部分的群組頁面名稱。

* **开放组**

   選取 `Open Group` 表示任何匿名網站訪客可以檢視內容，並將取消選取 `Member Only Group`.

* **仅限成员加入的组**

   選取 `Member Only Group` 表示只有群組的成員可以檢視內容，並將取消選取 `Open Group`.

在 **範本** tab可讓您從社群群組範本清單中選取，這些範本是當社群網站的結構或範本中包含群組功能時所指定。

![group-template](assets/group-template.png)

在 **影像** tab可上傳影像，以顯示於社群網站的「群組」頁面上的群組。 預設樣式表會將影像大小調整為170 x 90畫素。

![group-image](assets/group-image.png)

藉由選取 **建立群組** 按鈕，群組的頁面會根據所選的範本建立，且會為成員資格建立使用者群組，且會更新「群組」頁面以顯示新的子社群。

例如，「群組」頁面中有一個名為「焦點群組」的新子社群，其影像縮圖已上傳，頁面將會如下所示（仍以社群群組管理員身分登入）：

![group-page](assets/group-page.png)

選取 `Focus Group` 連結會在瀏覽器中開啟「焦點群組」頁面，該頁面的初始外觀是根據所選範本，並在主要社群網站的功能表底下包含一個子功能表：

![open-group-page](assets/open-group-page.png)

### 社群群組成員清單元件 {#community-group-member-list-component}

此 `Community Group Member List` 元件僅供群組範本的開發人員使用。

### 附加信息 {#additional-information}

如需詳細資訊，請參閱 [社群群組Essentials](/help/communities/essentials-groups.md) 適用於開發人員的頁面。

如需與社群群組相關的其他資訊，請造訪 [管理使用者和使用者群組](/help/communities/users.md).
