---
title: 使用Facebook和Twitter进行社交登录
seo-title: 使用Facebook和Twitter进行社交登录
description: 社交登录允许网站访客使用其Facebook或Twitter帐户登录。
seo-description: 社交登录允许网站访客使用其Facebook或Twitter帐户登录。
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2787'
ht-degree: 1%

---


# 使用Facebook和Twitter进行社交登录 {#social-login-with-facebook-and-twitter}

社交登录是一种功能，用于向站点访客显示使用其Facebook或Twitter帐户登录的选项。 因此，在AEM成员用户档案中包括允许的Facebook或Twitter数据。

![socialloginweretail](assets/socialloginweretail.png)

## 社交登录概述 {#social-login-overview}

要包含社交登录，需要 *创建* 自定义Facebook和Twitter应用程序。

虽然we-retail示例提供Facebook和Twitter应用程序及云服务示例，但生产网站上不提供 [这些示例](../../help/sites-administering/production-ready.md)。

所需的步骤包括：

1. [对所有AEM发布实例](#adobe-granite-oauth-authentication-handler) 启用OAuth身份验证。

   未启用OAuth，尝试登录失败。

1. **创建** 社交应用程序和云服务。

   * 要支持使用Facebook登录：

      * 创建Facebook [应用程序](#create-a-facebook-app)。
      * 创建和发 [布Facebook Connect云服务](#create-a-facebook-connect-cloud-service)。
   * 要支持使用Twitter登录，请执行以下操作：

      * 创建Twitter [应用程序](#create-a-twitter-app)。
      * 创建和发布 [Twitter Connect云服务](#create-a-twitter-connect-cloud-service)。


1. [**为社区** 站点启用](#enable-social-login) “社交登录”。

有两个基本概念：

1. **范围** （权限）指定允许应用程序请求的数据。

   * 默认情况下，Facebook和Twitter [AdobeGranite OAuth应用程序和提供者实例](#adobe-granite-oauth-application-and-provider) ，在其范围内包括基本的应用程序权限。

1. **字段** （参数）指定使用URL参数请求的实际数据。

   * 这些字段在AEM Communities [Facebook OAuth提供者和](#aem-communities-facebook-oauth-provider)[AEM CommunitiesTwitter OAuth提供者中指定](#aem-communities-twitter-oauth-provider)。
   * 默认字段对于大多数用例来说已足够，但可以修改。

## Facebook登录 {#facebook-login}

### Facebook API版本 {#facebook-api-version}

社交登录和we-retail Facebook示例是在Facebook Graph API版本1.0时开发的。自AEM 6.4 GA和AEM 6.3 SP1社交登录更新以与较新的Facebook Graph API 2.5版本一起使用。

>[!NOTE]
>
>对于较旧的AEM版本，如果您在日志中遇到 **异常。无法从中提取令牌**，请升级到该AEM版本的最新CFP。

有关Facebook Graph API版本信息，请参 [阅Facebook API更改日志](https://developers.facebook.com/docs/apps/changelog)。

### 创建Facebook应用程序 {#create-a-facebook-app}

需要正确配置的Facebook应用程序才能启用Facebook社交登录。

要创建Facebook应用程序，请按照Facebook的说明，网址为 [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/)。 对其说明所做的更改不会反映在以下信息中。

通常，从Facebook API v2.7开始：

* *添加新Facebook应用程序*
   * 对于 *平台*，选择网站：
      * 对于 *站点URL*，输入 `  https://<server>:<port>.`
      * 在“ *显示名称*”中，输入一个标题以用作Facebook连接服务的标题。
      * 对于 *类别*，建议选择“ *页面应用程序*”，但可以是任何内容。
      * *添加产品： Facebook登录*
      * 对于 *有效的OAuth重定向URI*，请输入 `  https://<server>:<port>.`

>[!NOTE]
>
>对于开发，http://localhost:4503将起作用。

创建应用程序后，找到“应用 **[!UICONTROL 程序ID]** ”和“ **[!UICONTROL 应用程序机密]** ”设置。 配置Facebook云服务时需 [要此信息](#createafacebookcloudservice)。

### 创建Facebook ConnectCloud Service {#create-a-facebook-connect-cloud-service}

通过 [](#adobe-granite-oauth-application-and-provider) 创建云服务配置实例化的AdobeGranite OAuth应用程序和提供程序实例，标识新用户所添加的Facebook应用程序和成员组。

1. 在AEM作者实例上，以管理员权限登录。
1. 从全局导航中，选 **[!UICONTROL 择工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Facebook社交登录配置]**。
1. 选择配置上 **[!UICONTROL 下文路径]**。

   **[!UICONTROL 上下文路径]** 应与您在创建／编辑社区站点时选择的云配置路径相同。

1. 检查您的上下文路径是否已启用以在其下创建云服务。
1. 转至“工 **[!UICONTROL 具]** ”>“ **[!UICONTROL 常规]** ” **[!UICONTROL >“配]**&#x200B;置浏览器”。 选择上下文并编辑属性。 启用云配置（如果尚未启用）。

   ![config-propertiespng](assets/config-propertiespng.png)

1. **创建／编辑** Facebook云服务配置。

   ![fsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL 标题]** (*必需*)输入标识Facebook应用程序的显示标题。 建议使用与Facebook应用程序的“显 *示名称* ”输入的名称。
   * **[!UICONTROL 应用程序ID/API密钥]***(*&#x200B;必需 ***)输入*** Facebook应用程序的应用程序ID。 它标识从对 [话框创建的AdobeGranite OAuth应用程序和](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) Provider实例。
   * **[!UICONTROL 应用程序密]** 码(*必需*)输入Facebook应 ***用程序的*** 应用程序密码。
   * **[!UICONTROL 创建用户]** 如果选中此项，则使用Facebook帐户登录将创建AEM用户条目，并将其作为成员添加到所选用户组。  默认为选中（强烈推荐）。
   * **[!UICONTROL 掩码用户ID]**:取消选择。
   * **[!UICONTROL 范围电子邮件]**:应从Facebook获取用户的电子邮件id。
   * **[!UICONTROL 添加到用户组]** ，选择“添加用户组”，为要向其 [添加用户的社](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 区站点，选择一个或多个成员组。

   >[!NOTE]
   >
   >可随时添加或删除组。 但现有用户的会员资格不会受到影响。 自动会员资格仅适用于更新此字段后创建的新用户。 对于禁用匿名用户的站点，选择将用户添加到该封闭的社区站点对应的社区成员组。

   * Select **[!UICONTROL SAVE]**.
   * **[!UICONTROL 发布]**.



结果是一个 [AdobeGranite OAuth应用程序和提供程序实例](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) ，除非添加其他范围（权限），否则不需要进一步修改。 默认范围是Facebook登录的标准权限。 如果需要其他范围，则需要直接编辑OSGI配置。 如果有修改直接通过系统／控制台完成，请避免从触屏UI编辑云服务配置以避免覆盖。

### AEM CommunitiesFacebook OAuth提供商 {#aem-communities-facebook-oauth-provider}

AEM Communities提供程序扩展 [了AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 实例。

此提供者需要编辑才能：

* 允许用户更新
* 在范围内添加 [其他字段](#adobe-granite-oauth-application-and-provider)

   * 默认情况下，并非所有默认允许的字段都包含在内。

如果需要编辑，请在每个AEM发布实例上：

1. 以管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md)。 例如，http://localhost:4503/system/console/configMgr。
1. 找到AEM CommunitiesFacebook OAuth提供商。
1. 选择要打开进行编辑的铅笔图标。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth提供者ID]**

      (*必需*)默认值 *为soco -facebook*。 不要编辑。

   * **[!UICONTROL Cloud Service配置]**

      默认值为 `/etc/  cloudservices /  facebookconnect`. 不要编辑。

   * **[!UICONTROL OAuth提供程序服务配置]**

      默认值为 `/apps/social/facebookprovider/config/`. 不要编辑。

   * **[!UICONTROL 启用标记]**

      请勿编辑。

   * **[!UICONTROL 用户路径]**

      存储用户数据的存储库中的位置。 对于社区站点，要确保成员能够视图彼此的用户档案，路径应为默 *认/home/users/community*。

   * **[!UICONTROL 启用字段]**

      如果选中，则在向Facebook发出请求时指定列出的字段，以供用户验证和获取信息。 将取消选择默认值。

   * **[!UICONTROL 字段]**

      启用“字段”后，调用Facebook图形API时将包括以下字段。 必须允许在云服务配置中定义的范围内使用这些字段。 其他字段可能需要Facebook批准。 引用Facebook文档的“Facebook登录权限”部分。 作为参数添加的默认字段为：

      * id
      * 名称
      * first_name
      * last_name
      * 链接
      * 区域设置
      * 图片
      * 时区
      * updated_time
      * 已验证
      * 电子邮件

   如果添加或更改了任何字段，请更新相应的默认同步处理程序配置以更正映射。

   * **[!UICONTROL 更新用户]**

      如果选中此项，则每次登录时都会刷新存储库中的用户数据，以反映用户档案更改或请求的其他数据。 “默认”(Default)为取消选择。


#### 后续步骤 {#next-steps}

Facebook和Twitter的后续步骤相同：

* [发布云服务配置](#publishcloudservices)
* [为社区站点启用](#enable-social-login)

## Twitter登录 {#twitter-login}

### 创建Twitter应用程序 {#create-a-twitter-app}

需要配置的Twitter应用程序才能启用Twitter社交登录。

请按照最新说明，在https://apps.twitter.com上新建一个Twitter应 [用程序](https://apps.twitter.com/)。

一般而言：

1. 输入一 *个名称* ，该名称将向网站的用户标识您的Twitter应用程序。
1. 输入&#x200B;*说明*.
1. 对于 *网站* -输入 `https://<server>`。
1. 对于 *回呼URL* —— 输入 `https://server`。

   >[!NOTE]
   >
   >无需指定端口。
   >
   >对于开发，https://127.0.0.1/将起作用。

1. 创建应用程序后，找到 **[!UICONTROL 消费者(API)密钥]****[!UICONTROL 和消费者(API)机密]**。 配置Twitter云服务时需 [要此信息](#createatwittercloudservice)。

#### 权限 {#permissions}

在Twitter应用程序管理员的权限部分：

* **[!UICONTROL 访问]**:选择 `Read only`。

   * 不支持其他选项

* **[!UICONTROL 其他权限]**:（可选）选 `Request email addresses from users`择。

   * 如果未选择，AEM中的用户用户档案将不包括其电子邮件地址。
   * Twitter的说明说明需要采取其他步骤。

对社交登录发出的唯一REST请求是 *[GET帐户／验证凭据](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*。

### 创建Twitter ConnectCloud Service {#create-a-twitter-connect-cloud-service}

通过 [](#adobe-granite-oauth-application-and-provider) 创建云服务配置实例化的AdobeGranite OAuth应用程序和提供程序实例，标识新用户所添加的Twitter应用程序和成员组。

1. 在创作实例上，使用管理员权限登录。
1. 从全局导航中，选 **[!UICONTROL 择工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Twitter社交登录配置]**。
1. 选择上 **[!UICONTROL 下文路径]** 配置。

   上下文路径应与您在创建／编辑社区站点时选择的云配置路径相同。

1. 检查您的上下文路径是否已启用以在其下创建云服务。
1. 转至“工 **[!UICONTROL 具]** ”>“ **[!UICONTROL 常规]** ” **[!UICONTROL >“配]**&#x200B;置浏览器”。 选择上下文并编辑属性。 启用云配置（如果尚未启用）。

   ![twitterconfigpropping](assets/twitterconfigproppng.png)

1. 创建／编辑Twitter云服务配置。

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL 标题]**

      (必&#x200B;*需*)输入标识Twitter应用程序的显示标题。 建议使用与Twitter应用程序的“显 *示名称* ”输入的名称。

   * **[!UICONTROL 使用者密钥]**

      (*必需*)输入 **Twitter应用程序的消费者** (API)密钥。 它标识从对 [话框创建的AdobeGranite OAuth应用程序和](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) Provider实例。

   * **[!UICONTROL 使用者密钥]**

      (*必需*)输入 ***Twitter应用程序的消费者*** (API)机密。

   * **[!UICONTROL 创建用户]**

      如果选中此项，则使用Twitter帐户登录将创建AEM用户条目，并将其作为成员添加到所选用户组。 默认为选中（强烈推荐）。

   * **[!UICONTROL 隐藏用户 ID]**

      取消选择。

   * **[!UICONTROL 添加到用户组]**

      选择“添加用户组”，为要向其 [添加用户](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 的社区站点选择一个或多个成员组。
   >[!NOTE]
   >
   >可随时添加或删除组。 但现有用户的会员资格不会受到影响。 自动会员资格仅适用于更新此字段后创建的新用户。 对于禁用匿名用户的站点，将用户添加到用于该封闭社区站点的相应社区成员组。

1. 选择 **[!UICONTROL 保存]** 和 **[!UICONTROL 发布]**。

结果是一个 [AdobeGranite OAuth应用程序和提供程序实例](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) ，无需进一步修改。 默认范围是Twitter登录的标准权限。

### AEM CommunitiesTwitter OAuth提供者 {#aem-communities-twitter-oauth-provider}

AEM Communities配置扩展了 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 实例。 此提供程序需要编辑才能允许用户更新。

如果需要编辑，请在每个AEM发布实例上：

1. 以管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   例如，http://localhost:4503/system/console/configMgr。

1. 找到AEM CommunitiesTwitter OAuth提供者。
1. 选择要打开进行编辑的铅笔图标。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth提供者ID]**

   (*必需*)默认值 *为soco -twitter*。 不要编辑。

   * **[!UICONTROL Cloud Service配置]**

      The default value is *conf.* 不要编辑。

   * **[!UICONTROL OAuth提供程序服务配置]**

      默认值为 `/apps/social/twitterprovider/config/`. 不要编辑。

   * **[!UICONTROL 用户路径]**

      存储用户数据的存储库中的位置。 对于社区站点，要确保成员能够视图彼此的用户档案，路径应为默认路径 `/home/users/community`。

   * **[!UICONTROL 启用参数]** ，不进行编辑
   * **[!UICONTROL URL参数]** 不编辑
   * **[!UICONTROL 更新用户]**

      如果选中此项，则每次登录时都会刷新存储库中的用户数据，以反映用户档案更改或请求的其他数据。 将取消选择默认值。


#### 后续步骤 {#next-steps-1}

Facebook和Twitter的后续步骤相同：

* [发布云服务配置](#publishcloudservices)
* [为社区站点启用](#enable-social-login)

## 启用社交登录 {#enable-social-login}

### AEM Communities站点控制台 {#aem-communities-sites-console}

配置云服务后，在创建或管理社区站点时，可以使用“用户管理设置”子面板为社 [区站点启用相](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) 关的 [“社交登录](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) ” [设置](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties)。

1. 选择保存社交登录配置的站点配置上下文。

1. 在“常规”选项卡上，设置云配置。

   ![managesites_png](assets/managesites_png.png)

1. 在“设置”选项卡上，启 **[!UICONTROL 用“社交登录]** ”并保存。

   ![usermgmt_png](assets/usermgmt_png.png)

## 测试社交登录 {#test-social-login}

* 确保 [已在所有发布实例上启用Adobe](#adobe-granite-oauth-authentication-handler) Granite OAuth身份验证处理程序。
* 确保已发布云服务。
* 确保已发布社区站点。
* 在浏览器中启动已发布的站点。
例如，http://localhost:4503/content/sites/engage/en.html
* 选择 **[!UICONTROL 登录]**。
* 选择“ **[!UICONTROL 使用Facebook登录]** ” **[!UICONTROL 或“使用Twitter登录”]**。
* 如果尚未登录到Facebook或Twitter，请使用相应的凭据登录。
* 可能需要根据Facebook或Twitter应用程序显示的对话框授予权限。
* 请注意，页面顶部的工具栏会更新以反映成功登录。
* 选择 **[!UICONTROL 用户档案]**:用户档案页显示用户的头像图像、名字和姓氏。 它还根据允许的字段／参数显示Facebook或Twitter用户档案中的信息。

## AEM平台OAuth配置 {#aem-platform-oauth-configurations}

### AdobeGranite OAuth身份验证处理程序 {#adobe-granite-oauth-authentication-handler}

默 `Adobe Granite OAuth Authentication Handler` 认情况下不启用，并且必 ***须在所有AEM发布实例上启用。***

要在发布时启用身份验证处理程序，只需打开OSGi配置并保存它：

* 以管理员权限登录。
* 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md)。
例如，http://localhost:4503/system/console/configMgr
* 找到 `Adobe Granite OAuth Authentication Handler`。
* 选择以打开要编辑的配置。
* 选择&#x200B;**[!UICONTROL 保存]**。

![chlimage_1-489](assets/chlimage_1-489.png)

>[!CAUTION]
>
>请注意，不要将身份验证处理程序与AdobeGranite OAuth应用程序和提供者的 *Facebook或Twitter实例混淆*。

![chlimage_1-490](assets/chlimage_1-490.png)

### AdobeGranite OAuth应用程序和提供程序 {#adobe-granite-oauth-application-and-provider}

创建Facebook或Twitter的云服务时，将创建实例 `Adobe Granite OAuth Authentication Handler` 的实例。

要查找Facebook或Twitter应用程序的已创建实例，请执行以下操作：

1. 以管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   例如，http://localhost:4503/system/console/configMgr。

1. 找到AdobeGranite OAuth应用程序和提供程序。

   * 找到客户端 **[!UICONTROL ID与应用]** ID匹 **[!UICONTROL 配的实例]**。

      ![chlimage_1-491](assets/chlimage_1-491.png)

      除以下属性外，保留配置的其他属性：

   * **[!UICONTROL 配置ID]**

      (必&#x200B;*需*)OAuth配置ID必须唯一。 创建云服务时自动生成。

   * **[!UICONTROL 客户端 ID]**

      (*必需*)创建云服务时提供的应用程序 ID。

   * **[!UICONTROL 客户端密钥]**

      (*必需*)创建云服务时提供的应用程序密码。

   * **[!UICONTROL 范围]**

      (可&#x200B;*选*)可从提供商那里询问允许的其他范围。 默认范围涵盖提供社交身份验证和用户档案数据所需的权限。

   * **[!UICONTROL 提供者ID]**

      (*必需*)创建云服务时，将设置AEM Communities的提供程序ID。 不要编辑。 对于Facebook Connect，此值为 *soco -facebook*。 对于Twitter Connect，此值为 *soco -twitter*。

   * **[!UICONTROL 组]**

      (建&#x200B;*议*)将创建的用户添加到的一个或多个成员组。 对于AEM Communities，建议列表社区站点的成员组。

   * **[!UICONTROL 回调 URL]**

      (可&#x200B;*选*)为OAuth提供者配置的URL，用于将客户端重定向回。 使用相对url来使用原始请求的主机。 留空将改用最初请求的URL。 后缀“/callback/j_security_check”自动附加到此url。
   >[!NOTE]
   >
   >回调的域必须向提供者（Facebook或Twitter）注册。

对于每个OAuth身份验证处理程序配置，在实例中创建了两个其他配置：

* Apache Jackrabbit Oak默认同步处理程序(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler)-无需进行任何编辑，但您可以查看用户字段映射Facebook字段如何映射到CQ用户用户档案节点。 另请注意，“Sync Handler Name”与OAuth提供程序配置的配置ID匹配。
* Apache Jackrabbit Oak外部登录模块(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory)-无需进行任何编辑，但您可能会注意到“标识提供者名称”和“同步处理程序名称”是相同的，并分别指向相应的OAuth和同步处理程序配置。

有关详细信息，请参 [阅使用Apache Oak外部登录模块进行身份验证](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)。

## OAuth用户遍历性能 {#oauth-user-traversal-performance}

对于使用Facebook或Twitter登录名注册的社区站点，当站点访客使用其社交登录名时执行的查询的遍历性能可以通过添加以下Oak索引而得到改善。

如果日志中显示遍历警告，则建议添加此索引。

在作者实例上，以管理权限登录：

1. 从全局导航：选 **择工[具、CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md)。**
1. 从ntBaseLucene的副本创建名为ntBaseLucene-oauth的索引：

   * 在节点下 `/oak:index`
   * 选择节点 `ntBaseLucene`
   * 选择复 **[!UICONTROL 制]**
   * 选择 `/oak:index`
   * 选择粘 **[!UICONTROL 贴]**
   * 将ntBaseLucene的副本重命名为 `ntBaseLucene-oauth`

1. 修改节点ntBaseLucene-oauth的属性：

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**: `oauthid-123****`
   * **[!UICONTROL 重新索引]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. 在节点/oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties下：

   * 删除除cqTags外的所有子节点。
   * 将cqTags重命名为 `oauthid-123****`
   * 修改节点的属性 `oauthid-123****`

      * **[!UICONTROL name]**: `oauthid-123****`
   * 选择 **[!UICONTROL 全部保存]**。


* 对于名 **称** ，将123 `oauthid-123`替换为Facebook ID *或Twitter ID(API)KeyPai：在AdobeGranite Granite Uth Application和Facebook配置中，Client Id为Adobe Client Id客户端ID的值的Facebook* ID或TwitterAPI ****************[](social-login.md#adobe-granite-oauth-application-and-provider) KeyKeyPremin。

   ![chlimage_1-492](assets/chlimage_1-492.png)

有关其他信息和工具，请参 [阅Oak查询和索引](../../help/sites-deploying/queries-and-indexing.md)。

## Dispatcher Configuration {#dispatcher-configuration}

请参 [阅配置Dispatcher for Communities](dispatcher.md)。
