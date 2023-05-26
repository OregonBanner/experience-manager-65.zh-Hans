---
title: 创作新社区站点
seo-title: Author a New Community Site
description: 如何创作新的AEM Communities站点
seo-description: How to author a new AEM Communities site
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 2%

---

# 创作新社区站点{#author-a-new-community-site}

## 创建社区站点 {#create-a-community-site}

使用创作实例创建社区站点。 在AEM创作实例上：

1. 使用管理员权限登录。
1. 从全局导航，转到 **[!UICONTROL Communities]** > **[!UICONTROL 站点]**.

社区站点控制台提供了一个向导，引导用户完成创建社区站点的步骤。 可以前进到 `Next` 步骤或 `Back` 到上一步，然后再在最后一步中提交站点。

要开始创建新社区站点，请执行以下操作：

* 选择 `Create` 按钮。

![createcommunitysite](assets/createcommunitysite.png)

### 步骤1：站点模板 {#step-site-template}

![创建站点的模板](assets/create-site.png)

在 [站点模板步骤](/help/communities/sites-console.md#step2013asitetemplate)，输入URL的标题、描述和名称，然后选择社区站点模板，例如：

* **社区站点标题**: `Getting Started Tutorial`
* **社区站点描述**: `A site for engaging with the community.`
* **社区站点根目录**：(对于默认根，保留为空 `/content/sites`)
* **云配置**：（如果未指定云配置，则保留为空）提供指向指定云配置的路径。
* **社区站点基本语言**：（对于单语言：英语，保持不变）使用下拉列表选择一种语言 *或更多* 可用语言的基础语言 — 德语、意大利语、法语、日语、西班牙语、葡萄牙语（巴西）、繁体中文、简体中文。 将为每种添加的语言创建一个社区站点，并按照中所述的最佳实践存在于同一站点文件夹中 [翻译多语言站点的内容](/help/sites-administering/translation.md). 每个站点的根页面将包含一个由所选语言之一的语言代码命名的子页面，例如“en”表示英语，“fr”表示法语。

* **社区站点名称**：参与

   * 双击名称，因为创建站点后名称不易更改
   * 初始URL将显示在社区站点名称下方
   * 对于有效的URL，请附加基本语言代码+ &quot;。html&quot;
   * *例如*， https://localhost:4502/content/sites/ `engage/en.html`

* **模板**：下拉菜单以选择 `Reference Site`

* 选择&#x200B;**下一步**。

### 第2步：设计 {#step-design}

“设计”步骤分为两个部分，用于选择主题和品牌推广横幅：

#### 社区站点主题 {#community-site-theme}

选择要应用于模板的所需样式。 选中后，主题将覆盖一个复选标记。

#### 社区站点品牌化 {#community-site-branding}

（可选）上传横幅图像以在网站页面上显示。 横幅将固定到浏览器的左边缘，位于社区网站标题和导航链接之间。 横幅高度将裁剪为120像素。 不会调整横幅大小以适合浏览器的宽度和120像素高度。

![社区站点品牌化](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

选择&#x200B;**下一步**。

### 步骤3：设置 {#step-settings}

在设置步骤中，选择之前 `Next`，请注意，有7个部分提供了对配置的访问权限，这些配置涉及用户管理、标记、审核、组管理、分析和翻译。

#### 用户管理 {#user-management}

选中所有复选框 [User Management](/help/communities/sites-console.md#user-management)

* 允许网站访客自行注册
* 允许网站访客在不登录的情况下查看网站
* 允许成员发送和接收来自其他社区成员的消息
* 允许使用Facebook登录，而不是注册和创建用户档案
* 允许使用Twitter登录，而不是注册和创建用户档案

>[!NOTE]
>
>对于生产环境，需要创建自定义Facebook和Twitter应用程序。 参见 [使用Facebook和Twitter进行社交登录](/help/communities/social-login.md).

![社区站点设置](assets/site-settings.png)

#### 标记 {#tagging}

AEM可以应用于社区内容的标记可通过选择之前通过 [标记控制台](/help/sites-administering/tags.md#tagging-console) (例如 [教程命名空间](/help/communities/setup.md#create-tutorial-tags))。

使用预输入搜索可以轻松查找命名空间。 例如，

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

如果Adobe Analytics已获得许可并且配置了Analytics云服务和框架，则可以启用Analytics并选择框架。

参见 [适用于社区功能的Analytics配置](/help/communities/analytics.md).

![分析](assets/analytics.png)

#### 翻译 {#translation}

此 [翻译设置](/help/communities/sites-console.md#translation) 指定站点的基本语言，以及是否可以翻译UGC和可以翻译成哪种语言（如果有）。

* Check **允许机器翻译**
* 保留默认机器翻译服务选择的默认翻译语言
* 保留默认翻译提供商和配置
* 由于没有语言副本，因此不需要全局存储
* 选择 **翻译整个页面**
* 保留默认持久性选项

![translation-set](assets/translation-settings.png)

### 步骤4：创建社区站点 {#step-create-communities-site}

选择 **创建。**

![create-site](assets/create-site2.png)

该过程完成后，新站点的文件夹将显示在社区 — 站点控制台中。

![communitiessitesconsole](assets/communitiessitesconsole.png)

## 发布社区站点 {#publish-the-community-site}

应从“社区 — 站点”控制台管理已创建的站点，该控制台与可能创建新站点的主控台相同。

选择社区站点的文件夹以将其打开后，将鼠标悬停在站点图标上，以便显示四个操作图标：

![siteactionicons-1](assets/siteactionicons-1.png)

选择第四个省略号图标（“更多操作”）时，将显示“导出站点”和“删除站点”选项。

![siteactionsnew-1](assets/siteactionsnew-1.png)

从左到右分别是：

* **打开站点**

   选择铅笔图标以在作者编辑模式下打开社区站点，以添加和/或配置页面组件

* **编辑站点**

   选择属性图标以打开社区站点来修改属性，例如标题或更改主题

* **发布站点**

   选择世界图标以发布社区站点（例如，如果您的发布服务器在本地计算机上运行，则默认情况下将发布到localhost：4503）

* **导出站点**

   选择导出图标以创建同时存储在中的社区站点资源包 [包管理器](/help/sites-administering/package-manager.md) 并下载。
请注意，UGC未包含在站点包中。

* **删除站点**

   选择删除图标以从中删除社区站点 **[!UICONTROL 社区>站点控制台]**. 此操作删除与站点关联的所有项目，例如UGC、用户组、资源和数据库记录。

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>如果不使用发布实例的默认端口4503，则编辑默认复制代理以将端口号设置为正确的值。
>
>在创作实例上，从主菜单中：
>
>1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复制]** 菜单。
>1. 选择 **[!UICONTROL 作者代理]**.
>1. 选择 **[!UICONTROL 默认代理（发布）]**.
>1. 旁边 **[!UICONTROL 设置]**，选择 **[!UICONTROL 编辑]**.
>1. 在“代理设置”的弹出对话框中，选择 **[!UICONTROL 传输]** 选项卡。
>1. 在URI中，将端口号4503更改为所需的端口号。 例如，要使用端口6103：https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. 选择 **[!UICONTROL 确定]**.
>1. （可选）选择 **[!UICONTROL 清除]** 或 **[!UICONTROL 强制重试]** 以重置复制队列。


### 选择发布 {#select-publish}

确保发布服务器运行后，选择world图标以发布社区站点。

![publish-site](assets/publish-site.png)

成功发布社区站点后，会短暂显示一条消息“站点已发布”。

### 新建社区用户组 {#new-community-user-groups}

除了新社区站点外，还创建了新的用户组，这些用户组具有针对各种管理功能设置的相应权限。 有关详细信息，请访问 [社区站点的用户组](/help/communities/users.md#usergroupsforcommunitysites).

对于这个新的社区站点，假定站点在步骤1中名称为“engage”，则从以下位置可以看到四个新用户组： [组控制台](/help/communities/members.md) （全局导航：社区、组）：

* Community Engage社区管理员
* Community Engage组管理员
* Community Engage成员
* Community Engage审查方
* 社区参与拥有权限的成员
* Community Engage站点内容管理器

请注意 [艾伦·麦当劳](/help/communities/tutorials.md#demo-users) 是以下项的成员

* Community Engage社区管理员
* Community Engage审查方
* Community Engage成员（间接作为审查方组的成员）

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![参与](assets/engage.png)

## 配置身份验证错误 {#configure-for-authentication-error}

配置站点并将其推送到发布后， [配置登录映射](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`)。 好处是，如果未正确输入登录凭据，则身份验证错误将重新显示社区站点的登录页面，并显示错误消息。

添加 `Login Page Mapping` 作为

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## 可选步骤 {#optional-steps}

### 更改默认主页 {#change-the-default-home-page}

在使用发布站点进行演示时，将默认主页更改为新站点可能很有用。

为此，需要使用 [CRXDE](https://localhost:4503/crx/de) 精简以编辑 [资源映射](/help/sites-deploying/resource-mapping.md) 发布时显示的表。

要开始使用，请执行以下操作：

1. 在发布实例上，使用管理员权限登录。
1. 浏览到 [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. 在项目浏览器中，展开 `/etc/map.`
1. 选择 `http` 节点：

   * 选择 **创建节点：**

      * **名称** localhost.4503 (do *非* 使用“：”)

      * **类型** [sling：Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 包含新创建的 `localhost.4503` 选定的节点：

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
1. 浏览至https://localhost:4503/。

   * 到达https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>要禁用，只需为添加前缀 `sling:match` 带有“x”的属性值 —  `xlocalhost.4503/$`  — 和 **全部保存**.

![可选步骤](assets/optional-steps.png)

#### 疑难解答：保存映射时出错 {#troubleshooting-error-saving-map}

如果无法保存更改，请确保节点名称为 `localhost.4503`，且使用“点”分隔符，而不是 `localhost:4503` 带有“冒号”分隔符， `localhost`不是有效的命名空间前缀。

![错误消息](assets/error-message.png)

#### 故障排除：无法重定向 {#troubleshooting-fail-to-redirect}

“**$**&#39;位于正则表达式末尾 `sling:match`字符串是至关重要的，因此只有它 `https://localhost:4503/` ，否则重定向值将以URL中server：port之后可能存在的任何路径为前缀。 因此，当AEM尝试重定向到登录页面时，它会失败。

### 修改站点 {#modify-the-site}

最初创建站点后，作者可以使用 [“打开站点”图标](/help/communities/sites-console.md#authoring-site-content) 执行标准AEM创作活动。

此外，管理员可以使用 [“编辑站点”图标](/help/communities/sites-console.md#modifying-site-properties) 修改站点的属性，如标题。

进行任何修改后，请记住 **保存** 并重新&#x200B;**Publish** 网站。

>[!NOTE]
>
>如果不熟悉AEM，请查看文档 [基本处理](/help/sites-authoring/basic-handling.md) 和 [页面创作快速指南](/help/sites-authoring/qg-page-authoring.md).
