---
title: 稽核Essentials
seo-title: Reviews Essentials
description: 檢閱和檢閱摘要元件
seo-description: Reviews and Review Summary components
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---

# 稽核Essentials {#reviews-essentials}

此功能包含兩個共同運作的元件：稽核和稽核摘要。

檢閱是以「 」為基礎的複合元件 [評論系統](essentials-comments.md) 包含一或多個 [評等](rating-basics.md) （記事）元件。

不支援評論的匿名張貼。 網站訪客必須註冊並登入才能新增評論。 已登入的訪客（會員）可隨時更新其評論。

## 適用於使用者端的Essentials {#essentials-for-client-side}

### 审核 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>是 — 屬性可在下列位置編輯： <i>設計 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>另請參閱 <a href="reviews.md">使用評論</a></td>
  </tr>
 </tbody>
</table>

### 审核摘要 {#review-summary}

| **resourceType** | social/review/components/hbs/summary |
|---|---|
| [**包含**](scf.md#add-or-include-a-communities-component) | 是 — 屬性可在*design *模式中編輯 |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **範本** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **属性** | 另請參閱 [使用評論](reviews.md) |

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [檢閱API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [檢閱端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的評論(UGC) {#accessing-posted-reviews-ugc}

UGC應使用其中一個標準仲裁方法來仲裁。
另請參閱 [稽核使用者產生的內容](moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用存放區](working-with-srp.md) for UGC包含程式化存取UGC，無論選擇的儲存選項為何（例如ASRP、MSRP或JSRP）。

**UGC在存放庫中的位置和格式可能會有所變更，恕不發出警告**.

请参阅：

* [儲存資源提供者概觀](srp.md)  — 簡介和存放庫使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 程式碼指南。
* [SocialUtils重構](socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
