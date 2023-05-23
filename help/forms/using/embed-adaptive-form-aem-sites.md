---
title: 在AEM sites頁面中內嵌最適化表單或互動式通訊
seo-title: Embed an adaptive form or interactive communication in AEM sites page
description: 您可以將調適型表單內嵌在AEM網站頁面中。 使用者無需離開網站頁面，即可填寫及提交表單。
seo-description: You can embed adaptive forms in AEM sites pages. Users can fill and submit forms without leaving the site pages.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
feature: Adaptive Forms
exl-id: 00ee7929-649f-4cbb-be79-ba13ac73a16d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# 在AEM sites頁面中內嵌最適化表單或互動式通訊 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## 概述 {#overview}

AEM Forms可讓表單開發人員在AEM Sites頁面或AEM外部託管的網頁中，順暢地內嵌最適化表單和互動式通訊。 內嵌的最適化表單和互動式通訊功能完善，使用者無需離開頁面即可填寫和提交表單。 它有助於使用者停留在網頁上其他元素的上下文中，同時與表單或互動式通訊互動。

如需將最適化表單內嵌於外部網頁的相關資訊，請參閱 [將最適化表單內嵌於外部網頁](/help/forms/using/embed-adaptive-form-external-web-page.md).

在AEM Sites頁面中，您可以使用以下專案新增最適化表單或互動式通訊：

* **[AEM Forms容器元件](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms提供可新增至網站頁面的元件。 AEM Forms容器元件可讓您內嵌最適化表單和互動式通訊。

* **[資產瀏覽器](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
您可以在Assets下使用您建立的所有表單和互動式通訊。 您可以將表單作為資產拖放至頁面上。

## 前提条件 {#prerequisites}

若要將最適化表單或互動式通訊內嵌在使用可編輯範本的AEM網站頁面中，請確定AEM表單元件已設定為關聯範本中允許的元件。 如需詳細資訊，請參閱 **原則與屬性（配置容器）** 中的區段 [建立頁面範本](/help/sites-authoring/templates.md).

如果網站頁面使用靜態範本，您必須在網站頁面的段落系統中進行設定。 另請參閱 [在設計模式中設定元件](/help/sites-authoring/default-components-designmode.md) 以取得詳細資訊。

## 內嵌最適化表單或互動式通訊 {#af-component}

若要使用AEM Forms容器元件內嵌最適化表單或互動式通訊：

1. 以編輯模式開啟AEM sites頁面，您要在其中內嵌最適化表單或互動式通訊。
1. 從元件瀏覽器面板中，將AEM Forms容器元件拖放至頁面上。

   或者，您也可以在Assets瀏覽器中搜尋最適化表單或互動式通訊，並將其拖放至Sites頁面。 它將表單內嵌在AEM Forms容器中。

   >[!NOTE]
   >
   >不支援頁面上的多個AEM Forms容器元件。

1. 點選網站頁面中的內嵌AEM Forms容器元件，然後點選 ![settings_icon](assets/settings_icon.png) 在動作列上。 此 **[!UICONTROL 編輯AEM Forms容器]** 對話方塊開啟。
1. 在「編輯AEM Forms容器」對話方塊中，指定下列專案。

   * **資產型別：** 選取要內嵌的資產型別。 選項包括最適化表單和互動式通訊
   * **資產路徑**：瀏覽並選取要內嵌的最適化表單或互動式通訊。 如果您從「資產」瀏覽器中將其刪除，則會自動填入。
   * （僅限最適化表單） **貼文提交**：選取要在表單提交時觸發的動作。 您可以選擇顯示感謝訊息或感謝頁面。

      * **感謝訊息**：使用RTF編輯器撰寫訊息，以在表單提交時顯示。 只有當您選擇顯示感謝訊息時，才可使用此選項。
      * **感謝頁面**：瀏覽並選取表單提交時顯示的頁面。 只有當您選擇顯示感謝頁面時，才可使用此選項。
      * **提交時重新整理頁面**：啟用以重新整理包含內嵌最適化表單的頁面，以顯示感謝頁面。 否則，感謝頁面會取代AEM Forms容器中的最適化表單，而不會重新整理頁面。 只有當您選擇顯示感謝頁面時，才可使用此選項。
   * **主題**：選取定義最適化表單或互動式通訊元件樣式的主題。 樣式包含外觀屬性，例如字型樣式、背景顏色、尺寸和對齊方式。
   * **高度**：指定容器的高度。 保留空白以自動調整容器大小。
   * **CSS使用者端資源庫**：指定CSS使用者端資料庫的路徑。


1. 儲存設定。 最適化表單或互動式通訊現在內嵌在頁面中。

## 發佈內嵌式最適化表單和互動式通訊 {#publishing-embedded-adaptive-form-and-interactive-communication}

讓我們考慮以下在AEM網站頁面中發佈內嵌資產（最適化表單或互動式通訊）的情境：

* 如果您是第一次發佈AEM網站頁面，且其中包含內嵌的最適化表單或互動式通訊，請發佈網站頁面和內嵌資產。
* 如果您在已發佈的網站頁面中僅修改內嵌的最適化表單或互動式通訊，請發佈原始資產，而變更會反映在已發佈的網站頁面中。 已發佈的網站頁面包含對資產的引用，不需要重新發佈頁面。
* 如果您修改了網站頁面和內嵌的最適化表單或互動式通訊，請重新發佈網站頁面和內嵌資產。

## 修改內嵌的最適化表單和互動式通訊 {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM sites頁面會維護最適化表單的參考，以及AEM Forms容器中的互動式通訊。 因此，在原始最適化表單和互動式通訊中設定的所有設定和屬性（例如主題、樣式和提交動作）都會保留在內嵌的最適化表單和互動式通訊中。

若要修改內嵌式最適化表單和互動式通訊的任何設定或屬性，請執行下列任一項作業。

* 在各自的編輯器中以最適化表單或互動式通訊開啟原始表單並加以修改。
* 在編輯模式下，從網站頁面內點選最適化表單或互動式通訊，然後點選 **[!UICONTROL 在新視窗中編輯]**. 原始表單會以您可以修改的編輯模式開啟。

>[!NOTE]
>
>在原始最適化表單或互動式通訊中所做的變更會自動反映在內嵌表單中。 不過，請重新發佈最適化表單、互動式通訊或網站頁面，以反映已發佈頁面中的變更。

## 考量事項和最佳作法 {#considerations-and-best-practices}

將調適型表單內嵌於AEM網站頁面時，請記住下列幾點：

* 內嵌表單中不包含原始表單的頁首和頁尾。
* 使用者草稿和嵌入式表單的提交受到支援，並可在Forms入口網站上的「草稿」和「已提交的Forms」標籤中看到。
* 在原始表單上設定的提交動作會保留在內嵌表單中。
* 在原始表單上設定的體驗鎖定目標和A/B測試在內嵌表單中無法運作。 不過，您可以使用網站頁面上的體驗鎖定目標，根據使用者設定檔顯示不同的表單。
* 如果您已針對原始表單設定Adobe Analytics，則會在Adobe Analytics中擷取內嵌表單的分析資料。 但是，它不會出現在Forms Analytics報表中。
