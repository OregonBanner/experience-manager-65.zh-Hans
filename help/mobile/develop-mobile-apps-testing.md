---
title: 测试移动应用程序
description: 了解如何使用各种工具自动或手动测试您的移动应用程序。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
exl-id: e10e1904-7016-4eb0-9408-36297285f378
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# 测试移动应用程序{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

鉴于市场上有各种各样的设备和正在发布的设备，测试您的应用程序已变得势在必行。 在这个领域，功能和可用性可能会在应用商店中获得较低的评价，但一个缺陷可能会导致卸载您的应用程序。 测试计划和质量保证必须引起注意。 以下链接涵盖了必须一般解决的许多主题，例如识别您的环境、定义测试案例、测试类型、假设以及客户参与。 此外，还讨论了有助于测试工作的工具。 内部工具，如 [霍布斯](/help/sites-developing/hobbes.md)可帮助进行基于Web的UI测试。 [艰难的一天](/help/sites-developing/tough-day.md) 可以用模拟载荷来强调实例。 如果您的测试环境已经具有第三方工具（如Selenium）的经验，也可以使用这些工具。

在开发移动应用程序时，有许多特定于设备的新问题，必须与传统测试一起解决。

* 功能 — 您的应用程序是否满足所有要求？
* 可用性 — 应用程序是否易于使用且便于客户理解？
* 性能 — 在使用量激增期间会发生什么？ 应用程序元素（例如轻扫和轮播）是否非常快速，并且不会破坏体验？
* 失败或中断 — 当应用程序运行时有来电或通知时，会发生什么情况？ 如果网络中断或断电会发生什么情况？
* 安装和更新 — 安装体验如何？ 如何推送更新？
* 技术 — 您的应用程序是否从设备消耗过多的电力？
* 本地化 — 您的应用程序中的所有区域均经过翻译吗？
* 认证 — 您的应用程序是否已通过认证？ 客户是否确信它遵循所有数据隐私法律要求？

在自动和手动测试过程中，应该回答这些问题。

## 自动化测试 {#automated-testing}

应执行一定程度的自动化测试，以涵盖各种屏幕大小、内存限制、输入方法和操作系统。 它不但覆盖了多种测试用例，而且当引入新的功能或设备时，它可以加快回归测试的速度。 理想情况下，您的自动化工具应该减少或限制重复工作。 请使用工具或框架，以便您的测试工作适用于所有平台。 下图显示了用于基于Web的UI测试和移动应用程序测试的测试环境的简化结构。 图表的左侧显示了一系列使用浏览器的Selenium节点。 SeleniumGrid可以将常见的基于Web的UI测试群发到其中的任何节点。 Selenium中心还可以连接到Appium以进行跨平台应用程序测试。 只显示模拟器，但您可以合并用于Android™的adb和用于iOS设备的Xcode实用程序。 本文档稍后提供了一些链接，您可以在其中找到提及工具的特定详细信息。

![chlimage_1](assets/chlimage_1.jpeg)

## 手动测试 {#manual-testing}

除了自动测试之外，您的应用程序还应经历一个手动测试周期。 脚本无法复制在实际设备上运行应用程序的客户。 在这里，您也有许多选择。 您可以使用HockeyApp等平台定义有权访问和收集反馈的人员。 或者，您可以将整个过程外包给UTest、ElusiveStars或Testn等服务。 如果您有一组内部测试人员，但缺少各种设备，则可以利用云服务对其设备池执行手动测试。 SauceLabs就是其中一项服务。 您还可以远程将应用程序构建到PhoneGap Enterprise并在本地设备上安装作为验收测试或降级级别。 查看PhoneGap (`https://phonegap.com/`)网站以了解其最新功能和文档。 无论采用哪种方法，手动测试都应执行以下操作：

* 击中了一大群测试者，
* 针对大量设备进行测试（最好是实际的设备，但如果实际的设备不可用，则使用模拟器/模拟器），
* 提供信息性反馈：

   * 崩溃报告，
   * 分析/跟踪，
   * 可用性，
   * 关注领域，
   * 性能，
   * 数据/功耗等等。

## 工具 {#tools}

有多种工具可用于测试移动应用程序。 应根据您的具体情况选择要使用的解决方案：功能、价格、支持、覆盖范围等。 以下只是对某些可用工具和服务的一小部分说明。

**硒**

* 框架，包括用于测试脚本的API，以提供WebDriver并控制各种浏览器。
* 您可以将其与Appium一起使用，以在实际设备上进行测试。
* SeleniumGrid跨节点引导测试以进行并行测试。
* Selenium IDE有助于减少编写测试用例的情况。

有关更多信息，请参阅 [https://www.selenium.dev/](https://www.selenium.dev/).

**Testdroid**

* 基于云的测试服务，具有持续的集成挂接和实际的设备测试。
* 其中包括一个应用程序Crawler ，用于检查设备兼容性、分析日志、遍历视图、拍摄屏幕快照和监控性能。

有关更多信息，请参阅 [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium是用于自动化移动测试的常用跨平台框架。
* 此外，还随附了检查器以帮助代码测试用例的记录功能。

有关更多信息，请参阅 [https://appium.io/](https://appium.io/).

**酱汁实验室**

* SauceLabs提供了基于云的测试，并与持续集成集成。
* 测试在其云环境中自动运行，或者您可以启动特定设备或平台并执行手动测试以帮助调试问题。

有关更多信息，请参阅 [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* 一种外包服务，用于测试您的移动应用程序。
* 其中包含了大量的设备，并提供了多种类型的测试：性能、质量、功能、认证、本地化、数据消耗等等。

有关更多信息，请参阅 [https://apptestnow.com/](https://apptestnow.com/).

**曲棍球应用**

* HockeyApp属于手动测试范畴，在该范畴内，移动设备应用程序会被推送至个人应用商店，以便测试人员下载并试用该应用程序。

有关更多信息，请参阅 [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* 虽然Jenkins不是测试工具，但它是一个持续集成的框架，提供了自动化测试的主干。 可以使用许多第三方插件来扩展功能。 例如，SeleniumGrid插件提供了一个用于帮助管理Selenium中心和节点的UI。

有关更多信息，请参阅 [https://www.jenkins.io/](https://www.jenkins.io/) 和 [https://plugins.jenkins.io/](https://plugins.jenkins.io/).
