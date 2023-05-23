---
title: 社群主控台
seo-title: Communities Consoles
description: 社群主控台說明
seo-description: Community Consoles explained
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 1%

---

# 社群主控台 {#communities-consoles}

AEM Communities主控台可在製作環境中從全域導覽面板取得，可讓您存取管理工作，例如：

* [建立社群網站](sites-console.md)
* 新增 [群組](groups.md) 巢狀內嵌於網站內
* 管理 [社群網站範本](sites.md)
* 管理 [社群成員](members.md)
* [稽核](moderate-ugc.md) 使用者產生的內容(UGC)
* 建立 [自訂徽章](badges.md)
* 設定 [UGC的預設儲存空間](srp-config.md)

時間 [UGC儲存](working-with-srp.md) 設為製作和發佈環境共用的公用存放區， [稽核主控台](moderation.md)適用於製作和發佈環境，在UGC的單一例項上運作。

在作者環境中，以管理員許可權登入後， `Communities` 「導覽」和「工具」主控台提供主控台。

>[!NOTE]
>
>在發佈環境中， [社群網站](sites-console.md) 將會顯示 `Administration` 功能表專案（當登入成員具有適當許可權時）。

## 全域導覽面板 {#global-navigation-panel}

選取 `Adobe Experience Manager` 圖示開啟「全域導覽」面板，並存取兩個圖示：

* [導覽主控台](#navigation-console)
* [工具主控台](tools.md)

## 導覽主控台 {#navigation-console}

若要存取各種Communities主控台，請從全域導覽選取 **導覽，社群**.

![社区](assets/communities.png)

* [Sites](sites-console.md)

   您可以在作者環境中存取Sites主控台，以便建立和管理社群網站及其 [群組](groups.md).

* [审核](moderation.md)

   「調節」主控台適用於在製作環境中大量調節UGC。 在發佈環境中，指派了角色的社群成員可存取類似的大量稽核主控台。 [社群版主](users.md#publishenvironmentusersandgroups) 用於一或多個社群網站。

* [成員、群組](members.md)

   「成員」和「群組」主控台用於從作者環境管理存在於發佈環境中的社群成員和成員群組。

* [报表](reports.md)

   「報表」主控台是當社群網站具有下列條件時，可能產生工作總攬、頁面檢視和張貼內容(UGC)報表的地方 [已啟用Adobe Analytics](sites-console.md#analytics). 主控台僅適用於作者環境。

## 工具主控台 {#tools-console}

若要存取 [Communities工具](tools.md) （前身為administration console），從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL Communities]**
