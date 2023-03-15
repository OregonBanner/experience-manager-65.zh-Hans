---
title: 使用Facebook和Twitter进行社交登录
seo-title: Social Login with Facebook and Twitter
description: 社交登录允许网站访客使用其Facebook或Twitter帐户登录。
seo-description: Social login lets site visitors to sign in with their Facebook or Twitter account.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
role: Admin
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2783'
ht-degree: 1%

---

# 使用Facebook和Twitter进行社交登录 {#social-login-with-facebook-and-twitter}

社交登录是一种向网站访客显示使用其Facebook或Twitter帐户登录的选项的功能。 因此，将允许的Facebook或Twitter数据包含在其AEM成员配置文件中。

![socialloginweretail](assets/socialloginweretail.png)

## 社交登录概述 {#social-login-overview}

要包含社交登录，它是 *必需* 创建自定义Facebook和Twitter应用程序。

虽然we-retail示例提供了示例Facebook和Twitter应用程序及云服务，但它们在 [生产网站](../../help/sites-administering/production-ready.md).

所需步骤包括：

1. [启用OAuth身份验证](#adobe-granite-oauth-authentication-handler) 在所有AEM发布实例上。

   如果未启用OAuth，则登录尝试会失败。

1. **创建** 社交应用程序和云服务。

   * 要支持使用Facebook登录，请执行以下操作：

      * 创建 [facebook应用程序](#create-a-facebook-app).
      * 创建和发布 [facebook Connect云服务](#create-a-facebook-connect-cloud-service).
   * 要支持使用Twitter登录，请执行以下操作：

      * 创建 [twitter应用程序](#create-a-twitter-app).
      * 创建和发布 [twitter Connect云服务](#create-a-twitter-connect-cloud-service).


1. [**启用** 社交登录](#enable-social-login) 社区站点。

有两个基本概念：

1. **范围** （权限）指定允许应用程序请求的数据。

   * facebook和Twitter [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 默认情况下，实例会在其范围中包含基本应用程序权限。

1. **字段** (params)指定使用URL参数请求的实际数据。

   * 这些字段在 [AEM Communities Facebook OAuth提供程序](#aem-communities-facebook-oauth-provider) 和 [AEM Communities Twitter OAuth提供程序](#aem-communities-twitter-oauth-provider).
   * 对于大多数用例，默认字段即足够，但可以修改。

## facebook登录 {#facebook-login}

### facebook API版本 {#facebook-api-version}

社交登录和we-retail Facebook示例是在Facebook Graph API版本1.0时开发的。截至AEM 6.4 GA和AEM 6.3 SP1社交登录已更新，可与较新版本的Facebook Graph API 2.5配合使用。

>[!NOTE]
>
>对于较旧的AEM版本，如果您在日志中遇到异常 **无法从此中提取令牌**，请升级到该AEM版本的最新CFP。

有关Facebook Graph API版本信息，请参阅 [facebook API更改日志](https://developers.facebook.com/docs/apps/changelog).

### 创建Facebook应用程序 {#create-a-facebook-app}

需要正确配置的Facebook应用程序才能启用Facebook社交登录。

要创建Facebook应用程序，请按照Facebook的说明操作，网址为 [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). 对说明所做的更改不会反映在以下信息中。

一般来说，从Facebook API v2.7开始：

* *添加新的Facebook应用程序*
   * 对象 *Platform*，选择网站：
      * 对象 *站点URL*，输入 `  https://<server>:<port>.`
      * 对象 *显示名称*，输入标题以用作Facebook连接服务的标题。
      * 对象 *类别*，推荐选择 *页面应用程序*，但可以是任何内容。
      * *添加产品： Facebook登录*
      * 对象 *有效的OAuth重定向URI*，输入 `  https://<server>:<port>.`

>[!NOTE]
>
>在开发方面，http://localhost:4503将发挥作用。

创建应用程序后，找到 **[!UICONTROL 应用程序ID]** 和 **[!UICONTROL 应用程序密钥]** 设置。 此信息是配置 [facebook cloud service](#createafacebookcloudservice).

### 创建Facebook ConnectCloud Service {#create-a-facebook-connect-cloud-service}

此 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 通过创建Cloud Service配置实例化的实例，可标识Facebook应用程序以及添加新用户的成员组。

1. 在AEM创作实例上，使用管理员权限登录。
1. 在全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL facebook社交登录配置]**.
1. 选择配置 **[!UICONTROL 上下文路径]**.

   **[!UICONTROL 上下文路径]** 应与您在创建/编辑社区站点时选择的云配置路径相同。

1. 检查是否已启用上下文路径以在其下方创建云服务。
1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**. 选择上下文并编辑属性。 启用云配置（如果尚未启用）。

   ![config-propertiespng](assets/config-propertiespng.png)

   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。

1. **创建/编辑** facebook云服务配置。

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL 标题]** (*必需*)输入标识Facebook应用程序的显示标题。 建议使用与输入的相同的名称 *显示名称* 用于Facebook应用程序。
   * **[!UICONTROL 应用程序ID/API密钥]** (*必需*)输入 ***应用程序ID*** 用于Facebook应用程序。 这样可识别 [AdobeGranite OAuth应用程序和提供程序](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 通过对话框创建的实例。
   * **[!UICONTROL 应用程序密钥]** (*必需*)输入 ***应用程序密钥*** 用于Facebook应用程序。
   * **[!UICONTROL 创建用户]** 如果选中，使用Facebook帐户登录将创建AEM用户条目，并将其作为成员添加到选定的用户组。  默认选中（强烈推荐）。
   * **[!UICONTROL 隐藏用户ID]**：保留为取消选中状态。
   * **[!UICONTROL 设定电子邮件范围]**：应从Facebook获取用户的电子邮件id。
   * **[!UICONTROL 添加到用户组]** 选择“添加用户组”以选择一个或多个组 [成员组](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 用户将添加到其中的社区站点。

   >[!NOTE]
   >
   >可以随时添加或删除组。 但现有用户的成员资格不会受到影响。 自动成员资格仅适用于此字段更新后创建的新用户。 对于禁用匿名用户的站点，选择将用户添加到对应于该已关闭社区站点的社区成员组。

   * 选择 **[!UICONTROL 保存]**.
   * **[!UICONTROL 发布]**.


结果是 [AdobeGranite OAuth应用程序和提供程序](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 无需进一步修改的实例，除非添加了其他范围（权限）。 默认范围是Facebook登录的标准权限。 如果需要其他范围，则需要直接编辑OSGI配置。 如果直接通过系统/控制台进行了修改，请避免从触屏UI编辑云服务配置以避免覆盖。

### AEM Communities Facebook OAuth提供程序 {#aem-communities-facebook-oauth-provider}

AEM Communities提供商对 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 实例。

此提供程序需要编辑以：

* 允许用户更新
* 添加其他字段 [在范围内](#adobe-granite-oauth-application-and-provider)

   * 默认情况下，并不包括默认允许的所有字段。

如果需要进行编辑，请在每个AEM发布实例上：

1. 使用管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md). 例如，http://localhost:4503/system/console/configMgr。
1. 找到AEM Communities Facebook OAuth提供程序。
1. 选择铅笔图标以打开进行编辑。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth提供程序ID]**

      (*必需*)默认值为 *soco -facebook*. 不要编辑。

   * **[!UICONTROL Cloud Service配置]**

      默认值为 `/etc/  cloudservices /  facebookconnect`. 不要编辑。

   * **[!UICONTROL OAuth提供程序服务配置]**

      默认值为 `/apps/social/facebookprovider/config/`. 不要编辑。

   * **[!UICONTROL 启用标记]**

      不要编辑。

   * **[!UICONTROL 用户路径]**

      存储库中存储用户数据的位置。 对于社区站点，为确保成员有权查看彼此的配置文件，路径应为默认路径 */home/users/community*.

   * **[!UICONTROL 启用字段]**

      如果选中，则在向Facebook发出的用户身份验证和信息请求中会指定列出的字段。 默认值为取消选中。

   * **[!UICONTROL 字段]**

      启用字段后，在调用Facebook图形API时将包含以下字段。 这些字段必须允许在云服务配置中定义的作用域内。 其他字段可能需要Facebook批准。 参考Facebook文档的Facebook登录权限部分。 作为参数添加的默认字段包括：

      * id
      * name
      * 名字
      * last_name
      * 链接
      * 区域设置
      * 图片
      * 时区
      * update_time
      * 已验证
      * 电子邮件

   如果添加或更改了任何字段，请更新相应的默认同步处理程序配置以更正映射。

   * **[!UICONTROL 更新用户]**

      如果选中，会在每次登录时刷新存储库中的用户数据，以反映配置文件更改或请求的其他数据。 默认已取消选中。


#### 后续步骤 {#next-steps}

facebook和Twitter的后续步骤相同：

* [发布云服务配置](#publishcloudservices)
* [为社区站点启用](#enable-social-login)

## twitter登录 {#twitter-login}

### 创建Twitter应用程序 {#create-a-twitter-app}

需要配置的Twitter应用程序才能启用Twitter社交登录。

按照最新说明在处创建新的Twitter应用程序 [https://apps.twitter.com](https://apps.twitter.com/).

一般而言：

1. 输入 *名称* ，该选项会将您的Twitter应用程序标识给网站用户。
1. 输入&#x200B;*说明*.
1. 对象 *网站*  — 输入 `https://<server>`.
1. 对象 *回调URL*  — 输入 `https://server`.

   >[!NOTE]
   >
   >无需指定端口。
   >
   >在开发方面，https://127.0.0.1/将发挥作用。

1. 创建应用程序后，找到 **[!UICONTROL 使用者(API)密钥]** 和 **[!UICONTROL 使用者(API)密码]**. 配置 [twitter cloud service](#createatwittercloudservice).

#### 权限 {#permissions}

在Twitter应用程序管理的权限部分中：

* **[!UICONTROL 访问]**：选择 `Read only`.

   * 不支持其他选项

* **[!UICONTROL 其他权限]**：（可选）选择 `Request email addresses from users`.

   * 如果未选择，则AEM中的用户配置文件将不会包含其电子邮件地址。
   * twitter的说明中说明了需要执行的其他步骤。

对社交登录发出的唯一REST请求是 *[GET帐户/验证凭据](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### 创建Twitter ConnectCloud Service {#create-a-twitter-connect-cloud-service}

此 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 通过创建Cloud Service配置实例化的实例，可标识Twitter应用程序以及添加新用户的成员组。

1. 在创作实例上，使用管理员权限登录。
1. 在全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL twitter社交登录配置]**.
1. 选择 **[!UICONTROL 上下文路径]** 配置。

   上下文路径应与您在创建/编辑社区站点时选择的云配置路径相同。

1. 检查是否已启用上下文路径以在其下方创建云服务。
1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**. 选择上下文并编辑属性。 启用云配置（如果尚未启用）。

   ![twitterconfigpropng](assets/twitterconfigproppng.png)

   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。

1. 创建/编辑Twitter云服务配置。

   ![twittersocialloginping](assets/twittersocialloginpng.png)

   * **[!UICONTROL 标题]**

      (*必需*)输入标识Twitter应用程序的显示标题。 建议使用与输入的相同的名称 *显示名称* 用于Twitter应用程序。

   * **[!UICONTROL 使用者密钥]**

      (*必需*)输入 **使用者(API)密钥** 用于Twitter应用程序。 这样可识别 [AdobeGranite OAuth应用程序和提供程序](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 通过对话框创建的实例。

   * **[!UICONTROL 使用者密钥]**

      (*必需*)输入 ***Consumer(API)密码*** 用于Twitter应用程序。

   * **[!UICONTROL 创建用户]**

      如果选中，使用Twitter帐户登录将创建AEM用户条目，并将其作为成员添加到选定的用户组。 默认选中（强烈推荐）。

   * **[!UICONTROL 隐藏用户 ID]**

      保持取消选中状态。

   * **[!UICONTROL 添加到用户组]**

      选择“添加用户组”以选择一个或多个组 [成员组](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 用户将添加到其中的社区站点。
   >[!NOTE]
   >
   >可以随时添加或删除组。 但现有用户的成员资格不会受到影响。 自动成员资格仅适用于此字段更新后创建的新用户。 对于禁用匿名用户的站点，将用户添加到适用于该已关闭的社区站点的相应社区成员组。

1. 选择 **[!UICONTROL 保存]** 和 **[!UICONTROL Publish]**.

结果是 [AdobeGranite OAuth应用程序和提供程序](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 无需进一步修改的实例。 默认范围是Twitter登录的标准权限。

### AEM Communities Twitter OAuth提供程序 {#aem-communities-twitter-oauth-provider}

AEM Communities配置扩展了 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 实例。 此提供程序需要编辑，以允许用户更新。

如果需要进行编辑，请在每个AEM发布实例上：

1. 使用管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md).

   例如，http://localhost:4503/system/console/configMgr。

1. 找到AEM Communities Twitter OAuth提供程序。
1. 选择铅笔图标以打开进行编辑。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth提供程序ID]**

   (*必需*)默认值为 *soco -twitter*. 不要编辑。

   * **[!UICONTROL Cloud Service配置]**

      默认值为 *会议* 不要编辑。

   * **[!UICONTROL OAuth提供程序服务配置]**

      默认值为 `/apps/social/twitterprovider/config/`。不要编辑。

   * **[!UICONTROL 用户路径]**

      存储库中存储用户数据的位置。 对于社区站点，为确保成员有权查看彼此的配置文件，路径应为默认路径 `/home/users/community`.

   * **[!UICONTROL 启用参数]** 不编辑
   * **[!UICONTROL URL参数]** 不编辑
   * **[!UICONTROL 更新用户]**

      如果选中，会在每次登录时刷新存储库中的用户数据，以反映配置文件更改或请求的其他数据。 默认值为取消选中。


#### 后续步骤 {#next-steps-1}

facebook和Twitter的后续步骤相同：

* [发布云服务配置](#publishcloudservices)
* [为社区站点启用](#enable-social-login)

## 启用社交登录 {#enable-social-login}

### AEM Communities Sites控制台 {#aem-communities-sites-console}

配置云服务后，可以使用为社区站点的相关社交登录设置启用该服务 [User Management](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) 社区站点期间的设置子面板 [创建](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) 或 [管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. 选择保存社交登录配置的站点配置上下文。

1. 在常规选项卡上，设置云配置。

   ![managesites_png](assets/managesites_png.png)

1. 在设置选项卡上，启用 **[!UICONTROL 社交登录]** 并保存。

   ![usermgmt_png](assets/usermgmt_png.png)

## 测试社交登录 {#test-social-login}

* 确保 [AdobeGranite OAuth身份验证处理程序](#adobe-granite-oauth-authentication-handler) 已在所有发布实例上启用。
* 确保已发布云服务。
* 确保已发布社区站点。
* 在浏览器中启动已发布的站点。
例如， http://localhost:4503/content/sites/engage/en.html
* 选择 **[!UICONTROL 登录]**.
* 选择 **[!UICONTROL 使用Facebook登录]** 或 **[!UICONTROL 使用Twitter登录]**.
* 如果尚未登录Facebook或Twitter，请使用相应的凭据登录。
* 根据Facebook或Twitter应用程序显示的对话框，可能需要授予权限。
* 请注意，页面顶部的工具栏已更新以反映成功登录。
* 选择 **[!UICONTROL 个人资料]**：配置文件页面显示用户的头像图像、名字和姓氏。 它还根据允许的字段/参数显示Facebook或Twitter配置文件中的信息。

## AEM平台OAuth配置 {#aem-platform-oauth-configurations}

### AdobeGranite OAuth身份验证处理程序 {#adobe-granite-oauth-authentication-handler}

此 `Adobe Granite OAuth Authentication Handler` 默认未启用，并且 ***必须在所有AEM发布实例上启用。***

要在发布时启用身份验证处理程序，只需打开OSGi配置并保存它即可：

* 使用管理员权限登录。
* 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md).
例如， http://localhost:4503/system/console/configMgr
* 查找 `Adobe Granite OAuth Authentication Handler`.
* 选择以打开配置进行编辑。
* 选择&#x200B;**[!UICONTROL 保存]**。

![graniteoauth](assets/graniteoauth.png)

>[!CAUTION]
>
>请注意不要将身份验证处理程序与的Facebook或Twitter实例混淆 *AdobeGranite OAuth应用程序和提供程序*.

![graniteoauth1](assets/graniteoauth1.png)

### AdobeGranite OAuth应用程序和提供程序 {#adobe-granite-oauth-application-and-provider}

创建Facebook或Twitter的云服务时，实例 `Adobe Granite OAuth Authentication Handler` 创建。

要找到为Facebook或Twitter应用程序创建的实例，请执行以下操作：

1. 使用管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md).

   例如，http://localhost:4503/system/console/configMgr。

1. 找到AdobeGranite OAuth应用程序和提供程序。

   * 查找实例，其中 **[!UICONTROL 客户端ID]** 匹配 **[!UICONTROL 应用程序ID]**.

      ![graniteoauth2](assets/graniteoauth2.png)

      除以下属性外，配置的其他属性保持不变：

   * **[!UICONTROL 配置ID]**

      (*必需*) OAuth配置ID必须是唯一的。 在创建云服务时自动生成。

   * **[!UICONTROL 客户端 ID]**

      (*必需*)创建云服务时提供的应用程序ID。

   * **[!UICONTROL 客户端密钥]**

      (*必需*)创建云服务时提供的应用程序密码。

   * **[!UICONTROL 范围]**

      (*可选*)可从提供商处请求额外的允许范围。 默认范围包括提供社交身份验证和配置文件数据所需的权限。

   * **[!UICONTROL 提供程序ID]**

      (*必需*)AEM Communities的提供程序ID是在创建云服务时设置的。 不要编辑。 对于Facebook Connect，值为 *soco -facebook*. 对于Twitter Connect，值为 *soco -twitter*.

   * **[!UICONTROL 组]**

      (*推荐*)将创建的用户添加到的一个或多个成员组。 对于AEM Communities，建议列出社区站点的成员组。

   * **[!UICONTROL 回调 URL]**

      (*可选*)使用OAuth提供程序配置的URL，用于将客户端重定向回。 使用相对URL可使用原始请求的主机。 留空将改用最初请求的URL。 后缀“/callback/j_security_check”会自动附加到此URL 。
   >[!NOTE]
   >
   >回调的域必须向提供商(Facebook或Twitter)注册。

对于每个OAuth身份验证处理程序配置，在实例中创建了其他两个配置：

* Apache Jackrabbit Oak Default Sync Handler (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) — 此处不需要编辑，但您可以查看用户字段映射，了解Facebook字段如何映射到CQ用户配置文件节点。 另请注意，“同步处理程序名称”与OAuth提供程序配置的配置ID匹配。
* Apache Jackrabbit Oak外部登录模块(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) — 此处不需要编辑，但您可能会注意到“身份提供程序名称”和“同步处理程序名称”相同，分别指向相应的OAuth和同步处理程序配置。

有关更多信息，请参阅 [使用Apache Oak外部登录模块进行身份验证](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## OAuth用户遍历性能 {#oauth-user-traversal-performance}

对于数十万用户使用其Facebook或Twitter登录名注册的社区网站，可通过添加以下Oak索引来提高网站访客使用其社交登录名时执行的查询的遍历性能。

如果日志中出现遍历警告，建议添加此索引。

在创作实例上，使用管理权限登录：

1. 从全局导航：选择 **工具， [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. 从ntBaseLucene副本创建一个名为ntBaseLucene-oauth的索引：

   * 在节点下 `/oak:index`
   * 选择节点 `ntBaseLucene`
   * 选择 **[!UICONTROL 复制]**
   * 选择 `/oak:index`
   * 选择 **[!UICONTROL 粘贴]**
   * 将ntBaseLucene的副本重命名为 `ntBaseLucene-oauth`

1. 修改node ntBaseLucene-oauth的属性：

   * **[!UICONTROL indexPath]**： `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**： `oauthid-123****`
   * **[!UICONTROL 重新索引]**： `true`
   * **[!UICONTROL reindexCount]**： `1`

1. 在节点/oak：index/ntBaseLucene-oauth/indexRules/nt：base/properties下：

   * 删除除cqTags之外的所有子节点。
   * 将cqTags重命名 `oauthid-123****`
   * 修改节点的属性 `oauthid-123****`

      * **[!UICONTROL name]**： `oauthid-123****`
   * 选择 **[!UICONTROL 全部保存]**.


* 对于 **name** `oauthid-123`，替换 *123* 使用Facebook ***应用程序ID*** 或Twitter ***使用者(API)密钥*** 这就是 **客户端ID** 在 [AdobeGranite OAuth应用程序和提供程序](social-login.md#adobe-granite-oauth-application-and-provider) 配置。

   ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

有关其他信息和工具，请参阅 [Oak查询和索引](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher配置 {#dispatcher-configuration}

参见 [为社区配置Dispatcher](dispatcher.md).
