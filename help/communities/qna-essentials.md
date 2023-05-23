---
title: QnA Essentials
seo-title: QnA Essentials
description: 問題與解答論壇功能
seo-description: Questions and answers forum feature
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# QnA Essentials {#qna-essentials}

本頁提供使用問答(QnA)論壇功能的基本資訊。

## 適用於使用者端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">包含</a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> 範本</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> 属性</td>
   <td>另請參閱 <a href="working-with-qna.md">Q&amp;A論壇功能</a></td>
  </tr>
 </tbody>
</table>

* [使用者端自訂](client-customize.md)

## 伺服器端的Essentials {#essentials-for-server-side}

* [QnA API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 问题与解答功能 {#qna-function}

社群網站結構包含 [QnA函式](functions.md#qna-function) 將會有已設定的 `QnA` 以及影響稽核和標籤的設定。 QnA函式支援識別 [有特殊許可權的成員使用者群組](users.md#privileged-members-group).

### 存取QnA論壇貼文(UGC) {#accessing-qna-forum-posts-ugc}

UGC應使用其中一個標準仲裁方法來仲裁。
另請參閱 [稽核使用者產生的內容](moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用存放區](working-with-srp.md) for UGC包含程式化存取UGC，無論選擇的儲存選項為何（例如ASRP、MSRP或JSRP）。

**UGC在存放庫中的位置和格式可能會有所變更，恕不發出警告**.

请参阅：

* [儲存資源提供者概觀](srp.md)  — 簡介和存放庫使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 程式碼指南。
* [SocialUtils重構](socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
