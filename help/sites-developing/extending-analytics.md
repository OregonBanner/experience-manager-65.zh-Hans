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
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# 扩展事件跟踪{#extending-event-tracking}

AEM Analytics允许您跟踪网站上的用户交互。 作为开发人员，您可能需要：

* 跟踪访客与组件的交互方式。 这可以通过[自定义事件完成。](#custom-events)
* [访问ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [添加记录回调](#adding-record-callbacks)。

>[!NOTE]
>
>此信息基本上是通用的，但对于特定示例，它使用[Adobe Analytics](/help/sites-administering/adobeanalytics.md)。
>
>有关开发组件和对话框的一般信息，请参阅[开发组件](/help/sites-developing/components.md)。

## 自定义事件{#custom-events}

自定义事件跟踪任何依赖于页面上特定组件可用性的内容。 这还包括特定于模板的事件，因为页面组件被视为另一个组件。

### 跟踪页面加载时的自定义事件{#tracking-custom-events-on-page-load}

这可以使用伪属性`data-tracking`（旧记录属性仍受支持，以实现向后兼容）来完成。 可以将其添加到任何HTML标记。

`data-tracking`的语法为

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

您可以将任意数量的键值对作为第二个参数（称为有效负荷）进行传递。

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

在页面加载时，将收集所有`data-tracking`属性并将其添加到ContextHub的事件存储中，在该存储中，这些属性可以映射到Adobe Analytics事件。 未映射的事件将不会被Adobe Analytics跟踪。 有关映射事件的详细信息，请参阅[连接到Adobe Analytics](/help/sites-administering/adobeanalytics.md)。

### 页面加载后跟踪自定义事件{#tracking-custom-events-after-page-load}

要跟踪载入页面后发生的事件（如用户交互），请使用`CQ_Analytics.record` JavaScript函数：

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

位置

* `events` 是字符串或字符串数组(对于多个事件)。

* `values` 包含要跟踪的所有值
* `collect` 是可选的，将返回包含事件和数据对象的数组。
* `options` 是可选的，包含HTML元素和等链接跟 `obj` 踪选项 ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`。

* `componentPath` 是必需的属性，建议将其设置为  `<%=resource.getResourceType()%>`

例如，使用以下定义，用户单击&#x200B;**跳转到顶部**&#x200B;链接将触发两个事件`jumptop`和`headlineclick`:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## 访问ContextHub {#accessing-values-in-the-contexthub}中的值

ContextHub JavaScript API具有`getStore(name)`函数，该函数返回指定的存储（如果可用）。 存储具有`getItem(key)`函数，该函数返回指定密钥的值（如果可用）。 使用`getKeys()`函数，可以检索为特定存储定义的键的数组。

可以通过使用`ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`函数绑定函数来通知存储上的值更改。

获得ContextHub初始可用性通知的最佳方法是使用`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`函数。

**ContextHub的其他事件:**

所有商店都准备就绪：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

特定于存储：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>另请参见完整的[ContextHub API Reference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## 添加记录回调{#adding-record-callbacks}

使用函数`CQ_Analytics.registerBeforeCallback(callback,rank)`和`CQ_Analytics.registerAfterCallback(callback,rank)`注册回呼之前和之后。

这两个函数都将函数作为第一个参数，将秩作为第二个参数，这表示执行回呼的顺序。

如果回调返回false，则不执行执行链中后面的回调。
