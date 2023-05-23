---
title: 「教學課程：規劃互動式通訊」
seo-title: Plan your Interactive Communication
description: 規劃互動式通訊的結構
seo-description: Plan the anatomy for your Interactive Communication
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
feature: Interactive Communication
exl-id: ea0c8971-56f4-4094-87e4-1b222b73951f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 2%

---

# 教學課程：規劃互動式通訊 {#tutorial-plan-the-interactive-communication}

規劃互動式通訊的結構

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 數列。 建議您依照時間順序觀看本系列，以瞭解、執行和示範完整的教學課程使用案例。

規劃互動式通訊的第一步是完成互動式通訊的內容。 來自法律、金融、支援或行銷等部門的主題專家可以協助您完成內容。 內容完成之後，您必須加以分析，以識別建立互動式通訊所需的各種資產型別。

## 規劃考量事項 {#planning-considerations}

互動式通訊包含下列元素：

* **靜態文字** 大部分包括互動式通訊的通用部分，並包含在與所有客戶的通訊中。 例如，頁首、頁尾、稱呼或免責宣告。
* **來自後端系統的資料（表單資料模型）** 是客戶專屬的，會動態地與互動式通訊合併。 例如，可以使用表單資料模型來取得原則編號或位址。
* **版面配置或範本** 適用於互動式通訊的列印版和Web版。
* **訂購** 其中各種文欄位落出現在互動式通訊中。
* **由一線員工輸入的資料（代理程式UI）** 在傳送通訊前，誰在自訂通訊。 例如，付款到期日。

* **條件資料** 會根據預先定義的條件填入。 例如，產生互動式通訊的日期。
* **儲存在存放庫中的影像**，例如圖志和簽名影像。 公司標誌等影像會出現在大部分或全部的互動式通訊中。
* **圖表與表格** 在互動式通訊中簡化複雜資料表示法所需

## 互動式通訊剖析 {#anatomy-of-the-interactive-communication}

完成建立互動式通訊所使用的內容和元素後，您就可以建立互動式通訊的剖析。 解剖必須列出詳細資訊 [規劃考量事項](/help/forms/using/planning-interactive-communications.md#planning-considerations) 區段。 根據我們的使用案例，以下範例說明電信營運商傳送給客戶的每月帳單剖析。

解剖包含具有以下輸入模式的資料：

* 靜態文字
* 表單資料模型
* 代理 UI
* 條件資料
* 图像

在每個區段中，粗體文字代表靜態文字。 資料庫包含客戶、帳單和呼叫表格。 表單資料模型可接收來自任何這些表格的資料。 如需詳細資訊，請參閱 [建立表單資料模型](/help/forms/using/create-form-data-model0.md).

下表說明互動式通訊剖析中每個欄位的資料來源：

<table>
 <tbody>
  <tr>
   <td>分区</td>
   <td>靜態文字</td>
   <td>FDM </td>
   <td>代理 UI</td>
   <td>图像</td>
  </tr>
  <tr>
   <td>帳單詳細資訊</td>
   <td><p>商業發票否</p> <p>帳單日期</p> <p>帳單期間</p> <p>您的計畫</p> </td>
   <td><p>值 <strong>您的計畫 </strong>欄位</p> <p>表格 — 客戶</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>商業發票否</li>
     <li>帳單日期</li>
     <li>帳單期間</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>客戶詳細資料</td>
   <td><p>供應地點</p> <p>州代碼</p> <p>行動電話號碼</p> <p>備用連絡人號碼</p> <p>關係編號</p> <p>連線數目</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>名称</li>
     <li>地址</li>
     <li>行動電話號碼</li>
     <li>備用連絡人號碼</li>
     <li>關係編號</li>
    </ul> <p>表格 — 客戶</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>供應地點</li>
     <li>州代碼</li>
     <li>連線數目</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>帳單摘要</td>
   <td><p>上一個餘額</p> <p>付款</p> <p>調整</p> <p>費用目前帳單期間</p> <p>到期金額</p> <p>到期日期</p> </td>
   <td><p>的值 <strong>費用目前帳單期間 </strong> 欄位</p> <p>表格 — 用料表</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>上一個餘額</li>
     <li>付款</li>
     <li>調整</li>
     <li>到期金額</li>
     <li>到期日期</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>費用摘要</td>
   <td><p>通話費用</p> <p>電話會議費用</p> <p>簡訊費用 </p> <p>行動網際網路費用</p> <p>國家漫遊費用</p> <p>國際漫遊費用</p> <p>加值服務費用</p> <p>總費用</p> <p>應付帳款總計</p> <p>「加值服務費用」欄位的條件</p> </td>
   <td><p>下列欄位的值：</p>
    <ul>
     <li>通話費用</li>
     <li>電話會議費用</li>
     <li>簡訊費用 </li>
     <li>行動網際網路費用</li>
     <li>國家漫遊費用</li>
     <li>國際漫遊費用</li>
     <li>加值服務費用</li>
     <li>總費用（使用費用計算欄位）</li>
     <li>應付帳款總計（使用費用計算欄位）</li>
    </ul> <p>表格 — 用料表</p> </td>
   <td>無欄位</td>
   <td>--</td>
  </tr>
  <tr>
   <td>分項通話 — 傳出</td>
   <td><p>欄名稱：</p>
    <ul>
     <li>日期</li>
     <li>用时</li>
     <li>数字</li>
     <li>持续时间</li>
     <li>費用</li>
    </ul> </td>
   <td><p>所有值</p> <p>表格 — 呼叫</p> </td>
   <td>無欄位</td>
   <td>--</td>
  </tr>
  <tr>
   <td>立即付款</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>Paynow</td>
  </tr>
  <tr>
   <td>增值服務</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
