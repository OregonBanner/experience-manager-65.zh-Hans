---
title: 社区站点控制台
seo-title: Communities Sites Console
description: 如何访问社区站点控制台
seo-description: How to access the Communities Sites console
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '3278'
ht-degree: 4%

---

# 社区站点控制台 {#communities-sites-console}

社区站点控制台提供对以下内容的访问：

* 站点创建
* 网站编辑
* 站点管理
* [创建和编辑嵌套组](/help/communities/groups.md) （子社区）

参见 [AEM Communities快速入门](/help/communities/getting-started.md) 体验在创作环境中创建社区站点的速度以及如何从创作和发布环境创建社区组。

>[!NOTE]
>
>用于创建的主社区菜单 [社区站点](/help/communities/sites-console.md)， [社区站点模板](/help/communities/sites.md)， [社区组模板](/help/communities/tools-groups.md) 和 [社区功能](/help/communities/functions.md) 仅用于创作环境。

## 前提条件 {#prerequisites}

在创建社区站点之前，它是 *必需* 至：

* 确保一个或多个发布实例正在运行。
* 启用 [隧道服务](/help/communities/deploy-communities.md#tunnel-service-on-author) 管理成员和成员组。
* 识别 [主要发布者](/help/communities/deploy-communities.md#primary-publisher).
* [配置复制](/help/communities/deploy-communities.md#replication-agents-on-author) 当主发布服务器端口不是默认端口时(4503)。

为确保站点能够支持多种功能，最佳实践是执行以下步骤：

* 安装 [最新功能包](/help/communities/deploy-communities.md#latestfeaturepack).
* 启用 [Adobe Analytics](/help/communities/analytics.md) 适用于AEM Communities的。
* 配置 [电子邮件](/help/communities/email.md)
* 识别 [社区管理员](/help/communities/users.md#creating-community-members).
* [启用OAuth处理程序](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) 用于社交登录。

## 访问社区站点控制台 {#accessing-communities-sites-console}

在创作环境中，要访问社区站点控制台，请执行以下操作：

* 从全局导航： **[!UICONTROL Communities]** > **[!UICONTROL 站点]**

“社区站点”控制台显示任何现有的社区站点。 从此控制台中，可以创建、编辑、管理和删除社区站点。

要创建新的社区站点，请选择 **创建** 图标。

要访问现有社区站点，以便创作、修改、发布、导出或添加嵌套组，请选择站点的文件夹图标。

例如，下图显示了主要的社区站点控制台，其中显示了两个社区站点的文件夹： [启用](/help/communities/getting-started-enablement.md) 和 [参与](/help/communities/getting-started.md)：

![站点控制台](assets/site-console.png)

## 站点创建 {#site-creation}

站点创建控制台提供了一种分步方法，用于根据选定的站点来组装站点的功能 [社区站点模板](/help/communities/sites.md) 和设置。

创建的每个网站都包含登录功能，因为网站访客在发布内容、发送消息或参与群组之前需要登录。 其他包括的功能包括用户配置文件、消息传送、通知、网站菜单、搜索、主题设定和品牌推广。

通过选择 `Create` 按钮进行调试。

创建过程是一系列步骤，以包含要配置的一组功能的面板的形式呈现（以子面板的形式呈现）。 可以前进到 **下一个** 步骤或 **返回** 到上一步，然后再在最后一步中提交站点。

### 步骤1 ：站点模板 {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

在“站点模板”面板上，指定标题、描述、站点根、基本语言、名称和站点模板：

* **社区站点标题**

   站点的显示标题。

   标题会显示在已发布的站点以及站点管理员UI中。

* **社区站点描述**

   站点的描述。

   描述未出现在已发布的网站上。

* **社区站点根目录**

   站点的根路径。

   默认根目录为 `/content/sites`，但根目录可能会移到网站中的任何位置。

* **社区站点基本语言**

   （对于单语言则保持原样：英语）使用下拉菜单选择一种语言 *或更多* 可用语言的基础语言 — 德语、意大利语、法语、日语、西班牙语、葡萄牙语（巴西）、繁体中文、简体中文。 将为每种添加的语言创建一个社区站点，并按照中所述的最佳实践存在于同一站点文件夹中 [翻译多语言站点的内容](/help/sites-administering/translation.md). 每个站点的根页面将包含一个由所选语言之一的语言代码命名的子页面，例如“en”表示英语，“fr”表示法语。

* **社区站点名称**:

   显示在URL中的站点根页面的名称。

   * 请仔细检查名称，因为创建站点后更改名称并不容易。
   * 基本URL ( `https://server:port/site root/site name)` 将显示在 `Community Site Name`.

   * 对于有效的URL，请附加基本语言代码+ &quot;。html&quot;

      *例如*， `https://localhost:4502/content/sites/mysight/en.html`

* **社区站点模板** 菜单

   使用下拉菜单选择一个可用的 [社区站点模板](/help/communities/tools.md).

* 选择&#x200B;**下一步**。

### 第2步：设计 {#step-design}

“设计”面板包含2个子面板，用于选择主题和品牌推广横幅：

#### 社区站点主题 {#community-site-theme}

![Sitetheme](assets/sitetheme.png)

框架使用 `Twitter Bootstrap` 为站点提供响应式灵活设计。 可以选择多个预载的Bootstrap主题之一来设置所选社区站点模板的样式，或者可以上传Bootstrap主题。

选中后，主题将叠加一个不透明的蓝色复选标记。

在社区站点发布后，可以 [编辑属性](#modifying-site-properties) 并选择其他主题。

#### 社区站点品牌化 {#community-site-branding}

![网站品牌化](assets/site-branding.png)

社区站点品牌推广是作为标题显示在每个页面顶部的图像。

图像大小应设置为与页面在浏览器中的预期显示宽度一样宽，高度为120像素。

创建或选择图像时，请记住：

* 图像高度将裁剪为从图像的上边缘开始测量的120像素。
* 图像被固定到浏览器窗口的左边缘。
* 不调整图像大小，因此当图像宽度为……

   * 小于浏览器的宽度，图像将水平重复。
   * 大于浏览器的宽度，图像似乎将被裁剪。

* 选择&#x200B;**下一步**。

### 步骤3 ：设置 {#step-settings}

“设置”面板包含多个子面板，这些子面板演示了在进入创建站点的最后一步之前要配置的功能。

* [用户管理](#user-management)
* [标记](#tagging)
* [角色](#roles)
* [审核](#moderation)
* [ANALYTICS](#analytics)
* [翻译](#translation)
* [启用](#enablement)

>[!NOTE]
>
>**启用通道服务**
>
>有几个“设置”子面板允许分配一个受信任的成员来审核UGC、管理组或成为发布环境中启用资源的联系人。
>
>该惯例适用于发布端 [用户和用户组](/help/communities/users.md) （成员和成员组）。
>
>因此，在创作环境中创建社区站点并将受信任成员分配给各种角色时，必须从发布环境中检索成员数据。
>
>这是通过启用 ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` （创作环境）。

#### 用户管理 {#user-management}

![createsitesettings](assets/createsitesettings.png)

>[!NOTE]
>
>建议 [启用社区站点](/help/communities/overview.md#enablement-community) 保密（有关更多信息，请与您的客户代表联系）。
>
>当匿名网站访客被拒绝访问时，社区网站是私有的，不能自行注册，也不能使用社交登录。

* **允许用户注册**

   如果选中，站点访客可以通过自助注册成为社区成员。
如果未选中，则社区站点为 *受限* 必须将和站点访客分配到社区站点的成员组、提出请求或通过电子邮件向其发送邀请。 如果未选中，则不应允许匿名访问。
取消选中 *私有* 社区站点。 默认值为已选中。

* **允许匿名访问**

   如果选中，则社区站点为*open *并且任何站点访客都可以访问该站点。
如果未选中，则只有已登录成员才能访问该站点。
取消选中*private *community站点。 默认值为已选中。

* **允许发送消息**

   如果选中，则成员可以相互发送消息并发送给社区站点中的组。
如果未选中，则不会为社区设置消息。
默认值为未选中。

* **允许社交登录: Facebook**

   如果选中，则允许网站访客使用其Facebook帐户凭据登录。 选定的 [facebook云配置](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) 创建社区站点后，应将用户配置为将用户添加到社区站点的成员组。
如果未选中，则不会显示任何Facebook登录。
取消选中 *私有* 社区站点。 默认值为未选中。

* **允许社交登录: Twitter**

   如果选中，则允许网站访客使用其Twitter帐户凭据登录。 选定的 [twitter云配置](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) 创建社区站点后，应将用户配置为将用户添加到社区站点的成员组。
如果未选中，则不会显示任何Twitter登录。
取消选中 *私有* 社区站点。 默认值为未选中。

>[!NOTE]
>
>**允许社交登录**
>
>虽然示例Facebook和Twitter配置可能存在并且可选，但对于 [生产环境](/help/sites-administering/production-ready.md)，则需要创建自定义Facebook和Twitter应用程序。 参见 [使用Facebook和Twitter进行社交登录](/help/communities/social-login.md).

#### 标记 {#tagging}

![网站标记](assets/site-tagging.png)

可应用于社区内容的标记可通过选择之前通过 [标记控制台](/help/sites-administering/tags.md#tagging-console).

此外，为社区站点选择标记命名空间会限制在定义目录和资源时显示的选择。 参见 [标记启用资源](/help/communities/tag-resources.md) 以获取重要信息。

* 文本搜索框：开始键入以标识允许在网站上使用的标记。

#### 角色 {#roles}

![社区角色](assets/site-admin-2.png)

此 [社区成员的角色](/help/communities/users.md) 会分配这些设置。

使用提前输入搜索可以轻松查找社区成员。

* **社区管理员**

   开始键入以选择一个或多个社区成员或成员组，这些成员或成员组可以管理社区成员和成员组。

* **社区审查方**

   开始键入以选择一个或多个社区成员或成员组，这些成员或成员组将被信任为用户生成内容的审查方。

* **拥有权限的社区成员**

   开始键入以选择一个或多个社区成员或成员组，以便在以下情况下创建新内容 `Allow Privileged Member` 已为 [社区功能](/help/communities/functions.md).

* **社区管理员**

   开始键入以选择一个或多个站点管理员，这些管理员可以独立于其他站点管理员和默认社区管理员来处理站点结构。 他们可以在层次结构的任何级别创建组，并成为嵌套组的默认管理员（但以后可以从嵌套组的管理员角色中删除他们）。

#### 审核 {#moderation}

![网站审核](assets/site-moderation.png)

用于审核用户生成内容(UGC)的全局设置由这些设置控制。 单个组件具有用于控制审核的其他设置。

* **内容已通过预审**

   如果选中，则发布的社区内容只有在获得审查方批准后才会显示。 默认值为未选中。 有关更多信息，请参阅 [审核社区内容](/help/communities/moderate-ugc.md#premoderation).

* **标记阈值，达到此值后隐藏内容**

   如果大于0，则在从公共视图隐藏主题或帖子之前，必须标记该主题或帖子的次数。 如果设置为–1，则标记的主题或帖子永远不会从公共视图中隐藏。 默认值为5。

#### ANALYTICS {#analytics}

![site-analytics](assets/site-analytics.png)

* **启用 Analytics**

   仅在Adobe Analytics已 [已配置](/help/communities/analytics.md) 社区功能。
默认值为未选中。 选中后，会出现其他选择菜单：

![site-analytics-enable](assets/site-analytics-enable.png)

* **云配置框架引用**

   从下拉菜单中，选择为此社区站点配置的Analytics Cloud Service框架。
   `Communities` 是中的框架示例 [适用于社区功能的Analytics配置](/help/communities/analytics.md#aem-analytics-framework-configuration) 文档。

#### 翻译 {#translation}

![站点翻译](assets/site-translation.png)

* **允许机器翻译**

   选中后（默认取消选中），将在站点中为UGC启用机器翻译。 这不会影响任何其他内容，例如页面内容，即使站点设置为多语言站点也是如此。 参见 [翻译用户生成的内容](/help/communities/translate-ugc.md) 有关为AEM Communities配置许可翻译服务的信息。 参见 [翻译多语言站点的内容](/help/sites-administering/translation.md) 以了解完整的概述。

![allow-machine-translation](assets/allow-machine-translation.png)

* **为选定的语言启用机器翻译**

   为机器翻译启用的语言默认为指定的系统设置。 [翻译集成配置](/help/communities/translate-ugc.md#translation-integration-configuration). 可以通过删除默认设置和/或从下拉菜单中选择其他语言来覆盖此站点的这些默认设置。

* **选择翻译提供商**

   默认情况下，服务提供商是试用服务，使用 `microsoft` 仅供演示之用。 如果没有许可翻译服务提供商， **允许机器翻译** 应取消选中。

* **选择全球共享商店**

   对于具有多个语言副本的网站，全局共享存储区提供从每个语言副本中可见的单个会话线程。 这是通过选择作为语言副本包含的语言之一来实现的。 默认为 *无全局共享存储*.

* **选择翻译提供商配置**

   选择 [翻译集成框架](/help/sites-administering/tc-tic.md) 为许可翻译提供商创建。

* **为您的社区站点选择翻译选项**

   * **翻译整个页面**

      如果选择，则页面上的所有UGC都将翻译为该页面的基本语言。

      默认为 *未选择*.

   * **仅翻译选定内容**

      如果选择此选项，则翻译选项会显示在每个帖子旁边，以允许将单个帖子翻译为页面的基本语言。
默认为 *已选择*.

* **选择持久性选项**

   * **根据用户请求翻译贡献内容，并在此后持续**
如果选择，则在发出请求之前不会翻译内容。 翻译后，翻译将存储在存储库中。

      默认为 *未选择*.

   * **不保留翻译**

      如果选择，则翻译不会存储在存储库中。

      如果未选择，则会保留翻译。

      默认为 *未选择*.

* **智能渲染**

   选择以下选项之一：

   * `Always show contributions in the original language`（默认）
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### 启用 {#enablement}

![站点启用](assets/site-enablement.png)

此 `ENABLEMENT`当选定的社区站点模板包含 [指定任务功能](/help/communities/functions.md#assignments-function)，在许可启用功能并且 [已配置](/help/communities/enablement.md). 包含工作分配功能的引用站点模板是 `Reference Structured Learning Site Template.`

* **启用管理器**
（必需）仅 `Community Enablementmanagers` 可以选择组来管理此启用社区。 启用经理负责将成员分配给资源。 另请参阅 [管理用户和用户组](/help/communities/users.md).

* **Marketing Cloud 组织 ID**

   （可选）的ID [视频心率分析](/help/communities/analytics.md#video-heartbeat-analytics) 许可证。

* 选择&#x200B;**下一步**。

### 步骤4 ：创建社区站点 {#step-create-communities-site}

如果需要任何调整，请使用 **返回** 按钮来制作它们。

一次 **创建** 选择并启动，则创建站点的过程无法中断。

创建站点后：

* 不支持更改url（节点名称）。
* 对社区站点模板的未来更改不会影响已创建的社区站点。
* 禁用社区站点模板不会影响已创建的社区站点。
* 可以编辑 [结构](#modify-structure) 社区站点的属性。

![create-site](assets/create-site1.png)

当流程完成时，新站点的文件夹会显示在Communities Sites控制台中，作者可以在其中添加页面内容，管理员可以修改站点的属性。

![modify-site-property](assets/modify-site-property.png)

要修改社区站点，请选择其项目文件夹以将其打开：

![site-project](assets/site-project.png)

当使用鼠标将鼠标悬停在站点上或触摸站点卡时，将显示允许以下操作的图标： [在创作模式下编辑站点](#authoring-site-content)， [打开站点属性以进行修改](#modifying-site-properties)， [发布站点](#publishing-the-site)， [导出站点](#exporting-the-site)、和 [删除站点](#deleting-the-site).

## 创作站点内容 {#authoring-site-content}

可以使用与任何其他AEM网站相同的工具创作站点的内容。 要打开站点进行创作，请选择 `Open Site` 图标。 该站点将在新选项卡中打开，以便社区站点控制台保持可访问状态。

![site-content](assets/site-content.png)

>[!NOTE]
>
>如果不熟悉AEM，请查看文档 [基本处理](/help/sites-authoring/basic-handling.md) 和 [页面创作快速指南](/help/sites-authoring/qg-page-authoring.md).

## 修改站点属性 {#modifying-site-properties}

![edit-site](assets/edit-site.png)

在站点创建过程中指定的现有站点的属性，可以通过选择 `Edit Site`图标。

`Details of the following properties match the descriptions provided in the` [站点创建](#site-creation) 部分。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 修改基本 {#modify-basic}

BASIC面板允许修改：

* 社区站点标题
* 社区站点描述

不能修改社区站点名称。

选择其他社区站点模板不会影响现有社区站点，因为模板和站点之间没有连接。

相反， [结构](#modify-structure) 可以修改社区站点的。

### 修改结构 {#modify-structure}

“结构”面板允许修改最初从所选社区站点模板创建的结构。 在面板中，可以：

* 拖放其他 [社区功能](/help/communities/functions.md) 放入站点结构中。
* 在站点结构中的社区功能实例上：

   * **`gear icon`**

      编辑设置，包括显示标题和URL名称*以及 [拥有权限的成员组](/help/communities/users.md#privilegedmembersgroups).

   * **`trashcan icon`**

      从站点结构中移除（删除）函数。

   * **`grid icon`**

      修改网站顶级导航栏中显示的函数的顺序。

>[!NOTE]
>
>您可以更改“站点结构”中所有函数（顶部函数除外）的顺序。 因此，无法更改社区站点的主页。

>[!CAUTION]
>
>* 尽管显示标题可能会发生更改并且不会产生副作用，但建议不要编辑属于社区站点的社区函数的URL名称。
>
>例如，重命名URL将不会移动现有UGC，因此会导致“丢失”UGC。

>[!CAUTION]
>
>组函数必须 *非* 是 *第一个也不是唯一的* 在站点结构中的函数。
>
>任何其他函数，例如 [页面函数](/help/communities/functions.md#page-function)必须先包含并列出。

#### 示例：向社区站点结构添加目录函数 {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### 修改设计 {#modify-design}

“设计”面板允许应用新主题：

* [社区站点主题](#community-site-theme)
* [社区站点品牌化](#community-site-branding)

   * 滚动到面板底部以更改品牌图像。

### 修改设置 {#modify-settings}

通过“设置”面板，可以访问社区站点创建步骤3的子面板下的大多数设置：

* [用户管理](#user-management)
* [标记](#tagging)
* [审核](#moderation)
* [成员角色](#roles)
* [分析](#analytics)
* [翻译](#translation)

### 修改缩略图 {#modify-thumbnail}

利用“缩略图”面板，可以上传图像以在“社区站点”控制台中表示站点。

### 修改启用 {#modify-enablement}

“启用”面板允许访问在创建社区站点期间提供的设置。

请参阅 [启用](#enablement) 描述。

## 发布站点 {#publishing-the-site}

新建或修改社区站点后，可以通过选择 `Publish Site` 图标，将鼠标悬停在该站点上时显示。

![publish-site](assets/publish-site.png)

成功发布站点后将显示指示。

![站点已发布](assets/site-published.png)

### 使用嵌套组发布 {#publishing-with-nested-groups}

发布社区站点后，需要单独发布使用创建的每个子社区（嵌套组） [组控制台](/help/communities/groups.md).

## 导出站点 {#exporting-the-site}

![export-site](assets/export-site.png)

将鼠标悬停在站点上时，选择导出图标，以创建社区站点的资源包，该资源包均存储于 [包管理器](/help/sites-administering/package-manager.md) 并下载。

请注意，UGC未包含在站点包中。

## 删除站点 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

要删除社区站点，请选择将鼠标悬停在社区站点控制台中的站点上时显示的删除站点图标。 此操作删除与站点关联的所有项目，例如UGC、用户组、资源和数据库记录。

## 已创建社区用户组 {#created-community-user-groups}

发布新的社区站点后，将新建成员组（在发布环境中创建用户组），这些成员组具有为各种管理和成员角色设置的相应权限。

为成员组创建的名称包括 *site-name* 给定的站点位于 [步骤1](#step13asitetemplate) （显示在URL中的名称）以及唯一ID，以避免与具有不同社区站点根的具有相同站点名称的社区站点和组发生冲突。

例如，如果名为“Getting Started Tutorial”的网站的名称为“engage”，则版主的用户组将为：

* title： Community Engage版主
* 名称： community-*engage-uid* — 审查方

请注意，在创建站点时，任何被分配了版主或组管理员角色的成员，都将分配到相应的组，并分配到成员组。 发布新站点时，会在发布时创建这些组和成员分配。

有关详细信息，请参阅 [管理用户和用户组](/help/communities/users.md).

>[!NOTE]
>
>如果 [允许社交登录： Facebook](#user-management) 一旦用户组启用
>
>* `community-<site-name>-<uid>-members`
>
>创建，应用 [facebook cloud service](/help/communities/social-login.md#createafacebookcloudservice) 应配置为将用户添加到此组。

## 配置身份验证错误 {#configure-for-authentication-error}

默认情况下，当用户输入错误的凭据但登录失败时，社区站点将重定向到示例登录页面。 此示例登录不会出现在 [生产服务器](/help/sites-administering/production-ready.md).

要正确重定向，在配置站点并推送至发布站点后，请完成以下步骤以获得身份验证失败，从而重定向至社区站点：

* 在每个AEM发布实例上。
* 使用管理员权限登录。
* 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md).

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* 查找 `Adobe Granite Login Selector Authentication Handler`.
* 选择 `pencil` 图标以打开配置进行编辑。
* 输入 **登录页面映射** 如下所示：

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   例如：
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* 选择&#x200B;**保存**。

![auth-error](assets/auth-error.png)

### 测试身份验证重定向 {#test-authentication-redirection}

在配置了社区站点的登录页面映射的同一AEM发布实例上：

* 浏览到社区站点主页。

   * 例如， [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 选择“注销”。
* 选择“登录”。
* 输入明显不正确的凭据，如用户名“x”和密码“x”。
* 登录页面应显示“无效登录”错误。

![测试身份验证](assets/test-authentication.png)

## 从主站点控制台访问社区站点 {#accessing-community-sites-from-main-sites-console}

从全局导航站点控制台中，社区站点位于 `Community Sites` 文件夹。

虽然可以通过此方式访问社区站点，但对于管理任务，应从社区站点控制台访问社区站点。

![访问站点](assets/access-site.png)
