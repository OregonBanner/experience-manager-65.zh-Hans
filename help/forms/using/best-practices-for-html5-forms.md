---
title: HTML5表單的最佳作法
seo-title: Best practices for HTML5 forms
description: 調整您的XFA型HTML5 Forms以獲得最佳效能。
seo-description: Learn how to tune your XFA-based HTML5 Forms for best performance.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
feature: Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# HTML5表單的最佳作法{#best-practices-for-html-forms}

## 概述 {#overview}

AEM Forms有一個名為「HTML5表單」的元件。 它有助於以HTML5格式呈現現有XFA型PDF forms（XDP檔案）。 本檔案提供減少載入時間及改善行動裝置上HTML5表單效能的准則和建議。

大部分的行動裝置處理能力和記憶體功能有限。 這有助於改善行動裝置的待命時間。 在行動裝置上執行的網頁瀏覽器可存取有限的資源（有限的記憶體與處理功能）。 達到限制後，瀏覽器行為會變得緩慢。 本檔案提供保持HTML5表單大小處於核取狀態的建議。 較小的格式不會違反裝置的記憶體與處理能力限制，並提供順暢的體驗。

雖然如此，本文章中討論的建議僅針對HTML5表單，但這些建議同樣適用於XFA型PDF forms。 這些最佳實務共同為HTML5表單的整體效能做出貢獻。 需要精心規劃，以開發有效率且高生產力的表單。 讓我們開始吧：

## 節點是HTML5表單的貨幣，明智地使用它們 {#nodes-are-currency-of-html-forms-spend-them-wisely}

通常，XFA表單有多個元素。 例如，表格、文字欄位和影像。 每個元素都有許多屬性可控制元素的行為和外觀。 以HTML5格式轉譯XFA表單時，所有XFA元素和對應的屬性都會轉換為模型或HTMLDOM節點。 這些節點會增加DOM的大小和複雜性。 使HTML5表單呈現速度變慢。

瀏覽器更容易轉譯較精簡的DOM。 因此，您可以在XFA表單上執行下列最佳化來減少節點數量。 因此，請產生精簡DOM結構：

* 使用caption屬性來新增標籤至欄位。 請勿使用個別的Text元素來新增標籤。 它有助於減輕額外的重量，進而提升效能。 它還有助於避免版面問題。
* 將表單上Draw文字元素的數目維持在最小值。 繪圖元素有助於改善可讀性和外觀，但沒有任何資訊儲存功能。 建議將多個Draw文字元素合併為一個Draw文字元素。 不許翻動任何石頭，讓表單變得更精簡。

## Lite表單執行效能更佳，可保持資源壓縮狀態 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表單可包含多個外部資源，例如影像、JavaScript和CSS檔案。 每次瀏覽器請求表單時，都會透過網路傳送外部資源。 在網路上傳輸所需的時間與檔案大小成正比。

因此，減少外部資源的大小並只使用絕對需要的資源是改善表單效能的偏好方法。 您可以對XFA表單執行下列最佳化，以減少表單的外部資源大小：

* 使用 [壓縮影像](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). 它可減少呈現表單所需的網路活動和記憶體容量。 因此，表單載入時間會大幅縮短。
* 使用AEM Configuration Manager (Day CQHTML程式庫管理員)中的minify選項來壓縮JavaScript和CSS檔案。 如需詳細資訊，請參閱 [OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md).
* 啟用Web壓縮。 它可縮減源自表單的請求和回應大小。 如需詳細資訊，請參閱 [AEM表單伺服器的效能調整](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html).

## 保持興趣不變，僅顯示必要欄位  {#keep-the-interest-alive-show-only-required-fields}

HTML5表單可能會有數百頁。 含有大量欄位的表單在瀏覽器中載入緩慢。 您可以對XFA表單執行下列最佳化，以最佳化具有大量欄位和頁面的表單：

