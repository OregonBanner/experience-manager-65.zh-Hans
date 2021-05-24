---
title: 扩展ContextHub
seo-title: 扩展ContextHub
description: 定义新类型的ContextHub存储和模块（如果提供的存储和模块不符合您的解决方案要求）
seo-description: 定义新类型的ContextHub存储和模块（如果提供的存储和模块不符合您的解决方案要求）
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# 扩展ContextHub{#extending-contexthub}

定义新类型的ContextHub存储和模块（如果提供的存储和模块不符合您的解决方案要求）。

## 创建自定义存储候选项{#creating-custom-store-candidates}

ContextHub存储区是根据注册的存储候选区创建的。 要创建自定义存储，您需要创建并注册存储候选项。

包含创建和注册存储候选项的代码的javascript文件必须包含在[客户端库文件夹](/help/sites-developing/clientlibs.md#creating-client-library-folders)中。 文件夹的类别必须匹配以下模式：

```xml
contexthub.store.[storeType]
```

类别的`[storeType]`部分是`storeType`，该存储候选项在其中注册。 （请参阅[注册ContextHub存储候选项](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)）。 例如，对于`contexthub.mystore`的storeType，客户端库文件夹的类别必须为`contexthub.store.contexthub.mystore`。

### 创建ContextHub存储候选项{#creating-a-contexthub-store-candidate}

要创建存储候选项，请使用[`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent)函数来扩展一个基存储：

* [&#39;ContextHub.Store.PersiredStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&#39;ContextHub.Store.SessionStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&#39;ContextHub.Store.JSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&#39;ContextHub.Store.PersiredJSONPStore&#39;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

请注意，每个基本存储扩展了[`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core)存储。

以下示例创建`ContextHub.Store.PersistedStore`存储候选项的最简单扩展：

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

实际上，您的自定义商店候选者将定义其他函数或覆盖商店的初始配置。 [示例存储候选项](/help/sites-developing/ch-samplestores.md)安装在`/libs/granite/contexthub/components/stores`下的存储库中。 要从这些示例中学习，请使用CRXDE Lite打开Javascript文件。

### 注册ContextHub存储候选项{#registering-a-contexthub-store-candidate}

注册存储候选项以将其与ContextHub框架集成，并允许从中创建存储。 要注册存储候选项，请使用`ContextHub.Utils.storeCandidates`类的[`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)函数。

注册存储候选项时，将提供存储类型的名称。 从候选项创建存储时，使用存储类型来标识其所基于的候选项。

注册商店候选项时，需指明其优先级。 当使用与已注册的存储候选者相同的存储类型注册存储候选者时，使用具有较高优先级的候选者。 因此，您可以使用新实施来覆盖现有的存储候选项。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

在大多数情况下，只需要一个候选项，并且优先级可以设置为`0`，但如果您感兴趣，您可以了解有关[更高级注册的信息，](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)，该信息允许根据javascript条件(`applies`)和候选优先级选择少数存储实施之一。

## 创建ContextHub UI模块类型{#creating-contexthub-ui-module-types}

如果随ContextHub](/help/sites-developing/ch-samplemodules.md)一起安装的[模块类型不符合您的要求，请创建自定义UI模块类型。 要创建UI模块类型，请通过扩展`ContextHub.UI.BaseModuleRenderer`类，然后将其注册到`ContextHub.UI`来创建新的UI模块渲染器。

要创建UI模块渲染器，请创建一个`Class`对象，该对象包含渲染UI模块的逻辑。 类必须至少执行以下操作：

* 扩展`ContextHub.UI.BaseModuleRenderer`类。 此类是所有UI模块渲染器的基本实现。 `Class`对象定义名为`extend`的属性，该属性用于将此类命名为正在扩展的类。

* 提供默认配置。 创建`defaultConfig`属性。 此属性是一个对象，其中包含为[`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI模块定义的属性以及您需要的任何其他属性。

`ContextHub.UI.BaseModuleRenderer`的源位于/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js。  要注册渲染器，请使用`ContextHub.UI`类的[`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender)方法。 您需要提供模块类型的名称。 当管理员基于此呈现器创建UI模块时，他们会指定此名称。

在自执行的匿名函数中创建并注册渲染器类。 以下示例基于contexthub.browserinfo UI模块的源代码。 此UI模块是`ContextHub.UI.BaseModuleRenderer`类的简单扩展。

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

包含创建和注册渲染器的代码的javascript文件必须包含在[客户端库文件夹](/help/sites-developing/clientlibs.md#creating-client-library-folders)中。 文件夹的类别必须匹配以下模式：

```xml
contexthub.module.[moduleType]
```

类别的`[moduleType]`部分是用于注册模块渲染器的`moduleType`。 例如，对于`contexthub.browserinfo`的`moduleType`，客户端库文件夹的类别必须为`contexthub.module.contexthub.browserinfo`。
