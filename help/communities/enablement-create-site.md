---
title: 为Enablement创作新社区站点
seo-title: 为Enablement创作新社区站点
description: 创建社区站点以进行启用
seo-description: 创建社区站点以进行启用
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 2%

---


# 为Enablement {#author-a-new-community-site-for-enablement}创作新的社区站点

## 创建社区站点 {#create-community-site}

[社区站](/help/communities/sites-console.md) 点创建采用向导，可指导您完成创建社区站点的各个步骤。在最后一步中提交站点之前，可以前进到`Next`步骤或`Back`到上一步。

要开始创建新社区站点，请执行以下操作：

使用[作者实例](https://localhost:4502/)

* 使用管理员权限登录并导航到&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Sites]**。

* 选择&#x200B;**创建**。

### 第1步：站点模板{#step-site-template}

![启用站点模板](assets/enablement-site-template.png)

在&#x200B;**站点模板**&#x200B;步骤中，输入标题、说明和URL的名称，然后选择社区站点模板，例如：

* **社区站点标题**: `Enablement Tutorial`.

* **社区站点描述**: `A site for enabling the community to learn.`

* **社区站点根目录**:(默认根留空 `/content/sites`)

* **云配置**:（如果未指定云配置，则留空）提供指定云配置的路径。
* **社区站点基础语言**:(单语言未更改：英语)使用下拉框从可用 *语* 言(德语、意大利语、法语、日语、西班牙语、葡萄牙语（巴西）、繁体中文和简体中文)中选择一种或多种基本语言。将根据[多语言站点翻译内容](/help/sites-administering/translation.md)中介绍的最佳实践，为添加的每种语言创建一个社区站点，并且该站点将位于同一站点文件夹中。 每个站点的根页面将包含一个由所选语言之一的语言代码命名的子页面，如英语为“en”或法语为“fr”。

* **社区站点名称**: `enable`

   * 初始URL将显示在社区站点名称下方
   * 对于有效的URL，请附加基本语言代码+ &quot;。html&quot;
      *例如*,https://localhost:4502/content/sites/  `enable/en.html`

* **引用站点模板**:下拉选择  `Reference Structured Learning Site Template`

选择&#x200B;**下一步**。

### 第2步：设计{#step-design}

设计步骤分为两个部分，用于选择主题和品牌横幅：

#### 社区站点主题{#community-site-theme}

选择要应用于模板的所需样式。 选中后，主题将用复选标记覆盖。

#### 社区站点品牌{#community-site-branding}

（可选）上传要在网站页面上显示的横幅图像。 横幅被固定到浏览器的左边缘，位于社区站点标题和菜单（导航链接）之间。 横幅高度会被裁剪为120像素。 横幅的大小不会调整为适合浏览器的宽度和120像素高。

![chlimage_1-449](assets/chlimage_1-449.png)

![chlimage_1](assets/chlimage_1.jpeg)

选择&#x200B;**下一步**。

### 第3步：设置{#step-settings}

在“设置”步骤中，在选择`Next`之前，请注意有七个部分提供对涉及用户管理、标记、角色、协调、分析、翻译和启用的配置的访问。

#### 用户管理{#user-management}