* 評估將大型表單分割為多個表單。 您也可以使用表單集將所有較小的表單分組，並將它們顯示為單一單位。 表單集只會載入必要的表單。 此外，在表單集中，您可以設定不同表單中的通用欄位以共用資料繫結。 資料繫結可協助使用者僅填入一次一般資訊；資訊會自動填入後續的表單，進而大幅改善效能。 如需表單集的詳細資訊，請參閱 [AEM表單中的表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).
* 請考慮分割區段並將每個區段移至不同頁面。 HTML5表單會在頁面捲動請求時動態載入每個頁面。 記憶體中只會儲存捲動頁面（顯示的頁面和其前面的頁面），其餘頁面則會隨選載入。 因此，在其本身的頁面上分割和移動區段可縮短載入表單所需的時間。 您也可以使用表單的第一頁作為登入頁面。 它類似於書籍的目錄(TOC)。 表單登入頁面僅包含表單其他區段的連結。 它大幅改善表單第一頁的載入時間，並導致改善使用者體驗。
* 依預設，保持條件區段隱藏。 只有在符合特定條件時，才可看見這些區段。 這有助於將DOM的大小維持在最小。 您也可以使用標籤式導覽，一次只顯示一個截面。

## 越少越好，請減少頁數 {#less-is-more-reduce-the-number-of-pages}

HTML5表單可包含資料導向欄位（表格和子表單）。 這些欄位會展開執行階段表單的大小。 例如，HTML5表單中的資料驅動表格可以跨越數千列。 這類表格可能會導致版面配置和效能降低。 以下建議的最佳化可協助您縮短資料導向欄位HTML5表單的載入時間：

* 使用XFA指令碼完成分頁導覽，以顯示資料導向欄位（表格和子表單）。 在分頁導覽中，頁面上只會顯示特定資料。 它限制瀏覽器上色作業為一次顯示的欄位，並使表單導覽更容易。 此外，行動裝置上的使用者只對資料的子集感興趣。 它可幫助您提供絕佳的使用者體驗，並減少載入所需資料所需的時間。 您只需要一個的價格，就能得到兩個解決方案。  另請注意，分頁導覽無法直接使用。 您可以使用XFA指令碼來開發分頁導覽。

* 評估將多個唯讀欄合併為單一欄的情況。 它可減少顯示表單所需的記憶體。 此外，請避免顯示不需要使用者輸入任何內容的欄。
* 評估將資料驅動表單分割為 [表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)，則上述建議不會帶來許多改善專案。 例如，如果表格超過1000列，則每100列會移至不同的表單。 這有助於改善表單的載入時間和效能。  另請注意，表單集會產生所有表單的合併提交XML。 若要區分每個表單的資料，請使用不同的資料根。 如需詳細資訊，請參閱 [AEM Forms中的表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## 記錄檔案(DOR)的二進位功能 {#power-of-two-for-document-of-record-dor}

XFA表單可以有大量的專用於記錄檔案(DOR)的區段。 為了減少節點數並改善這類表單的效能，您可以維護不同的表單副本 — 一個副本用於填寫表單，另一個副本用於在伺服器上產生記錄檔案。 在填入XFA表單的副本中，顯示僅擷取資料所需的欄位。 在從產生記錄檔案XFA中，僅在表單的列印輸出中保留必填欄位。 在選擇建議的方法之前，請評估效能增益和維護額外負荷。

## 建議閱讀  {#recommended-reads}

Adobe Experience Manager (AEM)表單可協助您將複雜的交易轉換為簡單、愉快的數位體驗。 然而，需要共同努力開發有效率且高生產力的表單。 除了HTML5 Forms之外，以下是一些一般AEM最佳實務的建議閱讀：

* [部署和維護AEM的最佳作法](/help/sites-deploying/best-practices.md)
* [製作內容的最佳實務](/help/sites-authoring/best-practices.md)
* [管理AEM的最佳作法](/help/sites-administering/administer-best-practices.md)
* [開發解決方案的最佳作法](/help/sites-developing/best-practices.md)
* [使用最適化表單的最佳作法](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms伺服器未將字型內嵌至動態PDF表單](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## 快速參考卡 {#quick-reference-card}

您可以列印下列卡片（按一下卡片可下載高解析度版本），並將其放在您的案頭上以供快速參考：
[ ![HTML5 Forms最佳實務快速參考卡](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
