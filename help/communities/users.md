---
title: 管理用户和用户组
description: AEM Communities的用户可以自行注册和编辑其配置文件
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# 管理用户和用户组 {#managing-users-and-user-groups}

## 概述 {#overview}

在AEM Communities中的发布环境中，用户可以自行注册和编辑其配置文件。 根据相应的权限，他们还可以：

* 在社区站点中创建子社区(请参阅 [社区组](creating-groups.md))。

* [审核](moderation.md) 用户生成的内容(UGC)。

* 是 [特权](#privileged-members-group) 创建博客、日历、问题与解答和论坛条目。

在发布环境中注册的用户通常称为 *社区成员（成员）* 来区分他们 *用户* 在创作环境中。

通过将成员分配给以下项之一来授予权限： [成员（用户）组](#publish-group-roles) 在社区站点处于以下状态时动态创建 [已创建](sites-console.md) 或 [已修改](sites-console.md#modifying-site-properties) 创作环境中的。 在创作环境中工作时，成员可通过的 [通道服务](#tunnel-service).

按照设计，在发布环境中创建的成员和成员组不应出现在创作环境中。 在创作环境中创建的用户和用户组同样也打算保留在创作环境中。

当作者用户和发布用户来自同一用户列表时（例如从同一个LDAP目录同步），作者环境和发布环境中拥有相同权限和组成员资格的用户将不同步。 必须根据需要在发布和创作时分别建立成员和用户的角色。

对于 [发布场](topologies.md)，对一个发布实例所做的注册和修改需要与其他发布实例同步，以便它们能够访问相同的用户数据。 有关详细信息，请参阅 [用户同步](sync.md)，其中包含描述 [当……发生什么情况？](sync.md#what-happens-when).

### 贡献限制 {#contribution-limits}

为了防止垃圾邮件，可以限制成员的发布内容频率。 此外，可以自动限制新登记成员的缴款。

有关详细信息，请参阅 [成员贡献限制](limits.md).

### 动态创建的用户组 {#dynamically-created-user-groups}

创建新社区站点后，将动态创建新的用户组，这些用户组具有唯一ID (uid)和适当的权限，这些权限适合在创作环境中管理社区站点所需的各种管理功能(请参阅 [作者组角色](#author-group-roles))或发布环境(请参阅 [发布组角色](#publish-group-roles))。

组的名称由指定站点的名称生成。 [社区站点创建](sites-console.md#step13asitetemplate). 唯一ID可避免同一服务器上名称相似的社区站点和社区组的命名冲突。

例如，如果站点名称为&quot;*参与*&#x200B;对于标题为“参与”的网站，创建的用户组之一将是：

* 社区 *参与* 成员

## 创作环境 {#author-environment}

### 通道服务 {#tunnel-service}

使用创作环境时 [创建站点](sites-console.md)， [修改站点属性](sites-console.md#modifying-site-properties) 和 [管理社区成员和成员组](members.md)中，必须访问在发布环境中注册的用户和用户组。

通道服务使用创作实例上的复制代理提供此访问权限。

* 有关详细信息，请参阅 [配置说明](deploy-communities.md#tunnel-service-on-author) 在部署页面上。

此 [社区成员和组控制台](members.md) 仅用于管理仅在发布环境中注册的用户（成员）和用户组（成员组）。

要管理在创作环境中注册的用户和用户组，请使用 [安全控制台](../../help/sites-administering/security.md)

### 作者组角色 {#author-group-roles}

| 如果组成员…… | 主要角色 |
|---|---|
| 管理员 | 管理员组由系统管理员组成，系统管理员具有社区管理员的所有能力以及管理社区管理员组的能力。 |
| 社区管理员 | 社区管理员组会自动成为所有社区站点以及在站点上创建的任何社区组的成员。 社区管理员组的初始成员是管理员组。 在创作环境中，社区管理员可以创建社区站点、管理站点、管理成员（他们可以从社区中禁止成员）并审核内容。 |
| 社区&lt;*站点名称*> Sitecontentmanager | 社区站点内容管理器能够执行传统的AEM创作、内容创建和修改社区站点的页面。 |
| 无 | 匿名网站访客可能无法访问作者环境。 |

### 系统管理员 {#system-administrators}

管理员组的成员是系统管理员，他们能够为创作环境和发布环境执行AEM安装的初始设置。

出于演示和开发目的，管理员组有一个成员，其用户ID为 *管理员* 且密码为 *管理员*.

对于生产环境，应修改默认的管理员组。

请务必遵循 [安全核对清单](../../help/sites-administering/security-checklist.md).

## 发布环境 {#publish-environment}

### 成为会员 {#becoming-a-member}

在发布环境中，根据 [设置](sites-console.md#user-management) 在社区站点中，站点访客可以成为社区成员：

* 当社区站点为私有（已关闭）时：
   * 通过邀请
   * 按管理员的操作

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
| 社区&lt;*站点名称*>审查方 | 社区站点审查方是受信任的社区成员，他们能够在发布内容的页面上使用审查控制台或上下文中批量审查UGC。 |
| 社区&lt;*站点名称*> &lt;*组名称*>成员 | 社区组成员是已加入开放社区组或已被邀请加入已关闭社区组的社区成员。 他们能够在站点中成为该社区组的成员。 |
| 社区&lt;*站点名称*>组管理员 | 社区站点组管理员是受信任的社区成员，其任务是在社区站点中创建和管理子社区（组）。 包括提供上下文审核的功能。 |
| *拥有权限的成员安全组* | 手动创建和维护的用户组，用于限制内容创建。 请参阅 [拥有权限的成员组](#privileged-members-group). |
| 无 | 发现网站的匿名网站访客可以查看和搜索允许匿名访问的社区网站。 要参与并发布内容，用户必须自行注册（如果允许）并成为社区成员。 |

### 将成员分配给发布组角色 {#assigning-members-to-publish-group-roles}

时间 [创建社区站点](sites-console.md) 在创作环境中，或 [修改站点属性，](sites-console.md#modifying-site-properties) 可以为成员分配在发布环境中执行的各种角色，例如版主、组管理员、资源联系人或特权成员。

[启用通道服务](sync.md#accessingpublishusersfromauthor) 导致从发布上的成员而不是从创作上的用户显示分配选择。

所选成员将自动分配给 [适当组](#publish-group-roles) 社区站点（重新）发布时，其成员资格也将被包括。

### 拥有权限的成员组 {#privileged-members-group}

拥有权限的成员安全组的目的是将某些社区功能的内容创建限制在社区站点成员的拥有权限的子集。

拥有权限的成员组是使用 [社区组控制台](members.md).

创建拥有权限的成员组后，使用 [已启用通道服务](sync.md#accessingpublishusersfromauthor)，则现有社区站点的结构可能为 [已修改](sites-console.md#modify-structure) 将其社区功能的配置编辑为“允许拥有权限的成员”并添加已创建的组。

允许指定一个或多个特权成员组的社区功能包括：

* [博客功能](functions.md#blog-function)  — 限制创建新文章。
* [日历功能](functions.md#calendar-function)  — 限制创建新事件。
* [论坛功能](functions.md#forum-function)  — 限制创建新主题。
* [问题与解答功能](functions.md#qna-function)  — 限制新问题的创建。

当某个社区功能未受保护（未分配特权成员组）时，则允许所有社区站点成员创建功能内容（文章、事件、主题、问题）。

>[!NOTE]
>
>将用户添加到社区站点的拥有权限的成员组，将只授予他们创建权限，前提是他们也是同一社区站点的成员。

## 创建社区成员 {#creating-community-members}

### 存储库位置 {#repository-location}

为了使某些功能正常工作，需要创建具有适当权限的用户和用户组。

在中创建成员时 `/home/users/community`中，将继承为成员配置文件授予读取权限的适当ACL。

同样，应在中创建自定义社区用户组（如拥有权限的成员组） `/home/groups/community`.

使用 [社区成员和组控制台](members.md) 将在这些路径中创建用户和组。

要指定自定义路径，需要使用经典安全UI，该UI可在 [https://&lt;server>：&lt;port>/useradmin](http://localhost:4503/useradmin).

要为自定义成员路径提供读取权限，在所有发布实例上设置ACL，类似于 `/home/users/community`：

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

只有创作环境中才有四个单独的控制台：

| 控制台 | 工具、安全性、用户 | 工具、安全性、组 | 社区、成员 | 社区、组 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 作者用户 | 作者用户组 | 发布上的成员 | 发布上的成员组 |
| 需要 | 管理员权限 | 管理员权限 | 发布场的管理员权限、通道服务、用户同步 | 发布场的管理员权限、通道服务、用户同步 |

### 社区管理员角色 {#community-administrators-role}

如附注所述， [作者组角色](#author-group-roles) 图表，社区管理员组的成员可以创建社区站点、管理站点、管理成员（他们可以从社区中禁止成员）和审核内容。

执行创建用户并将其分配给启用管理员角色的相同步骤，但添加 `ommunity-administrators` 组（在用户的“组”选项卡下）。

### LDAP集成 {#ldap-integration}

AEM支持使用LDAP对用户进行身份验证和创建用户帐户。 有关详情，请参阅 [使用AEM 6配置LDAP](../../help/sites-administering/ldap-config.md).

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

这会导致用户自动分配到社区站点的成员组，并且存储库位置为 `/home/users/community` 和 `/home/groups/community`，以便他们继承查看彼此配置文件的相应权限。

* 此 `User auto membership` 值应为 `rep:authorizableId` 属性，而不是 `givenName` （显示名称）。

## 在AEM实例之间同步用户 {#synchronizing-users-among-aem-instances}

使用 [发布场](topologies.md)，通过将用户首先导入一个实例和，确保用户在每个发布实例上具有相同的路径 [启用用户同步](sync.md) ，将用户分发到其他发布实例。

如果导入用户组，为确保用户组在每个发布实例上具有相同的路径，请导入一个实例，然后 [创建资源包](../../help/sites-administering/package-manager.md#creating-a-new-package) ，并在所有其他发布实例上安装该包。

虽然通过用户同步来同步用户组将包含在将来的版本中，但目前只有 *会员资格* 用户同步运行时将同步的用户组的。

## 关于社区组 {#about-community-groups}

讨论组时，有两个不同的主题：

* **[社区组](overview.md#communitygroups)**

  社区组是子社区，可以在支持创建社区组的社区站点的发布环境中创建。 创建社区组会导致将更多页面添加到网站，并且会采用与其父社区站点类似的方式进行管理。 有关详细信息，请访问 [社区组要点](essentials-groups.md) 适用于开发人员和 [社区组](creating-groups.md) 供作者使用。

* **[成员组](../../help/sites-administering/security.md)**

  成员组是成员可能所属的组，并通过组控制台进行管理。 本页的大部分讨论都集中在成员组上。 自动为社区站点创建的成员组，其前缀为 *`Community`*，可称为社区组，因此必须考虑讨论的内容。
