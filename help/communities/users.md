---
title: 管理用户和用户组
seo-title: Managing Users and User Groups
description: AEM Communities用户可以自行注册和编辑其用户档案
seo-description: Users of AEM Communities can self-register and edit their profiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2168'
ht-degree: 0%

---

# 管理用户和用户组 {#managing-users-and-user-groups}

## 概述 {#overview}

在AEM Communities的发布环境中，用户可以自行注册和编辑其配置文件。 如果具有适当的权限，他们还可以：

* 在社区站点中创建子社区(请参阅 [社区团体](creating-groups.md))。

* [审核](moderation.md) 用户生成的内容(UGC)。

* Be [启用资源](resources.md) 联系人。

* Be [特权](#privileged-members-group) 为博客、日历、问题解答和论坛创建条目。

在发布环境中注册的用户通常称为 *社区成员（成员）* 要区分 *用户* 在创作环境中。

通过将成员分配给 [成员（用户）组](#publish-group-roles) 在社区站点为 [已创建](sites-console.md) 或 [修改](sites-console.md#modifying-site-properties) 来访问Advertising Cloud的帮助。 从创作环境工作时，成员可通过 [隧道服务](#tunnel-service).

根据设计，在发布环境中创建的成员和成员组不应显示在创作环境中。 在创作环境中创建的用户和用户组同样可以停留在创作环境中。

当创作用户和发布成员来自同一用户列表（如从同一LDAP目录同步）时，他们在创作和发布环境中不被视为具有相同权限和组成员资格的同一用户。 成员和用户的角色必须在发布和创作时酌情分开建立。

对于 [发布场](topologies.md)，则对一个发布实例进行的注册和修改需要与其他发布实例同步，以便它们能够访问相同的用户数据。 有关详细信息，请参阅 [用户同步](sync.md)，其中包含描述 [当……](sync.md#what-happens-when).

### 贡献限制 {#contribution-limits}

为了防止垃圾邮件，可以限制成员发布内容的频率。 此外，可自动限制新登记成员的缴款。

有关详细信息，请参阅 [会员缴费限制](limits.md).

### 动态创建的用户组 {#dynamically-created-user-groups}

创建新社区站点后，会使用唯一ID(uid)和相应权限动态创建新用户组，这些权限适用于在创作环境中管理社区站点所需的各种管理功能(请参阅 [作者组角色](#author-group-roles))或发布环境(请参阅 [发布组角色](#publish-group-roles))。

组的名称是在 [社区站点创建](sites-console.md#step13asitetemplate). 唯一ID可避免同一服务器上名称相似的社区站点和社区组发生命名冲突。

例如，如果网站名称为“*参与*&#x200B;对于标题为“We.Retail Engage”的网站，创建的用户组之一将为：

* 社区 *参与* 成员

## 创作环境 {#author-environment}

### 隧道服务 {#tunnel-service}

使用创作环境时 [创建站点](sites-console.md), [修改网站属性](sites-console.md#modifying-site-properties) 和 [管理社区成员和成员组](members.md)，则需要访问在发布环境中注册的用户和用户组。

隧道服务使用作者上的复制代理提供此访问。

* 有关详细信息，请参阅 [配置说明](deploy-communities.md#tunnel-service-on-author) 在部署页面上。

的 [社区成员和组控制台](members.md) 仅用于管理仅在发布环境中注册的用户（成员）和用户组（成员组）。

要管理在创作环境中注册的用户和用户组，请使用 [安全控制台](../../help/sites-administering/security.md)

### 作者组角色 {#author-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 管理员 | 管理员组由系统管理员组成，这些系统管理员具有社区管理员的所有能力以及管理社区管理员组的能力。 |
| 社区管理员 | 社区管理员组会自动成为所有社区站点以及网站上创建的任何社区组的成员。 社区管理员组的初始成员是管理员组。 在创作环境中，社区管理员能够创建社区站点、管理站点、管理成员（他们可以禁止社区成员）以及审核内容。 |
| 社区&lt;*网站名称*> Sitecontentmanager | 社区站点内容管理器能够执行传统的AEM创作、内容创建和修改社区站点的页面。 |
| 社区支持经理 | 社区支持管理器组由可供分配的用户组成，这些用户可以管理社区站点的支持管理器组。 |
| 社区&lt;*网站名称* > Siteenablementmanagers | 社区站点启用管理器组由分配给管理社区站点启用的用户组成 [资源](resources.md). |
| 无 | 匿名网站访客可能无法访问创作环境。 |

### 系统管理员 {#system-administrators}

管理员组的成员是系统管理员，他们能够为创作和发布环境执行AEM安装的初始设置。

出于演示和开发目的，管理员组的成员的用户ID为 *管理员* 密码为 *管理员*.

对于生产环境，应修改默认的管理员组。

请务必遵循 [安全检查列表](../../help/sites-administering/security-checklist.md).

## 发布环境 {#publish-environment}

### 成为会员 {#becoming-a-member}

在发布环境中，具体取决于 [设置](sites-console.md#user-management) 在社区站点中，站点访客可以成为社区成员：

* 当社区站点为私有（已关闭）时：
   * 通过邀请
   * 按管理员的操作

* 当社区站点为公共（打开）时：
   * 通过自行注册
   * 通过Facebook和Twitter进行社交登录

>[!NOTE]
>
>如果站点访客注册为一个开放社区站点的成员，则他们会自动成为同一发布环境中其他开放社区站点的成员。

### 发布组角色 {#publish-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 社区&lt;*网站名称*>成员 | 社区站点成员是注册用户。 他们可以登录、修改其用户档案、加入开放的社区组、向社区发布内容、向其他成员发送消息，以及关注网站活动。 |
| 社区&lt;*网站名称*>审核者 | 社区站点审核者是受信任的社区成员，能够使用审核控制台或在发布内容的页面上的上下文中批量审核UGC。 |
| 社区&lt;*网站名称*> &lt;*组名称*>成员 | 社区组成员是已加入开放社区组或已受邀加入封闭社区组的社区成员。 他们具有站点内该社区组的成员能力。 |
| 社区&lt;*网站名称*>组管理员 | 社区站点组管理员是受信任的社区成员，被分配来创建和管理社区站点中的子社区（组）。 其中包括提供上下文审核的功能。 |
| *特权成员安全组* | 为限制内容创建而手动创建和维护的用户组。 请参阅 [特权成员组](#privileged-members-group). |
| 无 | 发现网站的匿名网站访客可以查看和搜索允许匿名访问的社区网站。 要参与和发布内容，用户必须自行注册（如果允许）并成为社区成员。 |

### 为成员分配发布组角色 {#assigning-members-to-publish-group-roles}

When [创建社区站点](sites-console.md) 或 [修改网站属性，](sites-console.md#modifying-site-properties) 可以为成员分配在发布环境中执行的各种角色，如审核者、组管理员、资源联系人或特权成员。

[启用隧道服务](sync.md#accessingpublishusersfromauthor) 会导致在发布时从成员而不是作者用户显示分配选项。

所选成员将被自动分配给 [适当组合](#publish-group-roles) 社区网站重新发布后，将包含其成员资格。

### 拥有权限的成员组 {#privileged-members-group}

特权成员安全组的目的是将为某些社区功能创建内容限制为社区站点成员的特权子集。

特权成员组是使用 [“社区组”控制台](members.md).

在创建拥有权限的成员组后，使用 [隧道服务已启用](sync.md#accessingpublishusersfromauthor)，则现有社区站点的结构可能为 [修改](sites-console.md#modify-structure) 编辑其社区功能的“允许特权成员”配置，并添加创建的组。

允许指定一个或多个特权成员组的社区功能包括：

* [博客功能](functions.md#blog-function)  — 限制新文章的创建。
* [日历函数](functions.md#calendar-function)  — 限制新事件的创建。
* [论坛功能](functions.md#forum-function)  — 限制新主题的创建。
* [问题解答函数](functions.md#qna-function)  — 限制创建新问题。

当社区功能未得到保护（未分配特权成员组）时，允许所有社区站点成员创建功能内容（文章、事件、主题、问题）。

>[!NOTE]
>
>将用户添加到社区站点的特权成员组时，仅当用户也是同一社区站点的成员时，才会授予他们创建权限。

## 创建社区成员 {#creating-community-members}

### 存储库位置 {#repository-location}

为了使某些功能正常工作，需要创建具有相应权限的用户和用户组。

在中创建成员时 `/home/users/community`，则会继承为成员配置文件授予读取权限的正确ACL。

同样，应在中创建自定义社区用户组（如特权成员组） `/home/groups/community`.

使用 [社区成员和组控制台](members.md) 将在这些路径中创建用户和组。

要指定自定义路径，需要使用经典安全UI，该UI可在 [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

要为自定义成员路径授予读取权限，请在所有发布实例上设置ACL，类似于 `/home/users/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

为自定义成员组路径（如/home/groups/mycompany）在所有发布实例上设置的ACL与 `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台 {#consoles}

只有在创作环境中，才有四个单独的控制台可用：

| 控制台 | 工具、安全性、用户 | 工具、安全性、组 | 社区、成员 | 社区、组 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 创作用户 | 创作时的用户组 | 发布时的成员 | 发布时的成员组 |
| reamires | 管理权限 | 管理权限 | 管理员权限、隧道服务、发布场的用户同步 | 管理员权限、隧道服务、发布场的用户同步 |

### 社区支持经理角色 {#community-enablement-manager-role}

网站访客通常不允许在 [启用社区](overview.md#enablement-community) 因为每个成员都有相关费用。 支持学习者和资源由分配了 [角色](#author-group-roles) of `enablement manager` [在网站创建期间](sites-console.md#enablement) 作者（添加为组成员） `Community <site-name> Siteenablementmanagers`)。 的 `enablement manager` 也负责 [分配学习资源](resources.md) 向社区成员的作者。

仅是全球成员的用户 `Community Enablement Managers` 可选择组作为 `enablement manager` 特定社区站点。

创建可能被分配了 `Community Site Enablement Manager`，请使用经典UI安全控制台以指定路径：

在创作实例上：

1. 使用管理员权限登录，浏览到经典UI安全控制台。

   例如， [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 从编辑菜单中，选择 **[!UICONTROL 创建用户]**.
3. 填写 `Create User` 对话框。
   * 路径必须为 `/home/users/community`.
4. 选择&#x200B;**[!UICONTROL 创建]**。

   ![create-community-user](assets/create-community-user.png)

* 在左窗格中，搜索新创建的用户，然后选择以在右窗格中显示。

   ![社区用户](assets/view-community-user.png)

在左边窗格中：

1. 清除搜索框并选择 **[!UICONTROL 隐藏用户]**.
2. 定位和拖动 `community-enablementmanagers` 到 **[!UICONTROL 群组]** 选项卡。

   ![分配组](assets/assign-group.png)

### 社区管理员角色 {#community-administrators-role}

如 [作者组角色](#author-group-roles) 图表中，社区管理员组的成员能够创建社区站点、管理站点、管理成员（他们可以禁止社区成员）以及审核内容。

按照与创建用户并将其分配给的角色相同的步骤进行操作 [启用管理器](#communitysiteenablementmanagerrole)，但添加c `ommunity-administrators` 群组。

### LDAP集成 {#ldap-integration}

AEM支持使用LDAP对用户进行身份验证以及创建用户帐户。 详见 [使用AEM 6配置LDAP](../../help/sites-administering/ldap-config.md).

以下是特定于社区成员和成员组的一些配置详细信息。

1. 为每个AEM发布实例配置LDAP。
2. [LDAP标识提供程序](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 无特殊说明

3. [同步处理程序](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 设置以下属性：

      * **[!UICONTROL 用户自动成员资格]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL 用户路径前缀]**: `/community`
      * **[!UICONTROL 组路径前缀]**: `/community`

4. [外部登录模块](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 没有特别说明

这会导致用户被自动分配到社区站点的成员组和存储库位置 `/home/users/community` 和 `/home/groups/community`，以便他们继承相应的权限来查看彼此的配置文件。

* 的 `User auto membership` 值应为 `rep:authorizableId` 属性，而不是 `givenName` （显示名称）。

## 在AEM实例之间同步用户 {#synchronizing-users-among-aem-instances}

使用 [发布场](topologies.md)，请首先将用户导入一个实例，然后 [启用用户同步](sync.md) 来将用户分发到其他发布实例。

如果导入用户组，请确保用户组在每个发布实例上具有相同的路径，请导入到一个实例，然后 [创建资源包](../../help/sites-administering/package-manager.md#creating-a-new-package) 要导出，请在所有其他发布实例上安装该包。

虽然通过用户同步同步的用户组同步将包含在未来版本中，但当前仅 *会员资格* 当用户同步运行时，将同步用户组的。

## 关于社区组 {#about-community-groups}

讨论组时，有两个不同的主题：

* **[社区组](overview.md#communitygroups)**

   社区组是指在发布环境中为支持创建社区组的社区站点创建的子社区。 创建社区组会导致向网站添加更多页面，并以与其父社区站点类似的方式进行管理。 有关详细信息，请访问 [社区组要点](essentials-groups.md) 适用于开发人员和 [社区组](creating-groups.md) 作者。

* **[成员组](../../help/sites-administering/security.md)**

   成员组是成员可能属于的组，可通过“组”控制台进行管理。 本页讨论的大部分内容都是专门讨论会员组。 为社区站点自动创建的成员组，其前缀为 *`Community`*，可称为社区组，因此必须考虑讨论的背景。
