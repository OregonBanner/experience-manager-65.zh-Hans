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
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2804'
ht-degree: 1%

---


# 使用Facebook和Twitter进行社交登录{#social-login-with-facebook-and-twitter}

社交登录是一种功能，用于向站点访客演示使用其Facebook或Twitter帐户登录的选项。 因此，在其AEM会员用户档案中包含允许的Facebook或Twitter数据。

![socialoginweretail](assets/socialloginweretail.png)

## 社交登录概述{#social-login-overview}

要包含社交登录，创建自定义Facebook和Twitter应用程序时需要&#x200B;**。

尽管we-retail示例提供示例Facebook和Twitter应用程序及云服务，但在[生产网站](../../help/sites-administering/production-ready.md)上不提供。

所需步骤包括：

1. [对所有AEM发](#adobe-granite-oauth-authentication-handler) 布实例启用OAuth身份验证。

   未启用OAuth，尝试登录失败。

1. **创** 建社交应用程序和云服务。

   * 要支持使用Facebook登录，请执行以下操作：

      * 创建[Facebook应用程序](#create-a-facebook-app)。
      * 创建并发布[Facebook Connect云服务](#create-a-facebook-connect-cloud-service)。
   * 要支持使用Twitter登录，请执行以下操作：

      * 创建[Twitter应用程序](#create-a-twitter-app)。
      * 创建并发布[Twitter Connect云服务](#create-a-twitter-connect-cloud-service)。


1. [**启** 用社](#enable-social-login) 区站点的社交登录。

有两个基本概念：

1. **范围** （权限）指定允许应用程序请求的数据。

   * 默认情况下，Facebook和Twitter [AdobeGranite OAuth应用程序和Provider](#adobe-granite-oauth-application-and-provider)实例在其范围内包含基本应用程序权限。

1. **Fields** (params)指定使用URL参数请求的实际数据。

   * 这些字段在[AEM Communities Facebook OAuth提供者](#aem-communities-facebook-oauth-provider)和[AEM Communities Twitter OAuth提供者](#aem-communities-twitter-oauth-provider)中指定。
   * 对于大多数用例，默认字段已足够，但可以修改。

## Facebook登录{#facebook-login}

### Facebook API版本{#facebook-api-version}

在Facebook Graph API为1.0版时，开发了社交登录和we-retail Facebook示例。
自AEM 6.4 GA和AEM 6.3 SP1社交登录开始更新，可与较新的Facebook Graph API 2.5版本一起使用。

>[!NOTE]
>
>对于较早的AEM版本，如果日志&#x200B;**中遇到异常，则无法从此**&#x200B;提取令牌，请升级到该AEM版本的最新CFP。

有关Facebook图形API版本信息，请参阅[Facebook API changelog](https://developers.facebook.com/docs/apps/changelog)。

### 创建Facebook应用程序{#create-a-facebook-app}

需要正确配置的Facebook应用程序才能启用Facebook社交登录。

要创建Facebook应用程序，请按照Facebook的说明操作，网址为[https://developers.facebook.com/apps/](https://developers.facebook.com/apps/)。 以下信息不会反映对其说明所做的更改。

通常，自Facebook API v2.7起：

* *添加新Facebook应用程序*
   * 对于&#x200B;*Platform*，选择“网站：
      * 对于&#x200B;*站点URL*，输入`  https://<server>:<port>.`
      * 对于&#x200B;*显示名称*，输入用作Facebook连接服务标题的标题。
      * 对于&#x200B;*类别*，建议选择&#x200B;*页面应用程序*，但可以是任何内容。
      * *添加产品：Facebook登录*
      * 对于&#x200B;*有效的OAuth重定向URI*，请输入`  https://<server>:<port>.`

>[!NOTE]
>
>对于开发，http://localhost:4503将起作用。

创建应用程序后，找到&#x200B;**[!UICONTROL App ID]**&#x200B;和&#x200B;**[!UICONTROL App Secret]**&#x200B;设置。 配置[Facebook云服务](#createafacebookcloudservice)时需要此信息。

### 创建Facebook ConnectCloud Service{#create-a-facebook-connect-cloud-service}

通过创建云服务配置实例化的[AdobeGranite OAuth应用程序和Provider](#adobe-granite-oauth-application-and-provider)实例标识Facebook应用程序和新用户所添加的成员组。

1. 在AEM作者实例上，使用管理员权限登录。
1. 在全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Facebook Social登录配置]**。
1. 选择配置&#x200B;**[!UICONTROL 上下文路径]**。

   **[!UICONTROL 上]** 下文路径应与您在创建/编辑社区站点时选择的云配置路径相同。

1. 检查您的上下文路径是否已启用以在其下方创建云服务。
1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。 选择上下文并编辑属性。 如果未启用，请启用云配置。

   ![config-propertiespng](assets/config-propertiespng.png)

   * 有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。

1. **创建/** 编辑Facebook云服务配置。

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL 标题]** (*必需*)输入标识Facebook应用程序的显示标题。建议使用与Facebook应用程序的&#x200B;*显示名称*&#x200B;输入的相同名称。
   * **[!UICONTROL 应用程序ID/API密钥]** (*必需*)输 ***入*** Facebook应用程序的应用程序ID。它标识从对话框创建的[AdobeGranite OAuth应用程序和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider)实例。
   * **[!UICONTROL App Secret]** (必&#x200B;*需*)输入 ***Facebook应*** 用程序的App Secret。
   * **[!UICONTROL 创]** 建用户如果选中，使用Facebook帐户登录将创建AEM用户条目，并将其作为成员添加到选定用户组。选中默认值（强烈建议）。
   * **[!UICONTROL 蒙版用户ID]**:不选。
   * **[!UICONTROL 范围电子邮件]**:应从Facebook中获取用户的电子邮件id。
   * **[!UICONTROL 添加到用]** 户组选择“添加用户组”，为要向其添加 [用](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 户的社区站点选择一个或多个成员组。

   >[!NOTE]
   >
   >可随时添加或删除组。 但现有用户的会员资格不会受到影响。 自动会员资格仅适用于更新此字段后创建的新用户。 对于禁用匿名用户的站点，选择将用户添加到针对该已关闭的社区站点的相应社区成员组。

   * 选择&#x200B;**[!UICONTROL 保存]**。
   * **[!UICONTROL 发布]**.



结果是一个[AdobeGranite OAuth应用程序和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider)实例，除非添加其他范围（权限），否则不需要进一步修改。 默认范围是Facebook登录的标准权限。 如果需要其他范围，则需要直接编辑OSGI配置。 如果有修改可直接通过系统/控制台进行，请避免在触屏UI中编辑您的云服务配置以避免覆盖。

### AEM Communities Facebook OAuth提供程序{#aem-communities-facebook-oauth-provider}

AEM Communities提供程序扩展了[AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider)实例。

此提供者需要编辑才能：

* 允许用户更新
* 在作用域](#adobe-granite-oauth-application-and-provider)内添加其他字段[

   * 默认情况下，并非所有默认允许的字段都包含在内。

如果需要编辑，请在每个AEM发布实例上：

1. 使用管理员权限登录。
1. 导航到[Web控制台](../../help/sites-deploying/configuring-osgi.md)。 例如，http://localhost:4503/system/console/configMgr。
1. 找到AEM Communities Facebook OAuth提供者。
1. 选择要打开进行编辑的铅笔图标。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth提供程序ID]**

      （*必需*）默认值为&#x200B;*soco -facebook*。 不要编辑。

   * **[!UICONTROL Cloud Service配置]**

      默认值为 `/etc/  cloudservices /  facebookconnect`. 不要编辑。

   * **[!UICONTROL OAuth提供程序服务配置]**

      默认值为 `/apps/social/facebookprovider/config/`. 不要编辑。

   * **[!UICONTROL 启用标记]**

      请勿编辑。

   * **[!UICONTROL 用户路径]**

      存储用户数据的存储库中的位置。 对于社区站点，要确保成员能够视图彼此的用户档案，路径应为默认的&#x200B;*/home/users/community*。

   * **[!UICONTROL 启用字段]**

      如果选中，则在向Facebook发出请求时指定列出的字段，以供用户验证和获取信息。 将取消选择默认值。

   * **[!UICONTROL 字段]**

      启用“字段”后，在调用Facebook Graph API时，将包含以下字段。 必须在云服务配置中定义的范围内允许这些字段。 其他字段可能需要Facebook批准。 引用Facebook文档的“Facebook登录权限”部分。 作为参数添加的默认字段为：

      * id
      * name
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

      如果选中，则每次登录时都会刷新存储库中的用户数据，以反映用户档案更改或请求的其他数据。 “默认”为取消选择状态。


#### 后续步骤{#next-steps}

Facebook和Twitter的后续步骤相同：

* [发布云服务配置](#publishcloudservices)
* [为社区站点启用](#enable-social-login)

## Twitter登录{#twitter-login}

### 创建Twitter应用程序{#create-a-twitter-app}

需要配置的Twitter应用程序才能启用Twitter社交登录。

按照最新说明，在[https://apps.twitter.com](https://apps.twitter.com/)创建新的Twitter应用程序。

一般而言：

1. 输入&#x200B;*名称*，以便将您的Twitter应用程序标识给您网站的用户。
1. 输入&#x200B;*说明*.
1. 对于&#x200B;*website* — 输入`https://<server>`。
1. 对于&#x200B;*回调URL* — 输入`https://server`。

   >[!NOTE]
   >
   >无需指定端口。
   >
   >对于开发，https://127.0.0.1/将起作用。

1. 创建应用程序后，找到&#x200B;**[!UICONTROL Consumer(API)Key]**&#x200B;和&#x200B;**[!UICONTROL Consumer(API)Secret]**。 配置[Twitter云服务](#createatwittercloudservice)时需要此信息。

#### 权限 {#permissions}

在Twitter应用程序管理的权限部分：

* **[!UICONTROL 访问]**:选择 `Read only`。

   * 不支持其他选项

* **[!UICONTROL 其他权限]**:（可选）选 `Request email addresses from users`择。

   * 如果未选择，AEM中的用户用户档案将不包括其电子邮件地址。
   * Twitter的说明说明需要采取其他步骤。

对社交登录的唯一REST请求是&#x200B;*[GET帐户/验证凭据](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*。

### 创建Twitter ConnectCloud Service{#create-a-twitter-connect-cloud-service}

通过创建云服务配置实例化的[AdobeGranite OAuth应用程序和Provider](#adobe-granite-oauth-application-and-provider)实例标识Twitter应用程序和新用户所添加的成员组。

1. 在创作实例上，使用管理员权限登录。
1. 在全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Twitter社交登录配置]**。
1. 选择&#x200B;**[!UICONTROL 上下文路径]**&#x200B;配置。

   上下文路径应与您在创建/编辑社区站点时选择的云配置路径相同。

1. 检查您的上下文路径是否已启用以在其下方创建云服务。
1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。 选择上下文并编辑属性。 如果未启用，请启用云配置。

   ![twitterconfigpropp](assets/twitterconfigproppng.png)

   * 有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。

1. 创建/编辑Twitter云服务配置。

   ![twittersociallogpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL 标题]**

      （*必需*）输入标识Twitter应用程序的显示标题。 建议使用与Twitter应用程序的&#x200B;*显示名称*&#x200B;输入的相同名称。

   * **[!UICONTROL 使用者密钥]**

      （*必需*）输入Twitter应用程序的&#x200B;**消费者(API)密钥**。 它标识从对话框创建的[AdobeGranite OAuth应用程序和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider)实例。

   * **[!UICONTROL 使用者密钥]**

      （*必需*）输入Twitter应用程序的&#x200B;***Consumer(API)Secret***。

   * **[!UICONTROL 创建用户]**

      如果选中此项，则使用Twitter帐户登录将创建AEM用户条目，并将其作为成员添加到所选用户组。 选中默认值（强烈建议）。

   * **[!UICONTROL 隐藏用户 ID]**

      不选。

   * **[!UICONTROL 添加到用户组]**

      选择“添加用户组”，为要向其添加用户的社区站点选择一个或多个[成员组](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html)。
   >[!NOTE]
   >
   >可随时添加或删除组。 但现有用户的会员资格不会受到影响。 自动会员资格仅适用于更新此字段后创建的新用户。 对于禁用匿名用户的站点，将用户添加到相应的社区成员组，以用于该已关闭的社区站点。

1. 选择&#x200B;**[!UICONTROL SAVE]**&#x200B;和&#x200B;**[!UICONTROL Publish]**。

结果是不需要进一步修改的[AdobeGranite OAuth应用程序和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider)实例。 默认范围是Twitter登录的标准权限。

### AEM Communities Twitter OAuth提供程序{#aem-communities-twitter-oauth-provider}

AEM Communities配置扩展了[AdobeGranite OAuth应用程序和Provider](#adobe-granite-oauth-application-and-provider)实例。 此提供者需要编辑才能允许用户更新。

如果需要编辑，请在每个AEM发布实例上：

1. 使用管理员权限登录。
1. 导航到[Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   例如，http://localhost:4503/system/console/configMgr。

1. 找到AEM Communities Twitter OAuth提供者。
1. 选择要打开进行编辑的铅笔图标。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth提供程序ID]**

   （*必需*）默认值为&#x200B;*soco -twitter*。 不要编辑。

   * **[!UICONTROL Cloud Service配置]**

      默认值为&#x200B;*conf。* 不要编辑。

   * **[!UICONTROL OAuth提供程序服务配置]**

      默认值为 `/apps/social/twitterprovider/config/`. 不要编辑。

   * **[!UICONTROL 用户路径]**

      存储用户数据的存储库中的位置。 对于社区站点，要确保成员能够视图彼此的用户档案，路径应为默认`/home/users/community`。

   * **[!UICONTROL 启用]** 参数不编辑
   * **[!UICONTROL URL参]** 数不编辑
   * **[!UICONTROL 更新用户]**

      如果选中，则每次登录时都会刷新存储库中的用户数据，以反映用户档案更改或请求的其他数据。 将取消选择默认值。


#### 后续步骤{#next-steps-1}

Facebook和Twitter的后续步骤相同：

* [发布云服务配置](#publishcloudservices)
* [为社区站点启用](#enable-social-login)

## 启用社交登录{#enable-social-login}

### AEM Communities Sites Console {#aem-communities-sites-console}

配置云服务后，可在社区站点[创建](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation)或[管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties)期间使用[用户管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT)设置子面板为社区站点启用相关的社交登录设置。

1. 选择保存社交登录配置的站点配置上下文。

1. 在“常规”选项卡上，设置云配置。

   ![managesites_png](assets/managesites_png.png)

1. 在“设置”选项卡上，启用&#x200B;**[!UICONTROL 社交登录]**&#x200B;并保存。

   ![usermgmt_png](assets/usermgmt_png.png)

## 测试社交登录{#test-social-login}

* 确保已在所有发布实例上启用[AdobeGranite OAuth身份验证处理程序](#adobe-granite-oauth-authentication-handler)。
* 确保已发布云服务。
* 确保已发布社区站点。
* 在浏览器中启动已发布的站点。
例如，http://localhost:4503/content/sites/engage/en.html
* 选择&#x200B;**[!UICONTROL 登录]**。
* 选择&#x200B;**[!UICONTROL 使用Facebook]**&#x200B;登录或&#x200B;**[!UICONTROL 使用Twitter]**&#x200B;登录。
* 如果尚未登录Facebook或Twitter，请使用相应的凭据登录。
* 可能需要根据Facebook或Twitter应用程序显示的对话框授予权限。
* 请注意，页面顶部的工具栏会更新以反映成功登录。
* 选择&#x200B;**[!UICONTROL 用户档案]**:“用户档案”页显示用户的头像图像、名和姓。 它还会根据允许的字段/参数显示来自Facebook或Twitter用户档案的信息。

## AEM平台OAuth配置{#aem-platform-oauth-configurations}

### Adobe Granite OAuth身份验证处理程序{#adobe-granite-oauth-authentication-handler}

默认情况下，`Adobe Granite OAuth Authentication Handler`未启用，并且必须在所有AEM发布实例上启用&#x200B;***。***

要在发布时启用身份验证处理程序，只需打开OSGi配置并保存它：

* 使用管理员权限登录。
* 导航到[Web控制台](../../help/sites-deploying/configuring-osgi.md)。
例如，http://localhost:4503/system/console/configMgr
* 找到`Adobe Granite OAuth Authentication Handler`。
* 选择以打开要编辑的配置。
* 选择&#x200B;**[!UICONTROL 保存]**。

![graniteoauth](assets/graniteoauth.png)

>[!CAUTION]
>
>请注意，不要将身份验证处理函数与&#x200B;*AdobeGranite OAuth应用程序和提供者*&#x200B;的Facebook或Twitter实例混淆。

![graniteauth1](assets/graniteoauth1.png)

### Adobe Granite OAuth应用程序和提供程序{#adobe-granite-oauth-application-and-provider}

创建Facebook或Twitter的云服务时，将创建`Adobe Granite OAuth Authentication Handler`的实例。

要查找Facebook或Twitter应用程序的已创建实例，请执行以下操作：

1. 使用管理员权限登录。
1. 导航到[Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   例如，http://localhost:4503/system/console/configMgr。

1. 找到Adobe Granite OAuth应用程序和提供程序。

   * 找到&#x200B;**[!UICONTROL 客户端ID]**&#x200B;与&#x200B;**[!UICONTROL 应用程序ID]**&#x200B;匹配的实例。

      ![graniteauth2](assets/graniteoauth2.png)

      除以下属性外，请保持配置的其他属性不变：

   * **[!UICONTROL 配置ID]**

      （*必需*）OAuth配置ID必须唯一。 在创建云服务时自动生成。

   * **[!UICONTROL 客户端 ID]**

      （*必需*）创建云服务时提供的应用程序 ID。

   * **[!UICONTROL 客户端密钥]**

      （*必需*）创建云服务时提供的应用程序密码。

   * **[!UICONTROL 范围]**

      （*可选*）可从提供程序询问允许的其他范围。 默认范围涵盖提供社交身份验证和用户档案数据所需的权限。

   * **[!UICONTROL 提供者ID]**

      （*必需*）创建云服务时，将设置AEM Communities的提供程序ID。 不要编辑。 对于Facebook Connect，此值为&#x200B;*soco -facebook*。 对于Twitter Connect，该值为&#x200B;*soco -twitter*。

   * **[!UICONTROL 组]**

      （*推荐*）一个或多个成员组，已创建用户添加到其中。 对于AEM Communities，建议列表社区站点的成员组。

   * **[!UICONTROL 回调 URL]**

      （*可选*）配置了OAuth提供者的URL，以重定向客户端返回。 使用相对url来使用原始请求的主机。 如果留空，则改用最初请求的URL。 后缀“/callback/j_security_check”会自动附加到此url。
   >[!NOTE]
   >
   >回调的域必须向提供者（Facebook或Twitter）注册。

对于每个OAuth身份验证处理程序配置，在实例中还创建了两个其他配置：

* Apache Jackrabbit Oak默认同步处理程序(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) — 无需进行任何编辑，但您可以查看Facebook字段如何映射到CQ用户用户档案节点的用户字段映射。 另请注意，“同步处理程序名称”与OAuth提供程序配置的配置ID匹配。
* Apache Jackrabbit Oak外部登录模块(org.apache.jackrabbit.oak.spi.security.external.impl.ExternalLoginModuleFactory) — 无需进行任何编辑，但您可能会注意到“标识提供者名称”和“同步处理程序名称”是相同的，并分别指向相应的OAuth和同步处理程序配置。

有关详细信息，请参阅[Authentication with Apache Oak External Login Module](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)。

## OAuth用户遍历性能{#oauth-user-traversal-performance}

对于社区网站，如果有数十万用户使用Facebook或Twitter登录进行注册，则通过添加以下Oak索引，可以改善网站访客使用社交登录时所执行查询的遍历性能。

如果日志中显示遍历警告，则建议添加此索引。

在作者实例上，以管理权限登录：

1. 从全局导航：选择&#x200B;**工具，[CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md)。**
1. 从ntBaseLucene的副本创建名为ntBaseLucene-oauth的索引：

   * 在节点`/oak:index`下
   * 选择节点`ntBaseLucene`
   * 选择&#x200B;**[!UICONTROL 复制]**
   * 选择 `/oak:index`
   * 选择&#x200B;**[!UICONTROL 粘贴]**
   * 将ntBaseLucene的副本重命名为`ntBaseLucene-oauth`

1. 修改node ntBaseLucene-oauth的属性：

   * **[!UICONTROL indexPath]**:  `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**:  `oauthid-123****`
   * **[!UICONTROL reindex]**:  `true`
   * **[!UICONTROL reindexCount]**:  `1`

1. 在节点/oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties下：

   * 删除除cqTags外的所有子节点。
   * 将cqTags重命名为`oauthid-123****`
   * 修改节点`oauthid-123****`的属性

      * **[!UICONTROL name]**:  `oauthid-123****`
   * 选择&#x200B;**[!UICONTROL 保存全部]**。


* 对于&#x200B;**名称** `oauthid-123`，将&#x200B;*123*&#x200B;替换为作为&#x200B;**客户端ID&lt;a10/的值的Facebook ***应用程序ID***或Twitter ***消费者(API)密钥***>，在[AdobeGranite OAuth应用程序和提供程序](social-login.md#adobe-granite-oauth-application-and-provider)配置中。**

   ![graniteauth-crxde](assets/graniteoauth-crxde.png)

有关其他信息和工具，请参阅[Oak查询和索引](../../help/sites-deploying/queries-and-indexing.md)。

## 调度程序配置{#dispatcher-configuration}

请参阅[配置Dispatcher for Communities](dispatcher.md)。
