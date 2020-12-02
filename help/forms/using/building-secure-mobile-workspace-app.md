---
title: 构建适用于iOS的安全AEM Forms应用程序
seo-title: 构建适用于iOS的安全AEM Forms应用程序
description: 构建安全的AEM Forms应用程序的步骤。
seo-description: 构建安全的AEM Forms应用程序的步骤。
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# 构建适用于iOS的安全AEM Forms应用程序{#building-a-secure-aem-forms-app-for-ios}

您需要存档AEM Forms应用程序的Xcode项目以构建安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含托管的内部应用程序的配置信息，如应用程序的名称和托管位置。 有关属性列表文件的详细信息，请参阅[关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 登录以下网站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 创建应用程序ID。 有关创建App ID的详细步骤，请参阅[创建和配置App ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)。
1. 要为应用程序配置iOS应用程序的捆绑标识符，请单击&#x200B;**[!UICONTROL 配置应用程序ID]**。
1. 在网页底部，选择&#x200B;**[!UICONTROL 启用数据保护]**。 指定数据保护选项。

   单击&#x200B;**[!UICONTROL 完成]**。

1. 导航到“供应”->“分发”，然后使用步骤3中配置的App ID创建新用户档案。
1. 下载供应用户档案并将其添加到Xcode和iPad。
1. 登录到已安装和配置Xcode和iOS SDK的Mac计算机。
1. 在Xcode中打开`AEM Forms.xcodeproj`项目。
1. 单击&#x200B;**[!UICONTROL AEM Forms]**，在&#x200B;**[!UICONTROL 目标]**&#x200B;下，选择&#x200B;**[!UICONTROL AEM Forms]**。 选择&#x200B;**[!UICONTROL 构建设置]**&#x200B;选项卡，找到&#x200B;**[!UICONTROL 代码签名授权]**&#x200B;部分，在“授权”下拉菜单中，选择&#x200B;**[!UICONTROL LC Enterprise]**&#x200B;选项。
1. 在Xcode中找到并打开`LC Enterprise.entitlements`文件进行编辑。 在&#x200B;**XCode授权**&#x200B;下，添加与设置用户档案中存在的相同键值对。
1. 在&#x200B;**[!UICONTROL 构建设置]**&#x200B;选项卡中，单击&#x200B;**[!UICONTROL 全部]**，然后单击&#x200B;**[!UICONTROL 组合]**。
1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;列表中，展开&#x200B;**[!UICONTROL 代码签名]**。
1. 对于&#x200B;**[!UICONTROL 代码签名标识]**，选择相应的签名。 确保为&#x200B;**[!UICONTROL Debug]**、**[!UICONTROL Release]**&#x200B;和&#x200B;**[!UICONTROL 任何iOS SDK]**&#x200B;选择相同的签名。
1. 在&#x200B;**[!UICONTROL PROJECT]**&#x200B;下，选择&#x200B;**[!UICONTROL AEM Forms]**&#x200B;并确保为&#x200B;**[!UICONTROL 代码签名标识]**、**[!UICONTROL Debug]**、**[!UICONTROL 发行版]**&#x200B;和&#x200B;**[!UICONTROL 任何iOS SDK]**。
1. 构建和分发AEM Forms应用程序。 有关构建和分发AEM Forms应用程序的详细说明，请参阅[构建AEM Forms应用程序的安装程序](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)。
