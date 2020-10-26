---
title: 用户管理和安全
seo-title: 用户管理和安全
description: 了解AEM中的用户管理和安全。
seo-description: 了解AEM中的用户管理和安全。
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
translation-type: tm+mt
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '5487'
ht-degree: 2%

---


# 用户管理和安全{#user-administration-and-security}

本章介绍如何配置和维护用户授权，并描述身份验证和授权在AEM中工作的原理。

## AEM中的用户和用户组 {#users-and-groups-in-aem}

本节将更详细地介绍各种实体和相关概念，以帮助您配置易于维护的用户管理概念。

### 用户 {#users}

用户将使用其帐户登录AEM。 每个用户帐户都是唯一的，包含基本帐户详细信息以及分配的权限。

用户通常是组的成员，这简化了这些权限和／或权限的分配。

### 组 {#groups}

组是用户和／或其他组的集合；这些都称为组成员。

其主要目的是通过减少要更新的实体数来简化维护过程，因为对组所做的更改会应用于组的所有成员。 组通常反映：

* 应用程序中的角色；例如，有权浏览内容的人员，或有权提供内容的人员。
* 您自己的组织；当参与者被限制在内容树中的不同分支时，您可能希望扩展角色以区分来自不同部门的参与者。

因此，组往往保持稳定，而用户来来去的频率更高。

借助规划和整洁的结构，组的使用可以反映您的结构，为您提供清晰的概述和高效的更新机制。

### Built-in Users and Groups {#built-in-users-and-groups}

AEM WCM安装许多用户和用户组。 安装后首次访问安全控制台时，可以看到这些内容。

下表将每个项目与以下项目列表在一起：

* 简短描述
* 关于必要更改的任何建议

*请更改所有默认密码* （如果在某些情况下不删除帐户本身）。

<table>
 <tbody>
  <tr>
   <td>用户 ID</td>
   <td>类型</td>
   <td>描述</td>
   <td>推荐</td>
  </tr>
  <tr>
   <td><p>管理员</p> <p>默认密码：管理员</p> </td>
   <td>用户</td>
   <td><p>具有完全访问权限的系统管理帐户。</p> <p>此帐户用于AEM WCM和CRX之间的连接。</p> <p>如果意外删除了此帐户，将在重新启动存储库（在默认设置中）时重新创建它。</p> <p>管理员帐户是AEM平台的一项要求。 因此，无法删除此帐户。</p> </td>
   <td><p>Adobe强烈建议将此用户帐户的密码从默认值更改。</p> <p>最好在安装时，尽管可以在安装后完成。</p> <p>注意：不要将此帐户与CQ Servlet引擎的管理员帐户混淆。</p> </td>
  </tr>
  <tr>
   <td><p>匿名</p> <p> </p> </td>
   <td>用户</td>
   <td><p>保留对实例的未验证访问的默认权限。 默认情况下，它包含最小访问权限。</p> <p>如果意外删除了此帐户，将在启动时重新创建它。 它无法永久删除，但可以禁用。</p> </td>
   <td>请避免删除或禁用此帐户，因为这将对作者实例的功能产生负面影响。 如果有安全要求要求您删除它，请确保首先正确测试它对您的系统的影响。</td>
  </tr>
  <tr>
   <td><p>作者</p> <p>默认密码：作者</p> </td>
   <td>用户</td>
   <td><p>允许写入/content的作者帐户。 包含投稿人和冲浪者特权。</p> <p>可以用作Web主站点，因为它有权访问整个/content树。</p> <p>这不是内置用户，而是另一个geometrixx演示用户</p> </td>
   <td><p>Adobe建议完全删除帐户，或者从默认帐户更改密码。</p> <p>最好在安装时，尽管可以在安装后完成。</p> </td>
  </tr>
  <tr>
   <td>管理员</td>
   <td>组</td>
   <td><p>授予其所有成员管理员权限的组。 仅允许管理员编辑此组。</p> <p>具有完全访问权限。</p> </td>
   <td>如果在节点上设置“拒绝所有人”，则只有在再次为该组启用该权限时，管理员才具有访问权限。</td>
  </tr>
  <tr>
   <td>content-authors</td>
   <td>组</td>
   <td><p>负责内容编辑的组。 需要读取、修改、创建和删除权限。</p> </td>
   <td>您可以创建具有项目特定访问权限的您自己的内容作者组，前提是您添加读取、修改、创建和删除权限。</td>
  </tr>
  <tr>
   <td>contributor</td>
   <td>组</td>
   <td><p>允许用户编写内容的基本权限（仅在功能中）。</p> <p>不向/content树分配任何权限——必须为单个组或用户专门分配这些权限。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam用户</td>
   <td>组</td>
   <td>典型AEM Assets用户的现成参考组。 此组的成员具有相应的权限，可启用资产和集合的上传／共享。</td>
   <td> </td>
  </tr>
  <tr>
   <td>人</td>
   <td>组</td>
   <td><p>AEM中的每个用户都是组中每个人的成员，即使您可能看不到组或所有工具中的成员关系。</p> <p>可以将此组视为默认权限，因为它可用于为所有人（甚至是将来创建的用户）应用权限。</p> </td>
   <td><p>请勿修改或删除此组。</p> <p>修改此帐户还会产生其他安全影响。</p> </td>
  </tr>
  <tr>
   <td>标签管理员</td>
   <td>组</td>
   <td>允许编辑标记的组。</td>
   <td> </td>
  </tr>
  <tr>
   <td>用户管理员</td>
   <td>组</td>
   <td>授权用户管理，即创建用户和用户组的权利。</td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流编辑器</td>
   <td>组</td>
   <td>允许创建和修改工作流模型的组。</td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流用户</td>
   <td>组</td>
   <td><p>参与工作流的用户必须是组工作流用户的成员。 这使他／她能够完全访问：/etc/workflow/instances，以便他或她可以更新工作流实例。</p> <p>该组包含在标准安装中，但您必须手动将用户添加到该组。</p> </td>
  </tr>
 </tbody>
