---
title: 设置Xcode项目并构建iOS应用程序
seo-title: 设置Xcode项目并构建iOS应用程序
description: 介绍如何构建适用于iOS的标准AEM Forms应用程序。
seo-description: 介绍如何构建适用于iOS的标准AEM Forms应用程序。
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---


# 设置Xcode项目并构建iOS应用程序{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms应用的完整源代码。 该源包含构建自定义AEM Forms应用程序的所有组件。 源代码存档`adobe-lc-mobileworkspace-src-<version>.zip`是软件分发`adobe-aemfd-forms-app-src-pkg-<version>.zip`包的一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开[软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID才能登录软件分发。
1. 点按标题菜单中的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 过滤器]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL 解决方案]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项筛选结果。
1. 点按适用于您的操作系统的程序包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择软件包，然后单击&#x200B;**[!UICONTROL 安装]**。

1. 要下载源代码存档，请在浏览器中打开`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`。
源包将下载到您的设备上。

下图显示了`adobe-lc-mobileworkspace-src-<version>.zip`的提取内容。

![mws-content](assets/mws-content.png)

下表详细列出了`adobe-lc-mobileworkspace-src-[version]/ios`文件夹的内容。

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
   <td><p>资源、PhoneGap插件和应用程序的主模块</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>AEM Forms应用程序的Xcode项目</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>用于AEM Forms应用程序项目的HTML、CSS、图像和JavaScript文件</p> </td>
  </tr>
 </tbody>
</table>

有关代码签名和将设备添加到iOS配置门户的详细信息，请参阅[iOS代码签名设置、进程和疑难解答](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)。

## 构建标准AEM Forms应用程序{#set-up-the-xcode-project}

1. 执行以下步骤以在Xcode中设置项目并提供签名标识：

   登录到已安装和配置Xcode和iOS SDK的Mac计算机。

1. 将`adobe-lc-mobileworkspace-src-<version>.zip`存档从下载文件夹复制到`[User_Home]/Projects/`。
1. 解压`[User_Home]/Projects/[your-project]`目录中的存档。
1. 导航到` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios`目录。
1. 在Xcode中打开`AEM Forms.xcodeproj`项目。
1. 单击&#x200B;**AEM Forms**，在&#x200B;**目标**&#x200B;下，选择&#x200B;**AEM Forms**。 选择&#x200B;**构建设置**&#x200B;选项卡，找到&#x200B;**代码签名授权**&#x200B;部分，在调试和发行字段中执行下列操作之一：

   * 未指定字段以构建标准Mobile Workspace应用程序
   * 如[构建适用于iOS的安全AEM Forms应用程序](/help/forms/using/building-secure-mobile-workspace-app.md)中所述，指定字段以构建安全AEM Forms应用程序。

1. 在&#x200B;**构建设置**&#x200B;选项卡中，单击&#x200B;**全部**，然后单击&#x200B;**组合**。
1. 在&#x200B;**设置**&#x200B;列表中，展开&#x200B;**代码签名**。
1. 对于&#x200B;**代码签名标识**，选择相应的签名。 有关创建新签名的详细信息，请参阅[创建和下载开发配置用户档案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)。
1. 确保为&#x200B;**Debug**、**Release**&#x200B;和&#x200B;**任何iOS SDK**&#x200B;选择相同的签名。
1. 替换`AEM Forms-info.plist`文件中的以下代码：

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   将`yourserver.com`替换为服务器的相应主机名时，将显示以下内容。

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
   >仅当AEM Forms应用程序需要连接到不符合应用程序传输安全要求的服务器时，才需要执行此步骤。

1. 在&#x200B;**PROJECT**&#x200B;下，选择&#x200B;**AEM Forms**&#x200B;并确保为&#x200B;**代码签名标识**、**Debug**、**发行版**&#x200B;和&#x200B;**任何iOS SDK**。
1. 将置备的iPad连接到Mac计算机。
1. 为&#x200B;**AEM Forms**&#x200B;项目选择预配设备。

   ![ipad](assets/ipad.png)

   已选择预配设备iPad Air 2。

1. 选择&#x200B;**产品** > **清洁**。
1. 选择&#x200B;**产品** > **内部版本**。

## 为AEM Forms应用程序{#build-the-installer-for-the-mobile-workspace-app}构建安装程序

您需要存档Xcode项目以构建安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含托管的内部应用程序的配置信息，如应用程序的名称和托管位置。 有关属性列表文件的详细信息，请参阅[关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 将置备的iPad连接到Mac计算机。 有关设置iPad的详细信息，请参阅[创建和下载开发设置用户档案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 为&#x200B;**AEM Forms**&#x200B;项目选择预配设备。

   ![ipad-1](assets/ipad-1.png)

   已选择预配设备iPad Air 2。

1. 选择&#x200B;**产品** > **清洁**。
1. 选择&#x200B;**产品** > **内部版本**。
1. 选择&#x200B;**产品** > **存档**。
1. 在“管理器——存档”中，选择项目的最新存档，然后单击&#x200B;**分发**。
1. 选择&#x200B;**“为企业或临时部署保存”**&#x200B;作为分发方法，然后单击&#x200B;**“下一步”**。
1. 选择相应的&#x200B;**代码签名标识**&#x200B;并单击&#x200B;**下一步**。 单击&#x200B;**允许**&#x200B;应用签名。
1. 提供应用程序的名称，然后选择“保存为企业分发所用格式”**。**
1. 提供应用程序的&#x200B;**应用程序URL**。 例如，要在CRX服务器上承载应用程序，请提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`。
1. 在&#x200B;**标题**&#x200B;字段中，指定AEM Forms。
1. 单击&#x200B;**保存**&#x200B;并关闭Xcode。

   在指定位置创建安装程序文件`AEM Forms.ipa`和属性列表文件`AEM Forms-info.plist`。

1. 在编辑器中打开`AEM Forms-info.plist`文件。
1. 将。ipa文件URL中的所有空格替换为%20。
1. 保存并关闭`AEM Forms-info.plist`文件。