---
title: 扩展事件跟踪
seo-title: 扩展事件跟踪
description: AEM Analytics允许您跟踪网站上的用户交互
seo-description: AEM Analytics允许您跟踪网站上的用户交互
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 扩展事件跟踪{#extending-event-tracking}

AEM Analytics允许您跟踪网站上的用户交互。 作为开发人员，您可能需要：

* 跟踪访客如何与您的组件交互。 这可以通过自定义事 [件完成。](#custom-events)
* [访问ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [添加记录回调](#adding-record-callbacks)。

>[!NOTE]
>
>这些信息基本上是通用的，但它使用 [Adobe Analytics](/help/sites-administering/adobeanalytics.md) 作为特定示例。
>
>有关开发组件和对话框的一般信息，请参阅开 [发组件](/help/sites-developing/components.md)。

## 自定义事件 {#custom-events}

自定义事件跟踪任何依赖于页面上特定组件可用性的内容。 这还包括特定于模板的事件，因为页面组件被视为另一个组件。

### 页面加载时跟踪自定义事件 {#tracking-custom-events-on-page-load}

这可以使用伪属性(旧记录属 `data-tracking` 性仍受支持以实现向后兼容性)来完成。 可以将其添加到任何HTML标记。

的语 `data-tracking` 法

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

您可以将任意数量的键值对作为第二个参数传递，该参数称为“有效负荷”。

示例如下：

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

在页面加载时， `data-tracking` 将收集所有属性并将其添加到ContextHub的事件存储区，在该存储区，这些属性可以映射到Adobe Analytics事件。 Adobe Analytics不会跟踪未映射的事件。 有关映 [射事件的更多详细信息](/help/sites-administering/adobeanalytics.md) ，请参阅连接到Adobe Analytics。

### 页面加载后跟踪自定义事件 {#tracking-custom-events-after-page-load}

要跟踪加载页面后发生的事件（如用户交互），请使用 `CQ_Analytics.record` JavaScript函数：

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

位置

* `events` 是字符串或字符串数组（对于多个事件）。

* `values` 包含所有要跟踪的值
* `collect` 是可选的，它将返回一个包含事件和数据对象的数组。
* `options` 是可选的，并包含HTML元素和等链接跟 `obj` 踪选项 ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`。

* `componentPath` 是必需的属性，建议将其设置为 `<%=resource.getResourceType()%>`

例如，在以下定义中，用户单击“跳转 **到顶部** ”链接将触发两个事件 `jumptop` , `headlineclick`并且：

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## 在ContextHub中访问值 {#accessing-values-in-the-contexthub}

ContextHub javaScript API具有一个函数， `getStore(name)` 可返回指定的存储（如果可用）。 存储具有返 `getItem(key)` 回指定键值（如果可用）的函数。 使用该 `getKeys()` 函数，可检索为特定存储定义的键的数组。

通过使用函数绑定函数，可以通知您存储上的值变 `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` 化。

获得ContextHub初始可用性通知的最佳方式是使用该函 `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` 数。

**ContextHub的其他事件：**

所有商店都准备好：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

特定于商店：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>另请参阅完整的 [ContextHub API参考](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## 添加记录回调 {#adding-record-callbacks}

使用函数和注册回调之前和之 `CQ_Analytics.registerBeforeCallback(callback,rank)` 后 `CQ_Analytics.registerAfterCallback(callback,rank)`。

两个函数都将函数作为第一个参数，将秩作为第二个参数，这表示执行回呼的顺序。

如果回调返回false，则不执行执行链中后面的回调。
