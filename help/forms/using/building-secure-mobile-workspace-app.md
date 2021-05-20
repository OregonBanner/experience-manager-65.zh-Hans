---
title: 构建适用于iOS的安全AEM Forms应用程序
seo-title: 构建适用于iOS的安全AEM Forms应用程序
description: 构建安全AEM Forms应用程序的步骤。
seo-description: 构建安全AEM Forms应用程序的步骤。
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# 构建适用于iOS的安全AEM Forms应用程序{#building-a-secure-aem-forms-app-for-ios}

您需要存档AEM Forms应用程序的Xcode项目，以构建安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含托管的内部应用程序的配置信息，如应用程序的名称和托管位置。 有关属性列表文件的更多信息，请参阅[关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 登录到以下网站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 创建应用程序ID。 有关创建应用程序ID的详细步骤，请参阅[创建和配置应用程序ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)。
1. 要为您的应用程序配置iOS应用程序的包标识符，请单击&#x200B;**[!UICONTROL 配置应用程序ID]**。
1. 在网页底部，选择&#x200B;**[!UICONTROL 启用以进行数据保护]**。 指定数据保护选项。

   单击&#x200B;**[!UICONTROL 完成]**。

1. 导航到配置 — >分发，然后使用步骤3中配置的应用程序ID创建新配置文件。
1. 下载预配配置文件并将其添加到Xcode和iPad中。
1. 登录到已安装并配置Xcode和iOS SDK的Mac计算机。
1. 在Xcode中打开`AEM Forms.xcodeproj`项目。
1. 单击&#x200B;**[!UICONTROL AEM Forms]**&#x200B;下的&#x200B;**[!UICONTROL TARGETS]**，选择&#x200B;**[!UICONTROL AEM Forms]**。 选择&#x200B;**[!UICONTROL 生成设置]**&#x200B;选项卡，找到&#x200B;**[!UICONTROL 代码签名权利]**&#x200B;部分，然后在权利下拉列表中，选择&#x200B;**[!UICONTROL LC Enterprise]**&#x200B;选项。
1. 在Xcode中找到并打开`LC Enterprise.entitlements`文件进行编辑。 在&#x200B;**XCode授权**&#x200B;下，添加预配配置文件中存在的相同键值对。
1. 在&#x200B;**[!UICONTROL 生成设置]**&#x200B;选项卡中，单击&#x200B;**[!UICONTROL 全部]**，然后单击&#x200B;**[!UICONTROL 组合]**。
1. 从&#x200B;**[!UICONTROL 设置]**&#x200B;列表中，展开&#x200B;**[!UICONTROL 代码签名]**。
1. 对于&#x200B;**[!UICONTROL 代码签名标识]**，请选择相应的签名。 确保为&#x200B;**[!UICONTROL Debug]**、**[!UICONTROL Release]**&#x200B;和&#x200B;**[!UICONTROL 任何iOS SDK]**&#x200B;选择相同的签名。
1. 在&#x200B;**[!UICONTROL PROJECT]**&#x200B;下，选择&#x200B;**[!UICONTROL AEM Forms]**，并确保为&#x200B;**[!UICONTROL 代码签名标识]**、**[!UICONTROL Debug]**、**[!UICONTROL Release]**&#x200B;和&#x200B;**[!UICONTROL 任何iOS SDK]**&#x200B;选择适当的签名。
1. 构建和分发AEM Forms应用程序。 有关构建和分发AEM Forms应用程序的详细说明，请参阅[构建AEM Forms应用程序安装程序](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)。
