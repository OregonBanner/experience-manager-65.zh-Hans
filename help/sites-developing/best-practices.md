---
title: AEM開發人員的最佳作法
description: Adobe 工程和咨询团队开发了一组面向 AEM 开发人员的全面的最佳实践。
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 13%

---

# 最佳实践{#best-practices}

## 開發人員最佳實務 — 快速入門 {#best-practices-for-developers-getting-started}

Adobe 工程和咨询团队开发了一组面向 AEM 开发人员的全面的最佳实践。Adobe開發人員在開發核心AEM產品更新和客戶實作的客戶程式碼時，需遵守這些最佳實務。

在開始AEM開發專案之前，請先檢閱以下最佳實務：

* [開發實務](/help/sites-developing/development-practices.md)
* [內容架構](/help/sites-developing/content-architecture.md)
* [軟體架構](/help/sites-developing/software-architecture.md)
* [編碼提示](/help/sites-developing/coding-tips.md)
* [程式碼陷阱](/help/sites-developing/code-pitfalls.md)
* [JCR互動](/help/sites-developing/jcr-integration.md)
* [OSGi組合](/help/sites-developing/osgi-bundles.md)
* [Java API最佳作法](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### 其他最佳實務資訊 {#additional-best-practices-information}

以下區域提供開發最佳實務的特定檔案：

* [Sites](#sites)
* [社区](/help/sites-developing/best-practices.md#communities)
* [工具/HTL](/help/sites-developing/best-practices.md#tooling-htl)

以下表格中會說明並連結特定檔案。

如需管理、部署和維護或編寫的最佳實務，請參閱下列其中一項：

* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [製作最佳實務](/help/sites-authoring/best-practices.md)
* [部署最佳實務](/help/sites-deploying/best-practices.md)

## Sites {#sites}

管理和編寫您的網站內容有一些最佳實務，概述如下：

<table>
 <tbody>
  <tr>
   <td>標準觸控式UI背後的部分理論。</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">觸控式UI：概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">觸控式UI：結構</a></p> </td>
   <td>這些檔案提供觸控式UI的概念和結構概覽。</td>
  </tr>
  <tr>
   <td>觸控式UI：自訂主控台 </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">自訂觸控式UI主控台</a></td>
   <td>本檔案說明擴充觸控式UI主控台的最佳方式。</td>
  </tr>
  <tr>
   <td>觸控式UI：自訂頁面編寫</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">自訂觸控式UI頁面編寫</a></td>
   <td>說明如何延伸觸控式UI的頁面製作功能。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">开发和扩展工作流</a></td>
   <td><p>工作流程可讓您自動化Adobe Experience Manager (AEM)活動，並可代表AEM環境中發生的大量處理，因此強烈建議您仔細規劃工作流程實施。</p> </td>
  </tr>
 </tbody>
</table>

## 社区 {#communities}

[AEM Communities](/help/communities/overview.md) 簡化內部部署社群的建立和管理。

以下說明社群的一些最佳實務：

|  |  |  |
|---|---|---|
| 使用使用者產生內容(UGC)的最佳實務 | [編碼准則](/help/communities/code-guide.md) | 為開發彈性、可攜式程式碼的准則 [社交元件框架](/help/communities/scf.md) (SCF)。 |
| Communities元件的使用範例 | [社群元件指南](/help/communities/components-guide.md) | 互動式開發工具。 |

## 工具/HTL {#tooling-htl}

HTML範本語言(HTL)是隨AEM 6.0推出的新HTML範本系統。它取代了JSP和ESP，成為AEM慣用的範本系統。

|  |  |  |
|---|---|---|
| HTL 概述 | [HTL概述和語法](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | 本檔案說明HTL是什麼、如何移至HTL、範例專案、語法、運算式和陳述式 |
| 在Java中使用API | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | HTL Java Use-API讓HTL檔案能夠存取自訂Java類別中的helper方法。 |

>[!NOTE]
>
>以下多部分教學課程可能會是設定新AEM專案的最佳做法，其中會詳細說明核心元件、可編輯的範本、使用者端程式庫和元件開發：
>[《AEM Sites 快速入门》 - WKND 教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
