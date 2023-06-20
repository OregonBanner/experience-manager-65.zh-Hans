---
title: 测试移动应用程序
seo-title: Testing Mobile Apps
description: 测试移动应用程序
seo-description: null
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
exl-id: e10e1904-7016-4eb0-9408-36297285f378
source-git-commit: 17d13e9b201629d9d1519fde4740cf651fe89d2c
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# 测试移动应用程序{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

鉴于市场上有各种各样的设备和正在发布的设备，测试您的应用程序变得极其重要。 在这个领域，功能和可用性可能会让应用商店获得较低的评价，但一个缺陷可能会导致卸载您的应用程序。 在测试计划和质量保证方面需要引起注意。 以下链接涵盖了许多需要一般解决的主题，例如，识别您的环境、定义测试用例、测试类型、假设、客户参与等。 此外，还讨论了有助于测试工作的工具。 内部工具，如 [霍布斯](/help/sites-developing/hobbes.md)可帮助进行基于Web的UI测试。 [艰难的一天](/help/sites-developing/tough-day.md) 可以在模拟载荷下使实例受力。 如果您的测试环境已有使用第三方工具（如Selenium）的经验，也可以使用这些工具。

在开发移动应用程序时，必须与传统测试一起解决许多特定于设备的新问题。

* 功能 — 您的应用程序是否满足所有要求？
* 可用性 — 您的客户是否易于使用和理解该应用程序？
* 性能 — 在使用量激增期间会发生什么？ 应用程序元素（如轻扫和轮播）是否可以快速且不会偏离体验？
* 失败或中断 — 当应用程序运行时有来电或通知时，会发生什么情况？ 如果网络中断或断电会发生什么情况？
* 安装和更新 — 安装体验如何？ 如何推送更新？
* 技术 — 您的应用程序是否从设备消耗过多的电力？
* 本地化 — 您的应用程序中的所有区域是否都已翻译？
* 认证 — 您的应用程序是否已过认证？ 客户是否确信它符合所有数据隐私法律要求？

这些问题应在您的自动化和手动测试期间得到解答。

## 自动化测试 {#automated-testing}

应执行一定程度的自动化测试，以涵盖各种屏幕大小、内存限制、输入方法和操作系统。 它不仅覆盖了大部分测试用例，而且当引入新的特征或装置时，它可以加快回归测试。 理想情况下，您的自动化工具应减少或限制重复工作。 使用工具或框架，以便您的测试工作适用于所有平台。 下图显示了用于基于Web的UI测试和移动应用程序测试的测试环境的简化结构。 图表的左侧显示了一系列使用浏览器的Selenium节点。 SeleniumGrid可以将常见的基于Web的UI测试整理到其中的任何节点。 Selenium中心还可以连接到Appium以进行跨平台应用程序测试。 仅显示了模拟器，但您可以包括adb （适用于Android）和Xcode (适用于iOS设备)实用程序。 本文档稍后提供了一些链接，您可以在其中找到提及工具的特定详细信息。

![chlimage_1](assets/chlimage_1.jpeg)

## 手动测试 {#manual-testing}

除了自动测试之外，您的应用程序还应经历一个手动测试周期。 脚本无法复制在实际设备上运行应用程序的客户。 在这里，您也有许多选择。 您可以使用诸如HockeyApp之类的平台来定义有权访问和收集反馈的人员。 或者，您可以将整个过程外包给UTest、ElusiveStars或Testn等服务。 如果您有一组内部测试人员，但缺少各种设备，则可以利用云服务对其设备池执行手动测试。 SauceLabs就是提供此服务的一种工具。 您还可以远程将应用程序构建到PhoneGap Enterprise，并作为验收测试或降级级别安装到本地设备上。 查看PhoneGap (`https://phonegap.com/`)网站以了解其最新功能和文档。 无论采用何种方法，都应采用手动测试；

* 击中了一大群测试者，
* 针对大量设备进行测试（理想情况下是真实的设备，但如果真实的设备不可用，则为模拟器/模拟器），
* 提供信息性反馈：

   * 崩溃报告，
   * 分析/跟踪，
   * 可用性，
   * 关注领域，
   * 性能，
   * 数据/功耗等

## 工具 {#tools}

有多种工具可用于测试移动应用程序。 应根据您的具体情况选择使用的解决方案：功能、价格、支持、覆盖范围等。 以下只是对某些可用工具和服务的一小部分说明。

**硒元素**

* 一个框架，包括用于测试脚本的API，以提供WebDriver并控制各种浏览器。
* 您可以将其与Appium结合使用，以便在实际设备上进行测试。
* SeleniumGrid跨节点引导测试以进行并行测试。
* Selenium IDE有助于减少测试用例编写。

有关详细信息，请参阅 [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* 基于云的测试服务，具有持续的集成挂接和实际的设备测试。
* 包括一个应用程序Crawler ，用于检查设备兼容性、分析日志、遍历视图、拍摄屏幕快照和监视性能。

有关详细信息，请参阅 [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium是用于自动化移动测试的常用跨平台框架。
* 此外，检查器还包含记录功能，以帮助代码测试用例。

有关详细信息，请参阅 [https://appium.io/](https://appium.io/).

**酱汁实验室**

* SauceLabs提供了基于云的测试，并与持续集成集成。
* 测试在其云环境中自动运行，或者您可以启动特定设备或平台，并执行手动测试以帮助调试问题。

有关详细信息，请参阅 [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* 一种外包服务，将测试您的移动应用程序。
* 包括大量设备，并提供多种类型的测试：性能、质量、功能、认证、本地化、数据使用等。

有关详细信息，请参阅 [https://www.apptestnow.com](https://www.apptestnow.com/).

**曲棍球应用**

* HockeyApp属于手动测试范畴，其中移动设备应用程序会推送至个人应用商店，测试人员可以下载并试用该应用。

有关详细信息，请参阅 [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* 虽然Jenkins不是测试工具，但它是一个持续集成框架，为自动化测试提供了骨干。 提供了许多第三方插件来扩展功能。 例如，SeleniumGrid插件提供UI以帮助管理Selenium中心和节点。

有关详细信息，请参阅 [https://jenkins-ci.org/](https://jenkins-ci.org/) 和 [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
