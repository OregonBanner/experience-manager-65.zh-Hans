---
title: 轉譯器的檔案詳細資訊
seo-title: Document details for renderer
description: 有關轉譯器如何在AEM Forms工作區中運作，以轉譯各種支援的表單和檔案型別的概念資訊。
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# 轉譯器的檔案詳細資訊 {#document-details-for-renderer}

## 简介 {#introduction}

在AEM Forms工作區中，可順暢地支援多種表單型別。 其中包括：

* PDF forms(XDP / Acroform /一般PDF)
* 新HTML表單
* 图像
* 協力廠商應用程式（例如，通訊管理）

本檔案會從語意自訂/元件重複使用的角度來說明這些轉譯器的運作方式，以便在不中斷任何轉譯的情況下滿足客戶需求。 雖然AEM Forms工作區允許任何使用者介面/語意變更，但建議您不要變更不同表單型別的轉譯邏輯，否則可能無法預測結果。 本檔案旨在提供指導/知識以支援轉譯相同的表單、在不同的入口使用相同的工作區元件，而非用於修改轉譯邏輯本身。

## PDF forms {#pdf-forms}

PDF forms轉譯者 `PdfTaskForm View`.

XDP表單轉譯為PDF時， `FormBridge` JavaScript™由FormsAugmenter服務新增。 此JavaScript™ (在PDF表單內)有助於執行表單提交、表單儲存或離線建立表單等動作。

在AEM Forms工作區中，PDFTaskForm檢視會與 `FormBridge`javascript，透過下列位置出現的中介HTML： `/lc/libs/ws/libs/ws/pdf.html`. 流程為：

**PDFTaskForm檢視 — pdf.html**

通訊方式 `window.postMessage` / `window.attachEvent('message')`

此方法為父框架與iframe之間的標準通訊方式。 在新增新的事件接聽程式之前，會先移除先前開啟的PDF forms中的現有事件接聽程式。 此永久刪除也會考量在任務詳細資料檢視中的表單標籤和歷史記錄標籤之間切換。

**pdf.html - `FormBridge`轉譯PDF內的javascript**

通訊方式 `pdfObject.postMessage` / `pdfObject.messageHandler`

此方法是從HTML與PDFJavaScript通訊的標準方式。 PdfTaskForm檢視也會處理平面PDF並簡單呈現。

>[!NOTE]
>
>不建議修改PdfTaskForm檢視的pdf.html /內容。

## 新HTMLForms {#new-html-forms}

新的HTML表單會由NewHTMLTaskForm檢視轉譯。

使用部署在CRX上的行動表單套件將XDP表單轉譯為HTML時，也會新增其他 `FormBridge`JavaScript至表單，這會顯示儲存和提交表單資料的不同方法。

此JavaScript與上述PDF forms中提到的不同，但其用途類似。

>[!NOTE]
>
>不建議修改NewHTMLTaskForm檢視的內容。

## Flex Forms與指南 {#flex-forms-and-guides}

Flex Forms會分別以SwfTaskForm和HtmlTaskForm檢視來轉譯。

在AEM Forms工作區中，這些檢視會使用下列位置出現的中介SWF與組成彈性表單/指南的實際SWF溝通 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

通訊是透過以下方式進行 `swfObject.postMessage` / `window.flexMessageHandler`.

此通訊協定由 `WsNextAdapter.swf`. 現有 `flexMessageHandlers`在視窗物件上，會先從先前開啟的SWF表單中移除，然後再新增表單。 此邏輯也會考量在任務詳細資料檢視中的表單標籤和歷史記錄標籤之間切換。 `WsNextAdapter.swf` 用於執行各種表單動作，例如儲存或提交。

>[!NOTE]
>
>不建議修改 `WSNextAdapter.swf` 或SwfTaskForm / HtmlTaskForm檢視的內容。

## 協力廠商應用程式（例如，通訊管理） {#third-party-applications-for-example-correspondence-management}

協力廠商應用程式是使用ExtAppTaskForm檢視呈現。

**AEM Forms工作區通訊的第三方應用程式**

AEM Forms工作區監聽 `window.global.postMessage([Message],[Payload])`

[訊息] 可以是字串，指定為 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`在 `runtimeMap`. 協力廠商應用程式必須使用此介面，視需要通知AEM Forms工作區。 使用此介面是強制性的，因為AEM Forms工作區必須知道何時提交任務，才能清除任務視窗。

**AEM Forms工作區與協力廠商應用程式通訊**

如果顯示AEM Forms工作區的直接動作按鈕，則會呼叫 `window.[External-App-Name].getMessage([Action])`，其中 `[Action]` 是從 `routeActionMap`. 協力廠商應用程式必須監聽此介面，然後透過通知AEM Forms工作區 `postMessage ()` API。

例如，Flex應用程式可定義 `ExternalInterface.addCallback('getMessage', listener)` 以支援此通訊。 如果協力廠商應用程式想要透過自己的按鈕處理表單提交，您應指定 `hideDirectActions = true() in the runtimeMap` 而且您可以略過此監聽器。 因此，此建構是選用的。

如需有關協力廠商應用程式整合的詳細資訊，請參閱 [在AEM Forms工作區中整合通訊管理](/help/forms/using/integrating-correspondence-management-html-workspace.md).
