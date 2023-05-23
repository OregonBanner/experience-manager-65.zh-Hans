---
title: ContextHub
seo-title: ContextHub
description: ContextHub是一種用於儲存、操控和呈現內容資料的架構
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub是一種用於儲存、操控和呈現內容資料的架構。 使用者端Javascript API可讓您存取個人化內容的資料。

>[!NOTE]
>
>此 [We.Retail參考實作](/help/sites-developing/we-retail.md) 實作ContextHub，並可作為將ContextHub整合至您專案時的參考。

>[!CAUTION]
>
>包含範例ContextHub設定(用於 [We.Retail參考實作](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`)僅可作為建立您自己的設定的參考。
>
>請勿在專案中作為您自己的ContextHub設定使用。

## 持續性 {#persistence}

ContextHub會儲存持續存在於使用者端上的內容資料。 ContextHub Javascript API可讓您存取存放區，以視需要建立、更新和刪除資料。 因此，ContextHub代表頁面上的資料層。

每個ContextHub存放區都是預先定義存放區型別的例項：

* ContextHub提供數種 [範例存放區型別](/help/sites-developing/ch-samplestores.md).
* 使用AEM主控台 [建立存放區](ch-configuring.md#creating-a-contexthub-store).
* 開發人員可以 [建立自訂商店型別](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* 開發人員可以 [存取存放區資料](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) 透過Javascript。

## 分段 {#segmentation}

ContextHub包含區段引擎，可管理區段並決定針對目前內容解析哪些區段。 已定義數個區段。 您可以使用Javascript API來 [決定已解析的區段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## 演示文稿 {#presentation}

此 [contexthub工具列](/help/sites-authoring/ch-previewing.md) 可讓行銷人員和作者檢視並操控存放區資料，以便在編寫頁面時模擬使用者體驗。 工具列由提供存取ContextHub存放區的UI模組群組組成。

每個ContextHub UI模組都是預先定義模組型別的例項：

* ContextHub提供數種 [範例模組型別](/help/sites-developing/ch-samplemodules.md).
* 使用AEM主控台 [新增使用者介面模組](ch-configuring.md#adding-a-ui-module)，並至 [在UI模式下將其分組](ch-configuring.md#adding-a-ui-mode).

* 開發人員可以 [建立自訂模組型別](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

開發人員需要 [將ContextHub元件新增至頁面](/help/sites-developing/ch-adding.md).
