---
title: 测试和跟踪工具
seo-title: 测试和跟踪工具
description: AEM提供了组件UI测试框架以及组件测试和调试机制
seo-description: AEM提供了组件UI测试框架以及组件测试和调试机制
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
source-wordcount: '312'
ht-degree: 0%

---

# 测试和跟踪工具{#testing-and-tracking-tools}

## 测试 {#testing}

AEM提供：

* [用于测试组件UI的框架](/help/sites-developing/hobbes.md)。
* [用于测试和调试组件的机制](/help/sites-developing/developer-mode.md)。

以下是两个开源测试工具：

**硒**

Selenium用于在每个活动有一个用户的浏览器中进行功能测试。 它将测试步骤（点击）记录为HTML表或Java类。

有关更多信息，请参阅[https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**JMeter**

JMeter用于跟踪请求，可用于功能、性能和压力测试。

有关更多信息，请参阅[https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter)。

还有许多专有工具可用于自动化测试和管理测试计划。

### 跟踪 {#tracking}

以下工具可轻松使用。 但是，在所有情况下，一个关键问题是向项目团队的所有成员（合作伙伴和客户）提供数据。

**布吉利亚**

可根据您自己的要求配置的错误跟踪系统。

**电子表格**

尽管电子表格并非特别是错误跟踪工具，但通常会&#x200B;*mis*&#x200B;用于此目的，因为它们易于理解，并且大多数用户都有使用其功能的经验。

如果用于跟踪，则：

* 应该保持简单。
* 单个电子表格的数量应保持在最低水平。
* 必须定期更新。
* 只应维护一个主控副本，每个人都应知道主控副本的位置。
* 所有项目成员都可以访问它们。
* 如果安全性是一个问题（通常发生在大公司）并且无法进行通用访问，则只要每个人都知道这些是副本，并且无法更新，就可以分发副本。

同样，还有许多专有工具可用于跟踪错误和功能要求。
