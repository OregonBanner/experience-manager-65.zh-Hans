---
title: 使用PhoneGap CLI开发应用程序
seo-title: 使用PhoneGap CLI开发应用程序
description: 可查看本页，了解如何使用PhoneGap CLI开发应用程序。
seo-description: 可查看本页，了解如何使用PhoneGap CLI开发应用程序。
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# 使用PhoneGap CLI{#developing-apps-with-phonegap-cli}开发应用程序

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

在任何给定时间，作为开发人员，您都可以在设备或模拟器中运行应用程序，前提是您已配置开发环境。

要运行以下示例，您需要一个运行带Xcode的OSx(Mac)的系统，或安装Android SDK的Mac/Win/Linux系统。

## Bootstrap开发环境{#bootstrap-your-development-environment}

[设置PhoneGap CLI](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

对于iOS:要为iPhone和iPad进行开发，您需要Apple的Xcode IDE。

* 免费下载[此处](https://developer.apple.com/xcode/downloads/)。
* [PhoneGap iOS平台指南](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

对于Android:要为iPhone和iPad进行开发，您需要Google的Android Stuido IDE。

* 免费下载[此处](https://developer.android.com/sdk/index.html)。
* [PhoneGap Android平台指南](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## 下载源{#download-the-source}

成功预装开发环境后，请从AEM App Build Tile下载源：

* 单击PhoneGap Build拼贴下拉V形标记。

![chlimage_1-45](assets/chlimage_1-45.png)

* 单击“下载源”。
* 从“下载源”模式中选择所需的源。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>开发源包含应用程序的最新状态，同时包含未暂存的更改。 使用暂存源构建要提交到应用商店供应商的发行版候选。
>
>如果您从未暂存应用程序，选择暂存将触发暂存工作流(提示：这将在AppStore和Google PlayStore中提供的PhoneGap Enterprise Viewer应用程序中显示为分阶段应用程序)。

* 单击“下载”并将ZIP保存到计算机。
* 将下载的zip文件解压到您的工作区。

## 构建并加载应用程序（从源）{#build-and-load-the-app-from-source}

PhoneGap CLI可以通过单个命令创建平台项目、编译源和部署应用程序。

>[!NOTE]
>
>您可以单独执行所有这些步骤，请参阅[PhoneGap CLI文档](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/)。

1. 确保已安装PhoneGap CLI，请参阅上文。
1. 在控制台（或终端）窗口中，导航到解压缩源的根目录。
1. 输入以下命令：

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>如果此时出现问题，请回到故障拍摄的基础知识。
>
>1. 创建新文件夹（mkdir测试）
>1. 导览至此新文件夹（cd测试）
>1. 运行“phonegap create helloWorld”
>1. 导航到helloWorld(cd helloWorld)
>1. 运行“phonegap运行android”（或将android替换为上述ios）。
>1. 将打开模拟器，运行新创建的PhoneGap应用程序，如果到本机的JavaScript桥接器可以运行，则它会说“设备就绪”。

>
>
这将验证您的PhoneGap CLI开发环境是否已启动并正确运行。

## 使用Safari和IOS调试{#debug-javascripts-with-safari-and-ios-debug}调试Javascript

您可以使用Safari的开发人员工具调试应用程序的JavaScript，方法与使用Web应用程序相同。

## 启用Safari开发人员工具{#enable-safari-developer-tools}

要启用开发人员工具，请执行以下操作：

* 打开Safari首选项

   * 在菜单栏中单击Safari
   * 单击“首选项”

* 在“首选项”窗口中单击“高级”

![chlimage_1-47](assets/chlimage_1-47.png)

* 选中“在菜单栏中显示开发菜单”
* 关闭首选项窗口

## 将Safari连接到iOS {#connect-safari-to-ios}

可以将Safari连接到iOS设备或模拟器。

* 在控制台窗口中，导航到解压缩源的根目录。
* 输入以下命令，在您的设备或模拟器上启动您的应用程序。

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* 打开Safari
* 在菜单栏中单击“开发”
* 选择iOS模拟器子菜单
* 单击home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## 使用Safari的Web检查器调试JavaScript {#debug-javascript-with-safari-s-web-inspector}

您可以在源中的任意位置设置断点。 当您与模拟器或设备交互时，应用程序的执行将停止在这些断点处。 您可以遍历执行步骤并检查变量中的值。

* 在“Web检查器”窗口中单击“资源”
* 导览源树并单击所需的源文件
* 单击旁边的行号以添加断点
* 与设备或模拟器交互

![chlimage_1-49](assets/chlimage_1-49.png)

* 使用控制按钮可继续执行、跳过、跳入和跳出方法：

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>要查看变量值，请在当前方法中，悬停鼠标。

## 后续步骤 {#the-next-steps}

了解了使用PhoneGap CLI开发应用程序后，请参阅[访问设备功能](/help/mobile/phonegap-access-device-features.md)。
