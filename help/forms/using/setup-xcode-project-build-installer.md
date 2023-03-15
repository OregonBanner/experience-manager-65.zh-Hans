---
title: 设置Xcode项目并构建iOS应用程序
seo-title: Set up the Xcode project and build the iOS app
description: 介绍如何构建适用于iOS的标准AEM Forms应用程序。
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 5%

---

# 设置Xcode项目并构建iOS应用程序{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms应用程序的完整源代码。 源包含用于构建自定义AEM Forms应用程序的所有组件。 源代码存档， `adobe-lc-mobileworkspace-src-<version>.zip` 是 `adobe-aemfd-forms-app-src-pkg-<version>.zip` Software Distribution上的包。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 筛选器]** 部分：
   1. 选择 **[!UICONTROL Forms]** 从 **[!UICONTROL 解决方案]** 下拉列表。
   2. 选择包的版本和类型。 您还可以使用 **[!UICONTROL 搜索下载]** 用于筛选结果的选项。
1. 点按适用于您的操作系统的包名称，然后选择 **[!UICONTROL 接受EULA条款]**，然后点按 **[!UICONTROL 下载]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择资源包并单击 **[!UICONTROL 安装]**.

1. 要下载源代码存档，请打开 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 在浏览器中。
源包将在您的设备上下载。

下图显示了提取的 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

下表详细说明了 `adobe-lc-mobileworkspace-src-[version]/ios` 文件夹。

<table>
 <tbody>
  <tr>
   <th><p>目录</p> </th>
   <th><p>内容</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>资源、PhoneGap插件和应用程序的主要模块</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>适用于AEM Forms应用程序的Xcode项目</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>AEM Forms应用程序项目的HTML、CSS、图像和JavaScript文件</p> </td>
  </tr>
 </tbody>
</table>

有关代码签名和将设备添加到iOS配置门户的详细信息，请参阅 [iOS代码签名设置、流程和故障排除](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## 构建标准AEM Forms应用程序 {#set-up-the-xcode-project}

1. 执行以下步骤，在Xcode中设置项目并提供签名标识：

   登录到已安装并配置Xcode和iOS SDK的Mac计算机。

1. 复制 `adobe-lc-mobileworkspace-src-<version>.zip` 从downloads文件夹存档到 `[User_Home]/Projects/`.
1. 在中提取存档 `[User_Home]/Projects/[your-project]`目录。
1. 导航到 ` [User_Home]/Projects/ `[您的项目]`/adobe-lc-mobileworkspace-src-[version]/ios` 目录。
1. 打开 `AEM Forms.xcodeproj` Xcode中的项目。
1. 单击 **AEM Forms**，下 **目标**，选择 **AEM Forms**. 选择 **内部版本设置** 选项卡，找到 **代码签名权利** 部分，并在Debug和Release字段中执行以下操作之一：

   * 将字段保留为未指定以构建标准的移动工作区应用程序
   * 指定要使用的字段，如中所述 [构建适用于iOS的安全AEM Forms应用程序](/help/forms/using/building-secure-mobile-workspace-app.md) 以构建安全的AEM Forms应用程序。

1. 在 **内部版本设置** 选项卡，单击 **全部** 然后单击 **已合并**.
1. 从 **设置** 列表，展开 **代码签名**.
1. 对象 **代码签名标识**&#x200B;中，选择相应的签名。 有关创建新特征码的详细信息，请参见 [创建和下载开发设置配置文件](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. 确保为选择相同的签名 **调试**， **版本**、和 **任何iOS SDK**.
1. 将以下代码替换为 `AEM Forms-info.plist` 文件：

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   替换时，使用以下内容 `yourserver.com` 具有适用于您的服务器的主机名。

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >仅当AEM Forms应用程序需要连接到未遵循App Transport Security要求的服务器时，才需要执行此步骤。

1. 下 **项目**，选择 **AEM Forms** 并确保选择适当的签名 **代码签名标识**， **调试**， **版本** 和 **任何iOS SDK**.
1. 将预配的iPad连接到Mac计算机。
1. 为选择已设置的设备 **AEM Forms** 项目。

   ![ipad](assets/ipad.png)

   已选择预配的设备iPad Air 2。

1. 选择 **产品** > **干净**.
1. 选择 **产品** > **生成**.

## 构建AEM Forms应用程序的安装程序 {#build-the-installer-for-the-mobile-workspace-app}

您需要存档Xcode项目以生成安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含托管内部应用程序的配置信息，例如应用程序的名称和托管位置。 有关属性列表文件的详细信息，请参阅 [关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 将预配的iPad连接到Mac计算机。 有关配置iPad的详细信息，请参阅 [创建和下载开发设置配置文件](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 为选择已设置的设备 **AEM Forms** 项目。

   ![ipad-1](assets/ipad-1.png)

   已选择预配的设备iPad Air 2。

1. 选择 **产品** > **干净**.
1. 选择 **产品** > **生成**.
1. 选择 **产品** > **存档**.
1. 在“组织器 — 存档”中，选择项目的最新存档，然后单击 **分发**.
1. 选择 **保存以供企业或临时部署** 作为分发和点击的方法 **下一个**.
1. 选择适当的 **代码签名标识** 并单击 **下一个**. 单击 **允许** 以应用签名。
1. 提供应用程序的名称并选择 **保存以供企业分发**.
1. 提供 **应用程序URL** 应用程序的。 例如，要在CRX服务器上托管应用程序，请提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. 在 **标题** 字段中，指定AEM Forms。
1. 单击 **保存** 然后关闭Xcode。

   安装程序文件， `AEM Forms.ipa`和属性列表文件， `AEM Forms-info.plist`，则会在指定位置创建。

1. 打开 `AEM Forms-info.plist` 文件中的文件。
1. 将.ipa文件URL中的所有空格替换为%20。
1. 保存并关闭 `AEM Forms-info.plist` 文件。
