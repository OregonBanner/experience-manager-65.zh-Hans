---
title: 体验已发布的站点
seo-title: Experience the Published Site
description: 浏览到已发布的站点以启用
seo-description: Browse to a published site for enablement
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
exl-id: 801416ed-d321-45a2-8032-8935094a4d44
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 2%

---

# 体验已发布的站点 {#experience-the-published-site}


**[⇐创建和分配启用资源](resource.md)**

## 发布时浏览到新站点 {#browse-to-new-site-on-publish}

现在，新创建的社区站点及其支持资源和学习路径已发布，您可以体验支持教程站点。

首先浏览到创建站点时显示的URL，但在发布服务器上，例如

* 作者URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* 发布URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

如果 [默认主页已设置](enablement-create-site.md#changethedefaulthomepage)，然后只需浏览到 [http://localhost:4503/](http://localhost:4503/) 应该启动该站点。

首次访问已发布的网站时，该网站访客通常不会登录，并且会匿名。

**http://localhost:4503/content/sites/enable/en.html**

![enablement-login](assets/enablement-login.png)

## 匿名网站访客 {#anonymous-site-visitor}

匿名网站访客会立即看到此专用启用社区网站的登录页面。 请注意，自助注册或登录Facebook或Twitter时没有选项。

请注意，此主页显示四个菜单项： `Assignments, Ski Catalog, What's New` 和 `Discussions`，但未登录就无法访问任何内容。

>[!NOTE]
>
>可以授予对启用网站的匿名访问权限，而不允许网站访客自行注册。
>
>如果将启用资源设置为 `show in catalog` 和 `allow anonymous access`，匿名网站访客可以查看目录中的资源。

### 阻止对JCR的匿名访问 {#prevent-anonymous-access-on-jcr}

但是，有一个已知限制通过jcr内容和json向匿名访客公开社区网站内容 **[!UICONTROL 允许匿名访问]** 对于站点的内容，已禁用。 但是，可以使用Sling限制作为解决方法来控制此行为。

要保护您社区站点的内容不被匿名用户通过jcr内容和json访问，请执行以下步骤：

1. 在AEM创作实例上，转到https://&lt;host>：&lt;port>/editor.html/content/site/&lt;sitename>.html.

   >[!NOTE]
   >
   >不要转到本地化的网站。

1. 转到 **[!UICONTROL 页面属性]**.

   ![page-properties](assets/page-properties.png)

1. 转到 **[!UICONTROL 高级]** 选项卡。
1. 启用 **[!UICONTROL 身份验证要求]**.

   ![站点身份验证](assets/site-authentication.png)

1. 添加登录页面的路径。 例如：`/content/......./GetStarted`。
1. 发布页面。

## 已注册的成员 {#enrolled-member}

此体验依赖于用户 `Riley Taylor` 和 `Sidney Croft` 成为 [已创建](enablement-setup.md#publishcreateenablementmembers) 和 [已指定](resource.md#settings) 到 *滑雪课程* 学习路径通过他们在 *社区滑雪课程* 组。

登录方式

* `Username: riley`
* `Password: password`

如果用户配置文件不是通过自助注册创建的，则当某位成员首次登录时，将会显示其“配置文件”页面，以便他们能够根据需要对其进行验证和修改。

下次成员登录时，将显示由第一个菜单项标识的主页。

![registered-member](assets/enrolled-member.png)

### 指定任务 {#assignments}

在“工作总揽”页面中，显示了该成员专门分配到的所有学习路径和支持资源。

每项任务均提供以下基本信息：

* 任务类型
* 是否为新的分配
* 名称
* 与分配类型相关的详细信息
* 任务联系人、专家和作者（如果提供）

任务类型由卡片左上角的图标指示。 道路图像用于包含大量启用资源的学习路径。

![assignment1](assets/assignment1.png)

选择 *滑雪课程* 将显示学习路径引用的两个启用资源。

![assignment2](assets/assignment2.png)

选择 *滑雪课程1* 将打开启用资源的详细信息页面。

在详细信息页面中，成员能够了解， [费率](rating.md) 课程并添加 [评论](comments.md). 任何成员活动都将反映在网站的“新增功能”部分中。

与启用资源的交互将在可在创作环境中访问的“报告”部分中记录。

![assignment3](assets/assignment3.png)

### 滑雪板目录 {#ski-catalog}

“Ski Catalog”页面是已使用来自的标记标记标记的支持资源的目录。 `Tutorial` 命名空间。 两个 *滑雪课程* 资源使用 `Skiing` 标签，以便如果任何非 `All` 或 `Tutorial: Sports / Skiing` 选中时，不会显示任何内容。

如果尚未直接或通过学习路径为成员分配启用资源，则可以与目录中的启用资源进行交互，并通过评论和评级提供反馈。

![ski-catalog](assets/ski-catalog.png)

### 讨论 {#discussions}

除了对启用资源进行评级和注释之外([启用时](enablement-create-site.md#step33asettings))，社区站点模板， `Enablement Tutorial` 创建时间包括 [论坛功能](functions.md#forum-function) (标题为 `Discussions)`.

选择 `Discussions`链接并发布主题。

注销并以Sidney Croft（悉尼/密码）身份登录，然后回复问题，以及关注主题。

请注意，除了内联审核之外，还可以选择在社交媒体上共享主题或通过电子邮件发送主题。

![讨论](assets/discussions.png)

### 新增功能 {#what-s-new}

此 `What's New` 菜单项是给定以下项的标题： [活动流函数](functions.md#activity-stream-function) 在此社区站点的结构中。

仍然以Sidney身份登录，请选择 `What's New` 用于显示活动的链接。

![whats-new-menu](assets/whats-new-menu.png)

## 受信任的社区成员 {#trusted-community-member}

此体验假设 ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` 已分配角色 [审查方](enablement-create-site.md#moderation) 和 [资源联系人](resource.md#settings).

登录方式

* `Username: quinn`
* `Password: password`

登录后，请注意有新的菜单项， `Administration`，出现的原因是该成员被授予了审查方的角色。

![trusted-member-homepage](assets/trusted-member-homepage.png)

主页由第一个菜单项Assignments标识。 Quinn是版主和支持资源联系人，未注册任何支持资源或学习路径，因此没有可显示的任何内容。

### 管理 {#administration}

这里有的是两个学习者的活动， `Riley Taylor` 和 `Sidney Croft`. 通过选择 `Administration` 链接访问审核控制台，Quinn能够使用 [批量审核控制台](moderation.md) 审核他们的帖子。

选择侧面板图标可切换用于搜索社区内容的过滤器。

将鼠标悬停在评论卡片上会显示审核操作。

![管理](assets/administration.png)

## 有关作者的报告 {#reports-on-author}

可通过两种方式访问关于学习者和支持资源的报告。

在作者中，导航到 **社区， [资源控制台](resources.md)**，其中管理了启用资源，在选择社区站点后，可以生成报表

* 所有支持资源和学习路径
* 一个特定的启用资源或学习路径

导航到 **社区， [报表控制台](reports.md)**，并根据以下内容生成报告：

* 用于启用资源和学习路径的分配
* 特定时段内发布到社区站点的帖子
* 特定时段内社区站点的查看次数（站点访问）

* 帖子和视图可以是所有内容，也可以是特定内容：

   * 论坛
   * 论坛 - 主题
   * 问题与解答
   * 问题与解答 - 问题
   * 博客
   * 博客文章
   * 日程表
   * 日历事件

### 资源控制台 {#resources-console}

只需在发布时与资源部门进行一点活动和互动，即可查看有关作者的报告，这值得一看。

* 对于作者，请使用管理权限登录。
* 从主菜单导航到 **[!UICONTROL Communities]** > **[!UICONTROL 资源]**.
* 选择 `Enablement Tutorial` 站点。
* 选择 `Report` 图标，以显示所有资源的摘要。
* 选择一个资源，然后 `Report` 图标来查看有关该资源的报告。

请注意，显示来自Adobe Analytics的数据可能为时过早，显示这些数据可能需要1到12小时。 但是，基本的SCORM报告已经可用。

#### 滑雪课程资源报告 {#ski-lessons-resource-report}

![ski-learning-report](assets/ski-lessons-report.png)

#### 滑雪课程用户报告 {#ski-lessons-user-report}

* 选择 **[!UICONTROL 社区>资源]**

* 打开信息卡 `Enablement Tutorial`
* 打开信息卡 `Ski Lessons`
* 选择 `Report > User Report`

![ski-learning-user-report](assets/ski-lessons-user-report.png)

### 报表控制台 {#reports-console}

“报表”控制台允许生成以下项的报告：

* **指定任务** 用于任何启用社区站点
* **查看次数** 适用于任何社区站点
* **帖子** 适用于任何社区站点

对于工作分配报告：

* 对于作者，请使用管理权限登录。
* 导航到 **[!UICONTROL Communities]** > **[!UICONTROL 报告]** > **[!UICONTROL 任务报表]**.
* 选择 **[!UICONTROL 站点]** 从下拉菜单中(选择 `Enablement Tutorial`)。

* 选择 **[!UICONTROL 组]** (选择 `Community Ski Class`)

* 选择 **[!UICONTROL 分配]** (选择 `Ski Lessons`)

* 选择 **[!UICONTROL 生成]**

![报告分配](assets/report-assignment.png)

对于视图报告：

* 对于作者，请使用管理权限登录。
* 导航到 **[!UICONTROL Communities]** > **[!UICONTROL 报告]** > **[!UICONTROL 查看次数报表]**.
* 选择 **站点** 从下拉菜单中(选择 `Enablement Tutorial`)。

* 选择 **[!UICONTROL 内容类型]** (选择 `all`)。

* 选择 **[!UICONTROL 日期范围]** (选择 `Last 7 days`)。

* 选择 **[!UICONTROL 生成]**.

![报告视图](assets/report-views.png)

**[⇐创建和分配启用资源](resource.md)**
