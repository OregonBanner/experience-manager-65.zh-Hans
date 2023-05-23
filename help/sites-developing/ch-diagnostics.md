---
title: ContextHub 诊断
seo-title: ContextHub Diagnostics
description: ContextHub提供診斷頁面，您可在其中檢視ContextHub架構的概觀
seo-description: ContextHub provides a diagnostics page where you can see an overview of the ContextHub framework
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: b833c28b-76c6-42a2-b690-3e81ddf91bc2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# ContextHub 诊断 {#contexthub-diagnostics}

ContextHub提供診斷頁面，您可在其中檢視ContextHub架構的概觀。 若要開啟頁面，請前往 `contexthub.diagnostics.html` AEM編寫執行個體的頁面，例如：

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

「ContextHub診斷」頁面提供有關已建立的存放區和UI模組、已載入的使用者端程式庫資料夾，以及實用頁面的連結的資訊。

>[!NOTE]
>
>為了傳回診斷資訊，必須啟用偵錯模式，否則診斷頁面將為空白。 請參閱 [本檔案](ch-configuring.md#debugging-contexthub) 以取得如何啟用偵錯模式的詳細資訊。

>[!NOTE]
>
>對於ContextHub設定，仍位於其舊有路徑下，診斷頁面的位置為 `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## 商店 {#stores}

存放區區段會列出所有已設定的ContextHub存放區。 清單中的每個專案都包含下列資訊：

* **標題：** 此 [存放區型別](/help/sites-developing/ch-samplestores.md) 存放區所根據的。
* **路徑：** 存放設定的存放庫節點的路徑。
* **resourceType：** 定義存放區型別的存放庫節點的路徑。
* **clientlibs：** 已載入且實作存放區型別的使用者端程式庫的類別。

## 模組 {#modules}

模組區段會列出所有已設定的ContextHub UI模組。 清單中的每個專案都包含下列資訊：

* **標題：** 此 [UI模組型別](/help/sites-developing/ch-samplemodules.md) UI模組所根據。
* **路徑：** 存放設定的存放庫節點的路徑。
* **resourceType：** 定義UI模組型別的存放庫節點的路徑。
* **clientlibs：** 已載入且實作UI模組型別的使用者端程式庫的類別。

## Clientlibs {#clientlibs}

「Clientlibs」區段會列出ContextHub已載入的所有使用者端程式庫資料夾。 使用者端程式庫會進行分類：

* **kernel.js：** 實作ContextHub架構、區段引擎和存放區型別的使用者端資料庫。
* **ui.js：** 實作ContextHub UI和UI模組型別的使用者端程式庫。
* **style.css：** 從使用者端程式庫載入的CSS檔案。

## URL {#urls}

URL區段包含ContextHub功能的連結：

* **設定編輯器：** 開啟 [ContextHub設定頁面](ch-configuring.md) 您可以在此處設定存放區、UI模式和UI模組。

* **ContextHub模組的設定：** 開啟/etc/cloudsettings/default/contexthub.config.kernel.js檔案，其中包含ContextHub存放區設定的Javascript物件表示法。
* **ContextHub UI的設定：** 開啟/etc/cloudsettings/default/contexthub.config.ui.js檔案，其中包含ContextHub UI模式設定的Javascript物件表示法。
* **kernel.js：** 開啟/etc/cloudsettings/default/contexthub.kernel.js檔案，其中包含實作ContextHub架構、區段引擎和存放區型別的使用者端程式庫原始碼。
* **ui.js：** 開啟/etc/cloudsettings/default/contexthub.ui.js檔案，其中包含實作ContextHub UI和UI模組型別的使用者端程式庫原始碼。
* **style.css：** 開啟/etc/cloudsettings/default/contexthub.styles.css檔案，其中包含ContextHub UI和UI模組的CSS樣式。
