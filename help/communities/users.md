---
title: 管理用户和用户组
seo-title: Managing Users and User Groups
description: AEM Communities的用户可以自行注册和编辑其配置文件
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

在AEM Communities中，在发布环境中，用户可以自行注册和编辑其配置文件。 获得适当的权限后，他们还可以：

* 在社区站点中创建子社区(请参阅 [社区组](creating-groups.md))。

* [审核](moderation.md) 用户生成内容(UGC)。

* 是 [启用资源](resources.md) 联系人。

* 是 [特权](#privileged-members-group) 创建博客、日历、问题与解答和论坛条目。

在发布环境中注册的用户通常称为 *社区成员（成员）* 来区分他们 *用户* 在创作环境中。

通过为成员分配以下项之一来授予权限： [成员（用户）组](#publish-group-roles) 在社区站点为 [已创建](sites-console.md) 或 [修改时间](sites-console.md#modifying-site-properties) 创作环境中的。 在创作环境中工作时，成员可通过以下方式从发布环境中可见： [隧道服务](#tunnel-service).

根据设计，在发布环境中创建的成员和成员组不应出现在创作环境中。 在创作环境中创建的用户和用户组同样打算保留在创作环境中。

当创作用户和发布用户来自同一用户列表时（例如从同一LDAP目录同步），在创作环境和发布环境中他们不会被视为拥有相同权限和组成员资格的同一用户。 必须根据需要在发布和创作时分别建立成员和用户的角色。

对于 [发布场](topologies.md)，对一个发布实例所做的注册和修改需要与其他发布实例同步，以便它们可以访问相同的用户数据。 有关详细信息，请参阅 [用户同步](sync.md)，其中包含描述 [当……发生什么情况？](sync.md#what-happens-when).

### 贡献限制 {#contribution-limits}

为了防止垃圾邮件，可以限制成员发布内容的频率。 此外，可以自动限制新登记成员的缴款。

有关详细信息，请参阅 [成员缴款限制](limits.md).

### 动态创建的用户组 {#dynamically-created-user-groups}

创建新社区站点后，系统会使用唯一id (uid)和适当的权限动态创建新用户组，这些权限适合在创作环境中管理社区站点所需的各种管理功能(请参阅 [作者组角色](#author-group-roles))或发布环境(请参阅 [发布组角色](#publish-group-roles))。

组的名称由指定站点的名称生成，该名称创建于 [社区站点创建](sites-console.md#step13asitetemplate). 唯一ID可避免同一服务器上名称相似的社区站点和社区组的命名冲突。

例如，如果站点名称为“*参与*”对于名为“We.Retail Engage”的网站，则创建的用户组之一将是：

* 社区 *参与* 成员

## 创作环境 {#author-environment}

### 通道服务 {#tunnel-service}

使用创作环境时 [创建站点](sites-console.md)， [修改站点属性](sites-console.md#modifying-site-properties) 和 [管理社区成员和成员组](members.md)中，必须访问在发布环境中注册的用户和用户组。

通道服务使用创作实例上的复制代理提供此访问权限。

* 有关详细信息，请参阅 [配置说明](deploy-communities.md#tunnel-service-on-author) （在部署页面上）。

此 [社区成员和组控制台](members.md) 仅用于管理仅在发布环境中注册的用户（成员）和用户组（成员组）。

要管理在创作环境中注册的用户和用户组，请使用 [安全控制台](../../help/sites-administering/security.md)

### 作者组角色 {#author-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 管理员 | 管理员组由系统管理员组成，系统管理员具有社区管理员的所有能力以及管理社区管理员组的能力。 |
| 社区管理员 | 社区管理员组会自动成为所有社区站点以及在站点上创建的任何社区组的成员。 社区管理员组的初始成员是管理员组。 在创作环境中，社区管理员能够创建社区站点、管理站点、管理成员（他们可以从社区中禁止成员）和审核内容。 |
| 社区&lt;*站点名称*> Sitecontentmanager | 社区站点内容管理器能够为社区站点执行传统的AEM创作、内容创建和修改页面。 |
| 社区启用管理员 | “社区启用管理员”组由用户组成，这些用户可以指定管理社区站点的启用管理员组。 |
| 社区&lt;*站点名称* > Siteenablementmanagers | “社区站点启用管理员”组由指定管理社区站点启用的用户组成 [资源](resources.md). |
| 无 | 匿名网站访客不能访问作者环境。 |

### 系统管理员 {#system-administrators}

管理员组的成员是系统管理员，他们能够为创作和发布环境执行AEM安装的初始设置。

出于演示和开发目的，管理员组具有的用户ID为 *管理员* 且密码为 *管理员*.

对于生产环境，应修改默认的管理员组。

请务必遵循 [安全核对清单](../../help/sites-administering/security-checklist.md).

## 发布环境 {#publish-environment}

### 成为会员 {#becoming-a-member}

在发布环境中，具体取决于 [设置](sites-console.md#user-management) 在社区站点中，站点访客可以成为社区成员：

* 当社区站点为私有（关闭）时：
   * 通过邀请
   * 按管理员操作

* 当社区站点为公共（开放）时：
   * 通过自助注册
   * 通过使用Facebook和Twitter进行社交登录

>[!NOTE]
>
>如果网站访客注册为一个开放社区网站的成员，则他们会自动成为同一发布环境中其他开放社区网站的成员。

### 发布组角色 {#publish-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 社区&lt;*站点名称*>成员 | 社区站点成员是注册用户。 他们可以登录、修改个人资料、加入开放的社区组、向社区发布内容、向其他成员发送消息以及关注网站活动。 |
| 社区&lt;*站点名称*>版主 | 社区站点审查方是受信任的社区成员，他能够在发布内容的页面上使用审查控制台批量审查或上下文审查UGC。 |
| 社区&lt;*站点名称*> &lt;*组名称*>成员 | 社区组成员是已加入开放社区组或已被邀请加入封闭社区组的社区成员。 他们具有站点中该社区组的成员的能力。 |
| 社区&lt;*站点名称*>组管理员 | 社区站点组管理员是受信任的社区成员，其任务是在社区站点中创建和管理子社区（组）。 包括提供上下文审核的功能。 |
| *拥有权限的成员安全组* | 手动创建和维护的用户组，用于限制内容创建。 参见 [拥有权限的成员组](#privileged-members-group). |
| 无 | 发现网站的匿名网站访客可以查看和搜索允许匿名访问的社区网站。 要参与并发布内容，用户必须自行注册（如果允许）并成为社区成员。 |

### 将成员分配给发布组角色 {#assigning-members-to-publish-group-roles}

时间 [创建社区站点](sites-console.md) 在创作环境中，或 [修改站点属性，](sites-console.md#modifying-site-properties) 可以为成员分配在发布环境中执行的各种角色，例如版主、组管理员、资源联系人或拥有权限的成员。

[启用通道服务](sync.md#accessingpublishusersfromauthor) 导致从“发布”上的成员而不是“作者”上的用户显示分配选择。

选定的成员将自动分配给 [适当组](#publish-group-roles) 社区站点（重新）发布时，其成员资格将包含在内。

### 拥有权限的成员组 {#privileged-members-group}

拥有权限的成员安全组的目的是将某些社区功能的内容创建限制在社区站点成员拥有权限的子集。

拥有权限的成员组是使用 [社区组控制台](members.md).

创建拥有权限的成员组后，使用 [已启用通道服务](sync.md#accessingpublishusersfromauthor)，则现有社区站点的结构可能为 [修改时间](sites-console.md#modify-structure) 将其社区功能的配置编辑为“允许拥有权限的成员”并添加已创建的组。

允许指定一个或多个拥有权限的成员组的社区功能包括：

* [博客功能](functions.md#blog-function)  — 限制创建新文章。
* [日历功能](functions.md#calendar-function)  — 限制创建新事件。
* [论坛功能](functions.md#forum-function)  — 限制创建新主题。
* [问题与解答功能](functions.md#qna-function)  — 限制创建新问题。

当社区功能不安全（未分配拥有权限的成员组）时，则允许所有社区站点成员创建功能内容（文章、事件、主题、问题）。

>[!NOTE]
>
>将用户添加到社区站点的拥有权限的成员组时，只有该用户同时也是同一社区站点的成员，才会授予其创建权限。

## 创建社区成员 {#creating-community-members}

### 存储库位置 {#repository-location}

为了使某些功能正常工作，需要创建具有适当权限的用户和用户组。

在中创建成员时 `/home/users/community`，它们将继承赋予成员配置文件读取权限的正确ACL。

同样，自定义社区用户组（如拥有权限的成员组）应创建于 `/home/groups/community`.

使用 [社区成员和组控制台](members.md) 将在这些路径中创建用户和组。

要指定自定义路径，需要使用经典安全UI，可从以下位置访问： [https://&lt;server>：&lt;port>/useradmin](http://localhost:4503/useradmin).

要授予自定义成员路径的读取权限，请在所有发布实例上设置ACL，其形式类似于 `/home/users/community`：

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

要为所有发布实例上的自定义成员组路径（如/home/groups/mycompany）授予适当的权限，请设置类似于的ACL `/home/groups/community`：

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台 {#consoles}

只有创作环境中提供了四个单独的控制台：

| 控制台 | 工具、安全性、用户 | 工具、安全性、组 | 社区、成员 | 社区、组 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 作者用户 | 作者用户组 | 发布时的成员 | 发布时的成员组 |
| 需要 | 管理员权限 | 管理员权限 | 发布场的管理员权限、隧道服务、用户同步 | 发布场的管理员权限、隧道服务、用户同步 |

### 社区启用经理角色 {#community-enablement-manager-role}

通常不允许网站访客对进行自助注册。 [启用社区](overview.md#enablement-community) 因为每个成员都有相关的成本。 支持学习者和资源由分配了以下项的用户管理 [角色](#author-group-roles) 之 `enablement manager` [站点创建期间](sites-console.md#enablement) 作者（添加为组成员） `Community <site-name> Siteenablementmanagers`)。 此 `enablement manager` 还负责 [分配学习资源](resources.md) 对作者的社区成员。

仅全局成员用户 `Community Enablement Managers` 可以选择组作为 `enablement manager` 的特定社区站点。

创建可能分配了以下角色的用户： `Community Site Enablement Manager`，请使用经典UI安全控制台指定路径：

在创作实例上：

1. 以管理员权限登录，浏览至经典UI安全控制台。

   例如， [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 从“编辑”菜单中，选择 **[!UICONTROL 创建用户]**.
3. 填写 `Create User` 对话框。
   * 路径必须为 `/home/users/community`.
4. 选择&#x200B;**[!UICONTROL 创建]**。

   ![create-community-user](assets/create-community-user.png)

* 在左窗格中，搜索新创建的用户，然后选择以显示在右窗格中。

   ![community-user](assets/view-community-user.png)

在左边窗格中：

1. 清除搜索框并选择 **[!UICONTROL 隐藏用户]**.
2. 查找并拖动 `community-enablementmanagers` 到 **[!UICONTROL 组]** 选项卡。

   ![assign-group](assets/assign-group.png)

### 社区管理员角色 {#community-administrators-role}

如附注所述， [作者组角色](#author-group-roles) 图表，社区管理员组的成员可以创建社区站点、管理站点、管理成员（他们可以从社区中禁止成员）和审核内容。

执行与创建用户并将其分配给角色相同的步骤 [启用管理器](#communitysiteenablementmanagerrole)，但添加c `ommunity-administrators` 组（在用户的“组”选项卡下）。

### LDAP集成 {#ldap-integration}

AEM支持使用LDAP对用户进行身份验证以及创建用户帐户。 有关详情，请参阅 [使用AEM 6配置LDAP](../../help/sites-administering/ldap-config.md).

以下是特定于社区成员和成员组的一些配置详细信息。

1. 为每个AEM发布实例配置LDAP。
2. [LDAP身份提供程序](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 无特殊说明

3. [同步处理程序](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 设置以下属性：

      * **[!UICONTROL 用户自动成员资格]**： `community-<site name>-<uid>-members`
      * **[!UICONTROL 用户路径前缀]**： `/community`
      * **[!UICONTROL 组路径前缀]**： `/community`

4. [外部登录模块](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 无特殊说明

这会导致自动将用户分配给社区站点的成员组，并且存储库位置为 `/home/users/community` 和 `/home/groups/community`，以便他们继承查看彼此配置文件的相应权限。

* 此 `User auto membership` 值应为 `rep:authorizableId` 属性，而不是 `givenName` （显示名称）。

## 在AEM实例之间同步用户 {#synchronizing-users-among-aem-instances}

使用时 [发布场](topologies.md)，确保用户在每个发布实例上具有相同的路径，方法是首先将用户导入一个实例，然后 [启用用户同步](sync.md) 对于Sling，将用户分配到其他发布实例。

如果导入用户组，为确保用户组在每个发布实例上具有相同的路径，请导入一个实例，然后 [创建资源包](../../help/sites-administering/package-manager.md#creating-a-new-package) 导出，并在所有其他发布实例上安装该包。

虽然通过用户同步来同步用户组将包含在未来版本中，但目前仅 *会员资格* 用户同步运行时将同步的用户组的。

## 关于社区组 {#about-community-groups}

讨论组时，有两个不同的主题：

* **[社区组](overview.md#communitygroups)**

   社区组是子社区，可以在支持创建社区组的社区站点的发布环境中创建。 创建社区组后，会将更多页面添加到该网站，并按照与其父社区站点类似的方式进行管理。 有关详细信息，请访问 [社区组要点](essentials-groups.md) 适用于开发人员和 [社区组](creating-groups.md) 供作者使用。

* **[成员组](../../help/sites-administering/security.md)**

   成员组是成员可能所属的组，通过“组”控制台进行管理。 本页上的大部分讨论都专门针对成员组。 自动为社区站点创建的成员组，其前缀为 *`Community`*，可称为社区组，因此必须考虑讨论的内容。
