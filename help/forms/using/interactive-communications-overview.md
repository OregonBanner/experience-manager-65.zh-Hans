---
title: 互動式通訊概述
seo-title: Interactive Communications Overview
description: 本文包括概述、範例使用案例、建立工作流程，以及互動式通訊與信函之間的差異。
seo-description: Interactive Communication key capabilities, sample use cases, creation workflow, and differences between Interactive Communication and Correspondence Management
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
exl-id: 6cfbeec0-0be3-48b2-a4bb-fd19c69c92c7
source-git-commit: 415744ca5c46a1495fe90369c162158c7fc2f1d4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 7%

---


# 互動式通訊概述 {#interactive-communications-overview}

本文包括概述、範例使用案例、建立工作流程，以及互動式通訊與信函之間的差異。

![](do-not-localize/correspondence-management.png)

互動式通訊可集中處理及管理安全、個人化與互動式通訊的建立、集合與傳遞，例如商務信函、檔案、對帳單、利益通知、行銷郵件、帳單和歡迎套件。

## 重要功能 {#key-capabilities}

以下是互動式通訊的主要功能：

- 與表單資料模型開箱即用的整合，讓您輕鬆且簡化存取後端資料庫和其他CRM系統，例如MS® Dynamics
- 適用於列印與網頁頻道的整合式撰寫介面，可自動從列印頻道產生網頁頻道
- 以易於理解的視覺格式在列印和網頁中顯示資訊的圖表
- 檔案片段支援規則編輯器和表單資料模型
- 代理使用者介面會顯示互動式通訊的列印與網頁預覽
- 拖放元件以快速建構列印和網路頻道

## 建立互動式通訊 {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### 工作流 {#workflow}

若要建立互動式通訊，請 [建置區塊](#buildingblocks) 互動式通訊就緒，然後完成下列步驟：

1. 選擇以 [建立互動式通訊](/help/forms/using/create-interactive-communication.md).

1. 指定 [表單資料模型](/help/forms/using/data-integration.md)，預填服務，以及 [列印和Web Channel範本](/help/forms/using/web-channel-print-channel.md). 您可以選擇從列印管道產生Web Channel。

1. 使用 [拖放介面](/help/forms/using/introduction-interactive-communication-authoring.md)，視需要新增檔案片段、影像、要列印的元件以及互動式通訊的Web頻道。
1. 為插入的元件設定屬性，如下所示：

   1. [图像](/help/forms/using/create-interactive-communication.md#step2)
   1. [表格](/help/forms/using/create-interactive-communication.md#tables) （包括佈局片段）
   1. [圖表](/help/forms/using/chart-component-interactive-communications.md)
   1. [檔案片段](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. 預覽列印和Web通道，並視需要編輯互動式通訊。
1. 代理程式會使用Agent UI來 [準備互動式通訊](/help/forms/using/prepare-send-interactive-communication.md) 以傳送給收件者/貼文程式。

### 构建基块 {#buildingblocks}

以下是建立互動式通訊所需的建置組塊：

- [表單資料模型](/help/forms/using/data-integration.md)
- [列印和Web Channel範本](/help/forms/using/web-channel-print-channel.md)
- [檔案片段](/help/forms/using/document-fragments.md)
- 图像
- [主題](/help/forms/using/themes.md) 網路頻道

## 互動式通訊與通訊管理 {#interactive-communications-vs-correspondence-management}

互動式通訊是建立客戶通訊的預設和建議方法。 若要繼續使用在AEM 6.3 Forms和AEM 6.2 Forms中建立的字母，您需要 [安裝相容性套件](/help/forms/using/compatibility-package.md). 以下是互動式通訊與信函功能之間的比較。

<table>
 <tbody>
  <tr>
   <td><strong>功能</strong></td>
   <td><strong>交互式通信</strong></td>
   <td><strong>书信</strong></td>
  </tr>
  <tr>
   <td>输出</td>
   <td>列印與網頁</td>
   <td>打印</td>
  </tr>
  <tr>
   <td>Schema</td>
   <td>表單資料模型 </td>
   <td>資料字典 </td>
  </tr>
  <tr>
   <td>本地化</td>
   <td>不支援表單資料模型</td>
   <td>在資料字典中支援</td>
  </tr>
  <tr>
   <td>規則編輯器</td>
   <td>
    <ul>
     <li>用於建立內嵌條件的文字和條件支援規則編輯器</li>
     <li>互動式通訊編輯器支援在Web Channel的元件上套用規則</li>
    </ul> </td>
   <td>沒有用於建立條件運算式的UI</td>
  </tr>
  <tr>
   <td>创作</td>
   <td>用於建構列印和網頁通道的拖放介面</td>
   <td>無拖放機制 </td>
  </tr>
  <tr>
   <td>圖表</td>
   <td>列印及Web Channel中支援的圖表</td>
   <td>不受支持</td>
  </tr>
  <tr>
   <td>主题</td>
   <td>使用主題來設定Web Channel的樣式</td>
   <td>不支援主題</td>
  </tr>
   <tr>
   <td>草稿</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>提交內容</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
  <tr>
   <td>稽核</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>版本控制</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
   <td>批次處理</td>
   <td>支持 </td>
   <td>支持</td>
  </tr>
  <tr>
   <td>代理程式簽章</td>
   <td>不受支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>遠端功能</td>
   <td>不受支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>
