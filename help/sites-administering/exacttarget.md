---
title: 與ExactTarget整合
seo-title: Integrating with ExactTarget
description: 瞭解如何將AEM與ExactTarget整合。
seo-description: Learn how to integrate AEM with ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 與ExactTarget整合{#integrating-with-exacttarget}

將AEM與Exact Target整合可讓您透過Exact Target管理及傳送在AEM中建立的電子郵件。 它也可讓您透過AEM頁面上的AEM Forms使用Exact Target的銷售機會管理功能。

整合提供您下列功能：

* 能夠在AEM中建立電子郵件，並將其發佈到Exact Target以進行分發。
* 設定AEM表單動作以建立Exact Target訂閱者的功能。

設定ExactTarget後，您可以將電子報或電子郵件發佈至ExactTarget。 另請參閱 [將電子報發佈至電子郵件服務](/help/sites-authoring/personalization.md).

## 建立ExactTarget設定 {#creating-an-exacttarget-configuration}

可透過Cloudservices或工具新增ExactTarget設定。 本節將說明這兩種方法。

### 透過Cloudservices設定ExactTarget {#configuring-exacttarget-via-cloudservices}

若要在Cloud Services中建立ExactTarget組態：

1. 在歡迎頁面上，按一下 **Cloud Services**. (或直接存取 `https://<hostname>:<port>/etc/cloudservices.html`.)
1. 按一下 **ExactTarget** 然後 **設定**. ExactTarget組態視窗隨即開啟。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 輸入標題，並選擇性地輸入名稱並按一下 **建立**. 此 **ExactTarget設定** 組態視窗會開啟。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 輸入使用者名稱和密碼，然後選取API端點(例如， **https://webservice.exacttarget.com/Service.asmx**)。
1. 按一下 **連線到ExactTarget。** 成功連線後，您會看到成功對話方塊。 按一下 **確定** 以結束視窗。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 選取帳戶（如果可用）。 此帳戶適用於Enterprise 2.0客戶。 单击&#x200B;**确定**。

   已設定ExactTarget。 您可以按一下「 」以編輯設定 **編輯**. 您可以按一下「 」，前往「精確目標」 **前往ExactTarget**.

1. AEM現在提供資料擴充功能功能。 您可以匯入ExactTarget資料擴充功能欄。 除了已成功建立的ExactTarget設定外，按一下出現的「+」符號即可進行設定。 您可以從下拉式清單中選取任何現有的資料延伸模組。 如需如何設定資料擴充功能的詳細資訊，請參閱 [ExactTarget檔案](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   匯入的資料延伸模組欄稍後可透過 **文字和個人化** 元件。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 透過工具設定ExactTarget {#configuring-exacttarget-via-tools}

若要在工具中建立ExactTarget組態：

1. 在歡迎頁面上，按一下 **工具**. 或前往以下位置直接導覽： `https://<hostname>:<port>/misadmin#/etc`.
1. 選取 **工具**，則 **Cloud Services設定、** 則 **ExactTarget**.
1. 按一下 **新增** 以開啟**建立頁面**視窗。

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. 輸入 **標題** 並可選擇使用 **名稱**，然後按一下 **建立**.
1. 依照上一個程式中的步驟4輸入組態資訊。 請依照該程式完成設定ExactTarget。

### 新增多個設定 {#adding-multiple-configurations}

若要新增多個組態：

1. 在歡迎頁面上，按一下 **Cloud Services** 並按一下 **ExactTarget**. 按一下 **顯示設定** 當有一個或多個ExactTarget設定可用時顯示的按鈕。 列出所有可用的設定。
1. 按一下 **+** 在「可用設定」旁邊簽署。 如此將可開啟 **建立設定** 視窗。 按照之前的組態程式來建立新組態。
