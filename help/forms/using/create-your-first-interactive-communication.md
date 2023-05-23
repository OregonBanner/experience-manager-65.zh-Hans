---
title: 教學課程 — 建立您的第一個互動式通訊
seo-title: Create your first Interactive Communication
description: 瞭解如何建立您的第一個互動式通訊。
seo-description: Learn to create your first Interactive Communication.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
source-git-commit: 471d7f48dc4653000b4852dbbeb886b05e28e644
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# 教學課程：建立您的第一個互動式通訊 {#tutorial-create-your-first-interactive-communication}

瞭解如何建立您的第一個互動式通訊。

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

互動式通訊可集中處理及管理安全、個人化與互動式信函的建立、集合與傳遞，例如商務信函、檔案、對帳單、行銷郵件、帳單和歡迎套件。 互動式通訊可使用兩種管道來提供：列印和網路。 Print channel用於建立PDF和紙張通訊，而Web channel用於提供線上體驗。

本教學課程提供建立互動式通訊的端對端架構。 本教學課程可組織為一個使用案例和多個指南。 每個指南都可協助您建立功能，這些功能會作為建立互動式通訊的建置組塊。

下圖說明建立互動式通訊所需的組成要素。

![工作流](assets/workflow.gif)

在本教學課程結束時，您將能夠：

* 建立組成要素（表單資料模型、檔案片段和範本）
* 建立互動式通訊
* 測試並發佈互動式通訊

## 使用案例 {#use-case}

歷程從學習使用案例開始：

電信營運商透過電子郵件每月向客戶傳送帳單。 帳單是互動式通訊。 電子郵件包含：

* 受密碼保護的PDF，在本教學課程中稱為Print channel。 其中包含客戶詳細資料、帳單詳細資料、費用摘要、便利的帳單支付模式和使用方式詳細資料。
* 帳單網頁版本的連結，在本教學課程中稱為網頁管道。 帳單的網頁版本，除了PDF版本中涵蓋的詳細資訊外，還提供使用詳細資訊的圖形表示，以及根據Adobe Target的個人化優惠方案。 網頁版本也包含線上付款表單。 它有助於在不離開積體電路的情況下進行線上付款。
* 附加值服務的連結，例如線上儲存、音樂訂閱和隨選視訊訂閱。

## 前提条件 {#prerequisites}

* 設定AEM編寫執行個體。
* 安裝 [AEM Forms附加元件](/help/forms/using/installing-configuring-aem-forms-osgi.md) 在作者執行個體上
* 設定MYSQL資料庫
* 從資料庫提供者取得JDBC資料庫驅動程式（JAR檔案）。 教學課程中的範例是以MySQL資料庫為基礎，並使用Oracle的 [MySQL JDBC資料庫驅動程式](https://dev.mysql.com/downloads/connector/j/5.1.html).

## 步驟1：規劃互動式通訊 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

規劃互動式通訊的第一步是完成互動式通訊的內容。 內容完成之後，您必須加以分析，以識別建立互動式通訊所需的各種資產型別。

**目标：**

若要使用下列資料輸入模式來建立互動式通訊的剖析：

* 靜態文字
* 表單資料模型
* 代理 UI
* 條件資料
* 图像

[ ](/help/forms/using/planning-interactive-communications.md)

## 步驟2：建立表單資料模型 {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

表單資料模型可讓您將互動式通訊連線到不同的資料來源。 例如，AEM使用者設定檔、RESTful Web服務、以SOAP為基礎的Web服務、OData服務和關聯式資料庫。 表單資料模型是連線資料來源中可用的商業實體和服務的統一資料表示架構。 您可以搭配互動式通訊使用表單資料模型，從連線的資料來源擷取資料。 如需表單資料模型的詳細資訊，請參閱 [AEM Forms資料整合](/help/forms/using/data-integration.md).

**目标：**

* 將資料庫執行處理（MySQL資料庫）設定為資料來源
* 使用MySQL資料庫作為資料來源來建立表單資料模型
* 將資料模型物件新增至表單資料模型
* 設定表單資料模型的讀取和寫入服務
* 建立資料模型物件之間的關聯
* 檢視自動產生的範例資料
* 編輯範例資料
* 測試表單資料模型和已設定的服務（包含測試資料）

[ ](/help/forms/using/create-form-data-model0.md)

## 步驟3：建立檔案片段 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

檔案片段是通訊的可重複使用元件，用於構成互動式通訊。 檔案片段的型別有：文字、清單和條件。

**目标：**

* 建立檔案片段
* 建立變數
* 建立和套用規則

[ ](/help/forms/using/create-document-fragments.md)

## 步驟4：建立範本 {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

若要建立互動式通訊，您必須在AEM伺服器上擁有可供列印和Web Channels使用的範本。

列印頻道的範本是在AdobeForms Designer中建立並上傳至AEM伺服器。 建立互動式通訊時，即可使用這些範本。

Web channel的範本是在AEM中建立。 範本作者和管理員可以建立、編輯和啟用網頁範本。 建立並啟用後，這些範本便可在建立互動式通訊時使用。

**目标：**

* 使用AdobeForms Designer為列印頻道建立XDP範本
* 將XDP範本上傳至AEM Forms伺服器
* 建立和啟用網頁頻道的範本

[ ](/help/forms/using/create-templates-print-web.md)

## 步驟5：建立互動式通訊 {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

一旦您為Web版本建立了所有建置區塊（例如表單資料模型、檔案片段和範本），您就可以開始建立互動式通訊。

互動式通訊可透過兩種管道提供：列印和網路。 您也可以建立以Print channel為主體的互動式通訊。 Web channel的「列印為主版」選項可確保從Print channel衍生出Web channel的內容、繼承和資料繫結。

**目标：**

* 為列印頻道建立互動式通訊
* 建立Web channel的互動式通訊
* 以「列印為主版」建立列印與Web互動式通訊
* 在互動式通訊的Web版本中建立動態表格
* 在Web版本的互動式通訊中建立圖表
* 在互動式通訊的Web版本中建立超連結

[ ](/help/forms/using/create-interactive-communication0.md)

## 步驟6：發佈互動式通訊 {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

使用列印和Web通道建立及測試互動式通訊後，您就可以發佈這些資產。 本教學課程中說明的使用案例著重於將這些資產與電子郵件使用者端整合。 電子郵件使用者端可作為橋接器，將互動式通訊傳送至多個電子郵件地址。

**目标：**

* 將互動式通訊與電子郵件使用者端整合，以便向客戶傳送通訊
* 將PDF檔案加入為附件（在Print channel中建立的互動式通訊）
* 加入互動式通訊Web版本的連結
