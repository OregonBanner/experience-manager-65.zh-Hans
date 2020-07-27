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

AEM Forms提供AEM Forms应用程序的完整源代码。 源包含构建自定义AEM Forms应用程序的所有组件。 源代码存档是 `adobe-lc-mobileworkspace-src-<version>.zip` 软件分发软件包 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 的一部分。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 开放 [软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID登录软件分发。
1. 点按 **[!UICONTROL 标题]** 菜单中可用的Adobe Experience Manager。
1. 在过滤器 **[!UICONTROL 部分]** :
   1. 从“ **[!UICONTROL 解决方]** 案 **[!UICONTROL ”下]** 拉列表中选择“表单”。
   2. 选择包的版本和类型。 您还可以使用“搜 **[!UICONTROL 索下载]** ”选项筛选结果。
1. 点按适用于您的操作系统的包名称，选择“ **[!UICONTROL 接受EULA条款]**”，然后点 **[!UICONTROL 按下载]**。
1. 打开 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然后单 **[!UICONTROL 击“上传包]** ”以上传包。
1. Select the package and click **[!UICONTROL Install]**.

1. 要下载源代码存档，请在浏 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 览器中打开。
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
   <td><p>用于AEM Forms应用程序项目的HTML、CSS、图像和JavaScript文件</p> </td>
  </tr>
 </tbody>
</table>

有关代码签名和将设备添加到iOS配置门户的详细信息，请参 [阅iOS代码签名设置、流程和疑难解答](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)。

## 构建标准AEM Forms应用程序 {#set-up-the-xcode-project}

1. 执行以下步骤以在Xcode中设置项目并提供签名标识：

   登录到已安装和配置Xcode和iOS SDK的Mac计算机。

1. 将存档 `adobe-lc-mobileworkspace-src-<version>.zip` 从下载文件夹复制到 `[User_Home]/Projects/`。
1. 解压目录中的存 `[User_Home]/Projects/[your-project]`档。
1. 导航到 ` [User_Home]/Projects/ `[您的项目目录]`/adobe-lc-mobileworkspace-src-[version]/ios` 。
1. 在Xcode中 `AEM Forms.xcodeproj` 打开项目。
1. 单击 **AEM Forms**，在 **目标下**，选 **择AEM Forms**。 选择“ **构建设置** ”选项卡，找到“代 **码签名授权** ”部分，在“调试”和“发行”字段中执行下列操作之一：

   * 未指定字段以构建标准Mobile Workspace应用程序
   * 如构建iOS的安全AEM Forms应 [用程序以构建安全AEM Forms应用程序](/help/forms/using/building-secure-mobile-workspace-app.md) ，请指定相应的字段。

1. 在“构 **建设置** ”选项卡中， **单击“全部** ” **，然后单**&#x200B;击“组合”。
1. 从“设置 **”列表** ，展开“ **代码签名”**。
1. 对于 **代码签名标识**，请选择相应的签名。 有关创建新签名的详细信息，请参 [阅创建和下载开发供应用户档案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)。
1. 确保为Debug、Release和 **任何iOS** SDK选 **择同**&#x200B;一签名 ****。
1. 替换文件中的以下 `AEM Forms-info.plist` 代码：

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   替换为服务器 `yourserver.com` 的相应主机名时，将显示以下内容。

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

1. 在“项 **目**”下，选择 **AEM Forms** ，并确保为“代码签名身份”、“ **调试”、“发**&#x200B;行版”和“任何i SDK ************ SDK”选择适当的签名。
1. 将置备的iPad连接到Mac计算机。
1. 为AEM Forms项目选择预 **配的** 设备。

   ![ipad](assets/ipad.png)

   已选择预配设备iPad Air 2。

1. 选择 **产品** >清 **理**。
1. 选择 **“产品** ”> **“内部版本**”。

## 为AEM Forms应用程序构建安装程序 {#build-the-installer-for-the-mobile-workspace-app}

您需要存档Xcode项目以构建安装程序（.ipa文件）和属性列表（.plist文件）文件。 属性列表文件包含托管的内部应用程序的配置信息，如应用程序的名称和托管位置。 有关属性列表文件的详细信息，请参 [阅关于信息属性列表文件](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 将置备的iPad连接到Mac计算机。 有关设置iPad的详细信息，请参阅创 [建和下载开发设置用户档案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 为AEM Forms项目选择预 **配的** 设备。

   ![ipad-1](assets/ipad-1.png)

   已选择预配设备iPad Air 2。

1. 选择 **产品** >清 **理**。
1. 选择 **“产品** ”> **“内部版本**”。
1. 选择 **“产品** ”> **“存档**”。
1. 在“管理器——存档”中，选择项目的最新存档并单击“分 **发”**。
1. 选 **择“为企业保存”或“临时部署** ”作为分发方法，然后单击“下 **一步”**。
1. 选择相应的代 **码签名标识** ，然后单 **击下一步**。 单击 **“允** ”以应用签名。
1. 提供应用程序的名称，然后选择“ **保存为企业分发所用格式”**。
1. 提供应 **用程序** 的应用程序URL。 例如，要在CRX服务器上承载应用程序，请提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`。
1. 在“标 **题** ”字段中指定AEM Forms。
1. Click **Save** and close Xcode.

   将在指定位 `AEM Forms.ipa`置创建安装程序文 `AEM Forms-info.plist`件、属性列表文件。

1. 在编辑 `AEM Forms-info.plist` 器中打开文件。
1. 将。ipa文件URL中的所有空格替换为%20。
1. 保存并关闭 `AEM Forms-info.plist` 文件。