---
title: 在AEM站点页面中嵌入自适应表单或交互式通信
seo-title: 在AEM站点页面中嵌入自适应表单或交互式通信
description: 您可以在AEM站点页面中嵌入自适应表单。 用户无需离开网站页面即可填写和提交表单。
seo-description: 您可以在AEM站点页面中嵌入自适应表单。 用户无需离开网站页面即可填写和提交表单。
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---


# 在AEM站点页面中嵌入自适应表单或交互式通信 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## 概述 {#overview}

AEM Forms允许表单开发人员将自适应表单和交互式通信无缝嵌入AEM Sites网页或AEM以外托管的网页中。 嵌入式自适应表单和交互式通信功能齐全，用户无需离开页面即可填写和提交表单。 它帮助用户保持在网页上其他元素的上下文中，同时与表单或交互式通信交互。

有关在外部网页中嵌入自适应表单的信息，请参 [阅在外部网页中嵌入自适应表单](/help/forms/using/embed-adaptive-form-external-web-page.md)。

在AEM Sites页面中，您可以使用以下方式添加自适应表单或交互式通信：

* **[AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**&#x200B;容器组件“AEM Forms”提供了可添加到网站页面的组件。 AEM Forms容器组件允许您嵌入自适应表单和交互式通信。

* **[资产浏览](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**&#x200B;器您创建的所有表单和交互式通信均位于资产下。 您可以将表单作为资产拖放到页面上。

## 前提条件 {#prerequisites}

要在AEM站点页面中嵌入使用可编辑模板的自适应表单或交互式通信，请确保AEM表单组件在关联的模板中配置为允许的组件。 有关详细信息，请参 **阅创建页面模板中的策略** 和属 [性(布局容器)部分](/help/sites-authoring/templates.md)。

如果站点页面使用静态模板，您需要在站点页面的段落系统中配置它。 请参阅[在设计模式中配置组件](/help/sites-authoring/default-components-designmode.md)，以了解更多信息。

## 嵌入自适应表单或交互式通信 {#af-component}

要使用AEM Forms容器组件嵌入自适应表单或交互式通信，请执行以下操作：

1. 在编辑模式下打开AEM站点页面，您要在其中嵌入自适应表单或交互式通信。
1. 从“组件”浏览器面板中，将AEM Forms容器组件拖放到页面上。

   或者，您也可以在资产浏览器中搜索自适应表单或交互式通信，然后将其拖放到站点页面。 它将表单嵌入在AEM Forms容器中。

   >[!NOTE]
   >
   >不支持页面上的多个AEM Forms容器组件。

1. 点按站点页面中的嵌入式AEM Forms容器组 ![件，然后点按操](assets/settings_icon.png) 作栏上settings_icon。 将打 **[!UICONTROL 开编辑AEM Forms容器]** 对话框。
1. 在“编辑AEM Forms容器”对话框中，指定以下内容。

   * **资产类型：** 选择要嵌入的资产类型。 选项包括自适应表单和交互式通信
   * **资产路径**:浏览并选择要嵌入的自适应表单或交互式通信。 如果您从资产浏览器中删除它，则会自动填充它。
   * （仅限自适应表单） **发布提交**:选择要在提交表单时触发的操作。 您可以选择显示感谢信或感谢信页面。

      * **感谢信**:使用富文本编辑器编写消息，以在提交表单时显示。 此选项仅在您选择显示感谢信时可用。
      * **感谢页面**:浏览并选择要在提交表单时显示的页面。 此选项仅在您选择显示感谢页面时可用。
      * **提交时刷新页面**:启用此项可刷新包含嵌入的自适应表单的页面以显示感谢页面。 否则，感谢页面将替换AEM Forms容器中的自适应表单，而不刷新页面。 此选项仅在您选择显示感谢页面时可用。
   * **主题**:选择一个主题，它为自适应表单或交互式通信的组件定义样式。 样式包括字体样式、背景颜色、尺寸和对齐方式等外观属性。
   * **高度**:指定容器的高度。 将其留空可自动调整容器大小。
   * **CSS客户端库**:指定CSS客户端库的路径。


1. 保存设置。 自适应表单或交互式通信现在嵌入到页面中。

## 发布嵌入式自适应表单和交互式通信 {#publishing-embedded-adaptive-form-and-interactive-communication}

让我们考虑在AEM站点页面中发布嵌入式资产（自适应表单或交互式通信）的以下情况：

* 如果您是首次发布AEM站点页面，并且页面包含嵌入的自适应表单或交互式通信，请发布站点页面和嵌入式资产。
* 如果您仅在发布的站点页面中修改了嵌入的自适应表单或交互式通信，则发布原始资产，更改将反映在发布的站点页面中。 已发布的站点页面包含对资产的引用，并且不需要重新发布页面。
* 如果您修改了站点页面以及嵌入的自适应表单或交互式通信，请重新发布站点页面和嵌入的资产。

## 修改嵌入式自适应表单和交互式通信 {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM站点页面在AEM Forms容器保留对自适应表单和交互式通信的引用。 因此，在原始自适应表单和交互式通信中配置的所有配置和属性（如主题、样式和提交操作）都保留在嵌入的自适应表单和交互式通信中。

要修改嵌入式自适应表单和交互式通信的任何配置或属性，请执行下列操作之一。

* 在自适应表单中打开原始表单或在相应编辑器中进行交互式通信，并修改它们。
* 在编辑模式下，从站点页面中点击自适应表单或交互式通信，然后 **[!UICONTROL 在新窗口中点击编辑]**。 原始表单以可修改的编辑模式打开。

>[!NOTE]
>
>原始自适应表单或交互式通信中所做的更改会自动反映在嵌入式表单中。 但是，可以重新发布自适应表单、交互式通信或站点页面，以反映已发布页面中的更改。

## Considerations and best practices {#considerations-and-best-practices}

在AEM站点页面中嵌入自适应表单时，请牢记以下几点：

* 原始表单中的页眉和页脚不包括在嵌入的表单中。
* 支持嵌入表单的用户草稿和提交内容，并可在表单门户的“草稿和已提交”Forms选项卡中看到这些内容。
* 在原始表单上配置的提交操作将保留在嵌入式表单中。
* 在原始表单上配置的体验定位和A/B测试在嵌入式表单中无效。 但是，您可以在站点页面上使用体验定位根据用户用户档案显示不同的表单。
* 如果您为原始表单配置了Adobe Analytics，将在Adobe Analytics捕获嵌入表单的分析数据。 但是，表单分析报告中不提供此功能。

