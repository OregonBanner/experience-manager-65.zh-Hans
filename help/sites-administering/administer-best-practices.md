---
title: 協助管理員快速上手並執行的最佳實務
description: 尋找由Adobe工程和諮詢團隊編譯的最佳實務，以協助管理員開始運作。
uuid: 862d4fcf-ca61-4228-9344-b95a49b59b32
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f6468a0-7721-454f-9334-c449968b8fe7
exl-id: 576d87c8-cc96-45a0-b3cf-defb440babbb
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 7%

---

# 最佳实践{#best-practices}

最佳實務說明如何以最有效率且最有效的方式開發、管理或使用AEM。 這份不斷增加的主題清單包括AEM中的各種領域。

下列區域已提供有關最佳實務的檔案：

* [Assets](#assets)
* [Sites](#sites)

如需編寫、部署和維護或開發的最佳實務，請參閱下列其中一項：

* [製作最佳實務](/help/sites-authoring/best-practices.md)
* [開發最佳實務](/help/sites-developing/best-practices.md)
* [部署最佳實務](/help/sites-deploying/best-practices.md)

以下表格中會說明並連結特定檔案。

## Assets {#assets}

有關資產的最佳實務，包括Dynamic Media功能和Dynamic Media Classic整合，請參閱下列主題：

<table>
 <tbody>
  <tr>
   <td>Assets周圍不同區域的最佳實務，可增強負載下的系統穩定性和效能</td>
   <td><a href="/help/assets/best-practices-for-assets.md">用于资产的最佳实践</a></td>
   <td>包含資產周圍不同區域最佳實務指南的連結。 檢閱這些說明後，您將擁有建置和管理企業資產管理系統的知識和工具。</td>
  </tr>
  <tr>
   <td>如何組織您的內容（資料夾階層）</td>
   <td><a href="/help/assets/organize-assets.md">文件管理最佳实践</a></td>
   <td>許多處理設定檔是以資料夾為基礎，因為視訊、中繼資料、影像處理一律會套用至資料夾。 此最佳實務檔案說明如何定義及設定資料夾階層，因為階層對內容的處理方式有重大影響。 </td>
  </tr>
  <tr>
   <td>整合Scene7和AEM</td>
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">將Scene7與AEM整合的最佳實務</a></td>
   <td><p>說明何時開啟Polling Importer、如何測試整合，以及何時使用內容瀏覽器與直接上傳至Assets。</p> </td>
  </tr>
  <tr>
   <td>影像預設集選項</td>
   <td>瞭解 <a href="/help/assets/managing-image-presets.md#understanding-image-presets">影像預設集</a> 和 <a href="/help/assets/managing-image-presets.md#image-preset-options">影像預設集最佳作法</a></td>
   <td>作為檔案的一部分，於 <a href="/help/assets/managing-image-presets.md">管理影像預設集</a>，這些主題說明什麼是影像預設集，以及選取影像預設集選項的最佳作法。</td>
  </tr>
  <tr>
   <td>Dynamic Media與Scene7的直接整合</td>
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Scene7/AEM整合與Dynamic Media</a></td>
   <td>說明何時最好使用Dynamic Media解決方案、何時將S7與AEM整合，或何時同時使用兩者。</td>
  </tr>
 </tbody>
</table>

## Sites {#sites}

管理和編寫您的網站內容有一些最佳實務，概述如下：

<table>
 <tbody>
  <tr>
   <td>GDPR法規遵循</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR法規遵循</a></td>
   <td>歐盟資料隱私權的一般資料保護規範於2018年5月起生效。 AEM Sites符合GDPR。 本頁面將引導客戶完成在AEM Sites中處理GDPR請求的程式。 它描述了私有数据的存储位置，以及如何手动或使用代码删除私有数据。</td>
  </tr>
  <tr>
   <td>為您的執行個體定義預設UI。</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">為您的執行個體設定預設使用者介面</a></p> </td>
   <td>AEM有兩種UI：觸控最佳化和classic。 本節詳細說明如何為您的執行個體定義預設UI。</td>
  </tr>
  <tr>
   <td>多網站管理</td>
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM 最佳实践</a></td>
   <td>使用MSM自動化內容部署的最佳實務。 </td>
  </tr>
  <tr>
   <td>翻譯內容</td>
   <td><a href="/help/sites-administering/tc-bp.md">翻译最佳实践</a></td>
   <td>規劃及實作多語言網站的最佳作法。</td>
  </tr>
  <tr>
   <td>使用者管理</td>
   <td><a href="/help/sites-administering/security.md#best-practices">許可權和許可權最佳實務</a></td>
   <td>說明使用許可權和許可權時的最佳實務 </td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">工作流程最佳實務 — 設定</a></td>
   <td>工作流程可讓您自動化Adobe Experience Manager (AEM)活動，並可代表AEM環境中發生的大量處理，因此強烈建議您仔細計畫和設定工作流程實作。</td>
  </tr>
 </tbody>
</table>
