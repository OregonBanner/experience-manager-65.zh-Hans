---
title: 体验已发布的站点
seo-title: 体验已发布的站点
description: 浏览到已发布的站点以启用
seo-description: 浏览到已发布的站点以启用
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---



# 体验已发布的站点 {#experience-the-published-site}


**[◆创建和分配启用资源](resource.md)**

## 浏览到发布时的新站点 {#browse-to-new-site-on-publish}

现在，新创建的社区站点及其支持资源和学习路径已发布，您就可以体验Enablement Tutorial站点了。

首先，浏览到创建站点时显示的URL，但在发布服务器上，例如

* 作者URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* 发布URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

如果设 [置了默认主页](enablement-create-site.md#changethedefaulthomepage)，则只需浏览 [http://localhost:4503/](http://localhost:4503/) ，就可以启动站点。

首次到达已发布的站点时，站点访客通常尚未登录，且为匿名访客。

**http://localhost:4503/content/sites/enable/en.html**

![chlimage_1-433](assets/chlimage_1-433.png)

## 匿名网站访客 {#anonymous-site-visitor}

将立即向匿名站点访客显示此私人支持社区站点的登录页面。 请注意，没有自注册或登录Facebook或Twitter的选项。

注意，此主页显示四个菜单项：而 `Assignments, Ski Catalog, What's New``Discussions`且，如果不登录，就无法达成任何协议。

>[!NOTE]
>
>可以授予对支持站点的匿名访问权限，而不允许站点访问者自行注册。
>如果将启用资源设置为 `show in catalog` 和 `allow anonymous access`，则匿名站点访问者可以查看目录中的资源。

### 防止对JCR进行匿名访问 {#prevent-anonymous-access-on-jcr}

已知限制通过jcr内容和json向匿名访客公开社区站点内容，但 **[!UICONTROL 对于站点内容]** ，允许匿名访问是禁用的。 但是，可以使用Sling Restrictions作为解决方法来控制此行为。

要保护您的社区站点的内容免受匿名用户通过jcr内容和json访问，请执行以下步骤：

1. 在AEM作者实例中，转到https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html。

   >[!NOTE]
   >
   >请勿转到本地化的站点。

1. 转至页 **[!UICONTROL 面属性]**。

   ![page-properties-1](assets/page-properties-1.png)

1. 转到“高 **[!UICONTROL 级]** ”选项卡。
1. Enable **[!UICONTROL Authentication Requirement]**.

   ![site-authentication-1](assets/site-authentication-1.png)

1. 添加登录页面的路径。 For example, `/content/......./GetStarted`.
1. 发布页面。

## 已登记会员 {#enrolled-member}

这一经验并被指派给 `Riley Taylor` Ski Lessons `Sidney Croft` , [并且](enablement-setup.md#publishcreateenablementmembers) ，通过Ski Lessons Lossens Lansers [(](resource.md#settings) Ski Lessons)的用户，通过其成为Ski Lessons Ski Class Group的成员， **** Lim Lap。

登录方式

* `Username: riley`
* `Password: password`

如果用户配置文件不是通过自助注册创建的，则会在会员首次登录时显示其配置文件页面，以便他们根据需要验证和修改该配置文件。

下次成员登录时，将显示由第一个菜单项标识的主页。

![chlimage_1-434](assets/chlimage_1-434.png)

### 指定任务 {#assignments}

在“任务”页面中，会显示成员所分配的所有学习路径和具体分配给他们的启用资源。

每个分配都提供有关

* 任务类型
* 是否为新任务
* 名称
* 与分配类型相关的详细信息
* 任务联系人、专家和作者（如果提供）

分配类型由卡左上角的图标指示。 道路的图像是用于学习路径，其中包含的支持资源数量。

![chlimage_1-435](assets/chlimage_1-435.png)

选择 *“滑雪课* ”将显示学习路径引用的两个启动资源。

![chlimage_1-436](assets/chlimage_1-436.png)

选 *择Ski Lesson 1* ，将打开启用资源的详细信息页面。

从详细信息页面中，成员可以学习、评 [分课程](rating.md) ，并添加 [注释](comments.md)。 任何会员活动都将反映在站点的“新增功能”部分。

在创作环境中可访问的“报告”部分中将记录与启用资源的交互。

![chlimage_1-437](assets/chlimage_1-437.png)

### 滑雪目录 {#ski-catalog}

“Ski Catalog”（滑雪目录）页面是使用命名空间中的标记标记的启用资源 `Tutorial` 目录。 这两个 *滑雪课资源都使用标记* 进行标记 `Skiing` ，这样，如果选择了除或之外的任何标 `All` 记，则不会 `Tutorial: Sports / Skiing` 显示任何内容。

如果尚未直接或通过学习路径为成员分配启用资源，则可以与位于目录中的启用资源交互，并通过评论和评级提供反馈。

![chlimage_1-438](assets/chlimage_1-438.png)

### 讨论 {#discussions}

除了对启用资源进行评级和评论([启用](enablement-create-site.md#step33asettings))外，从中创建的社区站点模板还 `Enablement Tutorial` 包括论坛功能 [(标题为](functions.md#forum-function)`Discussions)`。

选择链 `Discussions`接并发布主题。

以Sidney Croft（sidney /密码）身份登录并回复问题，以及关注主题。

注意，除了内联协调之外，还有一些选项可用于在社交媒体上共享主题或通过电子邮件发送主题。

![chlimage_1-439](assets/chlimage_1-439.png)

### 新增功能 {#what-s-new}

菜 `What's New` 单项是此社区站点结构中 [赋予活动流功能](functions.md#activity-stream-function) 的标题。

仍以Sidney的身份登录，请选择 `What's New` 用于显示活动的链接。

![chlimage_1-440](assets/chlimage_1-440.png)

## 受信任的社区会员 {#trusted-community-member}

此体验假定 ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` 已分配审查方和资 [源联](enablement-create-site.md#moderation) 系人的角色 [](resource.md#settings)。

登录方式

* `Username: quinn`
* `Password: password`

登录后，请注意，会出现一个新的菜单项， `Administration`该菜单项显示是因为该成员被授予了审查方的角色。

![chlimage_1-441](assets/chlimage_1-441.png)

主页由第一个菜单项“任务”标识。 Quinn是主持人和启用资源联系人，未登记到任何启用资源或学习路径中，因此无需显示任何内容。

### 管理 {#administration}

这是两个学员的活动， `Riley Taylor` 和 `Sidney Croft`。 通过选择链 `Administration` 接以访问审核控制台，Quinn可以使用批量审核控制 [台审核其帖子](moderation.md) 。

选择侧面板图标可切换打开用于搜索社区内容的筛选器。

将指针悬停在评论卡上会显示审核操作。

![chlimage_1-442](assets/chlimage_1-442.png)

## 关于作者的报告 {#reports-on-author}

有两种方式可访问关于学员和支持资源的报告。

在创作时，导航到“社 **区”、“资[源”控制台](resources.md)**，在该控制台中管理启用资源，在选择社区站点后，可以为

* 所有支持资源和学习路径
* 一个特定的支持资源或学习路径

导航到“社 **区”、“报[告”控制台](reports.md)**，然后根据

* 支持资源和学习路径的分配
* 在特定时间段内发布到社区站点
* 特定时间段内社区站点的查看（站点访问）

* 帖子和视图可能针对所有内容，或针对特定内容：

   * 论坛
   * 论坛 - 主题
   * 问题与解答
   * 问题与解答 - 问题
   * 博客
   * 博客文章
   * 日历
   * 日历事件

### 资源控制台 {#resources-console}

在发布时，只需进行少量活动并与资源进行交互，即可查看有关作者的报告。

* 论作者
* 使用管理权限登录
* 从主菜单导航到“社区” **[!UICONTROL >“资源”]**
* 选择站 `Enablement Tutorial` 点
* 选择所 `Report` 有资源的摘要图标
* 选择一个资源，然后选择该 `Report` 资源上的报表的图标

请注意，显示Adobe Analytics数据可能为时过早，Adobe Analytics可能需要1到12小时才能显示。 但是，基本的SCORM报告已经可用。

#### 滑雪课资源报告 {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### 滑雪课用户报告 {#ski-lessons-user-report}

* 选择“ **[!UICONTROL 社区”>“资源”]**

* 打开卡 `Enablement Tutorial`
* 打开卡 `Ski Lessons`
* 选择 `Report > User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### 报告控制台 {#reports-console}

“报告”控制台允许生成

* **任何支持社区站点的分配** ,
* **任何社区站点的查看次数**
* **任何社区站点的帖子** ,

对于有关任务的报告：

* 论作者
* 使用管理权限登录
* 导航到“社 **[!UICONTROL 区”>“报告”>“任务”报告]**
* 从下 **[!UICONTROL 拉菜单]** (选择 `Enablement Tutorial`)中选择站点

* 选择 **[!UICONTROL 组]** (选择 `Community Ski Class`)

* 选择分 **[!UICONTROL 配]** (选择 `Ski Lessons`)

* 选择生 **[!UICONTROL 成]**

![chlimage_1-445](assets/chlimage_1-445.png)

对于有关视图的报告：

* 论作者
* 使用管理权限登录
* 导航到“社 **[!UICONTROL 区”>“报告”>“查看报告”]**
* 从下 **拉菜单&#x200B;**(选择`Enablement Tutorial`)中选择站点

* 选择 **[!UICONTROL 内容类型]** (选择 `all`)

* 选择日 **[!UICONTROL 期范围]** (选择 `Last 7 days`)

* 选择生 **[!UICONTROL 成]**

![chlimage_1-446](assets/chlimage_1-446.png)

**[◆创建和分配启用资源](resource.md)**
