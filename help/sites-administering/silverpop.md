---
title: 與Silverpop Engage整合
seo-title: Integrating with Silverpop Engage
description: 瞭解如何將AEM與Silverpop Engage整合
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# 與Silverpop Engage整合{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

將AEM與Silverpop Engage整合可讓您透過Silverpop管理及傳送在AEM中建立的電子郵件。 它也可讓您透過AEM頁面上的AEM Forms使用Silverpop的銷售機會管理功能。

整合提供您下列功能：

* 可在AEM中建立電子郵件，並將其發佈至Silverpop以進行發佈。
* 設定AEM表單動作以建立Silverpop訂閱者的功能。

設定Silverpop Engage後，您可以將電子報或電子郵件發佈至Silverpop Engage。

## 建立Silverpop設定 {#creating-a-silverpop-configuration}

可透過以下方式新增Silverpop設定： **Cloud Services**， **工具**，或 **API端點**. 本節將說明所有方法。

### 透過Cloud Services設定Silverpop {#configuring-silverpop-via-cloudservices}

若要在Cloud Services中建立Silverpop設定：

1. 在AEM中，點選或按一下 **工具** > **部署** > **Cloud Services**. (或直接存取 `https://<hostname>:<port>/etc/cloudservices.html`.)
1. 在協力廠商服務底下，按一下 **Silverop Engage** 然後 **設定**. Silverpop設定視窗隨即開啟。

   >[!NOTE]
   >
   >除非您從Package Share下載套件，否則Silverpop Engage不提供協力廠商服務選項。

1. 輸入標題，並選擇性地輸入名稱並按一下 **建立**. 隨即開啟** Silverpop設定**設定視窗。
1. 輸入使用者名稱和密碼，然後從下拉式清單中選取API端點。
1. 按一下 **連線到Silverpop。** 成功連線後，您會看到成功對話方塊。 按一下 **確定** 因此您會退出視窗。 您可以按一下「 」，前往Silverpop **前往Silverpop Engage**.
1. Silverpop已設定。 您可以按一下「 」以編輯設定 **編輯**.
1. 此外，Silverpop Engage架構也可藉由提供標題和名稱（選用）來設定個人化動作。 按一下「建立」即可成功為已設定的Silverpop連線建立架構。

   匯入的資料延伸模組欄稍後可透過AEM元件使用 —  **文字和個人化**.

### 透過工具設定Silverpop {#configuring-silverpop-via-tools}

若要在工具中建立Silverpop設定：

1. 在AEM中，點選或按一下 **工具** > **部署** > **Cloud Services**. 或前往以下位置直接導覽： `https://<hostname>:<port>/misadmin#/etc`.
1. 選取 **工具**，則 **Cloud Services設定、** 則 **Silverpop Engage**.
1. 按一下 **新增**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 在 **建立頁面** 視窗，輸入 **標題** 並可選擇使用 **名稱**，然後按一下 **建立**.
1. 依照上一個程式中的步驟4輸入組態資訊。 請依照該程式操作，以便完成設定Silverpop。

### 新增多個設定 {#adding-multiple-configurations}

若要新增多個組態：

1. 在歡迎頁面上，按一下 **Cloud Services** 並按一下 **Silverpop Engage**. 按一下 **顯示設定** 當有一個或多個Silverpop設定可用時顯示的按鈕。 列出所有可用的設定。
1. 按一下 **+** 在「可用設定」旁邊簽署。 它會開啟 **建立設定** 視窗。 請依照先前的組態程式操作，以便建立組態。

### 設定API端點以連線至Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

目前AEM有六個不安全的端點（參與1 - 6）。 Silverpop現在為現有端點提供兩個新的端點和已變更的連線端點。

若要設定API端點：

1. 前往 `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` 於 `https://<hostname>:<port>/crxde.`
1. 按一下右鍵並選取 **建立**，則 **建立節點**.
1. 輸入 **名稱** 作為 `sp-e0` 並選擇 **型別** 作為 `cq:Widget`.
1. 將兩個屬性新增至新新增的節點：

   1. **名稱**： `text`， **型別**： `String`， **值**： `Engage 0`
   1. **名稱**： `value`， **型別**： `String`， **值**： `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   按一下「全部儲存」。

1. 建立另一個節點，使用 **名稱** 作為 `sp-e7` 和 **型別** 作為 `cq:Widget`.

   將兩個屬性新增至新新增的節點：

   1. **名稱**： `text`， **型別**： `String`， **值**： `Pilot`
   1. **名稱**： `value`， **型別**： `String`， **值**： `https://apipilot.silverpop.com/XMLAPI`

1. 若要變更現有的API端點（參與1 - 6），請逐一按一下每個端點，然後以下列方式取代值：

   | **节点名称** | **現有端點值** | **新端點值** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. 按一下 **全部儲存**. AEM現在已準備好透過安全的端點連線至Silverpop。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
