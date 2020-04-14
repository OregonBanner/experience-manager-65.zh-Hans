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
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# 构建适用于iOS的安全AEM Forms应用程序 {#building-a-secure-aem-forms-app-for-ios}

您需要存档AEM Forms应用程序的Xcode项目以构建安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含托管的内部应用程序的配置信息，如应用程序的名称和托管位置。 有关属性列表文件的详细信息，请参 [阅关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 登录到以下网站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 创建应用程序ID。 有关创建应用程序ID的详细步骤，请参阅 [创建和配置应用程序ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)。
1. 要为应用程序的iOS应用程序配置捆绑标识符，请单击“配 **[!UICONTROL 置应用程序ID”]**。
1. 在网页底部，选择“启用 **[!UICONTROL 数据保护”]**。 指定数据保护选项。

   单击&#x200B;**[!UICONTROL 完成]**。

1. 导航到“供应”->“分发”，然后使用步骤3中配置的应用程序ID创建新用户档案。
1. 下载供应用户档案并将其添加到Xcode和iPad。
1. 登录到装有Xcode和iOS SDK的Mac计算机并进行配置。
1. 在Xcode中 `AEM Forms.xcodeproj` 打开项目。
1. 单击 **[!UICONTROL AEM Forms]**，在“目标” **[!UICONTROL 下]**，选 **[!UICONTROL 择“AEM Forms]**”。 选择“构 **[!UICONTROL 建设置]** ”选项卡，找到“代码签 **[!UICONTROL 名授权]** ”部分，在“授权”下拉列表中，选择 **** LC Enterprise选项。
1. 在Xcode中找到并 `LC Enterprise.entitlements` 打开文件进行编辑。 在 **XCode授权下**，添加与供应用户档案中存在的相同键值对。
1. 在“构建 **[!UICONTROL 设置]** ”选项卡中，单 **[!UICONTROL 击“全部]** ” **[!UICONTROL ，然后单击“]**&#x200B;组合”。
1. 从“设置 **[!UICONTROL ”列表]** ，展开“代 **[!UICONTROL 码签名”]**。
1. 对于“ **[!UICONTROL 代码签名标识]**”，请选择相应的签名。 确保为 **[!UICONTROL Debug]**、 **[!UICONTROL Release]**&#x200B;和 **[!UICONTROL Any iOS SDK选择同]**&#x200B;一签名。
1. 在“ **[!UICONTROL 项目]**”下，选择“ **[!UICONTROL AEM Forms]** ”并确保为“ **[!UICONTROL Code Identity Identity]**”、“ **[!UICONTROL Debug Identity”、“RELEASE Signing And]********** Any iSDK”选择适当的签名。
1. 构建和分发AEM Forms应用程序。 有关构建和分发AEM Forms应用程序的详细说明，请参 [阅构建AEM Forms应用程序的安装程序](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)。
