---
title: 扩展 ContextHub
seo-title: Extending ContextHub
description: 定義新型別的ContextHub存放區和模組，如果提供的儲存區和模組不符合您的解決方案需求
seo-description: Define new types of ContextHub stores and modules when the ones provided do not meet your solution requirements
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# 扩展 ContextHub{#extending-contexthub}

定義新型別的ContextHub存放區和模組，如果提供的儲存區和模組不符合您的解決方案需求。

## 建立自訂商店候選者 {#creating-custom-store-candidates}

ContextHub存放區是從已註冊的存放區候選項中建立的。 若要建立自訂商店，您需要建立並註冊商店候選商店。

包含建立及註冊候選商店之程式碼的javascript檔案必須包含在 [使用者端資料庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders). 資料夾的類別必須符合以下模式：

```xml
contexthub.store.[storeType]
```

此 `[storeType]` 類別的一部分為 `storeType` 存放區候選者註冊所在的區域。 (請參閱 [註冊ContextHub存放區候選者](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate))。 例如，若為storeType `contexthub.mystore`，使用者端程式庫資料夾的類別必須是 `contexthub.store.contexthub.mystore`.

### 建立ContextHub存放區候選專案 {#creating-a-contexthub-store-candidate}

若要建立候選商店，請使用 [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 擴充其中一個基礎存放區的函式：

* [&#39;ContextHub.Store.PersistedStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PersistedJSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

請注意，每個基礎存放區都會擴充 [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) 商店。

下列範例會建立 `ContextHub.Store.PersistedStore` 存放區候選者：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

實際上，您的自訂商店候選者將定義其他功能或覆寫商店的初始設定。 數個 [範例商店候選者](/help/sites-developing/ch-samplestores.md) 會安裝在以下的存放庫中 `/libs/granite/contexthub/components/stores`. 若要瞭解這些範例的內容，請使用CRXDE Lite開啟Javascript檔案。

### 註冊ContextHub存放區候選者 {#registering-a-contexthub-store-candidate}

註冊存放區候選項，以將其與ContextHub架構整合，並允許從中建立存放區。 若要註冊候選商店，請使用 [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 的功能 `ContextHub.Utils.storeCandidates` 類別。

註冊候選商店時，需提供商店型別的名稱。 從候選者建立存放區時，您可以使用存放區型別來識別它所依據的候選者。

註冊候選商店時，需指定其優先順序。 當使用與已註冊商店候選相同的商店型別註冊商店候選時，會使用具有較高優先順序的候選商店。 因此，您可以使用新的實作來覆寫現有的商店候選者。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多數情況下，只需要一個候選者，而且優先順序可以設定為 `0`，但如果您有興趣，可瞭解 [更進階的註冊，](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 可讓您根據javascript條件(`applies`)和候選者優先順序。

## 建立ContextHub UI模組型別 {#creating-contexthub-ui-module-types}

建立自訂UI模組型別，如果 [與ContextHub一起安裝](/help/sites-developing/ch-samplemodules.md) 不符合您的需求。 若要建立UI模組型別，請擴充以下擴充功能以建立新的UI模組轉譯器： `ContextHub.UI.BaseModuleRenderer` 類別，然後將其註冊至 `ContextHub.UI`.

若要建立UI模組化轉譯器，請建立 `Class` 包含轉譯UI模組之邏輯的物件。 您的類別至少必須執行下列動作：

* 擴充 `ContextHub.UI.BaseModuleRenderer` 類別。 此類別是所有UI模組轉譯器的基本實作。 此 `Class` 物件會定義名為的屬性 `extend` 用來將這個類別命名為要擴充的類別。

* 提供預設設定。 建立 `defaultConfig` 屬性。 此屬性是一個物件，其中包含為定義的屬性 [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模組，以及您需要的任何其他屬性。

的來源 `ContextHub.UI.BaseModuleRenderer` 位於/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。  若要註冊轉譯器，請使用 [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 方法 `ContextHub.UI` 類別。 您必須提供模組型別的名稱。 管理員根據此轉譯器建立UI模組時，會指定此名稱。

在自動執行的匿名函式中建立並註冊轉譯器類別。 以下範例是根據contexthub.browserinfo UI模組的原始碼。 此UI模組是 `ContextHub.UI.BaseModuleRenderer` 類別。

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

包含建立及註冊轉譯器之程式碼的javascript檔案必須包含在 [使用者端資料庫資料夾](/help/sites-developing/clientlibs.md#creating-client-library-folders). 資料夾的類別必須符合以下模式：

```xml
contexthub.module.[moduleType]
```

此 `[moduleType]` 類別的一部分為 `moduleType` 模組轉譯器註冊所在的區域。 例如，對於 `moduleType` 之 `contexthub.browserinfo`，使用者端程式庫資料夾的類別必須是 `contexthub.module.contexthub.browserinfo`.
