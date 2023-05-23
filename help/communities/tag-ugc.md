---
title: 標籤使用者產生的內容
seo-title: Tagging User Generated Content
description: 標籤使用者產生的內容(UGC)是社群成員如何協助其他成員搜尋內容
seo-description: Tagging of user generated content (UGC) is how community members can help other members search for content
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---

# 標籤使用者產生的內容 {#tagging-user-generated-content}

## 概述 {#overview}

標籤使用者產生的內容(UGC)是社群成員協助其他成員搜尋內容的方法。

標籤通常由作者和管理員在作者環境中套用。 標籤UGC的獨特之處在於UGC標籤是由發佈環境中的社群成員套用。

兩個應用程式的標籤名稱空間和分類相同。

## Communities功能 {#communities-features}

可設定為允許標籤的AEM Communities功能包括：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md#configuretheaddedforum)
* [问题与解答](working-with-qna.md)

## 管理標籤 {#administering-tags}

另請參閱 [管理標籤](../../help/sites-administering/tags.md#tagging-console) 用於建立和管理標籤名稱空間和分類。

另請參閱 [標籤Essentials](tag.md) 以取得開發人員資訊。

另請參閱 [使用社交標籤雲](tagcloud.md) 新增Social Tag Cloud元件至頁面，以方便使用套用的標籤搜尋已張貼的UGC。

### 標籤許可權 {#tag-permissions}

預設許可權已設定為不允許發佈環境中的每個人都讀取標籤名稱空間。

由於標籤已套用至發佈環境中的UGC，因此社群成員需要啟用讀取許可權，才能選取要套用的標籤。

另請參閱 [設定標籤許可權](../../help/sites-administering/tags.md#setting-tag-permissions).

以下為管理員將讀取許可權套用至 `/etc/tag/discussions` 適用於群組 `Community Engage Members`.

![tag-permissions](assets/tag-permissions.png)
