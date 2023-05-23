---
title: 無法在Google Chrome、Firefox、Microsoft&reg； Edge、Microsoft&reg； Internet Explorer或Apple Safari中開啟XFAPDF forms
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# 無法在Google Chrome、Firefox、Microsoft、Edge、Microsoft®Internet Explorer或Apple Safari中開啟XFA®PDF forms{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

許多近期的瀏覽器版本都包含對XFA型PDF forms的有限支援。 雖然這些瀏覽器可以開啟XFA型PDF forms，但提供的功能有限。 如果您無法在現代瀏覽器中開啟或提交XFAPDF表單，請使用下列其中一種方法：

* 使用 [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) 或 [Adobe®Adobe®Reader®](https://get.adobe.com/reader/)，版本8或更新版本，以開啟和提交XFA型PDF forms。
* 在Microsoft® Windows®上，Acrobat和Reader可讓您設定在受保護檢視模式中開啟PDF，這會阻止以XFA為基礎的PDF forms開啟。 請確定Acrobat或Reader中的「受保護的檢視」模式已停用。 如需詳細資訊，請參閱 [受保護的檢視（僅限Windows）](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (針對Forms開發人員) Adobe Experience Manager Forms也提供以下支援：

   * [將XFA型表單轉譯為HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) 讓表單可在支援HTML5的瀏覽器中開啟，包括在iPad等行動裝置上執行的瀏覽器。 表單的HTML5轉譯可維護表單設計的版面，並支援內嵌於XFA表單範本中的大部分表單邏輯（例如JavaScript、表單計算和表單驗證）。
   * [將XFA型表單轉換為行動回應式的最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). 這些表單提供回應式版面、個人化功能，並視需要新增或移除欄位或區段，以動態調整以符合使用者的回應。 此外，也提供用於各種資料來源的現成聯結器、記錄檔案功能，以及輕鬆連線至Adobe Analytics以進行效能評估。 如需詳細資訊，請參閱 [主要特色與功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en).

如此一來，您在XFA表單中的技術投資就會受到保護，並持續為使用者提供最佳體驗。 如需詳細資訊，請參閱 [Adobe Experience Manager Forms產品檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html).
