---
title: 扩展ContextHub
seo-title: 扩展ContextHub
description: 当提供的ContextHub存储和模块不符合您的解决方案要求时，定义新的ContextHub存储和模块类型
seo-description: 当提供的ContextHub存储和模块不符合您的解决方案要求时，定义新的ContextHub存储和模块类型
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
translation-type: tm+mt
source-git-commit: ed34f2200f4ff4f407f7b92165685af390f5f7e3

---


# 扩展ContextHub{#extending-contexthub}

当提供的ContextHub存储和模块不符合您的解决方案要求时，定义新的ContextHub存储和模块类型。

## 创建自定义商店候选 {#creating-custom-store-candidates}

ContextHub存储区是从注册存储候选区创建的。 要创建自定义商店，您需要创建和注册商店候选。

包含创建和注册存储候选项的代码的javascript文件必须包含在客户端库 [文件夹中](/help/sites-developing/clientlibs.md#creating-client-library-folders)。 文件夹的类别必须与以下模式匹配：

```xml
contexthub.store.[storeType]
```

类别 `[storeType]` 的一部分是注册商 `storeType` 店候选人的部分。 (请参 [阅注册ContextHub存储候选项](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate))。 例如，对于storeType，客 `contexthub.mystore`户端库文件夹的类别必须是 `contexthub.store.contexthub.mystore`。

### 创建ContextHub Store Candidate {#creating-a-contexthub-store-candidate}

要创建商店候选，请使用该函 [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 数扩展其中一个基本商店：

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

请注意，每个基本存储都扩展 [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) 存储。

以下示例创建了存储候选项的最 `ContextHub.Store.PersistedStore` 简单扩展：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

实际上，您的自定义商店候选者将定义其他函数或覆盖商店的初始配置。 以下 [存储库中安装了多个](/help/sites-developing/ch-samplestores.md) “候选存储”示例 `/libs/granite/contexthub/components/stores`。 要从这些范例中学习，请使用CRXDE Lite打开javascript文件。

### 注册ContextHub Store Candidate {#registering-a-contexthub-store-candidate}

注册一个存储候选项以将其与ContextHub框架集成，并允许从该框架创建存储。 要注册存储候选项，请使 [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) 用类的函 `ContextHub.Utils.storeCandidates` 数。

在注册商店候选者时，您需要提供商店类型的名称。 在从候选者创建商店时，可以使用商店类型来标识其所基于的候选者。

注册商店候选者时，您会指示其优先级。 当使用与已注册的存储候选者相同的存储类型来注册存储候选者时，使用具有较高优先级的候选者。 因此，您可以使用新的实施来覆盖现有存储候选。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多数情况下，只有一个候选者是必需的，并且优先级可以设置为 `0`，但如果您感兴趣，您可以了解更多高级注册，这允许根据javascript条件( [](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)`applies`)和候选优先级选择少数存储实现之一。

## 创建ContextHub UI模块类型 {#creating-contexthub-ui-module-types}

当随ContextHub一起安装的UI模块类 [型不符合您的要求时](/help/sites-developing/ch-samplemodules.md) ，创建自定义UI模块类型。 要创建UI模块类型，请通过扩展类然后向注册来创建新的UI `ContextHub.UI.BaseModuleRenderer` 模块渲染器 `ContextHub.UI`。

要创建UI模块渲染器，请创建一 `Class` 个对象，其中包含呈现UI模块的逻辑。 至少，您的班必须执行以下操作：

* 扩展 `ContextHub.UI.BaseModuleRenderer` 类。 该类是所有UI模块渲染器的基本实现。 该对 `Class` 象定义一个名为的属 `extend` 性，您可以使用该属性将该类命名为扩展类。

* 提供默认配置。 创建属 `defaultConfig` 性。 此属性是一个对象，其中包括为 [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模块定义的属性以及您需要的任何其他属性。

源位 `ContextHub.UI.BaseModuleRenderer` 于/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。  要注册呈示器，请使 [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) 用类的方 `ContextHub.UI` 法。 您需要为模块类型提供名称。 管理员根据此呈示器创建UI模块时，会指定此名称。

在自执行匿名函数中创建并注册呈示器类。 以下示例基于contexthub.browserinfo UI模块的源代码。 此UI模块是类的简单扩 `ContextHub.UI.BaseModuleRenderer` 展。

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

包含创建和注册呈示器的代码的javascript文件必须包含在客户端库 [文件夹中](/help/sites-developing/clientlibs.md#creating-client-library-folders)。 文件夹的类别必须与以下模式匹配：

```xml
contexthub.module.[moduleType]
```

类别 `[moduleType]` 的一部分是用于注册模 `moduleType` 块渲染器的部分。 例如，对于 `moduleType` ，客 `contexthub.browserinfo`户端库文件夹的类别必须是 `contexthub.module.contexthub.browserinfo`。
