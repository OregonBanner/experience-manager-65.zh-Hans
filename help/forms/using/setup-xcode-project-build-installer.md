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
source-git-commit: 72a582b7ac19322b81fd1a92de8fce34e55b9db1

---


# 设置Xcode项目并构建iOS应用程序{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms应用程序的完整源代码。 源包含用于构建自定义AEM Forms应用程序的所有组件。 源代码存档是 `adobe-lc-mobileworkspace-src-<version>.zip` 包共享上包的 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 导航到包shareURL: `https://<server>:<port>/crx/packageshare`.

1. 下载源包。 下载包时，它会添加到AEM Forms包管理器中。
1. 下载完毕后，导航到： `https://<server>:<port>/crx/packmgr/index.jsp`并安装 `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. 要下载源代码存档，请在您的浏 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 览器中打开。
源包将下载到您的设备上。

下图显示提取的内容 `adobe-lc-mobileworkspace-src-<version>.zip`。

![mws-content](assets/mws-content.png)

下表详细列出了文件夹的 `adobe-lc-mobileworkspace-src-[version]/ios` 内容。

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
   <td><p>适用于AEM Forms应用程序的Xcode项目</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>AEM Forms应用程序项目的HTML、CSS、图像和JavaScript文件</p> </td>
  </tr>
 </tbody>
</table>

有关代码签名和将设备添加到iOS Provisioning Portal的详细信息，请参阅 [iOS代码签名设置、进程和疑难解答](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)。

## 构建标准AEM Forms应用程序 {#set-up-the-xcode-project}

1. 执行以下步骤以在Xcode中设置项目并提供签名标识：

   登录到已安装并配置了Xcode和iOS SDK的Mac计算机。

1. 将下载文 `adobe-lc-mobileworkspace-src-<version>.zip` 件夹中的存档复制到 `[User_Home]/Projects/`。
1. 解压缩目录中的存 `[User_Home]/Projects/[your-project]`档。
1. 导航到您 ` [User_Home]/Projects/ `[的项目目录]`/adobe-lc-mobileworkspace-src-[version]/ios` 。
1. 在Xcode中 `AEM Forms.xcodeproj` 打开项目。
1. 单击 **AEM Forms**，在“目标” **下**，选 **择“AEM Forms**”。 选择“ **构建设置** ”选项卡，找到“代码签 **名授权** ”部分，在“调试”和“发行”字段中，执行下列操作之一：

   * 不指定字段以构建标准Mobile Workspace应用程序
   * 如构建适用于iOS的安全AEM Forms应用 [程序以构建安全AEM Forms应用程序中所述](/help/forms/using/building-secure-mobile-workspace-app.md) ，指定要构建的字段。

1. 在“构建 **设置** ”选项卡中，单 **击“全部** ” **，然后单击“**&#x200B;组合”。
1. 从“设置 **”列表** ，展开“代 **码签名”**。
1. 对于“ **代码签名标识**”，请选择相应的签名。 有关创建新签名的详细信息，请参阅创 [建和下载开发供应用户档案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)。
1. 确保为 **Debug**、 **Release**&#x200B;和 **Any iOS SDK选择同**&#x200B;一签名。
1. 在文件中替换以下代 `AEM Forms-info.plist` 码：

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   替换为服务器 `yourserver.com` 的相应主机名。

   ```java
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
   >仅当AEM Forms应用程序需要连接到不遵循App Transport Security要求的服务器时，才需要执行此步骤。

1. 在“ **项目**”下，选择“ **AEM Forms** ”并确保为“ **Code Identity Identity**”、“ **Debug Identity”、“RELEASE Signing And********** Any iSDK”选择适当的签名。
1. 将配置的iPad连接到Mac计算机。
1. 为 **AEM Forms项目选择已配置的设备** 。

   ![ipad](assets/ipad.png)

   已选择预置设备iPad Air 2。

1. 选择 **产品** >清 **理**。
1. 选择“ **产品** ”>“ **内部版本**”。

## 构建AEM Forms应用程序的安装程序 {#build-the-installer-for-the-mobile-workspace-app}

您需要存档Xcode项目以构建安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含托管的内部应用程序的配置信息，如应用程序的名称和托管位置。 有关属性列表文件的详细信息，请参 [阅关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 将配置的iPad连接到Mac计算机。 有关设置iPad的详细信息，请参阅创建和 [下载开发配置用户档案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 为 **AEM Forms项目选择已配置的设备** 。

   ![ipad-1](assets/ipad-1.png)

   已选择预置设备iPad Air 2。

1. 选择 **产品** >清 **理**。
1. 选择“ **产品** ”>“ **内部版本**”。
1. 选择 **产品** >存 **档**。
1. 在“管理器——存档”中，选择项目的最新存档，然后单击“分 **发”**。
1. 选 **择“保存为企业所用格式”或“临时部署所用格式** ”作为分发方法，然后单击“下 **一步”**。
1. 选择相应的代 **码签名标识** ，然后单击 **下一步**。 单击 **“允许** ”以应用签名。
1. 提供应用程序的名称，然后选择“ **保存为Enterprise分发所用格式”**。
1. 提供应 **用程序的应用** URL。 例如，要在CRX服务器上托管应用程序，请提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`。
1. 在“标 **题** ”字段中，指定AEM表单。
1. 单击 **保存** ，然后关闭Xcode。

   将在指定位 `AEM Forms.ipa`置创建安装程序文件 `AEM Forms-info.plist`和属性列表文件。

1. 在编辑 `AEM Forms-info.plist` 器中打开文件。
1. 将。ipa文件URL中的所有空格替换为%20。
1. 保存并关闭 `AEM Forms-info.plist` 文件。