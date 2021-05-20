---
title: 社区站点控制台
seo-title: 社区站点控制台
description: 如何访问社区站点控制台
seo-description: 如何访问社区站点控制台
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
role: Administrator
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3292'
ht-degree: 4%

---


# 社区站点控制台{#communities-sites-console}

社区站点控制台提供对以下项的访问：

* 网站创建
* 网站编辑
* 站点管理
* [创建和编辑嵌套群组](/help/communities/groups.md) （子社区）

请参阅[AEM Communities快速入门](/help/communities/getting-started.md)以体验在创作环境中创建社区站点的速度，以及如何从创作和发布环境创建社区组。

>[!NOTE]
>
>用于创建[社区站点](/help/communities/sites-console.md)、[社区站点模板](/help/communities/sites.md)、[社区组模板](/help/communities/tools-groups.md)和[社区功能](/help/communities/functions.md)的主“社区”菜单仅用于创作环境。

## 前提条件 {#prerequisites}

在创建社区站点之前，*必需*&#x200B;以：

* 确保一个或多个发布实例正在运行。
* 启用[隧道服务](/help/communities/deploy-communities.md#tunnel-service-on-author)以管理成员和成员组。
* 识别[主发布者](/help/communities/deploy-communities.md#primary-publisher)。
* [当主](/help/communities/deploy-communities.md#replication-agents-on-author) 发布者端口不是默认端口时配置复制(4503)。

为确保站点准备好支持许多功能，最佳做法是采取以下步骤：

* 安装[最新功能包](/help/communities/deploy-communities.md#latestfeaturepack)。
* 为AEM Communities启用[Adobe Analytics](/help/communities/analytics.md)。
* 配置[email](/help/communities/email.md)
* 识别[社区管理员](/help/communities/users.md#creating-community-members)。
* [为社交登](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) 录启用OAuth处理程序。

## 访问社区站点控制台{#accessing-communities-sites-console}

在创作环境中，要访问社区站点控制台，请执行以下操作：

* 从全局导航：**[!UICONTROL Communities]** > **[!UICONTROL Sites]**

“社区站点”控制台会显示任何现有的社区站点。 在此控制台中，可以创建、编辑、管理和删除社区站点。

要创建新社区站点，请选择&#x200B;**创建**&#x200B;图标。

要访问现有社区网站，为了创作、修改、发布、导出或添加嵌套群组，请选择网站的文件夹图标。

例如，下图显示了主社区站点控制台，其中显示了两个社区站点的文件夹：[enable](/help/communities/getting-started-enablement.md)和[engage](/help/communities/getting-started.md):

![站点控制台](assets/site-console.png)

## 网站创建{#site-creation}

站点创建控制台提供了根据所选[社区站点模板](/help/communities/sites.md)和设置来分步组合站点功能的方法。

创建的每个网站都包含登录功能，因为网站访客在发布内容、发送消息或参与群组之前，必须先登录。 其他包含的功能包括用户配置文件、消息、通知、网站菜单、搜索、主题和品牌。

通过选择位于社区站点控制台顶部的`Create`按钮，可启动该进程。

创建过程是一系列步骤，这些步骤以面板的形式呈现，其中包含要配置的一组特征（以子面板的形式呈现）。 在最后步骤中提交站点之前，可以前进到&#x200B;**下一步**&#x200B;步骤或&#x200B;**上一步。**

### 步骤1 :网站模板{#step-site-template}

![新站点模板](assets/newsitetemplate.png)

在“站点模板”面板中，指定了“标题”、“描述”、“站点根”、“基本语言”、“名称”和“站点模板”：

* **社区站点标题**

   网站的显示标题。

   标题会显示在已发布的网站以及网站管理员UI中。

* **社区站点描述**

   网站的描述。

   该描述不会显示在已发布的网站上。

* **社区站点根目录**

   站点的根路径。

   默认的根目录为`/content/sites`，但该根目录可以移动到网站中的任意位置。

* **社区站点基本语言**

   (单语言不受影响：英语)使用下拉菜单从可用语言(德语、意大利语、法语、日语、西班牙语、葡萄牙语（巴西）、中文（繁体）和中文（简体）)中选择一个&#x200B;*或多个*&#x200B;基本语言。 将为添加的每种语言创建一个社区站点，并按照[多语言站点翻译内容](/help/sites-administering/translation.md)中描述的最佳实践，将位于同一站点文件夹中。 每个站点的根页面将包含一个子页面，该子页面由所选语言之一的语言代码命名，如“en”表示英语，“fr”表示法语。

* **社区站点名称**:

   站点根页面在URL中显示的名称。

   * 请仔细检查名称，因为创建网站后，该名称不容易更改。
   * 基本URL(`https://server:port/site root/site name)`)将显示在`Community Site Name`的下方。

   * 对于有效的URL，请附加基本语言代码+ &quot;。html&quot;

      *例如*、  `https://localhost:4502/content/sites/mysight/en.html`

* **社区站点模** 板菜单

   使用下拉菜单选择可用的[社区站点模板](/help/communities/tools.md)。

* 选择&#x200B;**下一步**。

### 第2步：设计{#step-design}

“设计”面板包含2个用于选择主题和品牌横幅的子面板：

#### 社区站点主题{#community-site-theme}

![sitetheme](assets/sitetheme.png)

该框架使用[TwitterBootstrap](https://twitterbootstrap.org/)为网站引入响应式灵活设计。 可以选择多个预加载的Bootstrap主题之一来设置所选社区站点模板的样式，或者可以上传Bootstrap主题。

选择后，将使用不透明的蓝色复选标记覆盖主题。

社区网站发布后，可以[编辑属性](#modifying-site-properties)并选择其他主题。

#### 社区网站品牌{#community-site-branding}

![网站品牌化](assets/site-branding.png)

社区网站品牌化是在每个页面顶部显示为标题的图像。

图像的大小应与浏览器中页面的预期显示一样宽，高度应为120像素。

在创建或选择图像时，请记住：

* 图像高度将从图像的上边缘裁剪为120像素。
* 图像已固定到浏览器窗口的左边缘。
* 图像没有调整大小，因此当图像宽度为……

   * 小于浏览器的宽度，图像将水平重复。
   * 大于浏览器的宽度，图像将被裁剪。

* 选择&#x200B;**下一步**。

### 步骤3 :设置{#step-settings}

“设置”面板包含多个子面板，这些子面板显示要在移至创建站点的最后一步之前配置的功能。

* [用户管理](#user-management)
* [标记](#tagging)
* [角色](#roles)
* [审核](#moderation)
* [ANALYTICS](#analytics)
* [翻译](#translation)
* [启用](#enablement)

>[!NOTE]
>
>**启用隧道服务**
>
>几个“设置”子面板允许分配受信任成员以审核UGC、管理组或作为联系人，以在发布环境中获取启用资源。
>
>该约定适用于发布端[用户和用户组](/help/communities/users.md)（成员和成员组）在创作环境中不重复的情况。
>
>因此，在创作环境中创建社区站点并将可信成员分配给各种角色时，需要从发布环境中检索成员数据。
>
>这可以通过为创作环境启用` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)`来完成。

#### 用户管理{#user-management}

![创建站点设置](assets/createsitesettings.png)

>[!NOTE]
>
>建议将[启用社区站点](/help/communities/overview.md#enablement-community)设为私有（有关更多信息，请联系您的客户代表）。
>
>当匿名网站访客被拒绝访问、不能自行注册，以及不能使用社交登录时，社区网站是私有的。

* **允许用户注册**

   如果选中此选项，则网站访客可以通过自行注册成为社区成员。
如果未选中此选项，则社区站点将为*受限*，并且必须将站点访客分配给社区站点的成员组、发出请求或通过电子邮件发送邀请。 如果未选中，则不应允许匿名访问。
取消选中*private*&#x200B;社区站点的复选框。 默认选中。

* **允许匿名访问**

   如果选中，则社区站点将*打开*任何站点访客都可以访问该站点。
如果未选中，则只有已登录的成员才能访问该站点。
取消选中*私有*社区站点。 默认选中。

* **允许发送消息**

   如果选中，则成员可以向彼此发送消息，并向社区站点内的组发送消息。
如果未选中此选项，则不会为社区设置消息传送。
默认为未选中。

* **允许社交登录: Facebook**

   如果选中此项，则允许网站访客使用其Facebook帐户凭据登录。 所选[Facebook云配置](/help/communities/social-login.md#create-a-facebook-connect-cloud-service)应配置为在创建社区站点后将用户添加到社区站点的成员组。
如果未选中，则不会显示Facebook登录。
对于*private*&#x200B;社区站点，请保持未选中状态。 默认为未选中。

* **允许社交登录: Twitter**

   如果选中此项，则允许网站访客使用其Twitter帐户凭据登录。 所选[Twitter云配置](/help/communities/social-login.md#create-a-twitter-connect-cloud-service)应配置为在创建社区站点后将用户添加到社区站点的成员组。
如果未选中，则不会显示Twitter登录。
对于*private*&#x200B;社区站点，请保持未选中状态。 默认为未选中。

>[!NOTE]
>
>**允许社交登录**
>
>虽然示例Facebook和Twitter配置可能存在并且可供选择，但对于[生产环境](/help/sites-administering/production-ready.md)，则需要创建自定义Facebook和Twitter应用程序。 请参阅[使用Facebook和Twitter进行社交登录](/help/communities/social-login.md)。

#### 标记 {#tagging}

![网站标记](assets/site-tagging.png)

可应用于社区内容的标记可通过选择之前通过[Tagging Console](/help/sites-administering/tags.md#tagging-console)定义的标记命名空间来控制。

此外，为社区站点选择标记命名空间会限制在定义目录和资源时显示的选择。 请参阅[标记支持资源](/help/communities/tag-resources.md) ，以了解重要信息。

* 文本搜索框：开始键入内容以识别允许在网站上使用的标记。

#### 角色 {#roles}

![社区角色](assets/site-admin-2.png)

社区成员[的角色](/help/communities/users.md)分配有这些设置。

使用提前键入搜索，可轻松查找社区成员。

* **社区管理员**

   开始键入内容以选择一个或多个可管理社区成员和成员组的社区成员或成员组。

* **社区审查方**

   开始键入内容以选择一个或多个社区成员或成员组，这些成员或成员组将作为用户生成内容的审核者受信任。

* **拥有权限的社区成员**

   开始键入内容以选择一个或多个社区成员或成员组，以便在为[社区函数](/help/communities/functions.md)选择`Allow Privileged Member`时，能够创建新内容。

* **社区管理员**

   开始键入内容以选择一个或多个站点管理员，这些管理员可以独立于其他站点管理员和默认社区管理员处理站点结构。 他们可以在层次结构的任何级别创建群组，并成为嵌套群组的默认管理员（但以后可以从嵌套群组的管理员角色中删除这些群组）。

#### 审核 {#moderation}

![网站审核](assets/site-moderation.png)

审核用户生成内容(UGC)的全局设置由这些设置控制。 单个组件具有用于控制审核的其他设置。

* **内容已通过预审**

   如果选中此项，则在审核者批准后才会显示已发布的社区内容。 默认为未选中。 有关更多信息，请参阅[审核社区内容](/help/communities/moderate-ugc.md#premoderation)。

* **标记阈值，达到此值后隐藏内容**

   如果大于0，则在将主题或帖子隐藏到公共视图中之前必须标记其的次数。 如果设置为–1，则标记的主题或帖子永远不会在公共视图中隐藏。 默认值为5。

#### ANALYTICS {#analytics}

![site-analytics](assets/site-analytics.png)

* **启用 Analytics**

   仅当Adobe Analytics已[配置](/help/communities/analytics.md)用于Communities功能时才可用。
默认为未选中。 选中此选项后，将显示额外的选择菜单：

![启用site-analytics](assets/site-analytics-enable.png)

* **云配置框架引用**

   从下拉菜单中，选择为此社区站点配置的Analytics云服务框架。
   `Communities` 是“Analytics社区配置”功 [能文档中的框架](/help/communities/analytics.md#aem-analytics-framework-configuration) 示例。

#### 翻译 {#translation}

![站点翻译](assets/site-translation.png)

* **允许机器翻译**

   选中此选项（默认选项未选中）后，将为网站中的UGC启用机器翻译。 这不会影响任何其他内容，例如页面内容，即使该网站设置为多语言网站也是如此。 有关为AEM Communities配置授权翻译服务的信息，请参阅[翻译用户生成的内容](/help/communities/translate-ugc.md)。 请参阅[多语言站点的翻译内容](/help/sites-administering/translation.md)以获取完整概述。

![允许机器翻译](assets/allow-machine-translation.png)

* **为选定的语言启用机器翻译**

   为机器翻译启用的语言默认为由[翻译集成配置](/help/communities/translate-ugc.md#translation-integration-configuration)指定的系统设置。 通过删除默认设置和/或从下拉菜单中选择其他语言，可能会覆盖此网站的这些默认设置。

* **选择翻译提供商**

   默认情况下，服务提供商是仅用于演示的试用服务。 `microsoft`如果未授权翻译服务提供商，则应取消选中&#x200B;**允许机器翻译**。

* **选择全球共享商店**

   对于具有多个语言副本的网站，全局共享存储会提供单个会话线程，从每个语言副本中可见。 这可以通过选择其中一种语言作为语言副本来实现。 默认值为&#x200B;*无全局共享存储*。

* **选择翻译提供商配置**

   选择为授权翻译提供商创建的[翻译集成框架](/help/sites-administering/tc-tic.md)。

* **为您的社区站点选择翻译选项**

   * **翻译整个页面**

      如果选择，则页面上的所有UGC都将转换为页面的基本语言。

      默认值为&#x200B;*未选择*。

   * **仅翻译选定内容**

      如果选中，则每个帖子旁边都会显示一个翻译选项，允许将各个帖子翻译成该页面的基本语言。
默认值为*selected*。

* **选择持久性选项**

   * **根据用户请求翻译稿件并在**
之后保留如果选择，则在发出请求之前不会翻译内容。翻译后，翻译会存储在存储库中。

      默认值为&#x200B;*未选择*。

   * **不保留翻译**

      如果选中，则转换不会存储在存储库中。

      如果未选择，则保留翻译。

      默认值为&#x200B;*未选择*。

* **智能渲染**

   选择以下选项之一：

   * `Always show contributions in the original language` (默认)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### 启用 {#enablement}

![站点启用](assets/site-enablement.png)

当所选社区站点模板包含[分配函数](/help/communities/functions.md#assignments-function)时，`ENABLEMENT`设置适用，该函数在授权启用功能并配置[](/help/communities/enablement.md)时可用。 包含赋值函数的引用站点模板为`Reference Structured Learning Site Template.`

* **启用管理器**
（必需）只有群组的成 `Community Enablementmanagers` 员才能被选择来管理此启用社区。支持经理负责将成员分配给资源。 另请参阅[管理用户和用户组](/help/communities/users.md)。

* **Marketing Cloud 组织 ID**

   （可选）[视频心率分析](/help/communities/analytics.md#video-heartbeat-analytics)许可证的ID。

* 选择&#x200B;**下一步**。

### 步骤4 :创建社区站点{#step-create-communities-site}

如果需要进行任何调整，请使用&#x200B;**Back**&#x200B;按钮进行调整。

选择并启动&#x200B;**创建**&#x200B;后，创建站点的过程将无法中断。

创建网站后：

* 不支持更改URL（节点名称）。
* 将来对社区站点模板所做的更改将不会影响已创建的社区站点。
* 禁用社区站点模板不会影响已创建的社区站点。
* 可以通过修改社区站点的属性来编辑其[STRUCTURE](#modify-structure)。

![创建站点](assets/create-site1.png)

完成该过程后，新站点的文件夹将显示在社区站点控制台中，作者可以在此控制台中添加页面内容，或者管理员可以修改站点的属性。

![modify-site-property](assets/modify-site-property.png)

要修改社区站点，请选择其项目文件夹以将其打开：

![站点项目](assets/site-project.png)

将鼠标悬停在网站上或触摸网站卡片时，会显示允许[在创作模式下编辑网站的图标](#authoring-site-content)、[打开网站属性以进行修改](#modifying-site-properties)、[发布网站](#publishing-the-site)、[导出网站](#exporting-the-site)和[删除网站](#deleting-the-site)。

## 创作网站内容{#authoring-site-content}

网站内容的创作工具可能与任何其他AEM网站相同。 要打开站点进行创作，请选择将鼠标悬停在该站点上时显示的`Open Site`图标。 该站点将在新选项卡中打开，以便仍然可以访问社区站点控制台。

![站点内容](assets/site-content.png)

>[!NOTE]
>
>如果不熟悉AEM，请查看有关[基本操作](/help/sites-authoring/basic-handling.md)和[页面创作快速指南的文档](/help/sites-authoring/qg-page-authoring.md)。

## 修改站点属性{#modifying-site-properties}

![编辑站点](assets/edit-site.png)

在站点创建过程中指定的现有站点的属性可以通过选择鼠标悬停该站点时显示的`Edit Site`图标来修改。

`Details of the following properties match the descriptions provided in the` [网站](#site-creation) 创建区域。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 修改基本{#modify-basic}

基本面板允许修改：

* 社区站点标题
* 社区站点描述

不能修改社区站点名称。

选择其他社区站点模板对现有社区站点不会产生任何影响，因为模板和站点之间没有任何连接。

而是可以修改社区站点的[STRUCTURE](#modify-structure)。

### 修改结构{#modify-structure}

“结构”面板允许修改最初从所选社区站点模板创建的结构。 在面板中，可以：

* 将其他[社区函数](/help/communities/functions.md)拖放到站点结构中。
* 在站点结构中社区功能的实例上：

   * **`gear icon`**

      编辑设置，包括显示标题和URL名称*以及[特权成员组](/help/communities/users.md#privilegedmembersgroups)。

   * **`trashcan icon`**

      从站点结构中删除（删除）函数。

   * **`grid icon`**

      修改功能在网站顶级导航栏中显示的顺序。

>[!NOTE]
>
>除了顶部的函数外，您可以更改“网站结构”中所有函数的顺序。 因此，无法更改社区站点的主页。

>[!CAUTION]
>
>* 虽然显示标题可能会发生更改而不会产生副作用，但不建议编辑属于社区站点的社区函数的URL名称。
>
>
例如，重命名URL不会移动现有UGC，因此会产生“丢失”UGC的效果。

>[!CAUTION]
>
>组函数必须&#x200B;*不*&#x200B;是站点结构中的&#x200B;*第一个函数，也不是唯一的*&#x200B;函数。
>
>必须先包含并列出任何其他函数，如[page函数](/help/communities/functions.md#page-function)。

#### 示例：向社区站点结构添加目录函数{#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### 修改设计{#modify-design}

“设计”面板允许应用新主题：

* [社区站点主题](#community-site-theme)
* [社区站点品牌化](#community-site-branding)

   * 滚动到面板底部以更改品牌图像。

### 修改设置{#modify-settings}

“设置”面板允许访问社区站点创建步骤3的子面板下的大多数设置：

* [用户管理](#user-management)
* [标记](#tagging)
* [审核](#moderation)
* [成员角色](#roles)
* [Analytics](#analytics)
* [翻译](#translation)

### 修改缩略图{#modify-thumbnail}

缩略图面板允许上传图像以在社区站点控制台中表示站点。

### 修改启用{#modify-enablement}

启用面板允许访问在社区站点创建期间提供的设置。

请参阅[ENABLEMENT](#enablement)说明。

## 发布网站{#publishing-the-site}

在新创建或修改社区站点后，可以通过选择`Publish Site`图标来发布（激活）该站点，该图标将鼠标悬停在该站点上方。

![publish-site](assets/publish-site.png)

网站成功发布后，将显示一个指示。

![网站已发布](assets/site-published.png)

### 使用嵌套群组{#publishing-with-nested-groups}发布

发布社区站点后，必须单独发布使用[组控制台](/help/communities/groups.md)创建的每个子社区（嵌套组）。

## 导出站点{#exporting-the-site}

![导出站点](assets/export-site.png)

选择将鼠标悬停在站点上的导出图标，以创建社区站点的包，该包既存储在[包管理器](/help/sites-administering/package-manager.md)中，又已下载。

请注意，网站包中未包含UGC。

## 删除站点{#deleting-the-site}

![deleteicon](assets/deleteicon.png)

要删除社区站点，请选择删除站点图标，该图标将鼠标悬停在社区站点控制台中的站点上。 此操作会删除与网站关联的所有项目，如UGC、用户组、资产和数据库记录。

## 已创建社区用户组{#created-community-user-groups}

发布新社区站点后，新的成员组（在发布环境中创建用户组）将拥有为各种管理角色和成员角色设置的适当权限。

为成员组创建的名称包括&#x200B;*site-name*（在[Step 1](#step13asitetemplate)中为站点提供的名称）以及唯一ID，以避免与社区站点和组冲突，这些站点和组具有不同社区站点根的相同站点名称。

例如，如果标题为“Getting Started Tutorial”的网站的名称为“engage”，则审核者的用户组将为：

* 标题：社区参与审核者
* 名称：community-*engage-uid*-moderator

请注意，在创建站点时，任何以审核者或组管理员身份分配角色的成员都将被分配给相应的组，并被分配给成员组。 发布新站点时，将在发布时创建这些组和成员分配。

有关详细信息，请参阅[管理用户和用户组](/help/communities/users.md)。

>[!NOTE]
>
>如果[允许社交登录：Facebook](#user-management)在用户组启用后
>
>* `community-<site-name>-<uid>-members`
>
>
创建后，应将应用的[Facebook云服务](/help/communities/social-login.md#createafacebookcloudservice)配置为将用户添加到此组。

## 验证错误{#configure-for-authentication-error}的配置

默认情况下，当用户输入错误的凭据且无法登录时，社区站点将重定向到示例登录页面。 [生产服务器](/help/sites-administering/production-ready.md)上不存在此登录示例。

要正确重定向，请在配置了网站并将其推送到发布后，完成以下步骤以获取无法重定向到社区站点的身份验证：

* 在每个AEM发布实例上。
* 使用管理员权限登录。
* 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)。

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

* 找到`Adobe Granite Login Selector Authentication Handler`。
* 选择`pencil`图标以打开要编辑的配置。
* 按如下方式输入&#x200B;**登录页面映射**:

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   例如：
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* 选择&#x200B;**保存**。

![auth-error](assets/auth-error.png)

### 测试身份验证重定向{#test-authentication-redirection}

在使用社区站点的登录页面映射配置的同一AEM发布实例上：

* 浏览到社区站点主页。

   * 例如， [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 选择注销。
* 选择登录。
* 输入明显不正确的凭据，如用户名“x”和密码“x”。
* 登录页面应显示“登录无效”错误。

![测试验证](assets/test-authentication.png)

## 从主站点控制台{#accessing-community-sites-from-main-sites-console}访问社区站点

从全局导航站点控制台中，社区站点位于`Community Sites`文件夹中。

虽然可以通过这种方式访问社区站点，但是对于管理任务，应从社区站点控制台访问社区站点。

![访问站点](assets/access-site.png)



