---
title: 呈现器的文档详细信息
description: 有关渲染如何在AEM Forms工作区中用于渲染各种受支持表单和文件类型的概念信息。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 呈现器的文档详细信息 {#document-details-for-renderer}

## 简介 {#introduction}

在AEM Forms工作区中，无缝支持多种表单类型。 其中包括：

* PDF forms(XDP/Acroform/平面PDF)
* 新HTML表单
* 图像
* 第三方应用程序（例如，通信管理）

本文档从语义定制/组件重用的角度解释这些呈现器的工作，以便在不中断任何呈现的情况下满足客户需求。 虽然AEM Forms工作区允许进行任何用户界面/语义更改，但建议不更改各种表单类型的渲染逻辑，否则结果可能是不可预测的。 本文档旨在提供指导/知识以支持呈现相同的表单、在不同门户中使用相同的工作区组件，而不是用于修改呈现逻辑本身。

## PDF forms {#pdf-forms}

PDF forms呈现方式 `PdfTaskForm View`.

当XDP表单呈现为PDF时， `FormBridge` JavaScript™由FormsAugmenter服务添加。 此JavaScript™(在PDF表单内)有助于执行表单提交、表单保存或离线表单等操作。

在AEM Forms工作区中，PDFTaskForm视图与 `FormBridge`JavaScript，通过位于以下位置的中间HTML `/lc/libs/ws/libs/ws/pdf.html`. 其流程为：

**PDFTaskForm视图 — pdf.html**

通信使用 `window.postMessage` / `window.attachEvent('message')`

此方法是父帧和iframe之间的标准通信方式。 在添加新事件侦听器之前，将删除以前打开的PDF forms中的现有事件侦听器。 此清除还会考虑在任务详细信息视图中的表单选项卡和历史记录选项卡之间进行切换。

**pdf.html - `FormBridge`渲染PDF中的JavaScript**

通信使用 `pdfObject.postMessage` / `pdfObject.messageHandler`

此方法是HTML与PDFJavaScript进行通信的标准方式。 PdfTaskForm视图还会处理平面PDF并将其呈现。

>[!NOTE]
>
>不建议编辑PdfTaskForm视图的pdf.html /内容。

## 新HTMLForms {#new-html-forms}

新的HTML表单由NewHTMLTaskForm视图渲染。

当使用在CRX上部署的移动表单包将XDP表单呈现为HTML时，它还会添加其他 `FormBridge`表单的JavaScript，这会公开不同的表单数据保存和提交方法。

此JavaScript与上述PDF forms中引用的不同，但其用途类似。

>[!NOTE]
>
>Adobe不建议编辑NewHTMLTaskForm视图的内容。

## Flex Forms和指南 {#flex-forms-and-guides}

Flex Forms由SwfTaskForm渲染，参考线由HtmlTaskForm视图渲染。

在AEM Forms Workspace中，这些视图使用位于以下位置的中间SWF与构成Flex®表单/指南的实际SWF进行通信 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

通信是通过以下方式进行的 `swfObject.postMessage` / `window.flexMessageHandler`.

此协议由 `WsNextAdapter.swf`. 现有 `flexMessageHandlers`在窗口对象上，会先从以前打开的SWF表单中删除表单，然后再添加新表单。 该逻辑还会考虑在任务详细信息视图中的表单选项卡和历史记录选项卡之间进行切换。 此 `WsNextAdapter.swf` 用于执行各种表单操作，如保存或提交。

>[!NOTE]
>
>建议不要修改 `WSNextAdapter.swf` 或SwfTaskForm / HtmlTaskForm视图的内容。

## 第三方应用程序（例如，通信管理） {#third-party-applications-for-example-correspondence-management}

使用ExtAppTaskForm视图呈现第三方应用程序。

**第三方应用程序到AEM Forms工作区通信**

AEM Forms工作区侦听 `window.global.postMessage([Message],[Payload])`

[消息] 可以是指定为 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`在 `runtimeMap`. 第三方应用程序必须使用此界面来根据需要通知AEM Forms工作区。 必须使用此界面，因为AEM Forms工作区必须知道在提交任务时，它才能清除任务窗口。

**AEM Forms工作区到第三方应用程序通信**

如果AEM Forms工作区的直接操作按钮可见，则会调用 `window.[External-App-Name].getMessage([Action])`，其中 `[Action]` 是从 `routeActionMap`. 第三方应用程序必须侦听此界面，然后通过通知AEM Forms工作区 `postMessage ()` API。

例如，Flex应用程序可以定义 `ExternalInterface.addCallback('getMessage', listener)` 以支持此通信。 如果第三方应用程序希望通过自己的按钮处理表单提交，则应指定 `hideDirectActions = true() in the runtimeMap` 您可以跳过此侦听器。 因此，此结构是可选的。

有关与通信管理相关的第三方应用程序集成的更多信息，请参阅 [在AEM Forms工作区中集成通信管理](/help/forms/using/integrating-correspondence-management-html-workspace.md).
