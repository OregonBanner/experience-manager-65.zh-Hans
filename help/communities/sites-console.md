---
title: 社区站点控制台
seo-title: 社区站点控制台
description: 如何访问“社区站点”控制台
seo-description: 如何访问“社区站点”控制台
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
translation-type: tm+mt
source-git-commit: 89156f94f2d0494d44d4f0b99abfba4fafbc66d3

---


# 社区站点控制台 {#communities-sites-console}

通过“社区站点”控制台，可以访问：

* 站点创建
* 站点编辑
* 站点管理
* [创建和编辑嵌套组](/help/communities/groups.md) （子社区）

请参 [阅AEM Communities入门](/help/communities/getting-started.md) ，体验在创作环境中创建社区站点的速度，以及如何从创作和发布环境创建社区组。

>[!NOTE]
>
>主要的社区菜单用于创建社区 [站点](/help/communities/sites-console.md)、社区 [站点模板](/help/communities/sites.md)、社区 [组模板和社区功](/help/communities/tools-groups.md)[](/help/communities/functions.md) 能创作者只能在环境中使用。


## 前提条件 {#prerequisites}

在创建社区站点之前，必 *须* :

* 确保一个或多个发布实例正在运行。
* 启用隧道 [服务](/help/communities/deploy-communities.md#tunnel-service-on-author) ，以管理成员和成员组。
* 识别主 [发行商](/help/communities/deploy-communities.md#primary-publisher)。
* [在主发布者端口不是默认端口时](/help/communities/deploy-communities.md#replication-agents-on-author) ，配置复制(4503)。

最佳实践是，为确保站点准备好支持许多功能，请采取以下步骤：

* 安装最 [新的功能包](/help/communities/deploy-communities.md#latestfeaturepack)。
* 为 [AEM Communities启用Adobe Analytics](/help/communities/analytics.md) 。
* 配置电子 [邮件](/help/communities/email.md)
* 识别 [社区管理员](/help/communities/users.md#creating-community-members)。
* [为社交登录启用OAuth处理程序](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) 。

## 访问社区站点控制台 {#accessing-communities-sites-console}

在创作环境中，要访问“社区站点”控制台，请执行以下操作：

* 从全局导航：“社 **[!UICONTROL 区]** ”>“站 **[!UICONTROL 点”]**

“社区站点”控制台显示任何现有社区站点。 在此控制台中，可以创建、编辑、管理和删除社区站点。

要创建新社区站点，请选择“创 **建** ”图标。

要访问现有社区站点，为了创作、修改、发布、导出或添加嵌套组，请选择站点的文件夹图标。

例如，下图显示了主“社区站点”控制台，其中显示了两个社区站点的文件夹：启 [用](/help/communities/getting-started-enablement.md)[和参与](/help/communities/getting-started.md):

![chlimage_1-154](assets/chlimage_1-154.png)

## 站点创建 {#site-creation}

站点创建控制台提供了一种分步方法，可根据选定的社区站点模板和设置组合 [站点的功能](/help/communities/sites.md) 。

创建的每个站点都包含登录功能，因为站点访客必须先登录才能发布内容、发送消息或加入组。 其他包含的功能包括用户用户档案、消息、通知、网站菜单、搜索、主题和品牌。

通过选择位于“社区站点” `Create` 控制台顶部的按钮启动该过程。

创建过程是一系列步骤，这些步骤以面板的形式呈现，其中包含要配置的一组特征（以子面板的形式呈现）。 在最后一步中提交站点之前，可 **以前进****** 到下一步或后退到上一步。

### 第1步：站点模板 {#step-site-template}

![新站点模板](assets/newsitetemplate.png)

在“站点模板”面板中，将指定“标题”、“说明”、“站点根”、“基本语言”、“名称”和“站点模板”:

* **社区站点标题**

   站点的显示标题。

   标题显示在已发布的站点上以及站点管理员UI中。

* **社区站点描述**

   站点的说明。

   说明不显示在已发布的站点上。

* **社区站点根目录**

   站点的根路径。

   默认的根目 `/content/sites`录为，但根目录可能被移动到网站中的任意位置。

* **社区站点基本语言**

   (单一语言不更改：英语)使用下拉菜单从可用语言中选择一 *种或多种基本语言* -德语、意大利语、法语、日语、西班牙语、葡萄牙语（巴西）、繁体中文和简体中文。 将根据多语言站点翻译内容中所述的最佳实践，为添加的每种语言创建一个社区站点，并且该站点将存 [在于同一站点文件夹中](/help/sites-administering/translation.md)。 每个站点的根页面将包含一个子页面，该子页面由所选语言之一的语言代码命名，如英语为“en”或法语为“fr”。

* **社区站点名称**:

   站点的根页面的名称，该名称显示在URL中。

   * 多次检查名称，因为创建站点后该名称不易更改。
   * 基本URL( `https://server:port/site root/site name)` 将显示在下面 `Community Site Name`。

   * 对于有效的URL，请附加基本语言代码+ &quot;。html&quot;

      *例如*, `https://localhost:4502/content/sites/mysight/en.html`

* **“社区站点模板** ”菜单

   使用下拉菜单选择可用的社 [区站点模板](/help/communities/tools.md)。

* 选择&#x200B;**下一步**。

### 第2步：设计 {#step-design}

“设计”面板包含两个用于选择主题和品牌横幅的子面板：

#### COMMUNITY SITE THEME {#community-site-theme}

![sitetheme](assets/sitetheme.png)

该框架使 [用Twitter Bootstrap](https://twitterbootstrap.org/) ，为网站提供响应迅速、灵活的设计。 可以选择多个预加载Bootstrap主题之一来设置所选社区站点模板的样式，或者可以上传Bootstrap主题。

选择后，主题将用不透明的蓝色复选标记覆盖。

发布社区站点后，可以编辑属性 [并选择其](#modifying-site-properties) 他主题。

#### COMMUNITY SITE BRANDING {#community-site-branding}

![chlimage_1-155](assets/chlimage_1-155.png)

社区站点品牌是显示为每个页面顶部标题的图像。

图像的大小应与浏览器中页面的预期显示大小相同，高度应为120像素。

创建或选择图像时，请牢记：

* 图像高度将从图像的上边缘裁切为120像素。
* 图像被固定到浏览器窗口的左边缘。
* 图像不会调整大小，因此当图像宽度为……

   * 小于浏览器的宽度，图像将水平重复。
   * 大于浏览器的宽度后，图像将看起来会被裁掉。

* 选择&#x200B;**下一步**。

### 第3步：设置 {#step-settings}

“设置”面板包含几个子面板，这些子面板显示要配置的功能，然后移至创建站点的最后一步。

* [用户管理](#user-management)
* [标记](#tagging)
* [角色](#roles)
* [协调](#moderation)
* [分析](#analytics)
* [翻译](#translation)
* [支持](#enablement)

>[!NOTE]
>
>**启用隧道服务**
>
>“设置”子面板中的几个允许分配受信任成员以审核UGC、管理组或者成为发布环境中的启用资源的联系人。
>
>该约定适用于发布端用 [户和用户组](/help/communities/users.md) （成员和成员组）在创作环境中不重复。
>
>因此，在创作环境中创建社区站点并将受信任成员分配到各种角色时，必须从发布环境检索成员数据。
>
>这是通过为创作 ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` 环境启用来实现的。


#### USER MANAGEMENT {#user-management}

![创建站点设置](assets/createsitesettings.png)

>[!NOTE]
>
>建议将启用社 [区站点设为私有](/help/communities/overview.md#enablement-community) （有关详细信息，请与您的客户代表联系）。
>
>当匿名网站访客被拒绝访问、不能自行注册或不能使用社交登录时，社区站点是私有的。


* **允许用户注册**

   如果选中此项，站点访客可通过自助注册成为社区成员。
如果未选中此项，则会限 *制社区站点* ，并且必须将站点访客分配给社区站点的成员组、发出请求或通过电子邮件发送邀请。 如果未选中，则不允许匿名访问。
取消选中某个私 *人社区* 站点的选项。 选中默认值。

* **允许匿名访问**

   如果选中此项，则社区站点*打开*并且任何站点访客都可以访问该站点。
如果未选中，则只有登录成员才能访问站点。
取消选中*私人*社区站点。 选中默认值。

* **允许发送消息**

   如果选中此项，成员可以向彼此发送消息，也可以向社区站点内的组发送消息。
如果未选中，则不会为社区设置消息。
默认为未选中。

* **允许社交登录: Facebook**

   如果选中此项，则允许站点访客使用其Facebook帐户凭据登录。 应将选 [定的Facebook云配置配置为](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) ，在创建社区站点后，将用户添加到社区站点的成员组。
如果未选中，则不显示Facebook登录名。
对于私人社区站点， *不选中* “保留”。 默认为未选中。

* **允许社交登录: Twitter**

   如果选中此项，则允许站点访客使用其Twitter帐户凭据登录。 应将选 [定的Twitter云配置配置配置](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) ，以在创建社区站点后，将用户添加到社区站点的成员组。
如果未选中，则不显示Twitter登录名。
对于私人社区站点， *不选中* “保留”。 默认为未选中。

>[!NOTE]
>
>**允许社交登录**
>
>虽然Facebook和Twitter配置示例可能存在并可供选择，但对于生产 [环境](/help/sites-administering/production-ready.md)，必须创建自定义Facebook和Twitter应用程序。 请参 [阅使用Facebook和Twitter进行社交登录](/help/communities/social-login.md)。


#### TAGGING {#tagging}

![chlimage_1-156](assets/chlimage_1-156.png)

可应用于社区内容的标记通过选择之前通过标记控制台定义的标记命名空间来 [控制](/help/sites-administering/tags.md#tagging-console)。

此外，为社区站点选择标记命名空间会限制在定义目录和资源时显示的选择。 有关重 [要信息，请参阅标记启用资源](/help/communities/tag-resources.md) 。

* 文本搜索框：开始键入以标识允许在站点上使用的标记。

#### ROLES {#roles}

![社区角色](assets/site-admin-2.png)

社 [区成员的角色](/help/communities/users.md) ，会分配这些设置。

使用预先键入搜索可轻松查找社区成员。

* **社区管理员**

   开始键入以选择一个或多个社区成员或可管理社区成员和成员组的成员组。

* **社区审查方**

   开始键入内容以选择一个或多个要作为用户生成内容的版主信任的社区成员或成员组。

* **拥有权限的社区成员**

   开始键入内容以选择一个或多个社区成员或要授予成员组在为社区功能选择 `Allow Privileged Member` 内容后创建新内容 [的能力](/help/communities/functions.md)。

* **社区管理员**

   开始键入以选择一个或多个站点管理员，这些管理员可以独立于其他站点管理员和默认社区管理员处理站点结构。 他们可以在层次结构的任何级别创建组，并成为嵌套组的默认管理员（但稍后可以从嵌套组的管理员角色中删除这些组）。

#### MODERATION {#moderation}

![chlimage_1-157](assets/chlimage_1-157.png)

审核用户生成的内容(UGC)的全局设置由这些设置控制。 单个组件具有用于控制仲裁的其他设置。

* **内容已通过预审**

   如果选中此项，则发布的社区内容只有在审查方批准后才会显示。 默认为未选中。 有关详细信息，请参阅 [协调社区内容](/help/communities/moderate-ugc.md#premoderation)。

* **标记阈值，达到此值后隐藏内容**

   如果大于0，则主题或帖子在隐藏到公共视图之前必须标出的次数。 如果设置为-1，则标记的主题或帖子从不隐藏在公共视图中。 默认为5。

#### ANALYTICS {#analytics}

![chlimage_1-158](assets/chlimage_1-158.png)

* **启用 Analytics**

   仅在为Communities功能配置Adobe Analytics [后](/help/communities/analytics.md) ，才可用。
默认为未选中。 选中此项后，将显示另一个选择菜单：

![chlimage_1-159](assets/chlimage_1-159.png)

* **云配置框架引用**

   从下拉菜单中，选择为此社区站点配置的Analytics云服务框架。
   `Communities` 是Analytics Configuration for Communities Features文档中 [的框架示例](/help/communities/analytics.md#aem-analytics-framework-configuration) 。

#### TRANSLATION {#translation}

![chlimage_1-160](assets/chlimage_1-160.png)

* **允许机器翻译**

   选中（默认为未选中）后，站点内的UGC将启用机器翻译。 这不会影响任何其他内容，如页面内容，即使站点设置为多语言站点也是如此。 有关 [为AEM Communities配置许可翻译服务的信息](/help/communities/translate-ugc.md) ，请参阅翻译用户生成的内容。 有关 [完整概述，请参阅翻译多语言站点的内容](/help/sites-administering/translation.md) 。

![chlimage_1-161](assets/chlimage_1-161.png)

* **为选定的语言启用机器翻译**

   为机器翻译启用的语言默认为翻译集成配置指定的 [系统设置](/help/communities/translate-ugc.md#translation-integration-configuration)。 通过删除默认值和／或从下拉菜单中选择其他语言，此站点的这些默认设置可能会被覆盖。

* **选择翻译提供商**

   默认情况下，服务提供商是仅用于演示的试 `microsoft` 用版服务。 如果未获得翻译服务提供商的许可，则应 **取消选中“允许机器翻译** ”。

* **选择全球共享商店**

   对于具有多语言副本的网站，全局共享存储提供单个会话线程，每个语言副本中都可见。 这是通过选择作为语言副本包含的语言之一来实现的。 默认为 *无全局共享商店*。

* **选择翻译提供商配置**

   选择为许 [可的翻译提供者创建的翻译集成框架](/help/sites-administering/tc-tic.md) 。

* **为您的社区站点选择翻译选项**

   * **翻译整个页面**

      如果选择此项，则页面上的所有UGC都将转换为页面的基本语言。

      未选择 *默认值*。

   * **仅翻译选定内容**

      如果选择此项，则每个帖子旁边会显示一个翻译选项，允许将各个帖子翻译为页面的基本语言。
选中“默 *认”*。

* **选择持久性选项**

   * **根据用户请求翻译稿件，**&#x200B;然后再保留如果选择，则内容在发出请求前不会翻译。 翻译后，翻译会存储在存储库中。

      未选择 *默认值*。

   * **不保留翻译**

      如果选择此项，则翻译不会存储在存储库中。

      如果未选择，则保留翻译。

      未选择 *默认值*。

* **智能渲染**

   选择以下选项之一：

   * `Always show contributions in the original language` (默认)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### ENABLEMENT {#enablement}

![chlimage_1-162](assets/chlimage_1-162.png)

当选 `ENABLEMENT`定的社区站点模板包含分配功能 [时，这些设置适用](/help/communities/functions.md#assignments-function)，启用功能获得许可并配置时，这些功能 [可用](/help/communities/enablement.md)。 包含分配功能的引用站点模板是 `Reference Structured Learning Site Template.`

* **Enablement Managers**（必需）仅可选择用 `Community Enablementmanagers` 于管理此启用社区的组成员。 Enablement Manager负责将成员分配到资源。 另请参阅 [管理用户和用户组](/help/communities/users.md)。

* **Marketing Cloud 组织 ID**

   （可选）视频心率分析许 [可证的ID](/help/communities/analytics.md#video-heartbeat-analytics) 。

* 选择&#x200B;**下一步**。

### 第4步：创建社区站点 {#step-create-communities-site}

如果需要进行任何调整，请使 **用** “返回”按钮进行调整。

选 **择并启动** “创建”后，创建站点的过程将无法中断。

创建站点后：

* 不支持更改url（节点名称）。
* 将来对社区站点模板所做的更改不会影响创建的社区站点。
* 禁用社区站点模板不会影响创建的社区站点。
* 可以通过修改社 [区站点](#modify-structure) 的属性来编辑其STRUCTURE。

![chlimage_1-163](assets/chlimage_1-163.png)

完成该过程后，新站点的文件夹将显示在“社区站点”控制台中，作者可以从中添加页面内容，或管理员可以修改站点的属性。

![chlimage_1-164](assets/chlimage_1-164.png)

要修改社区站点，请选择其项目文件夹以将其打开：

![siteactions-1](assets/siteactions-1.png)

当鼠标悬停在站点上或触摸站点卡时，将显示允许以作者模式编辑站点的图标 [，打开站点属性进行修改](#authoring-site-content)，发布站点 [,](#modifying-site-properties)[](#publishing-the-site)[](#exporting-the-site)[](#deleting-the-site)导出站点并删除站点图标。

## 创作站点内容 {#authoring-site-content}

![chlimage_1-165](assets/chlimage_1-165.png)

站点内容的创作工具可能与任何其他AEM网站相同。 要打开站点进行创作，请选择鼠标 `Open Site` 悬停在站点上时显示的图标。 该站点将在新选项卡中打开，以便“社区站点”控制台仍可访问。

![chlimage_1-166](assets/chlimage_1-166.png)

>[!NOTE]
>
>如果不熟悉AEM，请视图有关基本操作 [的文档](/help/sites-authoring/basic-handling.md) ，以 [及页面创作快速指南](/help/sites-authoring/qg-page-authoring.md)。


## 修改站点属性 {#modifying-site-properties}

![chlimage_1-167](assets/chlimage_1-167.png)

通过选择鼠标悬停在站点上时显示的图标，可以修改在站点创建过程中指 `Edit Site`定的现有站点的属性。

`Details of the following properties match the descriptions provided in the` “ [站点创建](#site-creation) ”部分。

![chlimage_1-168](assets/chlimage_1-168.png)

### 修改基本 {#modify-basic}

BASIC面板允许修改：

* 社区站点标题
* 社区站点描述

社区站点名称不得修改。

选择其他社区站点模板不会影响现有的社区站点，因为模板和站点之间没有任何连接。

相反，社 [区站点的](#modify-structure) STRUCTURE可以被修改。

### 修改结构 {#modify-structure}

STRUCTURE面板允许修改最初从所选社区站点模板创建的结构。 从面板中，可以：

* 将其他社区功能拖 [放到站点结](/help/communities/functions.md) 构中。
* 在站点结构中社区功能的实例上：

   * **`gear icon`**

      编辑设置，包括显示标题和URL名称*以及特权成 [员组](/help/communities/users.md#privilegedmembersgroups)。

   * **`trashcan icon`**

      从站点结构中删除（删除）功能。

   * **`grid icon`**

      修改站点顶级导航栏中显示的函数顺序。

>[!NOTE]
>
>除了顶部的函数外，您可以更改“站点结构”中所有函数的顺序。 因此，不能更改社区站点的主页。


>[!CAUTION]
>
>* 虽然显示标题可以在不产生副作用的情况下进行更改，但不建议编辑属于社区站点的社区功能的URL名称。
>
>
例如，重命名URL不会移动现有UGC，因此具有“丢失”UGC的效果。


>[!CAUTION]
>
>组函数不能 *是**站点结构中的第一个* ，也不能是唯一的函数。
>
>必须首先包含并列出任何其 [他函数](/help/communities/functions.md#page-function)，如页面函数。


#### 示例：将目录功能添加到社区站点结构 {#example-adding-a-catalog-function-to-a-community-site-structure}

![chlimage_1-169](assets/chlimage_1-169.png)

### 修改设计 {#modify-design}

“设计”面板允许应用新主题：

* [社区站点主题](#community-site-theme)
* [社区站点品牌化](#community-site-branding)

   * 滚动到面板底部以更改品牌图像。

### 修改设置 {#modify-settings}

“设置”面板允许访问社区站点创建步骤3的子面板下的大多数设置：

* [用户管理](#user-management)
* [标记](#tagging)
* [审核](#moderation)
* [成员角色](#roles)
* [分析](#analytics)
* [翻译](#translation)

### 修改缩略图 {#modify-thumbnail}

THUMBNAIL面板允许上传图像以在“社区站点”控制台中代表站点。

### 修改启用 {#modify-enablement}

ENABLEMENT面板允许访问在社区站点创建过程中提供的设置。

请参阅 [ENABLEMENT](#enablement) description。

## 发布站点 {#publishing-the-site}

在新创建或修改社区站点后，可以通过选择鼠标悬停在站点上时显示的图标来发布（激活）该站 `Publish Site` 点。

![chlimage_1-170](assets/chlimage_1-170.png)

站点成功发布后，将显示一个指示。

![chlimage_1-171](assets/chlimage_1-171.png)

### 使用嵌套组发布 {#publishing-with-nested-groups}

发布社区站点后，必须单独发布使用“组”控制台创建的每个子社区(嵌套 [组)](/help/communities/groups.md)。

## 导出站点 {#exporting-the-site}

![chlimage_1-172](assets/chlimage_1-172.png)

选择导出图标，鼠标悬停在站点上，可创建存储在包管理器中和已下载的社区站点 [的包](/help/sites-administering/package-manager.md) 。

请注意，UGC未包含在站点包中。

## 删除站点 {#deleting-the-site}

![删除图标](assets/deleteicon.png)

要删除社区站点，请选择将鼠标悬停在Communities站点控制台中站点上时显示的“删除站点”图标。 此操作将删除与站点关联的所有项目，如UGC、用户组、资产和数据库记录。

## 创建的社区用户组 {#created-community-user-groups}

发布新社区站点后，新成员组(在发布环境中创建用户组)将具有为各种管理和成员角色设置的相应权限。

为成员组创建的名称包括步骤1 *（URL中显示的名称）中为站点指定的站点名称*[](#step13asitetemplate) ，以及一个唯一ID，以避免与社区站点以及具有不同社区站点根目录的站点名相同的组发生冲突。

例如，如果标题为“入门教程”的站点的名称为“engage”，则版主的用户组将为：

* title:社区参与版主
* name:community-*engage-uid*-moderators

请注意，在创建站点时，任何成员都将作为审核者或组管理员分配角色，并将其分配给相应的组以及成员组。 发布新站点时，将在发布时创建这些组和成员分配。

有关详细信息，请 [参阅管理用户和用户组](/help/communities/users.md)。

>[!NOTE]
>
>如果允 [许社交登录：在用户组启用后](#user-management) ,Facebook即会启用
>
>* `community-<site-name>-<uid>-members`
>
>
创建后，应将应 [用的Facebook云服务](/help/communities/social-login.md#createafacebookcloudservice) ，配置为将用户添加到此组。


## 配置身份验证错误 {#configure-for-authentication-error}

默认情况下，当用户输入错误的凭据且无法登录时，社区站点将重定向到示例登录页面。 此示例登录名在生产服务器上不 [存在](/help/sites-administering/production-ready.md)。

要正确重定向，在将站点配置并推送到发布后，请完成以下步骤，以使身份验证失败而重定向到社区站点：

* 在每个AEM发布实例上。
* 使用管理员权限登录。
* 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)。

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

* 找到 `Adobe Granite Login Selector Authentication Handler`。
* 选择图 `pencil` 标以打开要编辑的配置。
* 输入登 **录页面映射** ，如下所示：

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   例如：
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* 选择&#x200B;**保存**。

![chlimage_1-173](assets/chlimage_1-173.png)

### 测试身份验证重定向 {#test-authentication-redirection}

在配置了社区站点登录页面映射的同一AEM发布实例上：

* 浏览到社区站点主页。

   * 例如， [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 选择“注销”。
* 选择“登录”。
* 输入明显不正确的凭据，如用户名“x”和密码“x”。
* 登录页面应显示“登录名无效”错误。

![chlimage_1-174](assets/chlimage_1-174.png)

## 从“主站点”控制台访问社区站点 {#accessing-community-sites-from-main-sites-console}

在全局导航站点控制台中，社区站点位于文件夹 `Community Sites` 中。

虽然可以通过这种方式访问社区站点，但对于管理任务，应从“社区站点”控制台访问社区站点。

![chlimage_1-175](assets/chlimage_1-175.png)

