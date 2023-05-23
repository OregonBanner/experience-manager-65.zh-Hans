---
title: We.Retail參考實作
seo-title: We.Retail Reference Implementation
description: We.Retail是參考實作的技術預覽，說明使用AEM設定線上存在的建議方式
seo-description: We.Retail is a technology preview of a reference implementation that illustrates the recommended way of setting up an online presence with AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 9%

---

# We.Retail參考實作{#we-retail-reference-implementation}

## 简介 {#introduction}

We.Retail是參考實作和範例內容，說明使用Adobe Experience Manager設定線上存在的建議方式。

We.Retail運用最新AEM技術，例如HTL、回應式版面、可編輯範本、核心元件等。

雖然它說明了零售的垂直方向，但網站的設定方式可套用至任何垂直方向，而且只有產品目錄和購物車功能是零售專用的。

## 功能 {#features}

作為AEM標準參考實作，We.Retail會展示AEM一些最強大的功能。

| **专题** | **描述** | **有興趣嗎？** |
|---|---|---|
| [全域化網站結構](/help/sites-administering/tc-bp.md) | We.Retail包含即時複製到特定國家/地區網站的語言主版。 | [試試看！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [回應式佈局](/help/sites-authoring/responsive-layout.md) | 所有頁面都提供回應式版面，可動態調整以符合熒幕和裝置大小。 | [試試看！](/help/sites-developing/we-retail-responsive-layout.md) |
| [可編輯的範本](/help/sites-developing/page-templates-editable.md) | 所有頁面都以可編輯的範本為基礎，可讓非開發人員調整及自訂範本。 | [試試看！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML 模板语言](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | 所有元件都以HTL為基礎 |  |
| [電子商務功能](/help/commerce/cif-classic/developing/ecommerce.md) | 功能產品目錄 |  |
| [社群網站](/help/communities/overview.md) | 允許訪客加入社群討論、閱讀部落格等 |  |
| [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) | 所有元件均以新的核心元件為基礎，且更易於使用且可供使用者自行設定 | [試試看！](/help/sites-developing/we-retail-core-components.md) |
| [内容片段](/help/assets/content-fragments/content-fragments.md) | We.Retail體驗區段會展示透過內容片段重複使用內容的強大功能。 | [試試看！](/help/sites-developing/we-retail-content-fragments.md) |
| [体验片段](/help/sites-authoring/experience-fragments.md) | 體驗片段是一組一或多個元件，包括可在頁面中參考的內容和版面。 | [試試看！](/help/sites-developing/we-retail-experience-fragments.md) |

## 快速入门 {#getting-started}

We.Retail會以AEM範例內容的形式提供。 為了使用，只需 [正常啟動AEM](/help/sites-deploying/deploy.md#getting-started)，確定未停用範例內容。

>[!CAUTION]
>
>We.Retail不應安裝在生產執行個體上。 生產執行個體應於以下時間啟動： `nosamplecontent` [執行模式](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail以最新的AEM技術為基礎，因此不支援 [傳統UI編寫](/help/sites-classic-ui-authoring/home.md).

### 最新版本 {#latest-version}

雖然We.Retail是隨AEM發行而提供，但在發行後可能會進行內容及其功能的更新。 因此，可以 [從GitHub下載最新版本](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) 然後 [上傳](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) 和 [安裝](/help/sites-administering/package-manager.md#installing-packages) 它會以套件形式顯示在您的AEM執行個體上。

### 首要步骤 {#first-steps}

1. AEM啟動後（和/或安裝We.Retail），網站 **We.Retail** 可在以下位置找到： [網站主控台](/help/sites-authoring/basic-handling.md#global-navigation).
1. 例如，可以開啟以下頁面，它看起來應該像中顯示在 [附錄](#appendix) 下：

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail與Geometrixx {#we-retail-geometrixx}

Geometrixx及其許多化身可作為舊版AEM的範例內容。 自6.3版開始，We.Retail便已成為AEM隨附的範例內容，並作為新的標準參考實作。

We.Retail在技術上更健全，並運用最新的AEM技術，以更靈活、更可擴充，同時展示產品的最新功能。

### 功能比較 {#feature-comparison}

下表概略說明We.Retail與Geometrixx的主要功能。

* **可用** 表示在範例內容中找到功能的範例。
* **不可用** 這表示範例內容中沒有該功能的範例，但並不表示該功能本身沒有。

| **专题** | **We.Retail** | **Geometrixx** |
|---|---|---|
| 全域化網站結構 | 語言母版即時複製到特定國家/地區的網站 | 不可用 |
| 内容片段 | 可用 | 不可用 |
| 体验片段 | 可用 | 不可用 |
| 响应式布局 | 針對所有頁面 | 僅限Geometrixx Media |
| 可编辑模板 | 針對所有頁面 | 不可用 |
| HTL | 所有元件 | 有限 |
| 定位 | 針對所有頁面 | 僅限Geometrixx Outdoors |
| Screens | 可用 | 不可用 |
| 移动设备 | 不可用 | 可用 |
| 手稿 | 不可用 | 可用 |
| 輪播、下載、圖表元件 | 不可用 | 可用 |
| 欄控制項 | 取代為版面容器 | 可用 |
| Forms | 不可用 | 可用 |
| 营销活动 | 無電子郵件範例 | 可用 |

>[!NOTE]
>
>此清單力求完整，但不應視為詳盡無遺。

## Contribute {#contribute}

We.Retail已發行開放原始碼專案，並可從GitHub下載最新版原始碼。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-sample-we-retail專案](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

最新版本也可以 [已直接下載](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) 作為可安裝的套件。

如果您遇到問題，請歸檔 [GitHub問題](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

您可以隨意取用資料或協助撰寫 [提取請求](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## 预览 {#preview}

We.Retail歡迎頁面預覽：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
