---
title: 呈现器的文档详细信息
seo-title: 呈现器的文档详细信息
description: 关于如何在AEM Forms工作区中呈现各种支持的表单和文件类型的概念性信息。
seo-description: 关于如何在AEM Forms工作区中呈现各种支持的表单和文件类型的概念性信息。
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# 呈现器的文档详细信息 {#document-details-for-renderer}

## 简介 {#introduction}

在AEM Forms工作区中，可以无缝支持多个表单类型。 这些 Cookie 包括：

* PDF forms语（XDP/Acroform/平面PDF）
* 新的HTML表单
* 图像
* 第三方应用程序（例如，通信管理）

本文档从语义自定义／组件重用的角度解释了这些呈示器的工作，这样客户需求就得到满足，而不会中断任何再现。 尽管AEM Forms工作区允许任何用户界面／语义更改，但建议不要更改不同表单类型的呈现逻辑，否则结果可能不可预知。 此文档旨在提供指导／知识，以支持渲染相同的表单，在不同的门户中使用相同的工作区组件，而不是修改渲染逻辑本身。

## PDF forms {#pdf-forms}

PDF forms由呈现 `PdfTaskForm View`。

当XDP表单呈现为PDF时，FormsAugmenter `FormBridge` 服务会添加一个JavaScript™。 此JavaScript™（在PDF表单中）有助于执行表单提交、表单保存或脱机表单等操作。

在AEM Forms工作区中，PDFTaskForm视图通 `FormBridge`过中间HTML与javascript进行通信 `/lc/libs/ws/libs/ws/pdf.html`。 流程是：

**PDFTaskForm视图- pdf.html**

通过／进 `window.postMessage` 行通信 `window.attachEvent('message')`

此方法是父帧与iframe之间的标准通信方式。 在添加新事件之前，将删除先前打开的PDF forms的现有监听器。 此任务还会考虑在“表单”选项卡和“历史记录”选项卡之间切换的视图详细信息。

**pdf.html —— 渲染`FormBridge`的PDF中的javascript**

通过／进 `pdfObject.postMessage` 行通信 `pdfObject.messageHandler`

此方法是从HTML与PDFJavaScript进行通信的标准方式。 PdfTaskForm视图还可以处理简单的PDF并清晰地呈现它。

>[!NOTE]
>
>不建议修改PdfTaskForm视图的pdf.html/内容。

## 新HTMLForms {#new-html-forms}

新的HTML表单由NewHTMLTaskForm视图呈现。

当使用在CRX上部署的移动表单包将XDP表单呈现为HTML时，它还会向表单中添加其他 `FormBridge`JavaScript，它显示保存和提交表单数据的不同方法。

此JavaScript与上述PDF forms中所述的JavaScript不同，但用途类似。

>[!NOTE]
>
>不建议修改NewHTMLTaskForm视图的内容。

## Flex·Forms与指南 {#flex-forms-and-guides}

Flex·Forms由SwfTaskForm呈现，而指南由HtmlTaskForm视图呈现。

在AEM Forms工作区中，这些视图使用介质SWF与构成flex表单／指南的实际SWF进行通信， `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

通信使用/ `swfObject.postMessage` 进行 `window.flexMessageHandler`。

此协议由定义 `WsNextAdapter.swf`。 在添加 `flexMessageHandlers`新SWF表单之前，会删除先前打开的SWF表单中现有的on窗口对象。 该逻辑还考虑在任务详细信息视图中表单选项卡和历史记录选项卡之间的切换。 `WsNextAdapter.swf` 用于执行保存或提交等各种表单操作。

>[!NOTE]
>
>建议不要修改SwfTaskForm `WSNextAdapter.swf` /HtmlTaskForm视图或其内容。

## 第三方应用程序（例如，通信管理） {#third-party-applications-for-example-correspondence-management}

第三方应用程序使用ExtAppTaskForm视图呈现。

**第三方在AEM Forms工作区通信中的应用**

AEM Forms工作区监听 `window.global.postMessage([Message],[Payload])`

[消息] 可以是指定为 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`在 `runtimeMap`中 第三方应用程序必须使用此界面根据需要通知AEM Forms工作区。 必须使用此界面，因为AEM Forms工作区必须知道提交任务时，它才能清除任务窗口。

**AEM Forms工作区与第三方应用程序通信**

如果AEM Forms工作区的直接操作按钮可见，则它将调 `window.[External-App-Name].getMessage([Action])`用，从中 `[Action]` 读取的位置 `routeActionMap`。 第三方应用程序必须监听此界面，然后通过API通知AEM Forms工 `postMessage ()` 作区。

例如，Flex应用程序可以定 `ExternalInterface.addCallback('getMessage', listener)` 义支持此通信。 如果第三方应用程序希望通过其自己的按钮处理表单提交，则您应指 `hideDirectActions = true() in the runtimeMap` 定并可跳过此监听器。 因此，此构造是可选的。

您可以在AEM Forms工作区的“集成通信管理”中阅读有关通信管理的第 [三方应用程序集成的更多信息](/help/forms/using/integrating-correspondence-management-html-workspace.md)。
