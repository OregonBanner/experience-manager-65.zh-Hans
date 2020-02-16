---
title: 测试和跟踪工具
seo-title: 测试和跟踪工具
description: AEM为测试组件UI提供了一个框架，并为测试和调试组件提供了一个机制
seo-description: AEM为测试组件UI提供了一个框架，并为测试和调试组件提供了一个机制
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 测试和跟踪工具{#testing-and-tracking-tools}

## 测试 {#testing}

AEM提供：

* [用于测试组件UI的框架](/help/sites-developing/hobbes.md)。
* [用于测试和调试组件的机制](/help/sites-developing/developer-mode.md)。

以下是两个开放源代码测试工具：

**硒**

Selenium用于在每个活动有一个用户的浏览器中进行功能测试。 它将测试步骤（单击）记录为HTML表或Java类。

有关详细信息，请参 [阅https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**JMeter**

JMeter用于跟踪请求，可用于功能、性能和压力测试。

有关详细信息，请参 [阅https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter)。

还有许多用于自动化测试和管理测试计划的专有工具。

### 跟踪 {#tracking}

可轻松使用以下工具。 但是，在所有情况下，一个关键问题是项目团队的所有成员（合作伙伴和客户）都可以获得数据。

**Bugzilla**

可根据您自己的要求配置的错误跟踪系统。

**电子表格**

尽管电子表格并非特别是错误跟踪工具，但 **&#x200B;它们经常被误用于此目的，因为它们易于理解，并且大多数用户都有其功能经验。

如果这些用于跟踪，则：

* 应该保持简单。
* 个别电子表格的数量应保持在最低限度。
* 它们必须定期更新。
* 只应维护一个主副本，并且每个人都应知道主副本的位置。
* 所有项目成员都应可访问这些资源。
* 如果安全性是问题（通常发生在大公司），并且无法进行通用访问，则只要每个人都知道这些是副本，并且无法更新，就可以分发副本。

同样，还有许多用于跟踪错误和功能要求的专有工具。