</table>

## AEM中的权限 {#permissions-in-aem}

AEM使用ACL确定用户或用户组可以执行哪些操作以及在何处执行这些操作。

### 权限和ACL {#permissions-and-acls}

权限定义允许谁对资源执行哪些操作。 权限是访问控制评估 [的结果](#access-control-lists-and-how-they-are-evaluated) 。

您可以通过选择或清除单个AEM操作的复选框来更改授予／拒绝给定用户的 [权限](security.md#actions)。 复选标记表示允许执行操作。 没有复选标记表示操作被拒绝。

复选标记位于网格中的位置还指示用户在AEM中的哪些位置（即哪些路径）拥有哪些权限。

### 操作 {#actions}

可以对页面（资源）执行操作。 对于层次结构中的每个页面，您可以指定允许用户对该页面执行哪些操作。 [权限](#permissions-and-acls) 允许您允许或拒绝某个操作。

<table>
 <tbody>
  <tr>
   <td><strong>操作 </strong></td>
   <td><strong>描述 </strong></td>
  </tr>
  <tr>
   <td>读取</td>
   <td>允许用户读取页面和任何子页面。</td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p>用户可以：</p>
    <ul>
     <li>修改页面上和任何子页面上的现有内容。</li>
     <li>在页面或任何子页面上创建新段落。</li>
    </ul> <p>在JCR级别，用户可以通过修改资源的属性、锁定、版本控制、nt修改来修改资源，并且他们对定义jcr:content子节点的节点具有完全写入权限，例如cq:Page、nt:file、cq:Asset。</p> </td>
  </tr>
  <tr>
   <td>创建</td>
   <td><p>用户可以：</p>
    <ul>
     <li>创建新页面或子页面。</li>
    </ul> <p>如果 <strong>拒绝</strong> modify，则会明确排除jcr:content下的子树，因为创建jcr:content及其子节点被视为页面修改。 这仅适用于定义jcr:content子节点的节点。</p> </td>
  </tr>
  <tr>
   <td>删除</td>
   <td><p>用户可以：</p>
    <ul>
     <li>从页面或任何子页面中删除现有段落。</li>
     <li>删除页面或子页面。</li>
    </ul> <p>如果 <strong>拒绝</strong> modify，则jcr:content下的任何子树将被明确排除，作为删除jcr:content，其子节点将被视为页面修改。 这仅适用于定义jcr:content子节点的节点。</p> </td>
  </tr>
  <tr>
   <td>读取 ACL</td>
   <td>用户可以阅读页面或子页面的访问控制列表。</td>
  </tr>
  <tr>
   <td>编辑 ACL</td>
   <td>用户可以修改页面或任何子页面的访问控制列表。</td>
  </tr>
  <tr>
   <td>复制</td>
   <td>用户可以将内容复制到其他环境(例如，发布环境)。 该权限也会应用于任何子页面。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM会自动为集合中的角色分配（所有者、编辑者、查看器）生成用 [户组](/help/assets/manage-collections.md)。 但是，手动为此类组添加ACL可能会在AEM中引入安全漏洞。 Adobe建议您避免手动添加ACL。

### 访问控制列表及其评估方式 {#access-control-lists-and-how-they-are-evaluated}

AEM WCM使用访问控制列表(ACL)来组织应用于各个页面的权限。

访问控制列表由各个权限组成，用于确定实际应用这些权限的顺序。 该列表根据所考虑页面的层次结构而形成。 然后，从下到上扫描此列表，直到找到应用于页面的第一个适当权限。

>[!NOTE]
>
>示例中包含有ACL。 建议您查看并确定适合您的应用程序的内容。 要查看包含的ACL，请转至**CRXDE **，然后为以下节 **点选** 择“访问控制”选项卡：
>
>`/etc/cloudservices/facebookconnect/geometrixx-outdoorsfacebookapp`:允许所有人读取访问。
>`/etc/cloudservices/twitterconnect/geometrixx-outdoors-twitter-app`:允许所有人读取访问。
>`/home/users/geometrixx-outdoors`:允许所有人访问和 `*/profile*` 读取
>`*/social/relationships/following/*`。
>
>您的自定义应用程序可以设置对其他关系（如或） `*/social/relationships/friend/*` 的访问 `*/social/relationships/pending-following/*`权。
>
>当您创建特定于社区的ACL时，加入这些社区的成员可能会获得额外的权限。 例如，当用户在或加入社区时，可能会出现 `/content/geometrixx-outdoors/en/community/hiking` 这种情况 `/content/geometrixx-outdoors/en/community/winter-sports`。

### 权限状态 {#permission-states}

>[!NOTE]
>
>对于CQ 5.3用户：
>
>与以前的CQ版本相 **比** ，如 **果用户只需修改页面，则不** 应再授予创建和删除权限。 相反，仅当您希 **望用户** 能够创建、修改或删除现有页面上的组件时，才可授予修改操作。
>
>由于向后兼容性的原因，动作测试不考虑定义jcr:content **的节点的** 特殊处理。

| **操作** | **描述** |
|---|---|
| 允许（复选标记） | AEM WCM允许用户在此页面或任何子页面上执行操作。 |
| 拒绝（无复选标记） | AEM WCM不允许用户在此页面或任何子页面上执行此操作。 |

权限也会应用于任何子页面。

如果某个权限未从父节点继承，但至少有一个本地条目，则以下符号将附加到该复选框。 本地条目是在CRX 2.2接口中创建的条目（通配符ACL当前只能在CRX中创建。）

对于给定路径上的操作：

<table>
 <tbody>
  <tr>
   <td>*（星号）</td>
   <td>至少有一个本地条目（有效或无效）。 这些通配符ACL在CRX中定义。</td>
  </tr>
  <tr>
   <td>! （感叹号）</td>
   <td>至少有一个条目当前无效。</td>
  </tr>
 </tbody>
</table>

当您将指针悬停在星号或感叹号上时，工具提示会提供有关声明条目的更多详细信息。 工具提示分为两部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>列表有效条目。</p> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td>列表可能在树中其他位置有效的无效条目（由具有相应ACE的特殊属性表示，该属性限制了条目的范围）。 或者，这是一个条目，其效果已被在给定路径或祖先节点中定义的另一个条目撤销。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>如果没有为页面定义权限，则会拒绝所有操作。

以下是有关管理访问控制列表的建议：

* 请勿直接将权限分配给用户。 仅将它们分配给组。

   这将简化维护，因为组数量比用户数少得多，而且波动性也更小。

* 如果您希望组／用户只能修改页面，请勿授予他们创建或拒绝权限。 仅授予他们修改和读取权限。
* 少用拒绝。 尽可能仅使用“允许”。

   如果权限的应用顺序与预期顺序不同，则使用拒绝可能会产生意外效果。 如果用户是多个组的成员，来自一个组的拒绝语句可以取消来自另一个组的允许语句，反之亦然。 在发生这种情况时，很难保留概述，并且很容易导致无法预见的结果，而“允许”分配不会造成此类冲突。

   Adobe建议您使用“允许”而非“拒绝”查看 [最佳实践](#best-practices)。

在修改任一权限之前，请确保您了解它们的工作方式和相互关联。 请参阅CRX文档以说明AEM WCM如何评 [估访问权限](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated) ，以及设置访问控制列表的示例。

### 权限 {#permissions}

权限允许用户和用户组访问AEM页面上的AEM功能。

通过展开／折叠节点按路径浏览权限，并可以跟踪到根节点的权限继承。

通过选择或清除相应的复选框，可以允许或拒绝权限。

![cqsecuritypermissionstab](assets/cqsecuritypermissionstab.png)

### 查看详细权限信息 {#viewing-detailed-permission-information}

除网格视图外，AEM还为给定路径下的选定用户／组提供详细的权限视图。 详细信息视图提供其他信息。

除了查看信息外，您还可以将当前用户或用户组包含或排除在用户组之外。 请参 [阅添加权限时添加用户或用户组](#adding-users-or-groups-while-adding-permissions)。 此处所做的更改会立即反映在详细视图的上半部分。

要访问详细信息视图，请在“权 **限** ”选项卡 **中** ，单击任何选定组／用户和路径的“详细信息”。

![权限详细信息](assets/permissiondetails.png)

详细信息分为两部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>重复在树网格中看到的信息。 对于每个操作，都会显示一个图标，显示是允许还是拒绝该操作：</p>
    <ul>
     <li>无图标=无声明的条目</li>
     <li>（勾号）=声明的操作（允许）</li>
     <li>(-)=声明的操作（拒绝）</li>
    </ul> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td><p>显示执行以下操作的用户和用户组网格：</p>
    <ul>
     <li>声明给定路径的条目AND</li>
     <li>给定的可授权OR是组</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 模拟其他用户 {#impersonating-another-user}

With the [Impersonate functionality](/help/sites-authoring/user-properties.md#user-settings) a user can work on behalf of another user.

这意味着用户帐户可以指定其他可以使用其帐户操作的帐户。 换言之，如果允许用户-B模拟用户-A，则用户-B可以使用用户-A的完整帐户详细信息执行操作。

这允许模拟者帐户完成任务，就像他们使用的是模拟的帐户一样；例如，在缺勤期间或共享过多负荷的短期情况。

>[!NOTE]
>
>为了模拟以适用于非管理员用户，模拟者（在上述情况下，用户-B）需要在路径中具有“读取” `/home/users` 权限。
>
>有关如何实现此目的的详细信息，请参 [阅AEM中的权限](/help/sites-administering/security.md#permissions-in-aem)。

>[!CAUTION]
>
>如果一个帐户模拟另一个帐户，则很难查看。 当模拟开始和结束时，在审计日志中创建一个条目，但其他日志文件（如访问日志）不包含有关事件上已发生模拟的事实的信息。 因此，如果用户- B是模拟用户- A所有事件看起来就像是由用户- A个人执行。

>[!CAUTION]
>
>模拟用户身份时可以执行页面锁定。但是，以这种方式锁定的页面随后只能由被模拟的用户或拥有管理员权限的用户解锁。
>
>不能通过模拟锁定页面的用户的身份来解锁页面。

### 最佳实践 {#best-practices}

下面介绍了使用权限和权限时的最佳实践：

| 规则 | 原因 |
|--- |--- |
| *使用组* | 避免按用户分配访问权限。 原因有几：<ul><li>用户比组多，因此组可以简化结构。</li><li>组帮助提供所有帐户的概述。</li> <li>对于组，继承更简单。</li><li>用户来来去。 群体是长期的。</li></ul> |
| *积极* | 始终使用“允许”语句指定组的权利（尽可能）。 避免使用Deny语句。 按顺序评估组，并且对顺序的定义可以不同于用户。 换言之：您可能几乎无法控制语句的实现和评估顺序。 如果仅使用“允许”语句，则顺序不重要。 |
| *保持简单* | 在配置新安装时投入一些时间和思考将得到很好的回报。 应用清晰的结构将简化持续的维护和管理，确保您的当前同事和／或未来继任者都能轻松了解正在实施的内容。 |
| *测试* | 使用测试安装来练习并确保您了解不同用户和组之间的关系。 |
| *默认用户／用户组* | 始终在安装后立即更新默认用户和用户组，以帮助防止出现任何安全问题。 |

## Managing Users and Groups {#managing-users-and-groups}

用户包括使用该系统的用户和向系统提出请求的外国系统。

组是一组用户。

这两种配置都可以使用安全控制台中的用户管理功能进行配置。

### 通过安全控制台访问用户管理 {#accessing-user-administration-with-the-security-console}

您可以使用安全控制台访问所有用户、用户组和关联权限。 本节中描述的所有过程都在此窗口中执行。

要访问AEM WCM安全性，请执行下列操作之一：

* 从欢迎屏幕或AEM中的各个位置，单击安全图标：

![](do-not-localize/wcmtoolbar.png)

* 直接导航到 `https://<server>:<port>/useradmin`。 请确保以管理员身份登录到AEM。

此时将显示以下窗口：

![cqsecuritypage](assets/cqsecuritypage.png)

左侧的树将列表系统中当前的所有用户和用户组。 您可以选择要显示的列，对列的内容进行排序，甚至通过将列标题拖动到新位置来更改列的显示顺序。

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

这些选项卡提供对各种配置的访问：

<!-- ??? in table below. -->

| 选项卡· | 描述 |
|--- |--- |
| 过滤器框 | 用于筛选列出的用户和／或组的机制。 请参 [阅筛选用户和用户组](#filtering-users-and-groups)。 |
| 隐藏用户 | 一个切换开关，它将隐藏所有列出的用户，仅保留用户组。 请参 [阅隐藏用户和用户组](#hiding-users-and-groups)。 |
| 隐藏组 | 一个切换开关，它将隐藏所有列出的组，仅保留用户。 请参 [阅隐藏用户和用户组](#hiding-users-and-groups)。 |
| 编辑 | 允许您创建和删除以及激活和取消激活用户或组的菜单。 请参 [阅创建用户和](#creating-users-and-groups)[用户组和删除用户和用户组](#deleting-users-and-groups)。 |
| 属性 | 列表有关用户或用户组的信息，这些信息可以包含电子邮件信息、说明和名称信息。 还允许您更改用户的口令。 请参 [阅创建用户](#creating-users-and-groups)和用 [户组、修改用户和组属性](#modifying-user-and-group-properties) 以 [及更改用户密码](#changing-a-user-password)。 |
| 组 | 列表选定用户或组所属的所有组。 您可以将选定的用户或用户组分配给其他用户组，或将其从用户组中删除。 请参 [阅组](#adding-users-or-groups-to-a-group)。 |
| 成员 | 仅适用于组。 列表特定组的成员。 请参阅 [成员](#members-adding-users-or-groups-to-a-group)。 |
| 权限 | 您可以为用户或用户组分配权限。 允许您控制以下内容：<ul><li>与特定页面／节点相关的权限。 请参阅 [设置权限](#setting-permissions)。 </li><li>与创建和删除页面以及修改层次结构相关的权限。???允许您 [分配权限](#settingprivileges)，如层次结构修改，它允许您创建和删除页面，</li><li>与复制权 [限相关的权](#setting-replication-privileges) 限（通常从创作到发布），根据路径。</li></ul> |
| 模拟者 | 允许其他用户模拟该帐户。 当您需要用户代表其他用户时非常有用。 请参 [阅模拟用户](#impersonating-another-user)。 |
| 首选项 | 设置 [用户组或用户的首选项](#setting-user-and-group-preferences)。 例如，语言首选项。 |

### Filtering Users and Groups {#filtering-users-and-groups}

您可以通过输入筛选表达式来筛选列表，该过滤表达式会隐藏所有与该不匹配的用户和用户组。 您还可以使用“隐藏用户”和“隐藏 [用户组”按钮来隐藏用户](#hiding-users-and-groups) 和用户组。

要筛选用户或用户组，请执行以下操作：

1. 在左树列表中，在提供的空间中键入筛选表达式。 例如，输入 **admin** 会显示包含此字符串的所有用户和用户组。
1. 单击放大镜以过滤列表。

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. 如果要 **删除** 所有过滤器，请单击x。

### Hiding Users and Groups {#hiding-users-and-groups}

隐藏用户或用户组是筛选系统中所有用户和用户组列表的另一种方法。 有两种切换机制。 单击“隐藏用户”可隐藏视图中的所有用户，单击“隐藏组”可隐藏视图中的所有用户组（您不能同时隐藏用户和用户组）。 要使用筛选列表筛选表达式，请参 [阅筛选用户和组](#filtering-users-and-groups)。

要隐藏用户和用户组，请执行以下操作：

1. 在“安 **全** ”控制台中，单 **击“隐藏用户** ”或“隐 **藏组”**。 此时将突出显示所选按钮。

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. 要使用户或用户组重新显示，请再次单击相应的按钮。

### Creating Users and Groups {#creating-users-and-groups}

要创建新用户或用户组，请执行以下操作：

1. 在“安全 **控制台** ”树列表中，单击“编 **辑** ”，然后单击“ **创建用户** ”或“ ****&#x200B;创建组”。

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. 根据您是创建用户还是用户组，输入所需的详细信息。

   * 如果选择 **创建用户** ，则输入登录ID、名字和姓氏、电子邮件地址和密码。 默认情况下，AEM会根据姓氏的第一个字母创建一个路径，但您可以选择其他路径。

   ![createuserdial](assets/createuserdialog.png)

   * 如果选择 **创建组**，则输入组ID和可选说明。

   ![creategroupdialog](assets/creategroupdialog.png)

1. 单击&#x200B;**创建**。您创建的用户或用户组显示在树列表中。

### Deleting Users and Groups {#deleting-users-and-groups}

要删除用户或用户组，请执行以下操作：

1. 在“安 **全** ”控制台中，选择要删除的用户或组。 如果要删除多个项目，请按住Shift键单击或按住Ctrl键单击以选择这些项目。
1. 单击 **编辑** ，然后选择删除。 AEM WCM会询问您是要删除用户还是删除用户组。
1. 单击 **确定** ，或单击取消以取消您的操作。

### 修改用户和组属性 {#modifying-user-and-group-properties}

要修改用户和组属性，请执行以下操作：

1. 在“安 **全** ”控制台中，多次单击要修改的用户或用户组名称。

1. 单击“ **属性** ”选项卡，进行所需的更改，然后单击“ **保存”**。

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>用户的路径显示在用户属性的底部。 无法修改。

### 更改用户密码 {#changing-a-user-password}

请按照以下过程修改用户的口令。

>[!NOTE]
>
>无法使用安全控制台更改管理员密码。 要更改管理员帐户的口令，请使用Granite Operations [提供的](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) “用户”控制台。
>
>如果您在JEE上使用AEM Forms，请不要使用下面的说明更改密码，而是使用JEE管理控制台(/adminui)中的AEM Forms更改密码。

1. 在“安 **全** ”控制台中，多次单击要更改密码的用户名。
1. 单击“ **属性** ”选项卡（如果尚未激活）。
1. 单击“ **设置密码**”。 “Set Password（设置密码）”窗口将打开，您可以在其中更改密码。

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. 输入新密码两次；由于它们未以明文显示，因此这是为了确认——如果它们不匹配，系统会显示错误。
1. 单击 **“设置** ”以激活帐户的新密码。

### 将用户或用户组添加到用户组 {#adding-users-or-groups-to-a-group}

AEM优惠了三种将用户或用户组添加到现有用户组的不同方法：

* 在用户组中时，可以添加成员（用户或用户组）。
* 在成员中时，可以向组添加成员。
* 使用权限时，可以向用户组添加成员。

### 用户组——将用户或用户组添加到用户组 {#groups-adding-users-or-groups-to-a-group}

“ **组** ”选项卡显示当前帐户所属的组。 您可以使用它将选定帐户添加到组：

1. 多次-单击要分配给组的帐户（用户或组）的名称。
1. Click the **Groups** tab. 您会看到帐户已属于的列表组。
1. 在树列表中，单击要添加到帐户的组的名称，并将其拖至“组” **窗格** 。 （如果要添加多个用户，请按住Shift键并单击或按住Ctrl键并单击这些名称并拖动它们。）

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. 单击 **保存** ，以保存更改。

### 成员——将用户或用户组添加到用户组 {#members-adding-users-or-groups-to-a-group}

“成 **员** ”选项卡仅适用于组，并显示属于当前组的用户和组。 您可以使用它向组添加帐户：

1. 多次-单击要添加成员的组的名称。
1. Click the **Members** tab. 您会看到已属于此组的成员列表。
1. 在树列表中，单击要添加到组的成员的名称，然后将其拖动到“成员 **”窗** 格。 （如果要添加多个用户，请按住Shift键并单击或按住Ctrl键并单击这些名称并拖动它们。）

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. 单击 **保存** ，以保存更改。

### 添加权限时添加用户或用户组 {#adding-users-or-groups-while-adding-permissions}

要将成员添加到特定路径中的组：

1. 多次-单击要添加用户的组或用户的名称。

1. Click the **Permissions** tab.

1. 导览至要添加权限的路径，然后单击“详细 **信息”**。 详细信息窗口的下半部分提供有关谁对该页面具有权限的信息。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 选中“成员 **** ”列中要具有该路径权限的成员的复选框。 清除要删除其权限的成员的复选框。 您对单元格进行更改时，单元格中会出现一个红色三角形。
1. 单击&#x200B;**确定**&#x200B;以保存您的更改。

### 从组中删除用户或用户组 {#removing-users-or-groups-from-groups}

AEM优惠了三种从组中删除用户或用户组的不同方法：

* 在组用户档案中时，可以删除成员（用户或组）。
* 在成员用户档案下，可以从组中删除成员。
* 使用“权限”时，您可以从组中删除成员。

### 组——从组中删除用户或用户组 {#groups-removing-users-or-groups-from-groups}

要从组中删除用户或组帐户，请执行以下操作：

1. 多次-单击要从组中删除的组或用户帐户的名称。
1. Click the **Groups** tab. 您会看到选定帐户所属的组。
1. 在“ **组** ”窗格中，单击要从组中删除的用户或组的名称，然后单击“删 **除”**。 (如果要删除多个帐户，请按住Shift键单击或按住Ctrl键单击这些名称，然后单击“ **删除**”。)

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. 单击 **保存** ，以保存更改。

### 成员——从组中删除用户或用户组 {#members-removing-users-or-groups-from-groups}

要从组中删除帐户，请执行以下操作：

1. 多次-单击要从中删除成员的组的名称。
1. Click the **Members** tab. 您会看到已属于此组的成员列表。
1. 在“成 **员** ”窗格中，单击要从组中删除的成员的名称，然后单击“删 **除”**。 (如果要删除多个用户，请按住Shift键并单击或按住Ctrl键并单击这些名称，然后单击“ **删除**”。)

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. 单击 **保存** ，以保存更改。

### 添加权限时删除用户或用户组 {#removing-users-or-groups-while-adding-permissions}

要从特定路径的组中删除成员：

1. 多次单击要从中删除用户的组或用户的名称。

1. Click the **Permissions** tab.

1. 导览至要删除权限的路径，然后单击“详细 **信息”**。 详细信息窗口的下半部分提供有关谁对该页面具有权限的信息。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 选中“成员 **** ”列中要具有该路径权限的成员的复选框。 清除要删除其权限的成员的复选框。 您对单元格进行更改时，单元格中会出现一个红色三角形。
1. 单击&#x200B;**确定**&#x200B;以保存您的更改。

### 用户同步 {#user-synchronization}

当部署是发布场 [时](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，用户和组需要在所有发布节点之间同步。

要了解用户同步以及如何启用它，请参阅 [用户同步](/help/sites-administering/sync.md)。

## 管理权限 {#managing-permissions}

>[!NOTE]
>
>Adobe引入了新的基于触屏UI的权限管理主视图。 有关如何使用它的更多详细信息，请参 [阅此页](/help/sites-administering/touch-ui-principal-view.md)。

本节介绍如何设置权限，包括复制权限。

### 设置权限 {#setting-permissions}

权限允许用户在特定路径上对资源执行某些操作。 它还包括创建或删除页面的功能。

要添加、修改或删除权限：

1. 在“安 **全** ”控制台中，多次单击要设置节点权限或搜索节点的用户或 [用户组的名称](#searching-for-nodes)。

1. Click the **Permissions** tab.

   ![cquser权限](assets/cquserpermissions.png)

1. 在树网格中，选中一个复选框以允许选定的用户或用户组执行操作，或清除一个复选框以拒绝选定的用户或用户组执行操作。 有关详细信息，请单击“ **详细信息**”。

1. When finished, click **Save**.

### 设置复制权限 {#setting-replication-privileges}

复制权限是发布内容的权利，可以为组和用户设置该权限。

>[!NOTE]
>
>* 对组应用的任何复制权限均适用于该组中的所有用户。
>* 用户的复制权限将取代组的复制权限。
>* 允许复制权限的优先级高于拒绝复制权限。 请参 [阅AEM中的](#permissions-in-aem) “权限”以了解更多信息。

>



要设置复制权限：

1. 从列表中选择用户或组，单击多次以打开，然后单击“权 **限”**。
1. 在网格中，导航到您希望用户具有复制权限或搜索节 [点的路径。](#searching-for-nodes)

1. 在选 **定路径** 的复制列中，选中一个复选框以添加该用户或组的复制权限，或清除该复选框以删除复制权限。 AEM会在您所做更改但尚未保存的任何地方显示一个红色三角形。

   ![cquserreplicate权限](assets/cquserreplicatepermissions.png)

1. 单击 **保存** ，以保存更改。

### 搜索节点 {#searching-for-nodes}

添加或删除权限时，您可以浏览或搜索节点。

路径搜索有两种不同类型：

* 路径搜索——如果搜索字符串开始为“/”，则搜索将搜索给定路径的直接子节点：

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

在搜索框中，您可以执行以下操作：

| 操作 | 它的用途 |
|--- |--- |
| 向右箭头键 | 在搜索结果中选择子节点 |
| 向下箭头键 | 开始搜索。 |
| 输入（返回）键 | 选择子节点并将其加载到树网格中 |

* 全文搜索——如果搜索字符串不与“/”开始，则对路径“/content”下的所有节点执行全文搜索。

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

要搜索路径或全文，请执行以下操作：

1. 在“安全”控制台中，选择用户或用户组，然后单击“权 **限** ”选项卡。

1. 在搜索框中，输入要搜索的词。

### 模拟用户 {#impersonating-users}

您可以指定一个或多个允许模拟当前用户的用户。 这意味着他们可以将其帐户设置切换为当前用户的帐户设置，并代表此用户行事。

使用此函数时要小心，因为它可能允许用户执行其自己的用户无法执行的操作。 模拟用户时，系统会通知用户他们没有以自己的身份登录。

您可能希望使用此功能的情况有多种，包括：

* 如果您不在办公室，您可以在您不在的时候让其他人假冒您。 通过使用此功能，您可以确保某人具有您的访问权限，而您无需修改用户用户档案或提供您的密码。
* 您可以将其用于调试目的。 例如，查看网站如何查找具有受限访问权限的用户。 此外，如果用户抱怨技术问题，您可以模拟该用户来诊断和修复问题。

要模拟现有用户，请执行以下操作：

1. 在树列表中，选择要将其他用户模拟给其他用户的人员的姓名。 多次单击以打开。
1. Click the **Impersonators** tab.
1. 单击要能够模拟选定用户的用户。 将用户（将模拟）从列表拖动到“模拟”窗格。 该名称将显示在列表中。

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. 单击&#x200B;**保存**。

### 设置用户和用户组首选项 {#setting-user-and-group-preferences}

要设置用户和用户组首选项，包括语言、窗口管理和工具栏首选项：

1. 在左侧树中选择要更改其首选项的用户或组。 要选择多个用户或用户组，请按住Ctrl或Shift键并单击您的选择。
1. Click the **Preferences** tab.

   ![cqsecuritypreferences](assets/cqsecuritypreferences.png)

1. 根据需要对组或用户首选项进行更改，完成后单 **击** “保存”。

### 将用户或管理员设置为有权管理其他用户 {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

要设置用户或管理员具有删除／激活／取消激活其他用户的权限，请执行以下操作：

1. 将要授予管理其他用户权限的用户添加到管理员组并保存所做的更改。

   ![cqsecurityaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. 在用户的“权 **限** ”选项卡中，导航到“/”，在“复制”列中，选中允许复制的复选框（位于“/”），然后单击 **保存**。

   ![cqsecurityreplicate权限](assets/cqsecurityreplicatepermissions.png)

   选定用户现在可以取消激活、激活、删除和创建用户。

### 扩展项目级别的权限 {#extending-privileges-on-a-project-level}

如果您计划实施特定于应用程序的权限，以下信息将说明实施自定义权限时需要了解的内容以及如何在整个CQ中实施该权限：

层次结构修改权限由jcr-priviles的组合覆盖。 复制权限被命名 **为crx:replicate** ，该权限与jcr存储库的其他权限一起存储／评估。 但是，它没有在jcr级别上执行。

自定义权限的定义和注册正式属于Jackrabbit [API](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/api/security/authorization/PrivilegeManager.html) （从2.4版开始）的一部分(另 [请参阅JCR-2887](https://issues.apache.org/jira/browse/JCR-2887))。 JCR访问控制管理涵盖进一步的使用，如 [JSR 283](https://jcp.org/en/jsr/detail?id=283) （第16节）。 此外，Jackrabbit API定义了几个扩展。

权限注册机制反映在“存储库配置” **下的UI中**。

新（自定义）权限的注册本身受必须在存储库级别授予的内置权限保护(在JCR中：在ac mgt api中将“null”作为“absPath”参数传递，有关详细信息，请参阅jsr 333)。 默认情况 **下** ，管理员和所有管理员成员都具有该权限。

>[!NOTE]
>
>虽然实现负责验证和评估自定义权限，但除非它们是一聚合内置权限，否则将无法实施这些权限。
