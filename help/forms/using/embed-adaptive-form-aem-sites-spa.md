---
title: 在AEM Sites單頁應用程式中內嵌最適化表單或互動式通訊
seo-title: Embed adaptive forms or Interactive Communications in AEM Sites pages
description: 在AEM Sites頁面中內嵌最適化表單或互動式通訊。 使用者無需離開Sites頁面即可填寫及提交表單。
seo-description: You can embed adaptive forms or Interactive Communication in AEM Sites pages. Users can fill and submit forms without leaving the Sites page.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# 在AEM Sites單頁應用程式中內嵌最適化表單或互動式通訊{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概述 {#overview}

AEM Forms可讓表單開發人員在AEM Sites單頁應用程式(SPA)中順暢地內嵌最適化表單和互動式通訊。 內嵌的最適化表單和互動式通訊功能齊全，使用者無需離開頁面即可填寫和提交表單。 它有助於使用者停留在網頁上其他元素的上下文中，並同時與最適化表單或互動式通訊互動。

在AEM Sites單頁應用程式中，您可以使用新增最適化表單或互動式通訊 [AEM Forms SPA容器元件](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 它是AEM Sites SPA的AEM Forms元件，可新增至您的網站頁面。

如需在非SPA AEM Sites中內嵌最適化表單的相關資訊，請參閱 [在AEM Sites頁面中內嵌最適化表單或互動式通訊](/help/forms/using/embed-adaptive-form-aem-sites.md).

## 前提条件 {#prerequisites}

若要使用AEM Forms SPA Container元件在AEM Sites SPA中內嵌最適化表單或互動式通訊，請確定您已安裝：

* Java SE開發套件8或更新版本
* Apache Maven 3.3.1或更新版本
* AEM作者執行個體
* [AEM Forms 6.4.2附加元件套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 在作者執行個體上

## 安裝AEM Forms SPA容器元件 {#install-aem-forms-spa-container-component}

執行以下步驟，安裝AEM Forms SPA Container元件：

1. [複製或下載適用於SPA的AEM Forms元件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. 安裝適用於SPA的AEM Forms元件。 有關安裝元件的指示，請參閱 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 檔案。

   元件包含 [範例React元件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) ，可用來整合SPA容器元件與React型SPA專案。

1. [複製或下載以React為基礎的SPA專案](https://github.com/adobe/aem-sample-we-retail-journal).
1. 使用「 」中提供的指示，將SPA容器元件與React型SPA專案整合 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) 檔案。

   安裝AEM Forms SPA Container元件並將該元件與React型SPA專案整合後，您可以在AEM Sites頁面中內嵌最適化表單和互動式通訊。

## 內嵌最適化表單或互動式通訊 {#af-component}

若要使用AEM Forms for SPA Container元件內嵌最適化表單或互動式通訊：

1. 以編輯模式開啟AEM sites頁面，您要在其中內嵌最適化表單或互動式通訊。
1. 插入 **SPA適用的AEM表單** 元件時，可使用下列任一選項：

   * 點選「網站」頁面上的版面容器，然後點選 **+** 並選取 **SPA適用的AEM表單** 元件。

   * 在元件瀏覽器面板中，拖放 **SPA適用的AEM表單** 元件時。
   * 在Assets瀏覽器中搜尋最適化表單或互動式通訊，並將其拖放至Sites頁面。 它會將表單內嵌在SPA元件容器的AEM Forms中。

   >[!NOTE]
   >
   >不支援在頁面上呈現多個AEM Forms SPA Container元件。 一個頁面上可以有多個AEM Forms SPA Container，但一次只能轉譯一個元件。 請確定頁面上只顯示一個元件，以避免差異。

1. 點選網站頁面中的內嵌AEM Forms SPA容器元件，然後點選 ![settings_icon](assets/settings_icon.png) 在動作列上。 此 **編輯AEM Forms SPA容器** 對話方塊開啟。
1. 在 **編輯AEM Forms容器** 對話方塊中，指定下列專案：

   * **資產型別：** 選取要內嵌的資產型別。 選項包括 **最適化表單** 和 **互動式通訊**

   * **資產路徑**：瀏覽並選取要內嵌的最適化表單或互動式通訊。 如果使用Assets瀏覽器插入最適化表單或互動式通訊，則會自動填入欄位。
   * **頻道** （僅限互動式通訊）：選取要內嵌的互動式頻道型別。 選項包括 **網路頻道** 和 **Print Channel**.

   * **主題**：選取定義最適化表單或互動式通訊元件樣式的主題。 樣式包含外觀屬性，例如字型樣式、背景顏色、尺寸和對齊方式。

1. 點選 ![done_icon](assets/done_icon.png) 以儲存設定。 最適化表單或互動式通訊現在內嵌在頁面中。

## 發佈內嵌式最適化表單和互動式通訊 {#publish-embedded-adaptive-form-and-interactive-communication}

在AEM Sites頁面上發佈內嵌資產（最適化表單或互動式通訊）時，請考量下列情況：

* 如果您是第一次發佈AEM Sites頁面，且其中包含內嵌的最適化表單或互動式通訊，請發佈Sites頁面和內嵌資產。
* 如果您在已發佈的Sites頁面中僅修改內嵌的最適化表單或互動式通訊，請發佈原始資產，而變更會反映在已發佈的Sites頁面中。 已發佈的Sites頁面包含資產的參考，不需要重新發佈頁面。
* 如果您修改了Sites頁面和內嵌的最適化表單或互動式通訊，請重新發佈Sites頁面和內嵌資產。

## 修改內嵌的最適化表單和互動式通訊 {#modify-embedded-adaptive-form-and-interactive-communication}

AEM sites頁面會維護AEM Forms容器中適用性表單和互動式通訊的參考。 因此，在原始最適化表單和互動式通訊中設定的所有設定和屬性（例如主題、樣式和提交動作）都會保留在內嵌的最適化表單和互動式通訊中。

若要修改內嵌式最適化表單和互動式通訊的任何設定或屬性，請執行下列任一項作業。

* 在各自的編輯器中以最適化表單或互動式通訊開啟原始表單並加以修改。
* 在編輯模式下，從Sites頁面內點選最適化表單或互動式通訊，然後點選 **在新視窗中編輯**. 原始表單會在編輯模式下開啟。

## 考量事項和最佳作法 {#considerations-and-best-practices}

將調適型表單內嵌於AEM網站頁面時，請記住下列幾點：

* 內嵌表單中不包含原始表單的頁首和頁尾。
* 使用者草稿和嵌入式表單的提交受到支援，並可在Forms入口網站上的「草稿」和「已提交的Forms」標籤中看到。
* 在原始表單上設定的提交動作會保留在內嵌表單中。
* 在原始表單上設定的體驗鎖定目標和A/B測試在內嵌表單中無法運作。 不過，您可以使用Sites頁面上的體驗鎖定目標，根據使用者設定檔顯示不同的表單。
* 如果您已針對原始表單設定Adobe Analytics，則會在Adobe Analytics中擷取內嵌表單的分析資料。 但是，它不會出現在Forms Analytics報表中。
