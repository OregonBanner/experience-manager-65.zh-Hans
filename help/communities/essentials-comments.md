---
title: Comments Essentials
seo-title: Comments Essentials
description: 註解元件概觀
seo-description: Comments component overview
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 3%

---

# Comments Essentials {#comments-essentials}

此頁面提供使用註解系統（註解元件）的要點，以及管理使用者產生的內容(UGC)的選項，該內容是在成員發表註解或回覆時產生的。

註解元件建立註解系統，使得每個個別貼文都由註解元件（單數）表示。 它是包含在頁面上的註解系統。 呼叫註解系統時，將會建立個別註解。

## 適用於使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>是 — 屬性可在下列位置編輯： <i>設計 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td> 另請參閱 <a href="comments.md">使用註解</a></td>
  </tr>
 </tbody>
</table>

[使用者端自訂](client-customize.md)

### 每頁一個執行個體 {#one-instance-per-page}

分頁以及使用URL來快取和連結要求每個註解系統的URL必須是唯一的。 因此，每個頁面只允許一個註解系統例項。

其他功能已經包括註解系統。 这四个关键原则分别是：

* [博客](blog-developer-basics.md)
* [日程表](calendar-basics-for-developers.md)
* [文件库](essentials-file-library.md)
* [论坛](essentials-forum.md)
* [问题与解答](qna-essentials.md)
* [审核](reviews-basics.md)

### 標幟原因清單 {#flag-reason-list}

標幟原因清單可透過將flagreasonlist.hbs新增至您的應用程式以覆寫中的內容來自訂

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

這適用於延伸註解系統的任何元件。

## 伺服器端的Essentials {#essentials-for-server-side}

* [註解API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [評論端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取發表的評論(UGC) {#accessing-posted-comments-ugc}

UGC應使用其中一個標準仲裁方法來仲裁。
另請參閱 [稽核使用者產生的內容](moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用存放區](working-with-srp.md) for UGC包含程式化存取UGC，無論選擇的儲存選項為何（例如ASRP、MSRP或JSRP）。

**UGC在存放庫中的位置和格式可能會有所變更，恕不發出警告**.

请参阅：

* [儲存資源提供者概觀](srp.md)  — 簡介和存放庫使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 程式碼指南。
* [SocialUtils重構](socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
