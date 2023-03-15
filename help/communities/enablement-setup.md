---
title: 用于启用的初始设置
seo-title: Initial Setup
description: 用于启用的初始设置
seo-description: Initial Setup for Enablement
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---

# 用于启用的初始设置  {#initial-setup-for-enablement}

## 启动创作和发布实例 {#start-author-and-publish-instances}

出于开发和演示目的，需要运行一个作者实例和一个发布实例。

遵循基本AEM [快速入门](../../help/sites-deploying/deploy.md#getting-started) 说明，将导致

* 创作环境 [localhost：4502](http://localhost:4502/)
* 发布环境于 [localhost：4503](http://localhost:4503/)

对于AEM Communities，

* 创作环境用于：

   * 开发站点、模板、组件、支持资源和学习路径。
   * 为成员和成员组分配启用资源和学习路径。
   * 生成有关工作、视图和帖子的报告。
   * 管理和配置任务。

* 发布环境用于：

   * 根据由支持经理管理的主题进行学习/培训。
   * 对支持资源和学习路径进行评论和评级。
   * 联系资源联系人。

>[!NOTE]
>
>如果不熟悉AEM，请查看文档 [基本处理](../../help/sites-authoring/basic-handling.md) 和 [页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md).

## 安装最新的Communities版本 {#install-latest-communities-release}

本教程将创建 [启用社区站点](overview.md#enablement-community). 要确保已安装最新的功能包，请访问：

* [最新版本](deploy-communities.md#latest-releases)

有关创建 [参与社区站点](overview.md#engagement-community)，访问 [AEM Communities快速入门](getting-started.md).

## 配置启用功能 {#configure-enablement-features}

要学习本教程，必须正确安装和 [配置启用](enablement.md)，需要第三方产品，例如MySQL和FFmpeg。

## 配置 Analytics {#configure-analytics}

时间 [为社区站点配置了Adobe Analytics](analytics.md)，中提供了更多信息 [报告](reports.md) 在分配给社区成员（学习者）的启用资源和学习路径上生成。

## 配置通知电子邮件 {#configure-email-for-notifications}

通知功能，默认情况下可用于使用创建的所有站点 `Communities Sites` 控制台，提供通知的电子邮件渠道。

要为站点正确配置电子邮件，这是必需的。

参见 [配置电子邮件](email.md).

## 启用通道服务 {#enable-the-tunnel-service}

在创作环境中创建社区站点时，通过隧道服务，可以创建和管理在发布环境（成员）中注册的用户和用户组、将角色分配给受信任的社区成员以及将内容分配给学习者。

有关详细信息，请参阅 [管理用户和用户组](users.md).

有关启用通道服务的简单说明，请参见 [通道服务](deploy-communities.md#tunnel-service-on-author).

## 创建教程标记 {#create-tutorial-tags}

使用标记命名空间，创建用于参与和启用教程的标记 `Tutorial`.

使用 [标记控制台](../../help/sites-administering/tags.md#tagging-console) 要创建以下标记，请执行以下操作：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

然后按照说明执行以下操作：

1. [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [发布标记](../../help/sites-administering/tags.md#publishing-tags)

为AEM Communities快速入门Tutorials创建的标记示例包

[获取文件](assets/communities_tutorialtags-10.zip)

## 创建启用成员和组 {#create-enablement-members-and-groups}

对于启用社区站点，站点访客应该无法 [自助注册或使用社交登录](sites-console.md#user-management).

相反，使用 [隧道服务](#enable-the-tunnel-service) 已启用， [成员控制台](members.md) 用于在发布环境中注册新成员。

在本教程中，将在发布环境中创建三个成员。 两个成员将成为分配给学习路径的用户组的成员，而第三个成员将成为启用资源联系人。

在创作环境中创建第四个用户，并为其分配Communities管理员和Community Enablement Manager角色。

>[!NOTE]
>
>这些成员将在创建之前创建 *启用教程* 社区站点。
>
>如果它们是在之后创建的，则可以添加为成员 *启用教程成员组* 创建成员期间。
>
>相反，他们以后会 [已分配给成员组](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### 莱利·泰勒 — 注册者 {#riley-taylor-enrollee}

[创建成员](members.md#create-new-member) 将添加到学习者组 — 社区滑雪班组。

* **ID**：赖利
* **电子邮件**： riley.taylor@mailinator.com
* **密码**：密码
* **确认密码**：密码
* **名字**：赖利
* **姓氏**：泰勒

### 西德尼·克罗夫特 — 注册者 {#sidney-croft-enrollee}

[创建第二个成员](members.md#create-new-member) 将添加到社区滑雪班组的用户。

* **ID**：西德尼
* **电子邮件**： sidney.croft@mailinator.com
* **密码**：密码
* **确认密码**：密码
* **名字**：西德尼
* **姓氏**： Croft

### Quinn Harper — 启用资源联系人和审查方 {#quinn-harper-enablement-resource-contact-and-moderator}

[创建成员](members.md#create-new-member) 创建站点后，这些用户将被添加到社区站点的成员组。 此成员资格将允许将成员指定为启用 [资源联系人](resources.md#settings) 在为站点创建启用资源时。

* **ID**： quinn
* **电子邮件**： quinn.harper@mailinator.com
* **密码**：密码
* **确认密码**：密码
* **名字**：奎恩
* **姓氏**：Harper

### 添加用户组 — 社区滑雪类 {#add-a-user-group-community-ski-class}

[添加新组](members.md#create-new-group) 被命名为社区滑雪班。

* **ID**：community-ski-class
* **名称**：社区滑雪课
* **描述**：用于分配启用资源的示例组
* **将成员添加到组** &#39;添加&#39;：

   * 赖利
   * 西德尼

* 选择 **[!UICONTROL 保存]**

### 社区Ski类属性 {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>在创建社区站点期间，现有成员和组可以添加到社区站点的成员组。

## 社区管理员角色 {#community-administrator-role}

“社区管理员”组的成员可以创建社区站点、管理站点、管理成员（他们可以从社区中禁止成员）和审核内容。

### 创建用户 {#create-user}

创建用户 *作者*，分配了社区管理员角色：

* 在创作实例上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 使用管理员权限登录

   * 例如，用户名“管理员”/密码“管理员”

* 在主控制台中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**.
* 从 **[!UICONTROL 编辑]** 菜单，选择 **[!UICONTROL 添加用户]**.

* 在 `Create New User` 对话框输入：

   * **ID&amp;ast；**：天狼星
   * **电子邮件地址**： sirius.nilson@mailinator.com
   * **密码(&amp;A)；**：密码
   * **确认密码(&amp;A)；**：密码
   * **名字**：天狼星
   * **姓氏(&amp;A)；**：尼尔森

### 将Sirius分配给社区管理员组 {#assign-sirius-to-community-administrators-group}

向下滚动到 `Add User to Groups`：

* 输入“C”进行搜索

   * 选择 `Community Administrators`
   * 选择 `Community Enablement Managers`

* 选择 **[!UICONTROL 保存]**

![管理员角色](assets/admin-role.png)
