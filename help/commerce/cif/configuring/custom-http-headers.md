---
title: 自定义 HTTP 标头
description: 設定自訂HTTP標頭
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 5%

---

# 自定义 HTTP 标头 {#custom-http-headers}

## 概述 {#overview}

為了獲得對其後端的更多控制權，作者可以設定將傳送至商務引擎的自訂HTTP標頭，以及CIF已傳送的標頭。 常見的使用案例包括多商店設定，您可以在其中使用HTTP標頭控制商務後端的回應。

>[!NOTE]
>
>開發人員一律可使用GraphQL使用者端設定來設定自訂HTTP標頭。

## 配置 {#configuration}

若要設定自訂HTTP標頭，必須先定義它們。 自訂HTTP標頭必須先透過將其新增到來定義 `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` 使用OSGi設定的服務設定。

您可以在專案的「Cloud Service設定」頁面中設定HTTP標頭的值：

1. 前往「工具 — > Cloud Services -> CIF設定」中的「Cloud Service設定」頁面
1. 開啟現有設定或建立新設定
1. 前往「進階」索引標籤，尋找「自訂HTTP標頭」多欄位。 您可以選取先前定義的標頭，並為其指派值。

使用上述雲端服務設定的元件將會隨著每個GraphQL請求傳送這些HTTP標頭。

## 限制 {#restrictions}

雖然此服務允許定義任何標頭名稱，包括標準名稱，但無法用於設定。 換句話說，您無法使用此功能覆寫標準HTTP標頭。 可以找到受限制的標頭名稱清單 [此處](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). 除了這些以外，還有兩個標頭無法使用：

* &quot;Store&quot; - CIF用來識別Adobe Commerce存放區
* &quot;Preview-Version&quot; - CIF用來擷取分階段產品
