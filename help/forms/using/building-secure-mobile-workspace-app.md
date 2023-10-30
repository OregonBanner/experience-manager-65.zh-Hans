---
title: 为iOS构建安全的AEM Forms应用程序
description: 了解如何通过存档Xcode项目为iOS构建安全的AEM Forms应用程序。 这将创建安装程序（.ipa文件）和属性列表（.plist文件）文件。
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# 为iOS构建安全的AEM Forms应用程序 {#building-a-secure-aem-forms-app-for-ios}

您需要将AEM Forms应用程序的Xcode项目存档，以生成安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含内部托管应用程序的配置信息，例如应用程序的名称和托管位置。 有关属性列表文件的详细信息，请参阅 [关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 登录以下网站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 创建应用程序ID。 有关创建应用程序ID的详细步骤，请参阅 [创建和配置应用程序ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. 要为应用程序配置iOS应用程序的捆绑包标识符，请单击 **[!UICONTROL 配置应用程序ID]**.
1. 在网页底部，选择 **[!UICONTROL 启用数据保护]**. 指定数据保护选项。

   单击&#x200B;**[!UICONTROL 完成]**。

1. 导航到配置 — >分发，并使用在步骤3中配置的应用程序ID创建新配置文件。
1. 下载配置配置文件并将其添加到Xcode和iPad。
1. 登录到安装了Xcode并配置了iOS SDK的Mac计算机。
1. 打开 `AEM Forms.xcodeproj` Xcode中的项目。
1. 单击 **[!UICONTROL AEM Forms]**，下 **[!UICONTROL 目标]**，选择 **[!UICONTROL AEM Forms]**. 选择 **[!UICONTROL 内部版本设置]** 选项卡，找到 **[!UICONTROL 代码签名权利]** 区域，然后在授权下拉列表中，选择 **[!UICONTROL LC Enterprise]** 选项。
1. 找到并打开 `LC Enterprise.entitlements` 文件，以进行编辑。 在 **Xcode授权**，添加与预配配置文件中相同的键值对。
1. 在 **[!UICONTROL 内部版本设置]** 选项卡，单击 **[!UICONTROL 全部]** 然后单击 **[!UICONTROL 已合并]**.
1. 从 **[!UICONTROL 设置]** 列表，展开 **[!UICONTROL 代码签名]**.
1. 对象 **[!UICONTROL 代码签名标识]**&#x200B;中，选择相应的签名。 确保为以下对象选择相同的签名 **[!UICONTROL 调试]**， **[!UICONTROL 版本]**、和 **[!UICONTROL 任何iOS SDK]**.
1. 下 **[!UICONTROL 项目]**，选择 **[!UICONTROL AEM Forms]** 并确保选择适当的签名 **[!UICONTROL 代码签名标识]**， **[!UICONTROL 调试]**， **[!UICONTROL 版本]** 和 **[!UICONTROL 任何iOS SDK]**.
1. 构建和分发AEM Forms应用程序。 有关构建和分发AEM Forms应用程序的详细说明，请参阅 [构建AEM Forms应用程序的安装程序](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
