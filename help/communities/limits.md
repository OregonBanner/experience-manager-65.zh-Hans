---
title: 成員貢獻限制
seo-title: Member Contribution Limits
description: 貢獻限制功能可讓您限制防止垃圾訊息的貢獻
seo-description: Contribution limits feature lets you limit the contributions to protect against spam
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 1%

---

# 成員貢獻限制 {#member-contribution-limits}

## 概述 {#overview}

貢獻限制功能提供限制社群成員貢獻的功能，作為抵禦垃圾訊息的手段。

當成員受到限制時，任何超出允許貢獻數量的貼文都會導致超出限制的警報，並拒絕貼文。 社群成員可以前往社群訊息中心，並聯絡社群管理員，以便移除限制（如適用）。

貢獻限制可透過以下網址個別啟用： [成員主控台](members.md) 和/或設定為當網站訪客成為新成員時自動啟用。

使用「成員」主控台，社群管理員可隨時主動移除成員的貢獻限制，或是在成員傳送訊息給提出此請求的社群管理員時被動移除。

## AEM Communities使用者產生的內容貢獻限制設定 {#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi設定：

* 定義貢獻限制的特徵（一段時間內員額的數量）。
* 識別達到限制時能夠傳送訊息的成員。
* 識別永遠不需要限制的網域。

若要存取此OSGi設定：

* 在主要發行者上：
* 以管理員許可權登入。
* 存取 [網頁主控台](../../help/sites-deploying/configuring-osgi.md).

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 尋找 `AEM Communities User Generated Content Contribution Limits Configuration`.
* 選取編輯圖示。

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL 自動套用UGC貢獻限制]**

   如果勾選，當使用者註冊為社群成員時，會自動設定使用者的貢獻限制。 這會反映在社群成員的設定檔中，並可從 [成員主控台](members.md). 擁有網域允許清單中電子郵件地址的新成員永遠不會受到限制。

   預設為未勾選。

* **[!UICONTROL UGC限制]**

   貢獻數量上限。

   預設為10個貼文。

* **[!UICONTROL UGC限制頻率]**

   限制UGC限制的時段。

   預設值為60分鐘。

* **[!UICONTROL 網域]**

   一或多個電子郵件網域的允許清單。 選取+圖示以建立其他專案。

   當自動套用UGC貢獻限制時，擁有網域允許清單中電子郵件地址的使用者不受影響。 例如，如果網域 `mycompany.com` 會新增至網域清單，然後新增具有電子郵件地址的成員 `me@mycompany.com` 絕不會限制張貼。

   預設為空的允許清單。

* **[!UICONTROL 訊息收件者]**

   成員的一或多個可授權的ID清單，這些成員可修改成員的貢獻限制。 選取+圖示以建立其他專案。

   成員只能在達到限制時聯絡指定的成員。

   預設為無訊息收件者。

注意：預設設定在一小時內會限制10個貼文。
