---
title: AEM觸控式UI的結構
seo-title: Structure of the AEM Touch-Enabled UI
description: 在AEM中實作的觸控最佳化UI有幾項基礎原則，而且由數個關鍵元素組成
seo-description: The touch-optimized UI, as implemented in AEM, has several underlying principles and is made up of several key elements
uuid: 9a255238-1adc-4a40-9c37-30cb53ffb26c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 55dba890-4847-4986-b272-33480bc1d573
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 2%

---

# AEM觸控式UI的結構{#structure-of-the-aem-touch-enabled-ui}

AEM觸控式UI具備數個基本原則，且由數個關鍵元素組成：

## 控制台 {#consoles}

### 基本版面與調整大小 {#basic-layout-and-resizing}

UI同時適用於行動裝置和桌上型裝置，不過Adobe決定使用一種適用於所有熒幕和裝置的樣式，而不是建立兩種樣式。

所有模組都使用相同的基本版面，在AEM中這可以視為：

![chlimage_1-142](assets/chlimage_1-142.png)

版面配置會遵循回應式設計樣式，並配合您所使用的裝置/視窗大小。

例如，當解析度低於1024px （如同在行動裝置上）時，顯示器將會相應地調整：

![chlimage_1-143](assets/chlimage_1-143.png)

### 标题栏 {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

標題列會顯示全域元素，包括：

* 標誌與您目前使用的特定產品/解決方案；若為AEM，也會形成全域導覽的連結
* 搜索
* 存取說明資源的圖示
* 存取其他解決方案的圖示
* 任何等待您的警報或收件匣專案的指標（及存取權）
* 使用者圖示，以及設定檔管理的連結

### 工具栏 {#toolbar}

這與您的位置及表面工具相關，這些工具與控制以下頁面中的檢視或資產相關。 工具列是產品專屬的，但元素有一些共同之處。

工具列會在任何位置顯示目前可用的動作：

![chlimage_1-145](assets/chlimage_1-145.png)

也取決於目前是否選取資源：

![chlimage_1-146](assets/chlimage_1-146.png)

### 左边栏 {#left-rail}

您可以視需要開啟/隱藏左側邊欄，以顯示：

* **时间线**
* **引用**
* **过滤器**

預設值為 **僅內容** （欄隱藏）。

![chlimage_1-147](assets/chlimage_1-147.png)

## 页面创作 {#page-authoring}

編寫頁面時，結構區域如下。

### 内容框架 {#content-frame}

頁面內容會在內容框架中呈現。 內容框架完全獨立於編輯器 — 以確保不會因CSS或JavaScript而發生衝突。

內容框架位於視窗的右側區段、工具列下方。

![chlimage_1-148](assets/chlimage_1-148.png)

### 編輯器框架 {#editor-frame}

編輯器框架實現編輯功能。

編輯器框架是所有「 」的容器（抽象） *頁面製作元素*. 它位在內容框架頂端，並包括：

* 頂端工具列
* 側面板
* 所有覆蓋
* 任何其他頁面製作元素；例如，元件工具列

![chlimage_1-149](assets/chlimage_1-149.png)

### 側面板 {#side-panel}

其中包含兩個預設標籤，可讓您選取資產和元件；您可以從此處將其拖放到頁面上。

側面板預設為隱藏。 選取時，它將顯示在左側，或滑過以覆蓋整個視窗（當視窗大小低於1024畫素的寬度時；例如在行動裝置上）。

![chlimage_1-150](assets/chlimage_1-150.png)

### 側面板 — 資產 {#side-panel-assets}

在「資產」標籤中，您可以從資產範圍中選取。 您也可以篩選特定字詞，或選取群組。

![chlimage_1-151](assets/chlimage_1-151.png)

### 側面板 — 資產群組 {#side-panel-asset-groups}

在「資產」標籤中有一個下拉式清單，可用來選取特定資產群組。

![chlimage_1-152](assets/chlimage_1-152.png)

### 側面板 — 元件 {#side-panel-components}

在「元件」標籤中，您可以從元件範圍中選取。 您也可以篩選特定字詞，或選取群組。

![chlimage_1-153](assets/chlimage_1-153.png)

### 叠加 {#overlays}

這些會覆蓋內容框架，並由 [圖層](#layer) 瞭解如何與元件及其內容互動（完全透明）的機制。

這些覆蓋圖會在編輯器框架中顯示（包含所有其他頁面製作元素），但實際上會在內容框架中覆蓋適當的元件。

![chlimage_1-154](assets/chlimage_1-154.png)

### 圖層 {#layer}

圖層是獨立的功能組合，可啟動至：

* 提供不同的頁面檢視
* 可讓您操作和/或與頁面互動

這些圖層為整個頁面提供了複雜的功能，而不是為個別元件執行特定動作。

AEM隨附已為頁面製作實作的數個圖層；包括例如，編輯、預覽、註釋。

>[!NOTE]
>
>圖層是一個強大的概念，可影響使用者對頁面內容的檢視以及與頁面內容的互動。 開發自己的圖層時，您需要確保圖層在退出時進行清除。

### 圖層切換器 {#layer-switcher}

圖層切換器可讓您選擇要使用的圖層。 當關閉時，它會指出目前使用的圖層。

圖層切換器可從工具列（位於視窗頂端、編輯器框架內）以下拉式清單的形式提供。

![chlimage_1-155](assets/chlimage_1-155.png)

### 组件工具栏 {#component-toolbar}

每個元件例項在按一下後都會顯示其工具列（按一下或緩慢按兩下）。 工具列包含頁面上元件執行個體（可編輯）可用的特定動作（例如複製、貼上、開啟編輯器）。

根據可用的空間，元件工具列會放置在適當元件的右上角或右下角。

![chlimage_1-156](assets/chlimage_1-156.png)

## 更多信息 {#further-information}

如需觸控式UI概念的詳細資訊，請繼續閱讀文章 [AEM觸控式UI的概念](/help/sites-developing/touch-ui-concepts.md).

如需進一步的技術資訊，請參閱 [JS檔案集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) （觸控式頁面編輯器）。
