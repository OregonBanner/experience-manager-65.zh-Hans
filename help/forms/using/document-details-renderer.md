---
title: 文档呈示器的详细信息
seo-title: 文档呈示器的详细信息
description: 有关如何在AEM Forms工作区中呈现各种支持的表单和文件类型的概念性信息。
seo-description: 有关如何在AEM Forms工作区中呈现各种支持的表单和文件类型的概念性信息。
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 文档呈示器的详细信息 {#document-details-for-renderer}

## 简介 {#introduction}

在AEM Forms工作区中，可无缝支持多个表单类型。 这些 Cookie 包括：

* PDF表单（XDP / Acroform /平面PDF）
* 新HTML表单
* 图像
* 第三方应用程序（例如，通信管理）

本文档从语义自定义／组件重用的角度解释了这些呈示器的工作，这样在不中断任何再现的情况下就满足了客户要求。 虽然AEM Forms工作区允许任何用户界面／语义更改，但建议不要更改不同表单类型的渲染逻辑，否则结果可能无法预测。 此文档旨在提供指导／知识，以支持呈现相同的表单，在不同的门户中使用相同的工作区组件，而不用于修改呈现逻辑本身。

## PDF表单 {#pdf-forms}

PDF表单由渲染 `PdfTaskForm View`。

当XDP表单呈现为PDF时， `FormBridge` FormsAugmenter服务会添加JavaScript™。 此JavaScript™（在PDF表单中）有助于执行表单提交、表单保存或脱机表单等操作。

在AEM Forms工作区中，PDFTaskForm视图通过 `FormBridge`中间HTML与javascript通信 `/lc/libs/ws/libs/ws/pdf.html`。 流程是：

**PDFaskForm视图- pdf.html**

使用 `window.postMessage` / `window.attachEvent('message')`

此方法是在父帧和iframe之间进行通信的标准方式。 在添加新的PDF表单之前，将删除先前打开的PDF表单中的现有事件监听器。 此任务还考虑了“表单”选项卡和“历史记录”选项卡之间在“视图详细信息”中的切换。

**pdf.html —— 渲染`FormBridge`的PDF中的javascript**

使用 `pdfObject.postMessage` / `pdfObject.messageHandler`

此方法是与HTML中的PDF javascript进行通信的标准方式。 PdfTaskForm视图还可以处理简单的PDF并清晰地呈现它。

>[!NOTE]
>
>不建议修改PdfTaskForm视图的pdf.html/内容。

## 新的HTML表单 {#new-html-forms}

新的HTML表单由NewHTMLTaskForm视图呈现。

当使用在CRX上部署的移动表单包将XDP表单呈现为HTML时，它还会向表单添加额外的 `FormBridge` javascript，这会显示保存和提交表单数据的不同方法。

此javascript与上述PDF表单中提及的javascript不同，但用途类似。

>[!NOTE]
>
>不建议修改NewHTMLTaskForm视图的内容。

## Flex表单和指南 {#flex-forms-and-guides}

Flex表单由SwfTaskForm呈现，参考线由HtmlTaskForm视图呈现。

在AEM Forms工作区中，这些视图使用在 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

通信使用 `swfObject.postMessage` /进行 `window.flexMessageHandler`。

此协议由定义 `WsNextAdapter.swf`。 在添加新 `flexMessageHandlers`的SWF表单之前，将从先前打开的SWF表单中删除现有的on window对象。 该逻辑还考虑了任务详细信息视图中表单选项卡和历史记录选项卡之间的切换。 `WsNextAdapter.swf` 用于执行保存或提交等各种表单操作。

>[!NOTE]
>
>建议不要修改或 `WSNextAdapter.swf` 修改SwfTaskForm / HtmlTaskForm视图的内容。

## 第三方应用程序（例如，通信管理） {#third-party-applications-for-example-correspondence-management}

第三方应用程序使用ExtAppTaskForm视图呈现。

**与AEM Forms工作区通信的第三方应用程序**

AEM Forms工作区监听 `window.global.postMessage([Message],[Payload])`

[消息] 可以是指定为 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`in the `runtimeMap`. 第三方应用程序必须使用此界面根据需要通知AEM Forms工作区。 必须使用此界面，因为AEM Forms工作区必须知道提交任务时，以便它能够清除任务窗口。

**AEM Forms工作区与第三方应用程序通信**

如果AEM Forms工作区的直接操作按钮可见，则会调用该按 `window.[External-App-Name].getMessage([Action])`钮，其中[ `Action]` 从中读取 `routeActionMap`。 第三方应用程序必须侦听此界面，然后通过API通知AEM Forms工 `postMessage ()` 作区。

例如，Flex应用程序可以定义 `ExternalInterface.addCallback('getMessage', listener)` 以支持此通信。 如果第三方应用程序希望通过其自己的按钮处理表单提交，则您应指定并 `hideDirectActions = true() in the runtimeMap` 且您可以跳过此监听器。 因此，此构造是可选的。

您可以在AEM Forms工作区中的“集成对应管理”中阅读有关与 [对应管理相关的第三方应用程序集成的更多信息](/help/forms/using/integrating-correspondence-management-html-workspace.md)。
