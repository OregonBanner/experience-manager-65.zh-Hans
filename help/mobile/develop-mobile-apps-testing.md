---
title: 测试移动设备应用程序
seo-title: 测试移动设备应用程序
description: 测试移动设备应用程序
seo-description: 'null'
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
exl-id: e10e1904-7016-4eb0-9408-36297285f378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---

# 测试移动设备应用程序{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

鉴于市场上的设备种类繁多且正在发布的设备众多，测试您的应用程序变得极其重要。 在这个领域，功能和可用性在应用商店上可能会获得低评论，但单一缺陷可能会导致您的应用程序被卸载。 测试计划和质量保证中必须谨慎注意。 以下链接涵盖了许多通常需要解决的主题，例如，识别您的环境、定义测试案例、测试类型、假设、客户参与等。 此外，还讨论了有助于测试工作的工具。 内部工具（如[Hobbes](/help/sites-developing/hobbes.md)）有助于进行基于Web的UI测试。 [Tough Day](/help/sites-developing/tough-day.md) 可以通过模拟负载来压缩实例。如果您的测试环境已经具有使用第三方工具（如Selenium）的经验，则也可以使用这些工具。

在开发移动应用程序时，除了传统测试之外，还有许多新的特有问题需要解决。

* 功能 — 您的应用程序是否满足所有要求？
* 可用性 — 您的客户是否可以轻松使用和理解该应用程序？
* 性能 — 在使用率激增期间会发生什么情况？ 应用程序元素（如轻扫和轮播）是否会快速而且不会从体验中删除？
* 失败或中断 — 当应用程序运行时有来电或通知时会发生什么情况？ 如果发生网络中断或断电，会发生什么情况？
* 安装和更新 — 安装体验如何？ 如何推送更新？
* 技术 — 您的应用程序是否消耗了来自设备的过多电源？
* 本地化 — 应用程序中的所有区域是否都已翻译？
* 认证 — 您的应用程序是否已经认证？ 客户能否相信该规则遵循了所有数据隐私法律要求？

在自动和手动测试期间，应回答这些问题。

## 自动测试{#automated-testing}

应该执行一定程度的自动化测试，以涵盖屏幕大小、内存限制、输入方法和操作系统的各种不同。 它不仅覆盖了大部分测试用例，而且在引入新功能或设备时还能加快回归测试的速度。 理想情况下，您的自动化工具应该减少或限制重复工作。 使用工具或框架，以便您的测试工作可以跨所有平台进行。 下图显示了用于基于Web的UI测试和移动设备应用程序测试的测试环境的简化结构。 图表的左侧显示了一系列带有浏览器的Selenium节点。 SeleniumGrid可以将常见的基于Web的UI测试分发到其中的任何节点。 Selenium中心还可以连接到Appium以进行跨平台应用程序测试。 仅显示模拟器，但您可以为iOS设备合并adb、for Android和Xcode实用程序。 本文档后面提供了相关链接，您可以在其中找到上述工具的特定详细信息。

![chlimage_1](assets/chlimage_1.jpeg)

## 手动测试{#manual-testing}

除了自动测试之外，您的应用程序还应完成一系列手动测试。 无法通过脚本复制在实际设备上运行应用程序的客户。 在这里，你也有很多选择。 您可以使用HockeApp等平台来定义谁有权访问和收集反馈。 或者，您可以将整个过程外包给UTest、RomailedStars或Testin等服务。 如果您有一组内部测试人员，但缺少设备变体，则可以在云服务中对其设备池执行手动测试。 SauceLabs提供的服务之一。 您还可以远程构建应用程序到PhoneGap Enterprise，并在本地设备上安装，作为验收测试或降级级别。 有关最新功能和文档，请参阅[PhoneGap](https://phonegap.com/)网站。 无论采用何种方法，手动测试都应该；

* 击中了大量测试人员目标，
* 针对大量设备池进行测试（理想情况下是实际设备，但如果实际设备不可用，则会进行模拟器/模拟器），
* 提供信息反馈：

   * 崩溃报告，
   * analytics/跟踪，
   * 可用性，
   * 注意领域，
   * 性能，
   * 数据/功耗等

## 工具 {#tools}

有各种各样的工具可用于测试移动设备应用程序。 根据您的具体情况选择要使用的选件：功能、价格、支持、覆盖范围等。 以下只是对一些可用工具和服务的简短描述。

**硒**

* 该框架包含用于测试脚本的API，用于提供WebDriver并控制各种浏览器。
* 您可以将此功能与Appium结合使用，在实际设备上进行测试。
* SeleniumGrid将测试定向到各个节点，以便进行并行测试。
* Selenium IDE有助于减少测试用例的编写。

有关更多信息，请参阅[https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**Testdroid**

* 基于云的测试服务，具有连续的集成挂钩和真实设备测试。
* 包括App Crawler，用于检查设备兼容性、分析日志、遍历视图、拍摄屏幕截图并监视性能。

有关更多信息，请参阅[https://testdroid.com/](https://testdroid.com/)。

**阿皮姆**

* Appium是自动化移动测试的常用跨平台框架。
* 此外，检查器还具有帮助代码测试用例的记录功能。

有关更多信息，请参阅[https://appium.io/](https://appium.io/)。

**SauceLabs**

* SauceLabs提供基于云的测试，并与连续集成集成。
* 测试可在其云环境中自动运行，或者您可以启动特定设备或平台并执行手动测试以帮助调试问题。

有关更多信息，请参阅[https://saucelabs.com/](https://saucelabs.com/)。

**AppTestNow**

* 一种外包服务，可测试您的移动应用程序。
* 包括大量设备池，并提供多种类型的测试：性能、质量、功能、认证、本地化、数据使用情况等。

有关更多信息，请参阅[https://www.apptestnow.com](https://www.apptestnow.com/)。

**HockeApp**

* HockeApp属于手动测试，在手动测试中，移动设备应用程序会被推送到个人应用商店，测试人员可以在该应用商店下载并试用。

有关更多信息，请参阅[https://hockeyapp.net/features/](https://hockeyapp.net/features/)。

**詹金斯**

* Jenkins虽然不是测试工具，但是是一个连续的集成框架，为自动化测试提供了骨干。 提供了大量第三方插件来扩展功能。 例如，SeleniumGrid插件提供了一个UI，以帮助管理Selenium集线器和节点。

有关更多信息，请参阅[https://jenkins-ci.org/](https://jenkins-ci.org/)和[https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins)。
