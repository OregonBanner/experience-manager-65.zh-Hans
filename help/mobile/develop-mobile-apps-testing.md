---
title: 测试移动应用程序
seo-title: 测试移动应用程序
description: 'null'
seo-description: 'null'
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---


# 测试移动应用程序{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

鉴于市场上的各种设备和正在发布的设备种类繁多，测试您的App变得极其重要。 在这一领域，功能和可用性可能会在App Store上获得低评论，但单个缺陷可能导致卸载您的App。 测试计划和质量保证中必须小心。 以下链接涵盖了许多一般需要解决的主题，例如，确定您的环境、定义测试用例、测试类型、假设、客户参与等。 还讨论了有助于测试的工具。 内部工具（如[Hobbes](/help/sites-developing/hobbes.md)）可以帮助进行基于Web的UI测试。 [Tough ](/help/sites-developing/tough-day.md) Day可以通过模拟载荷对实例施加压力。如果您的测试环境已经具备Selenium等第三方工具的使用经验，也可以使用这些工具。

在开发移动应用程序时，除了传统测试之外，还有许多新的特有问题需要解决。

* 功能——应用程序是否满足所有要求？
* 可用性——客户是否可以轻松使用和理解该应用程序？
* 性能——在使用率激增期间会发生什么情况？ 应用程序元素（如轻扫和轮盘）是否快速且不会降低体验？
* 失败或中断——当应用程序运行时有来电或通知时，会发生什么情况？ 如果网络中断或断电，会发生什么情况？
* 安装和更新——安装体验如何？ 更新如何推出？
* 技术——您的应用程序是否消耗了来自设备的过多功能？
* 本地化-应用程序中的所有区域是否都已翻译？
* 认证——您的应用程序是否已通过认证？ 客户能否相信它遵守所有数据隐私法律要求？

这些问题应在自动化和手动测试过程中得到回答。

## 自动测试{#automated-testing}

应执行一定程度的自动测试，以涵盖各种屏幕大小、内存限制、输入方法和操作系统。 它不仅覆盖了大量测试用例，而且在引入新功能或新设备时，还可以加快回归测试。 理想情况下，您的自动化工具应减少或限制重复工作。 使用工具或框架，以便您的测试工作在所有平台上都适用。 下表显示了基于Web的UI测试和移动应用程序测试的测试环境的简化结构。 图表的左侧显示一系列带有浏览器的Selenium节点。 SeleniumGrid可以将常见的、基于Web的UI测试发布到这些节点中的任何一个。 Selenium集线器还可连接到Appium以进行跨平台应用程序测试。 只显示模拟器，但您可以为iOS设备加入adb、Android和Xcode实用程序。 此文档稍后会提供链接，您可以在其中找到所述工具的特定详细信息。

![chlimage_1](assets/chlimage_1.jpeg)

## 手动测试{#manual-testing}

除了自动测试，您的应用程序还应经历一个手动测试周期。 在实际设备上运行应用程序的客户不能被脚本复制。 你也有很多选择。 您可以使用HockeyApp等平台定义谁有权访问和收集反馈。 或者，您可以将整个流程外包给UTest、MacronableStars或Testin等服务。 如果您有一组内部测试人员，但没有设备的变体，则可以在云服务中对其设备池执行手动测试。 SauceLabs是提供此服务的一种服务。 您还可以将应用程序远程构建到PhoneGap Enterprise并作为验收测试或降级级别安装在本地设备上。 请访问[PhoneGap](https://phonegap.com/)网站，了解其最新功能和文档。 无论采用何种方法，手动测试都应该；

* 击中了一大目标测试人员，
* 针对大量设备进行测试（最好是真实设备，但如果真的设备不可用，则为模拟器／模拟器）,
* 提供有益的反馈：

   * 崩溃报告，
   * 分析／跟踪，
   * 可用性，
   * 关注领域，
   * 性能，
   * 数据／功耗等。

## 工具 {#tools}

可用于测试移动应用程序的各种工具。 根据您的具体情况选择使用哪些选项：功能、价格、支持、覆盖等。 以下只是一些可用工具和服务的简短说明。

**硒**

* 该框架包含一个API，用于测试脚本以供给WebDriver和控制各种浏览器。
* 您可以将它与Appium结合使用，在真实设备上进行测试。
* SeleniumGrid将测试定向到各个节点，以进行并行测试。
* Selenium IDE有助于减少测试用例编写。

有关详细信息，请参阅[https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**Testdroid**

* 基于云的测试服务，具有持续的集成挂钩和真实设备测试。
* 包括App Crawler，它可检查设备兼容性、分析日志、遍历视图、获取屏幕截图和监视性能。

有关详细信息，请参阅[https://testdroid.com/](https://testdroid.com/)。

**Appium**

* Appium是用于自动化移动测试的流行跨平台框架。
* 此外，检查器还具有帮助编写测试用例的记录功能。

有关详细信息，请参阅[https://appium.io/](https://appium.io/)。

**SauceLabs**

* SauceLabs提供基于云的测试并与持续集成集成。
* 测试在其云环境中自动运行，或者您可以开始特定设备或平台并执行手动测试以帮助调试问题。

有关详细信息，请参阅[https://saucelabs.com/](https://saucelabs.com/)。

**AppTestNow**

* 测试移动App的外包服务。
* 包括大量设备并优惠各种测试：性能、质量、功能、认证、本地化、数据消耗等。

有关详细信息，请参阅[https://www.apptestnow.com](https://www.apptestnow.com/)。

**HockeApp**

* HockeyApp属于手动测试，在手动测试中，移动应用被推送到个人应用商店，测试人员可在那里下载并试用它。

有关详细信息，请参阅[https://hockeyapp.net/features/](https://hockeyapp.net/features/)。

**詹金斯**

* 尽管Jenkins不是测试工具，但它是一个连续的集成框架，为自动测试提供了支柱。 大量第三方插件可用于扩展功能。 例如，SeleniumGrid插件提供了一个UI来帮助管理Selenium集线器和节点。

有关详细信息，请参阅[https://jenkins-ci.org/](https://jenkins-ci.org/)和[https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins)。
