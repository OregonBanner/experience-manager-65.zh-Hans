---
title: 创作社区站点
description: 了解如何创作Adobe Experience Manager Communities站点。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 2%

---

# 创作社区站点{#author-a-new-community-site}

## 创建社区站点 {#create-a-community-site}

使用创作实例创建社区站点。 在AEM创作实例上：

1. 使用管理员权限登录。
1. 从全局导航，转到 **[!UICONTROL Communities]** > **[!UICONTROL 站点]**.

社区站点控制台提供了一个向导，引导用户完成创建社区站点的各个步骤。 您可以前进到 `Next` 步骤或 `Back` 到上一步，然后再在最后一步中提交站点。

要开始创建社区站点，请执行以下操作：

* 选择 `Create` 按钮。

![createcommunitysite](assets/createcommunitysite.png)

### 步骤1：站点模板 {#step-site-template}

![创建站点的模板](assets/create-site.png)

在 [站点模板步骤](/help/communities/sites-console.md#step2013asitetemplate)，输入URL的标题、描述和名称，然后选择社区站点模板，例如：

* **社区站点标题**: `Getting Started Tutorial`
* **社区站点描述**: `A site for engaging with the community.`
* **社区站点根目录**：(对于默认根，保留为空 `/content/sites`)
* **云配置**：（如果未指定云配置，则保留为空）提供指定云配置的路径。
* **社区站点基本语言**：（对于单语言：英语，保持不变）使用下拉列表选择一种语言 *或更多* 可用语言的基础语言 — 德语、意大利语、法语、日语、西班牙语、葡萄牙语（巴西）、繁体中文、简体中文。 系统会为添加的每个语言创建一个社区站点，并按照中所述的最佳实践存在于同一站点文件夹中 [翻译多语言站点的内容](/help/sites-administering/translation.md). 每个站点的根页面都包含一个由所选语言之一的语言代码命名的子页面，例如“en”表示英语，“fr”表示法语。

* **社区站点名称**：参与

   * 双击名称，因为创建站点后不易对其进行更改
   * 初始URL显示在社区站点名称下方
   * 对于有效的URL，请附加基本语言代码+“.html”
   * *例如*， https://localhost:4502/content/sites/ `engage/en.html`

* **模板**：下拉以选择 `Reference Site`

* 选择&#x200B;**下一步**。

### 第2步：设计 {#step-design}

“设计”步骤包含两个部分，用于选择主题和品牌推广横幅：

#### 社区站点主题 {#community-site-theme}

选择要应用于模板的所需样式。 选中后，主题上覆盖有复选标记。

#### 社区站点品牌化 {#community-site-branding}

（可选）上传横幅图像以在网站页面上显示。 横幅将固定到浏览器的左边缘，位于社区站点标题和导航链接之间。 横幅高度将裁剪为120像素。 不会调整横幅的大小以适合浏览器的宽度和120像素的高度。

![社区站点品牌化](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

选择&#x200B;**下一步**。

### 步骤3：设置 {#step-settings}

在设置步骤中，选择 `Next`，共七个部分提供对配置的访问权限，这些配置涉及用户管理、标记、审核、组管理、分析和翻译。

#### 用户管理 {#user-management}

选中所有复选框 [User Management](/help/communities/sites-console.md#user-management)

* 允许网站访客自助注册
* 允许网站访客在不登录的情况下查看网站
* 允许成员发送和接收来自其他社区成员的消息
* 允许使用Facebook登录，而不是注册和创建用户档案
* 允许使用Twitter登录，而不是注册和创建配置文件

>[!NOTE]
>
>对于生产环境，需要创建自定义Facebook和Twitter应用程序。 请参阅 [使用Facebook和Twitter进行社交登录](/help/communities/social-login.md).

![社区站点设置](assets/site-settings.png)

#### 标记 {#tagging}

应用于社区内容的标记可通过选择之前通过定义的AEM命名空间来控制 [标记控制台](/help/sites-administering/tags.md#tagging-console) (例如 [教程命名空间](/help/communities/setup.md#create-tutorial-tags))。

使用提前输入搜索可以轻松查找命名空间。 例如，

* 类型 `tut`
* 选择 `Tutorial`

![标记](assets/tagging.png)

#### 角色 {#roles}

[社区成员角色](/help/communities/users.md) 通过“角色”部分中的设置进行分配。

要允许社区成员（或成员组）以社区管理员身份体验站点，请使用预输入搜索并从下拉菜单中的选项中选择成员或组名称。

例如，

* 类型 `q`
* 选择Quinn Harper

>[!NOTE]
>
>[通道服务](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) 允许选择仅存在于发布环境中的成员和组。

![新站点中的用户角色](assets/site-admin-1.png)

#### 审核 {#moderation}

接受默认全局设置 [审核](/help/communities/sites-console.md#moderation) 用户生成内容(UGC)。

![审核](assets/moderation1.png)

#### ANALYTICS {#analytics}

如果Adobe Analytics已获得许可并且已配置Analytics Cloud服务和框架，则可以启用Analytics并选择框架。

请参阅 [用于社区功能的Analytics配置](/help/communities/analytics.md).

![分析](assets/analytics.png)

#### 翻译 {#translation}

此 [翻译设置](/help/communities/sites-console.md#translation) 指定站点的基本语言，以及是否可以将UGC翻译成哪种语言（如果可以）。

* Check **允许机器翻译**
* 保留默认机器翻译服务选择的默认翻译语言
* 保留默认翻译提供商和配置
* 不需要全局存储，因为没有语言副本
* 选择 **翻译整个页面**
* 保留默认持久性选项

![翻译设置](assets/translation-settings.png)

### 步骤4：创建社区站点 {#step-create-communities-site}

选择 **创建。**

![create-site](assets/create-site2.png)

进程完成后，新站点的文件夹将显示在社区 — 站点控制台中。

![社区站点控制台](assets/communitiessitesconsole.png)

## 发布社区站点 {#publish-the-community-site}

创建的站点应从“社区 — 站点”控制台进行管理，该控制台与可能创建新站点的控制台相同。

选择社区站点的文件夹以将其打开后，将鼠标悬停在站点图标上，以便显示四个操作图标：

![siteactionicons-1](assets/siteactionicons-1.png)

选择第四个省略号图标（更多操作）时，将显示导出站点和删除站点选项。

![siteactionsnew-1](assets/siteactionsnew-1.png)

从左到右分别是：

* **打开站点**

  选择铅笔图标将在作者编辑模式下打开社区站点，您可以在其中添加或配置页面组件。

* **编辑站点**

  选择属性图标将打开社区站点以修改属性，例如标题或更改主题。

* **发布站点**

  选择世界图标将发布社区站点（例如，如果您的发布服务器在本地计算机上运行，则默认情况下将发布到localhost：4503）。

* **导出站点**

  选择导出图标将创建社区站点的资源包，此资源包同时存储在 [包管理器](/help/sites-administering/package-manager.md) 并下载。 站点包中未包含UGC。

* **删除站点**

  选择删除图标可从中删除社区站点 **[!UICONTROL 社区>站点控制台]**. 此操作将删除与站点关联的所有项目，例如UGC、用户组、资源和数据库记录。

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>如果未将默认端口4503用于发布实例，请编辑默认复制代理以将端口号设置为正确的值。
>
>在创作实例上，从主菜单中：
>
>1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复制]** 菜单。
>1. 选择 **[!UICONTROL 作者代理]**.
>1. 选择 **[!UICONTROL 默认代理（发布）]**.
>1. 旁边 **[!UICONTROL 设置]**，选择 **[!UICONTROL 编辑]**.
>1. 在“代理设置”弹出对话框中，选择 **[!UICONTROL 传输]** 选项卡。
>1. 在URI中，将端口号4503更改为所需的端口号。 例如，要使用端口6103：https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. 选择 **[!UICONTROL 确定]**.
>1. （可选）选择 **[!UICONTROL 清除]** 或 **[!UICONTROL 强制重试]** 以重置复制队列。

### 选择发布 {#select-publish}

确保发布服务器运行后，选择world图标以发布社区站点。

![publish-site](assets/publish-site.png)

成功发布社区站点后，会短暂显示一条消息“站点已发布”。

### 新建社区用户组 {#new-community-user-groups}

除了新社区站点外，还将创建新的用户组，这些用户组具有针对各种管理功能设置的相应权限。 有关详细信息，请访问 [社区站点的用户组](/help/communities/users.md#usergroupsforcommunitysites).

对于这个新的社区站点，在步骤1中给定站点名称“engage”（参与），将从以下位置看到四个新用户组： [群组控制台](/help/communities/members.md) （全局导航：社区、组）：

* 社区参与社区管理员
* 社区参与组管理员
* Community Engage成员
* Community Engage审查方
* 社区参与拥有权限的成员
* 社区参与站点内容管理器

[艾伦·麦当劳](/help/communities/tutorials.md#demo-users) 是以下成员之一

* 社区参与社区管理员
* Community Engage审查方
* Community Engage成员（间接作为审查方组的成员）

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![参与](assets/engage.png)

## 配置身份验证错误 {#configure-for-authentication-error}

配置站点并将其推送到发布后， [配置登录映射](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`)。 这样做的好处是，当登录凭据输入不正确时，身份验证错误会重新显示社区站点的登录页面，并显示错误消息。

添加 `Login Page Mapping` 作为

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## 可选步骤 {#optional-steps}

### 更改默认主页 {#change-the-default-home-page}

在使用发布站点进行演示时，将默认主页更改为新站点可能很有用。

为此，需要使用 [CRXDE](https://localhost:4503/crx/de) 简化以编辑 [资源映射](/help/sites-deploying/resource-mapping.md) 发布时显示的表。

要开始使用，请执行以下操作：

1. 在发布实例上，使用管理员权限登录。
1. 浏览至 [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. 在项目浏览器中，展开 `/etc/map.`
1. 选择 `http` 节点：

   * 选择 **创建节点：**

      * **名称** localhost.4503 (do *非* 使用“：”)

      * **类型** [sling：Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 具有新创建的 `localhost.4503` 选定的节点：

   * 添加属性:

   * **名称** sling：match
      * **类型** 字符串
      * **值** localhost.4503/$（必须以“$”字符结尾）

   * 添加属性:

      * **名称** sling：internalRedirect
      * **类型** 字符串
      * **值** /content/sites/engage/en.html

1. 选择 **全部保存。**
1. （可选）删除浏览历史记录。
1. 浏览https://localhost:4503/。

   * 抵达https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>要禁用，只需在 `sling:match` 带有“x”的属性值 —  `xlocalhost.4503/$`  — 和 **全部保存**.

![可选步骤](assets/optional-steps.png)

#### 疑难解答：保存映射时出错 {#troubleshooting-error-saving-map}

如果无法保存更改，请确保节点名称为 `localhost.4503`，且使用“点”分隔符，而不是 `localhost:4503` 带有“冒号”分隔符， `localhost`不是有效的命名空间前缀。

![错误消息](assets/error-message.png)

#### 故障排除：无法重定向 {#troubleshooting-fail-to-redirect}

“**$**&#39;正则表达式末尾 `sling:match`字符串至关重要，因此 `https://localhost:4503/` 否则重定向值将前缀为URL中server：port之后可能存在的任何路径。 因此，当AEM尝试重定向到登录页面时，它会失败。

### 修改站点 {#modify-the-site}

最初创建站点后，作者可以使用 [“打开站点”图标](/help/communities/sites-console.md#authoring-site-content) 执行标准的AEM创作活动。

此外，管理员可以使用 [“编辑站点”图标](/help/communities/sites-console.md#modifying-site-properties) 以修改站点的属性，如标题。

进行任何修改后，请记住 **保存** 并且&#x200B;**Publish** 网站。

>[!NOTE]
>
>如果不熟悉AEM，请查看文档 [基本处理](/help/sites-authoring/basic-handling.md) 和 [页面创作快速指南](/help/sites-authoring/qg-page-authoring.md).
