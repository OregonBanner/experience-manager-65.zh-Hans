---
title: 组件概述
seo-title: Components
description: 组件是模块化单元，可实施特定功能以在您的网站上展示您的内容
seo-description: Components are modular units which realize specific functionality to present your content on your website
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 52%

---

# 组件概述{#components-overview}

此页面概述了 Adobe Experience Manager (AEM) 组件，例如那些[用于页面创作](/help/sites-authoring/default-components-foundation.md)的组件。

## 什么是组件？ {#what-exactly-is-a-component}

* 模块化单元，可实施特定功能以在您的网站上展示您的内容。
* 可重用的。
* 作为存储库的一个文件夹中的独立单元开发。
* 没有隐藏的配置文件。
* 可以包含其他组件。
* 可以在任何AEM系統中的任何地方執行。 它們也可以限製為可在特定元件下執行。
* 拥有标准化的用户界面。
* 具有可配置的编辑行为。
* 使用根據Granite UI元件的子元素建置的對話方塊
* 使用以下專案開發 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) （建議）或JSP。
* 可以开发以创建扩展默认功能的自定义组件。

由于组件是模块化的，因此您可以：

* 在本地实例上开发新组件。
* 将它部署到测试环境。
* 将它部署到实时创作环境，作者和/或管理员可在该环境中添加和配置内容。
* 将它部署到实时发布环境，它在该环境中用于为您网站的访客呈现内容。特定元件（例如Communities）也接受使用者的輸入。

每个 AEM 组件：

* 是一种资源类型。
* 是一个完全实施特定功能的脚本的集合。
* 可以在中運作 *隔離*，表示在AEM或入口網站中。

## AEM中的現成元件 {#out-of-the-box-components-within-aem}

AEM隨附多種多樣的 [現成可用的元件](/help/sites-authoring/default-components.md) 提供完整的功能，包括：

* 段落系统 ( `parsys`)
* 頁面( `responsivegrid`  — 僅限觸控式UI)
* 文本
* 影像（含隨附文字）
* 工具栏

提供的元件及其在 [範例We.Retail網站](/help/sites-developing/we-retail.md) 已提供說明如何實作和使用元件。 这些组件随所有源代码一起提供，可以按原样使用或用作已修改或扩展的组件的起点。

### 核心元件與基礎元件 {#core-components-and-foundation-components}

有兩組Adobe提供的AEM元件可供使用：

* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)
* [基礎元件](/help/sites-authoring/default-components-foundation.md)

**核心元件** 推出AEM 6.3，提供有彈性且功能豐富的撰寫功能。 此 [We.Retail參考網站](/help/sites-developing/we-retail.md) 說明如何使用核心元件，並代表元件開發的目前最佳實務。

**基礎元件** AEM有許多版本，且在標準AEM安裝中可立即使用。 雖然仍受支援，但大部分已過時、不再增強，且以舊版技術為基礎。

>[!NOTE]
>
>[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 代表元件設計和開發的目前最佳實務，並作為參考實作。
>
>[AEM現代化工具](modernization-tools.md) 可協助移轉至核心元件。

### 查看可用组件 {#viewing-available-components}

有关 AEM 实例中的所有可用组件的概述，请使用[组件控制台](/help/sites-authoring/default-components-console.md)。

或者，您也可以使用 CRXDE Lite 获取存储库中所有可用组件的列表。

1. 在 **[!UICONTROL CRXDE Lite]** 中，从工具栏中选择&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 查询]**，这将打开&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;选项卡中，选择 `XPath` 作为&#x200B;**[!UICONTROL 类型]**。

1. 在&#x200B;**[!UICONTROL 查询]**&#x200B;输入字段中，输入以下字符串：

   `//element(*, cq:Component)`

1. 单击&#x200B;**[!UICONTROL 执行]**，这将列出组件。

## 其他資源 {#further-reading}

下列頁面提供有關開發這些和其他元件的更詳細資訊：

* [AEM元件 — 基本知識](/help/sites-developing/components-basics.md)
* [開發AEM元件](/help/sites-developing/developing-components.md)
* [開發AEM元件 — 程式碼範例](/help/sites-developing/developing-components-samples.md)
* [設定多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md)
* [开发人员模式](/help/sites-developing/developer-mode.md)
* [測試您的UI](/help/sites-developing/hobbes.md)
* [內容片段的元件](/help/sites-developing/components-content-fragments.md)
* [取得JSON格式的頁面資訊](/help/sites-developing/pageinfo.md)
* [國際化元件](/help/sites-developing/i18n.md)
* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)
* [使用隐藏条件](/help/sites-developing/hide-conditions.md)
* 经典 UI

   * [AEM Components （傳統UI）](/help/sites-developing/developing-components-classic.md)
   * [使用和擴充Widget （傳統UI）](/help/sites-developing/widgets.md)
   * [使用xtype （傳統UI）](/help/sites-developing/xtypes.md)
   * [開發Forms (Classic UI)](/help/sites-developing/developing-forms.md)