建议[启用社区](/help/communities/overview.md#enablement-community)为私有。

当拒绝匿名站点访客访问、不能自行注册或不能使用社交登录时，社区站点是私有的。

确保取消选择[用户管理](/help/communities/sites-console.md#user-management)的大多数复选框：

* 请勿允许站点访客自行注册。
* 请勿允许匿名网站访客视图该网站。
* 是否允许社区成员之间进行消息传递是可选的。
* 请勿允许使用Facebook登录。
* 请勿允许使用Twitter登录。

![用户管理](assets/user-mgmt.png)

#### 标记{#tagging}

可应用于社区内容的标记通过选择先前通过[标记控制台](/help/sites-administering/tags.md#tagging-console)定义的AEM命名空间(如[教程命名空间](/help/communities/enablement-setup.md#create-tutorial-tags))进行控制。

此外，为社区站点选择标记命名空间会限制在定义目录和启用资源时显示的选择。 有关重要信息，请参阅[标记Enablement Resources](/help/communities/tag-resources.md)。

使用预先键入搜索可轻松查找命名空间。 例如，

* 类型 `tut`
* 选择 `Tutorial`

![启用标记](assets/enablement-tagging.png)

### 角色{#roles}

[社区成](/help/communities/users.md) 员角色通过“角色”部分中的设置进行分配。

要让社区成员（或成员组）以社区管理者身份体验站点，请使用“预先键入”搜索并从下拉列表的选项中选择成员或组名称。

例如，

* 类型 `q`
* 选择[Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[隧道](/help/communities/deploy-communities.md#tunnel-service-on-author) 服务允许选择仅存在于发布环境中的成员和组。

![启用角色](assets/site-admin.png)

#### 协调{#moderation}

接受[协调](/help/communities/sites-console.md#moderation)用户生成内容(UGC)的默认全局设置。

![chlimage_1-452](assets/chlimage_1-452.png)

#### 分析{#analytics}

从下拉列表中，选择为此社区站点配置的Analytics云服务框架。

屏幕截图中显示的选择`Communities`是[配置文档中的框架示例。](/help/communities/analytics.md#aem-analytics-framework-configuration)

![chlimage_1-454](assets/chlimage_1-454.png)

#### TRANSLATION {#translation}

[转换设置](/help/communities/sites-console.md#translation)指定UGC是否可以转换为哪种语言（如果可以）。

* 检查&#x200B;**允许机器翻译**
* 使用默认设置

![chlimage_1-456](assets/chlimage_1-456.png)

#### ENABLEMENT {#enablement}

对于支持社区，必须确定一个或多个社区支持管理者。

* **Enablement Managers**
（必需） 
`Community Enablement Managers` 可选择组来管理此社区站点。

   * 类型 `s`
   * 选择 `Sirius Nilson`

* **Marketing Cloud组织**
Id（可选）在启用报告中包含视频心跳分析时必 [需的](/help/communities/analytics.md#video-heartbeat-analytics) Adobe Analytics帐户ID。

![chlimage_1-457](assets/chlimage_1-457.png)

选择&#x200B;**下一步**。

### 第4步：创建社区站点{#step-create-community-site}

选择&#x200B;**创建。**

![chlimage_1-458](assets/chlimage_1-458.png)

完成该过程后，新站点的文件夹会显示在“社区”>“站点”控制台中。

![enablesitecreated](assets/enablementsitecreated.png)

### 发布新社区站点{#publish-the-new-community-site}

创建的站点应从社区——站点控制台进行管理，该控制台与创建新站点的控制台相同。

选择社区站点的文件夹后，将指针悬停在站点图标上，以显示四个操作图标：

![站点操作图标](assets/siteactionicons.png)

选择省略号图标（更多操作图标）时，将显示“导出站点”和“删除站点”选项。

![站点操作新](assets/siteactionsnew.png)

从左至右为：

* **打开站点**

   选择铅笔图标以在作者编辑模式下打开社区站点，以添加和／或配置页面组件。

* **编辑站点**

   选择属性图标以打开社区站点以修改属性，如标题或更改主题。

* **发布站点**

   选择“全球”图标以发布社区站点（默认情况下为localhost:4503）。

* **导出站点**

   选择导出图标以创建社区站点的包，该包既存储在[包管理器](/help/sites-administering/package-manager.md)中，又已下载。
请注意，UGC未包含在站点包中。

* **删除站点**

   要删除社区站点，请选择将鼠标悬停在“社区站点”控制台中该站点上时显示的“删除站点”图标。 此操作将删除与站点关联的所有项目，如UGC、用户组、资产和数据库记录。

   ![启用站点操作](assets/enablesiteactions.png)

#### 选择发布{#select-publish}

选择“全球”图标以发布社区站点。

![chlimage_1-465](assets/chlimage_1-465.png)

将显示该网站已发布。

![chlimage_1-466](assets/chlimage_1-466.png)

## 社区用户和用户组{#community-users-user-groups}

### 注意新社区用户组{#notice-new-community-user-groups}

与新社区站点一起，还会创建新用户组，这些用户组具有为各种管理功能设置的适当权限。 有关详细信息，请访问[社区站点的用户组](/help/communities/users.md#usergroupsforcommunitysites)。

对于此新社区站点，如果在步骤1中为站点名称“enable”，则可以从[社区成员和组控制台](/help/communities/members.md#groups-console)中查看发布环境中存在的新用户组：

![community_usergroup](assets/community_usergroup.png)

### 将成员分配给社区启用成员组{#assign-members-to-community-enable-members-group}

在创作时，启用隧道服务后，可以将在初始设置中创建的[用户分配给新创建的社区站点的社区成员组。](/help/communities/enablement-setup.md#publishcreateenablementmembers)

使用“社区组”控制台，可以单独添加成员，也可以通过组中的成员关系添加成员。

在此示例中，将组`Community Ski Class`添加为组`Community Enable Members`的成员以及成员`Quinn Harper`。

* 导航到&#x200B;**社区，组**&#x200B;控制台
* 选择&#x200B;*社区启用成员*&#x200B;组
* 在&#x200B;**将成员添加到组**&#x200B;搜索框中输入“ski”
* 选择&#x200B;*社区滑雪课*（学员组）
* 在搜索框中输入“quinn”
* 选择&#x200B;*Quinn Harper*（启用资源联系人）

* 选择&#x200B;**保存**

![chlimage_1-418](assets/chlimage_1-418.png)

## 发布时的配置{#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![enablement-login](assets/enablement-login.png)

### 配置身份验证错误{#configure-for-authentication-error}

在配置站点并将其推送到发布后，在发布实例上配置登录映射[(](/help/communities/sites-console.md#configure-for-authentication-error))。 `Adobe Granite Login Selector Authentication Handler`优点是，当登录凭据输入不正确时，身份验证错误将重新显示社区站点的登录页面，并显示错误消息。

将`Login Page Mapping`添加为：

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### （可选）更改默认主页{#optional-change-the-default-home-page}

当为演示目的使用发布站点时，将默认主页更改为新站点可能会很有用。

为此，需要使用[CRX|DE](https://localhost:4503/crx/de) Lite在发布时编辑[资源映射](/help/sites-deploying/resource-mapping.md)表。

开始：

1. 在发布时，访问CRXDE并使用管理员权限登录

   * 例如，浏览至[https://localhost:4503/crx/de](https://localhost:4503/crx/de)并使用`admin/admin`登录

1. 在项目浏览器中，展开`/etc/map`
1. 选择`http`节点

   * 选择&#x200B;**创建节点**

      * **名** 称localhost.4503

         (do *not* use &#39;:&#39;)

      * **排** [版：映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 选择新创建的`localhost.4503`节点

   * 添加属性

      * **命名** 空间：匹配
      * **TypeString** 
      * **** Valuelocalhost.4503/$

   （必须以“$”字符结尾）

   * 添加属性

      * **命名** 空间：internalRedirect
      * **TypeString** 
      * **值** /content/sites/enable/en.html


1. 选择&#x200B;**保存全部**
1. （可选）删除浏览历史记录
1. 浏览到https://localhost:4503/

   * 请访问https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>要禁用，只需用“x” - `xlocalhost.4503/$` —— 和&#x200B;**全部保存**&#x200B;预先添加`sling:match`属性值。

![chlimage_1-364](assets/chlimage_1-364.png)

#### 疑难解答：保存映射{#troubleshooting-error-saving-map}时出错

如果无法保存更改，请确保节点名称为`localhost.4503`（带有“点”分隔符），而不是带有“冒号”分隔符的`localhost:4503`(因为`localhost`不是有效的命名空间前缀)。

![chlimage_1-365](assets/chlimage_1-365.png)

#### 疑难解答：无法重定向{#troubleshooting-fail-to-redirect}

常规表达式符`sling:match`字符串结尾的“**$**”至关重要，因此仅映射了`https://localhost:4503/`，否则重定向值将优先于URL中server:port之后可能存在的任何路径。 因此，当AEM尝试重定向到登录页面时，将失败。

## 修改社区站点{#modifying-the-community-site}

最初创建站点后，作者可以使用[打开站点图标](/help/communities/sites-console.md#authoring-site-content)执行标准AEM创作活动。

此外，管理员还可以使用[编辑站点图标](/help/communities/sites-console.md#modifying-site-properties)来修改站点的属性，如标题。

进行任何修改后，请记住&#x200B;**保存**&#x200B;并重新&#x200B;**发布**&#x200B;站点。

>[!NOTE]
>
>如果不熟悉AEM，请视图有关[基本操作](/help/sites-authoring/basic-handling.md)和[页面创作快速指南的文档。](/help/sites-authoring/qg-page-authoring.md)

### 添加目录{#add-a-catalog}

为此社区站点选择的社区站点模板应包含目录功能。

否则，可轻松添加目录功能。 这将允许未分配给启用资源或学习路径的社区的其他成员从目录中选择启用资源。

如果站点结构已包含目录功能，则其标题可以更改。

要修改站点的结构，请导航到&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Sites]**&#x200B;控制台，打开`enable`文件夹，然后选择&#x200B;**编辑站点**&#x200B;图标以访问`Enablement Tutorial`的属性。

选择“结构”面板以添加目录或修改现有目录：

* **标题**: `Ski Catalog`

* **URL**: `catalog`

* **选择所有命名空间**:保留为默认值。

* 选择&#x200B;**保存**。

![chlimage_1-299](assets/chlimage_1-299.png)

使用“职位”图标将“目录”功能移动到“工作总揽”之后的第二个职位。

![chlimage_1-300](assets/chlimage_1-300.png)

选择右上角的&#x200B;**保存**&#x200B;以将更改保存到社区站点。

然后重新发布站点&#x200B;**。**

