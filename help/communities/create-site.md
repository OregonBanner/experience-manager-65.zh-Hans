---
title: 创作新社区站点
seo-title: 创作新社区站点
description: 如何创作新的AEM Communities站点
seo-description: 如何创作新的AEM Communities站点
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
translation-type: tm+mt
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# 创作新社区站点{#author-a-new-community-site}

## 创建社区站点 {#create-a-community-site}

使用作者实例创建社区站点。 在AEM作者实例上：

1. 使用管理员权限登录。
1. 从全局导航，转到导航、 **社区、站点。**

“社区站点”控制台提供了一个向导，用于指导用户完成创建社区站点的各个步骤。 在最后一步中提交站点之 `Next` 前，可 `Back` 以前进到步骤或前一步。

要开始创建新社区站点，请执行以下操作：

* 选择按 `Create`钮。

![创建社区站点](assets/createcommunitysite.png)

### 第1步：站点模板 {#step-site-template}

![创建站点的模板](assets/create-site.png)

在“站 [点模板”步骤中](/help/communities/sites-console.md#step2013asitetemplate)，输入标题、说明、URL的名称，然后选择社区站点模板，例如：

* **社区站点标题**: `Getting Started Tutorial`
* **社区站点描述**: `A site for engaging with the community.`
* **社区站点根目录**:(默认根目录留空 `/content/sites`)
* **云配置**:（如果未指定云配置，则留空）提供指向指定云配置的路径。
* **社区站点基本语言**:(对于单种语言，请保持不变：英语)使用下拉列表从可用语言( *德语、意大利语* 、法语、日语、西班牙语、葡萄牙语（巴西）、繁体中文（繁体中文）和简体中文)中选择一种或多种基本语言。 将根据多语言站点翻译内容中所述的最佳实践，为添加的每种语言创建一个社区站点，并且该站点将存 [在于同一站点文件夹中](/help/sites-administering/translation.md)。 每个站点的根页面将包含一个子页面，该子页面由所选语言之一的语言代码命名，如英语为“en”或法语为“fr”。

* **社区站点名称**:参与

   * 多次-检查名称，因为创建站点后该名称不易更改
   * 初始URL将显示在“社区站点名称”下方
   * 对于有效的URL，请附加基本语言代码+ &quot;。html&quot;
   * *例如*,https://localhost:4502/content/sites/ `engage/en.html`

* **模板**:下拉选择 `Reference Site`

Select **Next**

### 第2步：设计 {#step-design}

设计步骤分为两个部分，用于选择主题和品牌横幅：

#### COMMUNITY SITE THEME {#community-site-theme}

选择要应用到模板的所需样式。 选择后，主题将覆盖一个复选标记。

#### COMMUNITY SITE BRANDING {#community-site-branding}

（可选）上传要在网站页面中显示的横幅图像。 横幅被固定到浏览器的左边，位于社区站点标题和导航链接之间。 横幅高度会被裁剪为120像素。 横幅的大小不会调整为适合浏览器的宽度和120像素高。

![chlimage_1-58](assets/chlimage_1-58.png) ![chlimage_1-59](assets/chlimage_1-59.png)

选择&#x200B;**下一步**。

### 第3步：设置 {#step-settings}

在“设置”步骤中，在选择 `Next`之前，请注意，有七个部分提供对涉及用户管理、标记、审核、组管理、分析、翻译和启用的配置的访问。

请访问 [AEM Communities的Enablement](/help/communities/getting-started-enablement.md) 入门教程，以体验使用启用功能的经验。

#### 用户管理 {#user-management}

选中用户管理的所 [有复选框](/help/communities/sites-console.md#user-management)

* 允许站点访客自行注册
* 允许站点访客视图站点而不登录
* 允许成员发送和接收来自其他社区成员的消息
* 允许使用Facebook登录，而不是注册和创建用户档案
* 允许使用Twitter登录，而不是注册和创建用户档案

>[!NOTE]
>
>对于生产环境，必须创建自定义Facebook和Twitter应用程序。 请参 [阅使用Facebook和Twitter进行社交登录](/help/communities/social-login.md)。

![社区站点设置](assets/site-settings.png)

#### TAGGING {#tagging}

可以通过选择之前通过标记控制台定义的AEM命名空间(如教程命名空间)来控制可应用于社 [区内容的标](/help/sites-administering/tags.md#tagging-console) 记 [](/help/communities/setup.md#create-tutorial-tags)。

使用预先键入搜索可轻松查找命名空间。 例如，

* 类型 `tut`
* 选择 `Tutorial`

![chlimage_1-60](assets/chlimage_1-60.png)

#### ROLES {#roles}

[社区成员角色](/help/communities/users.md) ，通过“角色”部分中的设置进行分配。

要让社区成员（或成员组）以社区管理者的身份体验站点，请使用“预先键入”搜索并从下拉框的选项中选择成员或用户组名称。

例如，

* 类型 `q`
* 选择 [奎恩·哈珀](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[隧道服务](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) ，允许选择仅在发布环境中存在的成员和组。

![新站点中的用户角色](assets/site-admin-1.png)

#### MODERATION {#moderation}

接受审核用户生成的 [内容](/help/communities/sites-console.md#moderation) (UGC)的默认全局设置。

![chlimage_1-61](assets/chlimage_1-61.png)

#### ANALYTICS {#analytics}

如果Adobe Analytics已获得许可，且已配置Analytics云服务和框架，则可以启用Analytics并选择框架。

请参 [阅社区分析配置功能](/help/communities/analytics.md)。

![chlimage_1-62](assets/chlimage_1-62.png)

#### TRANSLATION {#translation}

“翻 [译设置](/help/communities/sites-console.md#translation) ”指定站点的基本语言，以及UGC是否可以翻译成哪种语言（如果可以）。

* 选中“ **允许机器翻译”**
* 默认的机器翻译服务将默认语言保留为翻译的选定语言
* 保留默认翻译提供者和配置
* 不需要全球商店，因为没有语言副本
* 选择转 **换整个页面**
* 保留默认持久性选项

![chlimage_1-63](assets/chlimage_1-63.png)

#### ENABLEMENT {#enablement}

创建参与社区时留空。

有关快速创建启用社区的类似教 [程](/help/communities/overview.md#enablement-community)，请参 [阅AEM Communities for Enablement入门](/help/communities/getting-started-enablement.md)。

选择&#x200B;**下一步**。

### 第4步：创建社区站点 {#step-create-communities-site}

Select **Create.**

![chlimage_1-64](assets/chlimage_1-64.png)

完成该过程后，新站点的文件夹将显示在“社区——站点”控制台中。

![社区站点控制台](assets/communitiessitesconsole.png)

## 发布社区站点 {#publish-the-community-site}

创建的站点应从社区——站点控制台进行管理，该控制台与创建新站点的控制台相同。

选择社区站点的文件夹以将其打开后，将指针悬停在站点图标上方，以显示四个操作图标：

![siteactionicons-1](assets/siteactionicons-1.png)

选择第四个省略号图标（更多操作）时，将显示“导出站点”和“删除站点”选项。

![siteactionsnew-1](assets/siteactionsnew-1.png)

从左至右为：

* **打开站点**

   选择铅笔图标以在创作编辑模式下打开社区站点，以添加和／或配置页面组件

* **编辑站点**

   选择属性图标以打开社区站点以修改属性，如标题或更改主题

* **发布站点**

   选择“全球”图标以发布社区站点（例如，如果发布服务器在本地计算机上运行，则默认情况下为localhost:4503）

* **导出站点**

   选择导出图标以创建存储在包管理器中和已下载的社区站点 [的包](/help/sites-administering/package-manager.md) 。
请注意，UGC未包含在站点包中。

* **删除站点**

   选择删除图标以从“社区”>“站点”控制台 **[!UICONTROL 中删除社区站点]**。 此操作将删除与站点关联的所有项目，如UGC、用户组、资产和数据库记录。

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>如果未对发布实例使用默认端口4503，请编辑默认复制代理，将端口号设置为正确的值。
>
>在创作实例上，从主菜单：
>
>1. 导航到工 **[!UICONTROL 具>操作>复制]** 菜单。
>1. 选择作 **[!UICONTROL 者上的代理]**。
>1. 选择 **[!UICONTROL 默认代理（发布）]**。
>1. 在“设 **[!UICONTROL 置]**”旁，选 **[!UICONTROL 择编辑]**。
>1. 在“代理设置”的弹出对话框中，选择“传 **[!UICONTROL 输]** ”选项卡。
>1. 在URI中，将端口号4503更改为所需的端口号>
   >    * 例如，要使用端口6103:
      >      https://localhost:6103/bin/receive?sling:authRequestLogin=1
>
1. 选择 **[!UICONTROL 确定]**。
1. （可选）选择“清 **[!UICONTROL 除]** ”或“强 **[!UICONTROL 制重试]** ”以重置复制队列。




### Select Publish {#select-publish}

在确保发布服务器正在运行后，选择全球图标以发布社区站点。

![chlimage_1-65](assets/chlimage_1-65.png)

社区站点成功发布后，将短暂显示一条消息：

![chlimage_1-66](assets/chlimage_1-66.png)

### 新社区用户组 {#new-community-user-groups}

与新社区站点一起，会创建新用户组，这些用户组具有针对各种管理功能设置的相应权限。 有关详细信息，请 [访问社区站点的用户组](/help/communities/users.md#usergroupsforcommunitysites)。

对于此新社区站点，如果在步骤1中将站点名称设为“参与”，则四个新用户组可能会从“组”控制台中看 [到](/help/communities/members.md) (全局导航：社区、组):

* 社区参与社区经理
* 社区参与组管理员
* 社区参与会员
* 社区参与版主
* 社区参与特权成员
* 社区参与站点内容管理器

请注意， [Aaron McDonald](/help/communities/tutorials.md#demo-users) 是

* 社区参与社区经理
* 社区参与版主
* 社区参与会员（间接作为版主组的成员）

![chlimage_1-67](assets/chlimage_1-67.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![chlimage_1-68](assets/chlimage_1-68.png)

## 配置身份验证错误 {#configure-for-authentication-error}

将站点配置并推送到发布后，在发 [布实例上配置登录映射](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`)。 优点是，当未正确输入登录凭据时，身份验证错误将重新显示社区站点的登录页面并显示错误消息。

添加为 `Login Page Mapping`

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## 可选步骤 {#optional-steps}

### 更改默认主页 {#change-the-default-home-page}

当出于演示目的使用发布站点时，将默认主页更改为新站点可能很有用。

为此，需要使 [用CRXDE](https://localhost:4503/crx/de) Lite在发布时 [编辑资源映射表](/help/sites-deploying/resource-mapping.md) 。

开始：

1. 在发布实例上，使用管理员权限登录。
1. 浏览至 [https://localhost:4503/crx/de](https://localhost:4503/crx/de)。
1. 在项目浏览器中，展开 `/etc/map.`
1. 选择节 `http` 点：

   * 选择 **创建节点：**

      * **名称** localhost.4503(不 *要* “:”)

      * **Type** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 选择新创建 `localhost.4503` 的节点：

   * 添加属性：

      * **名称** sling:match
      * **Type** String
      * **值** localhost.4503/$（必须以“$”字符结尾）
   * 添加属性：

      * **名称** sling:internalRedirect
      * **Type** String
      * **值** /content/sites/engage/en.html


1. 选择“ **全部保存”。**
1. （可选）删除浏览历史记录。
1. 浏览至https://localhost:4503/。

   * 请访问https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>要禁用，只需在属性 `sling:match` 值前加上“x” - `xlocalhost.4503/$` -和“ **全部保存”**。

![chlimage_1-69](assets/chlimage_1-69.png)

#### 疑难解答：保存映射时出错 {#troubleshooting-error-saving-map}

如果无法保存更改，请确保节点名称为“点”分隔符，而不是“冒号”分隔符，因为这 `localhost.4503``localhost:4503``localhost`不是有效的命名空间前缀。

![chlimage_1-70](assets/chlimage_1-70.png)

#### 疑难解答：重定向失败 {#troubleshooting-fail-to-redirect}

常规表达式字符&#x200B;**串结尾的“$**`sling:match``https://localhost:4503/` ”至关重要，因此只能精确映射，否则重定向值将前缀于URL中server:port之后可能存在的任何路径。 因此，当AEM尝试重定向到登录页面时，它将失败。

### 修改站点 {#modify-the-site}

最初创建站点后，作者可以使用“打开站点”图 [标来执行标准](/help/communities/sites-console.md#authoring-site-content) AEM创作活动。

此外，管理员还可以使 [用“编辑站点](/help/communities/sites-console.md#modifying-site-properties) ”图标来修改站点的属性，如标题。

在进行任何修改后，请记 **住保存** ，然后重&#x200B;**新发布站点** 。

>[!NOTE]
>
>如果不熟悉AEM，请视图有关基本操作 [的文档](/help/sites-authoring/basic-handling.md) ，以 [及页面创作快速指南](/help/sites-authoring/qg-page-authoring.md)。

