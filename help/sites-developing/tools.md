---
title: 测试和跟踪工具
seo-title: Testing and Tracking Tools
description: AEM提供了用于测试组件UI的框架和用于测试和调试组件的机制
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# 测试和跟踪工具{#testing-and-tracking-tools}

## 测试 {#testing}

AEM 提供：

* [用于测试组件UI的框架](/help/sites-developing/hobbes.md).
* [用于测试和调试组件的机制](/help/sites-developing/developer-mode.md).

以下是两个开源测试工具：

**硒元素**

Selenium用于在浏览器中测试功能，每个活动有一个用户。 它将测试步骤（单击次数）记录为HTML表或Java类。

有关详细信息，请参阅 [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMet**

JMeter用于跟踪请求，并可用于功能、性能和压力测试。

有关详细信息，请参阅 [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

还有许多用于自动化测试和管理测试计划的专有工具。

### 跟踪 {#tracking}

以下工具可轻松使用。 但是，在所有情况下，关键问题是向项目团队的所有成员（合作伙伴和客户）提供数据。

**Bugzilla**

可以根据自己的要求配置的错误跟踪系统。

**电子表格**

虽然不是专门用于错误跟踪的工具，但电子表格通常 *mis*&#x200B;用于此目的，因为它们易于理解，并且大多数用户都对其功能具有体验。

如果这些内容用于跟踪，则：

* 它们应该保持简单。
* 应尽量减少单个电子表格的数量。
* 它们必须定期更新。
* 只应维护一个主控副本，每个人都应知道主控副本的位置。
* 它们应可供所有项目成员访问。
* 如果安全性是一个问题（通常发生在大公司）并且无法进行通用访问，那么只要每个人都知道这些是副本并且不能更新，就可以分发副本。

同样，还有许多用于跟踪错误和功能要求的专有工具。
