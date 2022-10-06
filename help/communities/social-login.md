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

社交登录功能可向网站访客展示使用其Facebook或Twitter帐户登录的选项。 因此，请在其AEM成员配置文件中包含允许的Facebook或Twitter数据。

![socialloginweretail](assets/socialloginweretail.png)

## 社交登录概述 {#social-login-overview}

要包含社交登录，请 *必需* 创建自定义Facebook和Twitter应用程序。

虽然we-retail示例提供了示例Facebook和Twitter应用程序及云服务，但它们在 [生产网站](../../help/sites-administering/production-ready.md).

所需的步骤包括：

1. [启用OAuth身份验证](#adobe-granite-oauth-authentication-handler) 在所有AEM发布实例上。

   未启用OAuth时，尝试登录失败。

1. **创建** 社交应用程序和云服务。

   * 要支持使用Facebook登录，请执行以下操作：

      * 创建 [Facebook应用程序](#create-a-facebook-app).
      * 创建和发布 [Facebook Connect云服务](#create-a-facebook-connect-cloud-service).
   * 要支持使用Twitter登录，请执行以下操作：

      * 创建 [Twitter应用程序](#create-a-twitter-app).
      * 创建和发布 [Twitter Connect云服务](#create-a-twitter-connect-cloud-service).


1. [**启用** 社交登录](#enable-social-login) 社区站点。

有两个基本概念：

1. **范围** （权限）指定允许应用程序请求的数据。

   * facebook和Twitter [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 默认情况下，实例在其范围内包含基本的应用程序权限。

1. **字段** (params)使用URL参数指定请求的实际数据。

   * 这些字段在 [AEM Communities Facebook OAuth提供程序](#aem-communities-facebook-oauth-provider) 和 [AEM Communities Twitter OAuth提供程序](#aem-communities-twitter-oauth-provider).
   * 对于大多数用例，默认字段已足够，但可以修改。

## Facebook登录 {#facebook-login}

### Facebook API版本 {#facebook-api-version}

Social登录和we-retail Facebook示例是在Facebook Graph API版本1.0时开发的。自AEM 6.4 GA和AEM 6.3 SP1起，社交登录已更新，可与较新的Facebook Graph API 2.5版本配合使用。

>[!NOTE]
>
>对于旧版AEM，如果您在日志中遇到异常 **无法从此提取令牌**，请升级到该AEM版本的最新CFP。

有关Facebook图形API版本信息，请参阅 [Facebook API changelog](https://developers.facebook.com/docs/apps/changelog).

### 创建Facebook应用程序 {#create-a-facebook-app}

需要正确配置的Facebook应用程序才能启用Facebook社交登录。

要创建Facebook应用程序，请按照Facebook在 [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). 以下信息未反映对其说明所做的更改。

一般情况下，自Facebook API v2.7起：

* *添加新的Facebook应用程序*
   * 对于 *平台*，选择网站：
      * 对于 *网站URL*，输入 `  https://<server>:<port>.`
      * 对于 *显示名称*，输入用作Facebook连接服务标题的标题。
      * 对于 *类别*，推荐选择 *页面应用程序*，但可以是任何内容。
      * *添加产品：Facebook登录*
      * 对于 *有效的OAuth重定向URI*，输入 `  https://<server>:<port>.`

>[!NOTE]
>
>对于开发， http://localhost:4503将有效。

创建应用程序后，找到 **[!UICONTROL 应用程序ID]** 和 **[!UICONTROL 应用程序密钥]** 设置。 配置 [Facebook云服务](#createafacebookcloudservice).

### 创建Facebook ConnectCloud Service {#create-a-facebook-connect-cloud-service}

的 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 实例通过创建云服务配置进行实例化，用于标识Facebook应用程序和新用户所添加到的成员组。

1. 在AEM创作实例上，使用管理员权限登录。
1. 从全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Facebook Social登录配置]**.
1. 选择配置 **[!UICONTROL 上下文路径]**.

   **[!UICONTROL 上下文路径]** 应与您在创建/编辑社区站点时选择的云配置路径相同。

1. 检查上下文路径是否已启用以在其下创建云服务。
1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**. 选择上下文并编辑属性。 如果尚未启用，则启用云配置。

   ![config-propertiespng](assets/config-propertiespng.png)

   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档以了解更多信息。

1. **创建/编辑** Facebook云服务配置。

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL 标题]** (*必需*)输入标识Facebook应用程序的显示标题。 建议使用与 *显示名称* (对于Facebook应用程序)。
   * **[!UICONTROL 应用程序ID/API密钥]** (*必需*)输入 ***应用程序ID*** (对于Facebook应用程序)。 这标识了 [AdobeGranite OAuth应用程序和提供程序](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 从对话框创建的实例。
   * **[!UICONTROL 应用程序密钥]** (*必需*)输入 ***应用程序密钥*** (对于Facebook应用程序)。
   * **[!UICONTROL 创建用户]** 如果选中此项，则使用Facebook帐户登录将创建一个AEM用户条目，并将其作为成员添加到选定的用户组。  默认选中（强烈建议）。
   * **[!UICONTROL 掩码用户ID]**:保持取消选中状态。
   * **[!UICONTROL 范围电子邮件]**:应从Facebook获取用户的电子邮件id。
   * **[!UICONTROL 添加到用户组]** 选择添加用户群组以选择一个或多个 [成员组](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) ，以向其添加用户的社区站点。

   >[!NOTE]
   >
   >可以随时添加或删除组。 但现有用户的成员资格不会受到影响。 自动成员资格仅适用于更新此字段后创建的新用户。 对于禁用匿名用户的网站，选择将用户添加到相应的社区成员组，以便用于该封闭的社区网站。

   * 选择 **[!UICONTROL 保存]**.
   * **[!UICONTROL 发布]**.


结果是 [AdobeGranite OAuth应用程序和提供程序](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 实例，除非添加其他范围（权限），否则不需要进一步修改。 默认范围是Facebook登录的标准权限。 如果需要其他范围，则需要直接编辑OSGI配置。 如果有修改是直接通过系统/控制台完成的，请避免从触屏UI编辑云服务配置以避免覆盖。

### AEM Communities Facebook OAuth提供程序 {#aem-communities-facebook-oauth-provider}

AEM Communities提供商将 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 实例。

此提供程序将需要编辑以：

* 允许用户更新
* 添加其他字段 [范围](#adobe-granite-oauth-application-and-provider)

   * 默认情况下，并非包含所有默认允许的字段。

如果需要编辑，请在每个AEM发布实例上：

1. 使用管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md). 例如， http://localhost:4503/system/console/configMgr。
1. 找到AEM Communities Facebook OAuth提供程序。
1. 选择要打开以进行编辑的铅笔图标。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth提供程序ID]**

      (*必需*)默认值为 *索科 — facebook*. 请勿编辑。

   * **[!UICONTROL Cloud Service配置]**

      默认值为 `/etc/  cloudservices /  facebookconnect`. 请勿编辑。

   * **[!UICONTROL OAuth提供程序服务配置]**

      默认值为 `/apps/social/facebookprovider/config/`. 请勿编辑。

   * **[!UICONTROL 启用标记]**

      请勿编辑。

   * **[!UICONTROL 用户路径]**

      存储用户数据的存储库中的位置。 对于社区站点，要确保成员有权查看彼此的配置文件，路径应为默认路径 */home/users/community*.

   * **[!UICONTROL 启用字段]**

      如果选中此项，则在向Facebook发出用户身份验证和信息请求时指定列出的字段。 将取消选择默认值。

   * **[!UICONTROL 字段]**

      启用字段后，在调用Facebook图形API时，将包含以下字段。 必须允许在云服务配置中定义的范围内使用字段。 其他字段可能需要Facebook批准。 请参阅Facebook文档的Facebook登录权限部分。 作为参数添加的默认字段包括：

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

      如果选中此项，则每次登录时都会刷新存储库中的用户数据，以反映配置文件更改或请求的其他数据。 取消选择默认值。


#### 后续步骤 {#next-steps}

facebook和Twitter的后续步骤相同：

* [发布云服务配置](#publishcloudservices)
* [为社区站点启用](#enable-social-login)

## Twitter登录 {#twitter-login}

### 创建Twitter应用程序 {#create-a-twitter-app}

需要配置的Twitter应用程序才能启用Twitter社交登录。

按照最新说明创建新的Twitter应用程序，网址为 [https://apps.twitter.com](https://apps.twitter.com/).

一般而言：

1. 输入 *名称* 将您的Twitter应用程序标识给您网站的用户。
1. 输入&#x200B;*说明*.
1. 对于 *网站*  — 输入 `https://<server>`.
1. 对于 *回调URL*  — 输入 `https://server`.

   >[!NOTE]
   >
   >无需指定端口。
   >
   >对于开发， https://127.0.0.1/将有效。

1. 创建应用程序后，找到 **[!UICONTROL 消费者(API)密钥]** 和 **[!UICONTROL 消费者(API)密钥]**. 配置 [Twitter云服务](#createatwittercloudservice).

#### 权限 {#permissions}

在Twitter应用程序管理的权限部分：

* **[!UICONTROL 访问]**:选择 `Read only`.

   * 不支持其他选项

* **[!UICONTROL 其他权限]**:（可选）选择 `Request email addresses from users`.

   * 如果未选择，则AEM中的用户配置文件将不包含其电子邮件地址。
   * Twitter的说明说明了需要采取的其他步骤。

对社交登录发出的唯一REST请求是 *[GET帐户/验证凭据](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### 创建Twitter ConnectCloud Service {#create-a-twitter-connect-cloud-service}

的 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 实例通过创建云服务配置进行实例化，用于标识Twitter应用程序和新用户所添加到的成员组。

1. 在创作实例上，使用管理员权限登录。
1. 从全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Twitter Social登录配置]**.
1. 选择 **[!UICONTROL 上下文路径]** 配置。

   上下文路径应与您在创建/编辑社区站点时选择的云配置路径相同。

1. 检查上下文路径是否已启用以在其下创建云服务。
1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**. 选择上下文并编辑属性。 如果尚未启用，则启用云配置。

   ![twitterconfigpropping](assets/twitterconfigproppng.png)

   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档以了解更多信息。

1. 创建/编辑Twitter云服务配置。

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL 标题]**

      (*必需*)输入标识Twitter应用程序的显示标题。 建议使用与 *显示名称* (对于Twitter应用程序)。

   * **[!UICONTROL 使用者密钥]**

      (*必需*)输入 **消费者(API)密钥** (对于Twitter应用程序)。 这标识了 [AdobeGranite OAuth应用程序和提供程序](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) 从对话框创建的实例。

   * **[!UICONTROL 使用者密钥]**

      (*必需*)输入 ***消费者(API)密钥*** (对于Twitter应用程序)。

   * **[!UICONTROL 创建用户]**

      如果选中此项，则使用Twitter帐户登录将创建一个AEM用户条目，并将其作为成员添加到选定的用户组。 默认选中（强烈建议）。

   * **[!UICONTROL 隐藏用户 ID]**

      保持取消选中状态。

   * **[!UICONTROL 添加到用户组]**

      选择添加用户群组以选择一个或多个 [成员组](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) ，以向其添加用户的社区站点。
   >[!NOTE]
   >
   >可以随时添加或删除组。 但现有用户的成员资格不会受到影响。 自动成员资格仅适用于更新此字段后创建的新用户。 对于禁用匿名用户的网站，将用户添加到相应的社区成员组，该组专门用于该封闭的社区网站。

1. 选择 **[!UICONTROL 保存]** 和 **[!UICONTROL 发布]**.

结果是 [AdobeGranite OAuth应用程序和提供程序](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) 不需要进一步修改的实例。 默认范围是Twitter登录的标准权限。

### AEM Communities Twitter OAuth提供程序 {#aem-communities-twitter-oauth-provider}

AEM Communities配置将 [AdobeGranite OAuth应用程序和提供程序](#adobe-granite-oauth-application-and-provider) 实例。 此提供程序将需要编辑才能允许用户更新。

如果需要编辑，请在每个AEM发布实例上：

1. 使用管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md).

   例如， http://localhost:4503/system/console/configMgr。

1. 找到AEM Communities Twitter OAuth提供程序。
1. 选择要打开以进行编辑的铅笔图标。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth提供程序ID]**

   (*必需*)默认值为 *索科 — twitter*. 请勿编辑。

   * **[!UICONTROL Cloud Service配置]**

      默认值为 *conf.* 请勿编辑。

   * **[!UICONTROL OAuth提供程序服务配置]**

      默认值为 `/apps/social/twitterprovider/config/`。请勿编辑。

   * **[!UICONTROL 用户路径]**

      存储用户数据的存储库中的位置。 对于社区站点，要确保成员有权查看彼此的配置文件，路径应为默认路径 `/home/users/community`.

   * **[!UICONTROL 启用参数]** 不编辑
   * **[!UICONTROL URL参数]** 不编辑
   * **[!UICONTROL 更新用户]**

      如果选中此项，则每次登录时都会刷新存储库中的用户数据，以反映配置文件更改或请求的其他数据。 将取消选择默认值。


#### 后续步骤 {#next-steps-1}

facebook和Twitter的后续步骤相同：

* [发布云服务配置](#publishcloudservices)
* [为社区站点启用](#enable-social-login)

## 启用社交登录 {#enable-social-login}

### AEM Communities站点控制台 {#aem-communities-sites-console}

配置云服务后，可以使用为社区站点启用相关的社交登录设置 [用户管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) 社区站点期间的设置子面板 [创建](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) 或 [管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. 选择保存社交登录配置的网站配置上下文。

1. 在常规选项卡上，设置云配置。

   ![managesites_png](assets/managesites_png.png)

1. 在“设置”选项卡上，启用 **[!UICONTROL 社交登录]** 并保存。

   ![usermgmt_png](assets/usermgmt_png.png)

## 测试社交登录 {#test-social-login}

* 确保 [AdobeGranite OAuth身份验证处理程序](#adobe-granite-oauth-authentication-handler) 已在所有发布实例上启用。
* 确保云服务已发布。
* 确保社区站点已发布。
* 在浏览器中启动已发布的网站。
例如， http://localhost:4503/content/sites/engage/en.html
* 选择 **[!UICONTROL 登录]**.
* 选择 **[!UICONTROL 使用Facebook登录]** 或 **[!UICONTROL 使用Twitter登录]**.
* 如果尚未登录Facebook或Twitter，请使用相应的凭据登录。
* 可能需要授予权限，具体取决于Facebook或Twitter应用程序显示的对话框。
* 请注意，页面顶部的工具栏已更新，以反映成功登录。
* 选择 **[!UICONTROL 用户档案]**:用户档案页面显示用户的头像图像、名字和姓氏。 它还会根据允许的字段/参数显示Facebook或Twitter配置文件中的信息。

## AEM Platform OAuth配置 {#aem-platform-oauth-configurations}

### AdobeGranite OAuth身份验证处理程序 {#adobe-granite-oauth-authentication-handler}

的 `Adobe Granite OAuth Authentication Handler` 默认情况下未启用，并且 ***必须在所有AEM发布实例上启用。***

要在发布时启用身份验证处理程序，只需打开OSGi配置并保存它：

* 使用管理员权限登录。
* 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md).
例如， http://localhost:4503/system/console/configMgr
* 定位 `Adobe Granite OAuth Authentication Handler`.
* 选择以打开要编辑的配置。
* 选择&#x200B;**[!UICONTROL 保存]**。

![graniteauth](assets/graniteoauth.png)

>[!CAUTION]
>
>请注意，不要将身份验证处理程序与的Facebook或Twitter实例混淆 *AdobeGranite OAuth应用程序和提供程序*.

![graniteauth1](assets/graniteoauth1.png)

### AdobeGranite OAuth应用程序和提供程序 {#adobe-granite-oauth-application-and-provider}

创建Facebook或Twitter的云服务时， `Adobe Granite OAuth Authentication Handler` 创建时。

要找到为Facebook或Twitter应用程序创建的实例，请执行以下操作：

1. 使用管理员权限登录。
1. 导航到 [Web控制台](../../help/sites-deploying/configuring-osgi.md).

   例如， http://localhost:4503/system/console/configMgr。

1. 找到AdobeGranite OAuth应用程序和提供程序。

   * 找到实例，其中 **[!UICONTROL 客户端ID]** 匹配 **[!UICONTROL 应用程序ID]**.

      ![graniteauth2](assets/graniteoauth2.png)

      除以下属性外，请保持配置的其他属性不变：

   * **[!UICONTROL 配置ID]**

      (*必需*)OAuth配置ID必须唯一。 创建云服务时自动生成。

   * **[!UICONTROL 客户端 ID]**

      (*必需*)创建云服务时提供的应用程序ID。

   * **[!UICONTROL 客户端密钥]**

      (*必需*)创建云服务时提供的应用程序密钥。

   * **[!UICONTROL 范围]**

      (*可选*)可向提供商询问其他允许的范围。 默认范围涵盖提供社交身份验证和用户档案数据所需的权限。

   * **[!UICONTROL 提供程序ID]**

      (*必需*)创建云服务时设置AEM Communities的提供程序ID。 请勿编辑。 对于Facebook Connect，值为 *索科 — facebook*. 对于Twitter Connect，值为 *索科 — twitter*.

   * **[!UICONTROL 组]**

      (*建议*)一个或多个成员组，已创建用户将被添加到该成员组。 对于AEM Communities，建议列出社区站点的成员组。

   * **[!UICONTROL 回调 URL]**

      (*可选*)与OAuth提供程序配置的URL，用于重定向回客户端。 使用相对URL来使用原始请求的主机。 将留空，以改用最初请求的URL。 后缀“/callback/j_security_check”会自动附加到此URL中。
   >[!NOTE]
   >
   >回调的域必须向提供程序(Facebook或Twitter)注册。

对于每个OAuth身份验证处理程序配置，实例中还创建了两个其他配置：

* Apache Jackrabbit Oak默认同步处理程序(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) — 无需进行编辑，但您可以查看用户字段映射Facebook字段如何映射到CQ用户配置文件节点。 另请注意，“同步处理程序名称”与OAuth提供程序配置的配置ID匹配。
* Apache Jackrabbit Oak外部登录模块(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) — 无需进行编辑，但您可能会注意到“身份提供程序名称”和“同步处理程序名称”相同，并分别指向相应的OAuth和同步处理程序配置。

有关更多信息，请参阅 [使用Apache Oak外部登录模块进行身份验证](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## OAuth用户遍历性能 {#oauth-user-traversal-performance}

对于社区网站，如果有数十万用户使用Facebook或Twitter登录方式进行注册，则添加以下Oak索引可以提高网站访客使用其社交登录方式时执行查询的遍历性能。

如果日志中出现遍历警告，建议添加此索引。

在创作实例上，使用管理权限登录：

1. 从全局导航：选择 **工具， [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. 从ntBaseLucene的副本创建名为ntBaseLucene-oauth的索引：

   * 在节点下 `/oak:index`
   * 选择节点 `ntBaseLucene`
   * 选择 **[!UICONTROL 复制]**
   * 选择 `/oak:index`
   * 选择 **[!UICONTROL 粘贴]**
   * 将ntBaseLucene的副本重命名为 `ntBaseLucene-oauth`

1. 修改ntBaseLucene-oauth节点的属性：

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**: `oauthid-123****`
   * **[!UICONTROL 重新索引]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. 在节点/oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties下：

   * 删除除cqTags之外的所有子节点。
   * 将cqTags重命名为 `oauthid-123****`
   * 修改节点的属性 `oauthid-123****`

      * **[!UICONTROL name]**: `oauthid-123****`
   * 选择 **[!UICONTROL 全部保存]**.


* 对于 **name** `oauthid-123`，替换 *123* 和Facebook ***应用程序ID*** 或Twitter ***消费者(API)密钥*** 即 **客户端ID** 在 [AdobeGranite OAuth应用程序和提供程序](social-login.md#adobe-granite-oauth-application-and-provider) 配置。

   ![graniteauth-crxde](assets/graniteoauth-crxde.png)

有关其他信息和工具，请参阅 [Oak查询和索引](../../help/sites-deploying/queries-and-indexing.md).

## 调度程序配置 {#dispatcher-configuration}

请参阅 [为社区配置Dispatcher](dispatcher.md).
