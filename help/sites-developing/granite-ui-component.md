---
title: 建立新的Granite UI欄位元件
seo-title: Creating a New Granite UI Field Component
description: Granite UI提供一系列設計用於表單的元件，稱為欄位
seo-description: Granite UI provides a range of components designed to be used in forms, called fields
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# 建立新的Granite UI欄位元件{#creating-a-new-granite-ui-field-component}

Granite UI提供一系列設計用於表單的元件；這些稱為 *欄位* 在Granite UI辭彙中。 標準Granite表單元件可在下列網址取得：

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>這些Granite UI表單欄位特別令人感興趣，因為它們用於 [元件對話方塊](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>如需欄位的完整詳細資訊，請參閱 [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

使用Granite UI Foundation架構來開發及/或擴充Granite元件。 此變數有兩個元素：

* 伺服器端：

   * 基礎元件的集合

      * 基礎 — 模組化、可組合、可分層、可重複使用
      * 元件 — Sling元件
   * 協助開發應用程式的協助程式


* 使用者端：

   * 提供一些辭彙(即HTML語言的延伸)的clientlibs集合，以透過Hypermedia導向的UI實現一般互動模式

一般Granite UI元件 `field` 由兩個感興趣的檔案組成：

* `init.jsp`：處理一般處理；標籤、說明，並提供呈現欄位時所需的表單值。
* `render.jsp`：這是執行欄位實際呈現的位置，且需要為您的自訂欄位覆寫；包含於 `init.jsp`.

請參閱 [Granite UI檔案 — 欄位](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 如果您想要更多詳細資料。

如需範例，請參閱：

* `cqgems/customizingfield/components/colorpicker`

   * 提供者： [程式碼範例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>由於此機制使用JSP，i18n和XSS不是現成可用的。 這表示您需要國際化並逸出字串。 下列目錄包含來自標準例證的類屬欄位，您可以將這些欄位作為參照：
>
>`/libs/granite/ui/components/foundation/form` 目錄

## 建立元件的伺服器端指令碼 {#creating-the-server-side-script-for-the-component}

您的自訂欄位應該只會覆寫 `render.jsp` 指令碼，您可在其中提供元件的標籤。 您可以將JSP （即轉譯指令碼）視為標籤的外包裝。

1. 建立使用 `sling:resourceSuperType` 繼承自下列專案的屬性：

   `/libs/granite/ui/components/foundation/form/field`

1. 覆寫指令碼：

   `render.jsp`

   在此指令碼中，您需要產生超媒體標籤（即包含超媒體可供使用的擴充標籤），讓使用者端知道如何與產生的元素互動。 這應該遵循Granite UI伺服器端風格的編碼。

   自訂時，您唯一的 *必須* full為讀取表單值(初始化於 `init.jsp`)從請求取得，使用：

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   如需更多詳細資訊，請參閱現成可用的Granite UI欄位的實作；例如 `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >目前JSP是慣用的指令碼編寫方法，因為在HTL中不易將資訊從一個元件傳遞至另一個元件（在表單/欄位的內容中很常見）。

## 建立元件的使用者端程式庫 {#creating-the-client-library-for-the-component}

若要將特定使用者端行為新增至元件：

1. 建立類別的clientlib `cq.authoring.dialog`.
1. 建立類別的clientlib `cq.authoring.dialog` 並定義 `JS`/ `CSS` 裡面有。

   定義您的 `JS`/ `CSS` 在clientlib內。

   >[!NOTE]
   >
   >目前，Granite UI不提供任何您可以直接用來新增JS行為的現成接聽程式或鉤點。 因此，若要將其他JS行為新增至元件，您必須實作JS連結至自訂類別，然後在標籤產生期間將其指派至元件。
