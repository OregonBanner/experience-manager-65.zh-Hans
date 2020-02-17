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

---


# 测试移动应用程序{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

鉴于市场上的各种设备和正在发布的设备种类繁多，测试您的App变得极其重要。 在这个领域，功能和可用性可能在App Store上获得低评论，但单个缺陷可能导致您的App被卸载。 测试计划和质量保证中必须小心谨慎。 以下链接涵盖了许多一般需要解决的主题，例如，识别您的环境、定义测试用例、测试类型、假设、客户参与等。 还讨论了有助于测试的工具。 内部工具(如 [Hobbes](/help/sites-developing/hobbes.md))可以帮助进行基于Web的UI测试。 [“艰难的一天](/help/sites-developing/tough-day.md) ”(Tough Day)可以通过模拟负载来压缩实例。 如果您的测试环境已经具有第三方工具（如Selenium）的使用经验，则也可以使用这些工具。

开发移动应用程序时，除了传统测试之外，还有许多新的问题需要解决。

* 功能——应用程序是否满足所有要求？
* 可用性——客户是否可以轻松使用和理解该应用程序？
* 性能——在使用激增期间会发生什么情况？ 应用程序元素（如轻扫和轮盘）是否快速且不会降低体验？
* 失败或中断——当应用程序运行时有来电或通知时会发生什么情况？ 如果网络中断或断电，会出现什么情况？
* 安装和更新——安装体验如何？ 如何推出更新？
* 技术——您的应用程序是否消耗了来自设备的过多功能？
* 本地化——应用程序中的所有区域是否均已翻译？
* 认证——您的应用程序是否已通过认证？ 客户能否相信它符合所有数据隐私法律要求？

这些问题应在自动化和手动测试过程中得到回答。

## 自动测试 {#automated-testing}

应执行一定程度的自动测试以涵盖各种屏幕尺寸、内存限制、输入方法和操作系统。 它不仅覆盖了大量测试用例，而且在引入新特性或新设备时能够加快回归测试。 理想情况下，自动化工具应减少或限制工作重复。 使用工具或框架，以便您的测试工作在所有平台上都适用。 下图显示了基于Web的UI测试和移动应用程序测试的测试环境的简化结构。 图表的左侧显示了一系列带有浏览器的Selenium节点。 SeleniumGrid可以将基于Web的常见UI测试分发到这些节点中的任何节点。 Selenium Hub还可以连接到Appium以进行跨平台应用程序测试。 仅显示模拟器，但您可以为iOS设备加入adb、Android和Xcode实用程序。 本文档后面提供了链接，您可以在其中找到所述工具的特定详细信息。

![chlimage_1](assets/chlimage_1.jpeg)

## 手动测试 {#manual-testing}

除了自动测试，您的应用程序还应经历一个手动测试周期。 在实际设备上运行应用程序的客户不能被脚本复制。 这里，您也有许多选择。 您可以使用HockeyApp等平台定义谁有权访问和收集反馈。 或者，您可以将整个流程外包给UTest、MacrohableStars或Testin等服务。 如果您有一组内部测试人员，但设备没有变化，则可以使用云服务在他们的设备池中执行手动测试。 SauceLabs就是提供此服务的一种。 您还可以将应用程序远程构建到PhoneGap Enterprise并作为验收测试或降级级别安装在本地设备上。 有关 [PhoneGap的最新功能和文档](https://phonegap.com/) ，请参阅PhoneGap网站。 无论采用何种方法，手动测试都应该；

* 击中了众多测试人员的目标，
* 针对大量设备（最好是真实设备，但如果真的设备不可用，则为模拟器／模拟器）进行测试，
* 提供信息反馈：

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
* 您可以将它与Appium结合使用，以在实际设备上进行测试。
* SeleniumGrid将测试定向到各个节点，以进行并行测试。
* Selenium IDE有助于减少测试用例的编写。

有关详细信息，请参 [阅https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**Testdroid**

* 基于云的测试服务，具有连续集成挂钩和实际设备测试。
* 包括App Crawler，它可检查设备兼容性、分析日志、遍历视图、获取屏幕截图和监视性能。

有关详细信息，请参 [阅https://testdroid.com/](https://testdroid.com/)。

**Appium**

* Appium是用于自动化移动测试的流行跨平台框架。
* 此外，检查器还具有记录功能，可帮助编写测试用例代码。

有关详细信息，请参 [阅https://appium.io/](https://appium.io/)。

**SauceLabs**

* SauceLabs提供基于云的测试并与持续集成集成。
* 测试可在其云环境中自动运行，或启动特定设备或平台并执行手动测试以帮助调试问题。

有关详细信息，请参 [阅https://saucelabs.com/](https://saucelabs.com/)。

**AppTestNow**

* 测试移动App的外包服务。
* 包括大量设备并提供各种测试类型：性能、质量、功能、认证、本地化、数据消耗等。

有关详细信息，请参 [阅https://www.apptestnow.com](https://www.apptestnow.com/)。

**HockeyApp**

* HockeyApp属于手动测试，在手动测试中，移动应用程序被推送到个人应用商店，测试人员可以在那里下载并试用。

有关详细信息，请参 [阅https://hockeyapp.net/features/](https://hockeyapp.net/features/)。

**詹金斯**

* Jenkins虽然不是测试工具，但是它是一个连续的集成框架，为自动测试提供了骨干。 有许多第三方插件可用于扩展功能。 例如，SeleniumGrid插件提供了一个UI来帮助管理Selenium集线器和节点。

有关详细信息，请 [参阅](https://jenkins-ci.org/) https://jenkins-ci.org/ [和https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins)。
