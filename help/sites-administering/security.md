---
title: 用户管理和安全性
description: 了解AEM中的用户管理和安全性。
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: Security
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '5401'
ht-degree: 1%

---

# 用户管理和安全性{#user-administration-and-security}

本章介绍如何配置和维护用户授权，还描述了在AEM中如何进行身份验证和授权的理论基础。

## AEM中的用户和组 {#users-and-groups-in-aem}

本节将更详细地介绍各种实体和相关概念，以帮助您配置易于维护的用户管理概念。

### 用户 {#users}

用户使用其帐户登录AEM。 每个用户帐户都是唯一的，包含基本帐户详细信息以及分配的权限。

用户通常是组的成员，这简化了权限和/或权限的分配。

### 组 {#groups}

组是用户集合或其他组，或同时是两者。 这些集合均称为组的成员。

它们的主要目的是通过减少要更新的实体数量来简化维护过程，因为对组所做的更改将应用于组的所有成员。 群组通常反映：

* 应用程序中的角色；例如允许浏览内容的人或允许贡献内容的人。
* 您自己的组织；当来自不同部门的参与者被限制到内容树中的不同分支时，您可能希望扩展角色以区分这些参与者。

因此，群组倾向于保持稳定，而用户更频繁地来来往。

有了规划和干净的结构，组的使用可以反映您的结构，为您提供清晰的概述和有效率的更新机制。

### 内置用户和组 {#built-in-users-and-groups}

AEM WCM安装了多个用户和组。 在安装后首次访问Security Console时，将会看到这些集合。

下表列出了每个项目以及：

* 简短描述
* 关于必要更改的任何建议

*更改所有默认密码* （如果在某些情况下不删除帐户本身）。

<table>
 <tbody>
  <tr>
   <td>用户 ID</td>
   <td>类型</td>
   <td>描述</td>
   <td>推荐</td>
  </tr>
  <tr>
   <td><p>管理员</p> <p>默认密码：admin</p> </td>
   <td>用户</td>
   <td><p>具有完全访问权限的系统管理帐户。</p> <p>此帐户用于AEM WCM和CRX之间的连接。</p> <p>如果意外删除此帐户，则会在重新启动存储库时重新创建此帐户（在默认设置中）。</p> <p>管理帐户是AEM平台的一项要求。 因此，无法删除此帐户。</p> </td>
   <td><p>Adobe建议您更改此用户帐户的默认密码。</p> <p>最好在安装时进行，不过之后可以完成。</p> <p>注意：请勿将此帐户与CQ Servlet引擎的管理员帐户混淆。</p> </td>
  </tr>
  <tr>
   <td><p>匿名</p> <p> </p> </td>
   <td>用户</td>
   <td><p>拥有对实例进行未经身份验证访问的默认权限。 默认情况下，此帐户具有最低访问权限。</p> <p>如果意外删除此帐户，则会在启动时重新创建此帐户。 无法永久删除它，但可以禁用它。</p> </td>
   <td>避免删除或禁用此帐户，因为它会对创作实例的运行产生负面影响。 如果安全要求要求您删除它，请确保首先正确测试它对您的系统的影响。</td>
  </tr>
  <tr>
   <td><p>作者</p> <p>默认密码：作者</p> </td>
   <td>用户</td>
   <td><p>允许写入/content的作者帐户。 包含投稿人和浏览者权限。</p> <p>可用作网站管理员，因为它有权访问整个/content树。</p> <p>此帐户不是内置用户，而是其他Geometrixx演示用户</p> </td>
   <td><p>Adobe建议彻底删除该帐户，或者更改默认密码。</p> <p>最好在安装时进行，不过之后可以完成。</p> </td>
  </tr>
  <tr>
   <td>管理员</td>
   <td>组</td>
   <td><p>为其所有成员授予管理员权限的组。 仅允许管理员编辑此组。</p> <p>具有完全访问权限。</p> </td>
   <td>即使您在节点上设置了“deny-everyone”，管理员仍可以访问该节点</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>组</td>
   <td><p>负责内容编辑的组。 需要读取、修改、创建和删除权限。</p> </td>
   <td>如果您添加了读取、修改、创建和删除权限，则可以创建自己的具有项目特定访问权限的内容作者组。</td>
  </tr>
  <tr>
   <td>参与者</td>
   <td>组</td>
   <td><p>允许用户写入内容的基本权限（如中所示，仅限功能）。</p> <p>不向/content树分配任何权限。 必须为单个组或用户分配。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam-users</td>
   <td>组</td>
   <td>适用于典型AEM Assets用户的现成参考组。 此组成员具有相应的权限，可以启用资产和收藏集的上传/共享。</td>
   <td> </td>
  </tr>
  <tr>
   <td>每个人</td>
   <td>组</td>
   <td><p>AEM中的每个用户都是组的成员，即使您可能看不到所有工具中的组或成员资格关系。</p> <p>可以将此组视为默认权限，因为它可用于为每个人（甚至是将来的创建用户）应用权限。</p> </td>
   <td><p>请勿修改或删除此组。</p> <p>修改此帐户可能会带来其他安全隐患。</p> </td>
  </tr>
  <tr>
   <td>tag-administrator</td>
   <td>组</td>
   <td>允许编辑标记的组。</td>
   <td> </td>
  </tr>
  <tr>
   <td>user-administrator</td>
   <td>组</td>
   <td>授权用户管理，即创建用户和组的权利。</td>
   <td> </td>
  </tr>
  <tr>
   <td>workflow编辑器</td>
   <td>组</td>
   <td>允许创建和修改工作流模型的组。</td>
   <td> </td>
  </tr>
  <tr>
   <td>workflow-users</td>
   <td>组</td>
   <td><p>参与工作流的用户必须是组workflow-users的成员。 授予用户/etc/workflow/instances的完全访问权限，以便他们可以更新工作流实例。</p> <p>该组包含在标准安装中，但您必须手动将用户添加到该组。</p> </td>
  </tr>
 </tbody>
</table>

## AEM中的权限 {#permissions-in-aem}

AEM使用ACL来确定用户或组可以执行的操作以及在何处可以执行这些操作。

### 权限和ACL {#permissions-and-acls}

权限定义谁可以对资源执行哪些操作。 权限是以下各项的结果 [访问控制](#access-control-lists-and-how-they-are-evaluated) 评估。

您可以通过选中或清除单个AEM的复选框，更改授予/拒绝给特定用户的权限 [操作](security.md#actions). 复选标记表示允许执行某个操作。 无复选标记表示操作被拒绝。

选中标记在网格中的位置还指示用户在AEM中的哪些位置（即哪些路径）具有哪些权限。

### 操作 {#actions}

可以对页面（资源）执行操作。 对于层级中的每个页面，您可以指定允许用户在该页面上执行的操作。 [权限](#permissions-and-acls) 允许您允许或拒绝操作。

<table>
 <tbody>
  <tr>
   <td><strong>操作 </strong></td>
   <td><strong>描述 </strong></td>
  </tr>
  <tr>
   <td>读取</td>
   <td>允许用户读取该页面及其任何子页面。</td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p>用户可以：</p>
    <ul>
     <li>修改页面和任何子页面上的现有内容。</li>
     <li>在页面或任何子页面上创建段落。</li>
    </ul> <p>在JCR级别，用户可以通过编辑资源的属性、锁定、版本控制和nt-modifications来编辑资源，并且他们对定义jcr：content子节点的节点具有完全写入权限。 例如cq：Page、nt：file、cq：Asset。</p> </td>
  </tr>
  <tr>
   <td>创建</td>
   <td><p>用户可以：</p>
    <ul>
     <li>创建页面或子页面。</li>
    </ul> <p>如果 <strong>修改</strong> 被拒绝，jcr：content下的子树被排除，因为创建jcr：content及其子节点被视为页面修改。 此规则仅适用于定义jcr：content子节点的节点。</p> </td>
  </tr>
  <tr>
   <td>删除</td>
   <td><p>用户可以：</p>
    <ul>
     <li>从页面或任何子页面中删除现有段落。</li>
     <li>删除页面或子页面。</li>
    </ul> <p>如果 <strong>修改</strong> 被拒绝jcr：content下的任何子树都因删除jcr：content而被排除，其子节点被视为页面修改。 此规则仅适用于定义jcr：content子节点的节点。</p> </td>
  </tr>
  <tr>
   <td>读取 ACL</td>
   <td>用户可以读取页面或子页面的访问控制列表。</td>
  </tr>
  <tr>
   <td>编辑 ACL</td>
   <td>用户可以修改该页面或任何子页面的访问控制列表。</td>
  </tr>
  <tr>
   <td>复制</td>
   <td>用户可以将内容复制到其他环境（例如，发布环境）。 该权限还应用于任何子页面。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM在中自动为角色分配（所有者、编辑者、查看者）生成用户组 [收藏集](/help/assets/manage-collections.md). 但是，手动为此类组添加ACL可能会在AEM中引入安全漏洞。 Adobe建议您避免手动添加ACL。

### 访问控制列表及其评估方式 {#access-control-lists-and-how-they-are-evaluated}

AEM WCM使用访问控制列表(ACL)来组织应用于各种页面的权限。

访问控制列表由各个权限组成，用于确定应用这些权限的顺序。 根据所考虑页面的层次结构形成列表。 然后自下而上扫描此列表，直到找到应用于页面的第一个相应权限为止。

>[!NOTE]
>
>示例中包含ACL。 建议您查看并确定适合您的应用程序的内容。 要查看包含的ACL，请转到 **CRXDE** 并选择 **访问控制** 选项卡中的以下节点：
>
>* `/etc/cloudservices`
>* `/home/users/we-retail`
>
>您的自定义应用程序可以设置其他关系的访问权限，例如：
>
>* `*/social/relationships/friend/*`
>* 或 `*/social/relationships/pending-following/*`.
>
>在创建特定于社区的ACL时，加入这些社区的成员可能会被授予附加权限。 例如，当用户在以下位置加入社区时： `/content/we-retail/us/en/community`

### 权限状态 {#permission-states}

>[!NOTE]
>
>对于CQ 5.3用户：
>
>与以前的CQ版本相比， **创建** 和 **删除** 如果用户只能修改页面，则不再授予权限。 相反，授予 **修改** 仅当您希望用户能够在现有页面上创建、修改或删除组件时才执行操作。
>
>出于向后兼容的原因，操作测试不对定义节点的操作执行特殊处理 **jcr：content** 考虑在内。

| **操作** | **描述** |
|---|---|
| 允许（复选标记） | AEM WCM允许用户在此页面或任何子页面上执行该操作。 |
| 拒绝（无复选标记） | AEM WCM不允许用户在此页面或任何子页面上执行操作。 |

这些权限也将应用于任何子页面。

如果权限不是从父节点继承，而是至少具有一个本地条目，则以下符号将附加到复选框。 本地条目是在CRX 2.2接口中创建的条目（当前只能在CRX中创建通配符ACL。）

对于给定路径下的操作：

<table>
 <tbody>
  <tr>
   <td>* （星号）</td>
   <td>至少有一个本地条目（有效或无效）。 这些通配符ACL在CRX中定义。</td>
  </tr>
  <tr>
   <td>！ （感叹号）</td>
   <td>至少有一个条目当前无效。</td>
  </tr>
 </tbody>
</table>

当您将鼠标悬停在星号或感叹号上时，工具提示会提供有关已声明条目的更多详细信息。 工具提示分为两部分：

<table>
 <tbody>
  <tr>
   <td>上半部分</td>
   <td><p>列出有效条目。</p> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td>列出可能在树的其他位置生效的非有效条目（由带有限制条目范围的对应ACE的特殊属性所指示）。 或者，它是一个条目，其效果被在给定路径或祖先节点上定义的另一个条目所撤销。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>如果没有为页面定义权限，则会拒绝所有操作。

以下是有关管理访问控制列表的建议：

* 不要将权限直接分配给用户。 仅将其分配给组。

  这样做可简化维护工作，因为组的数量比用户数量少得多，而且波动性也小。

* 如果您希望组/用户只能修改页面，请不要授予他们创建或拒绝权限。 仅授予他们修改和读取权限。
* 请谨慎使用“拒绝”。 尽可能只使用“允许”。

  如果权限的应用顺序与预期顺序不同，则使用deny可能会导致意外效果。 如果用户是多个组的成员，则来自一个组的Deny语句可能会取消来自另一个组的Allow语句，反之亦然。 发生此类事件时，很难保持概览，并且容易导致不可预见的结果，而允许分配不会导致此类冲突。

  Adobe建议您使用“允许”而不是“拒绝”，请参见 [最佳实践](#best-practices).

在修改任一权限之前，请确保您了解它们的工作方式和相互关系。 请参阅说明AEM WCM方式的CRX文档 [评估访问权限](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated)、以及有关设置访问控制列表的示例。

### 权限 {#permissions}

通过权限，用户和组可以访问AEM页面上的AEM功能。

您可以通过展开/折叠节点来按路径浏览权限，并且一直跟踪到根节点的权限继承。

通过选中或清除相应的复选框，您可以允许或拒绝权限。

![cqsecuritypermissionstab](assets/cqsecuritypermissionstab.png)

### 查看详细的权限信息 {#viewing-detailed-permission-information}

与网格视图一起，AEM提供给定路径下选定用户/组的权限的详细视图。 详细信息视图提供其他信息。

除了查看信息之外，您还可以包括或排除组中的当前用户或组。 请参阅 [添加权限时添加用户或组](#adding-users-or-groups-while-adding-permissions). 此处所做的更改会立即反映在详细视图的上部。

要访问“详细信息”视图，请在 **权限** 选项卡，单击 **详细信息** 用于任何选择的组/用户和路径。

![权限详细信息](assets/permissiondetails.png)

详细信息分为两个部分：

<table>
 <tbody>
  <tr>
   <td>上半部分</td>
   <td><p>重复您在树网格中看到的信息。 对于每个操作，都有一个图标显示是允许还是拒绝该操作：</p>
    <ul>
     <li>无图标=无声明条目</li>
     <li>（勾号）=声明的操作（允许）</li>
     <li>(-) =声明的操作（拒绝）</li>
    </ul> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td><p>显示执行以下操作的用户和组的网格：</p>
    <ul>
     <li>为给定路径声明一个条目并</li>
     <li>给定的可授权还是组</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 模拟其他用户 {#impersonating-another-user}

使用 [模拟功能](/help/sites-authoring/user-properties.md#user-settings)，用户可代表其他用户工作。

也就是说，用户帐户可以指定可以与其帐户一起操作的其他帐户。 例如，如果允许用户B模拟用户A，则用户B可以使用用户A的完整帐户详细信息执行操作。

此功能允许模拟者帐户完成任务，就像他们使用自己所模拟的帐户一样。 例如，在缺勤期间或短期共用过度负荷。

>[!NOTE]
>
>要模拟非管理员用户的工作情况，模拟者（在上述情况下为用户B）需要在以下位置具有“读取”权限： `/home/users` 路径。
>
>请参阅 [AEM中的权限](/help/sites-administering/security.md#permissions-in-aem).

>[!CAUTION]
>
>如果一个帐户模拟另一个帐户，则很难查看。 模拟开始和结束时在审核日志中创建一个条目，但其他日志文件（如访问日志）不包含事件上已发生模拟的信息。 因此，如果用户B模拟用户A，则所有事件看起来就像用户A执行了它们。

>[!CAUTION]
>
>模拟用户身份时可以执行页面锁定。但是，以这种方式锁定的页面只能作为被模拟的用户或具有管理员权限的用户解锁。
>
>无法通过模拟锁定页面的用户的身份来解锁页面。

### 最佳实践 {#best-practices}

下面描述了使用权限和特权时的最佳实践：

| 规则 | 原因 |
|--- |--- |
| *使用组* | 避免逐个用户分配访问权限。 提出此建议的原因有多种：<ul><li>用户数多于组数，因此组简化了结构。</li><li>组可帮助提供所有帐户的概述。</li> <li>对组进行继承更简单。</li><li>用户来来去去。 组是长期的。</li></ul> |
| *积极的* | 始终使用Allow语句指定组的权限（如果可能）。 避免使用Deny语句。 按顺序评估组，并且按用户定义顺序可能有所不同。 换言之：您可能无法控制语句的实施和评估顺序。 如果您只使用“允许”语句，则顺序无关紧要。 |
| *保持简单* | 在配置新安装时花些时间和思考是值得的。 应用清晰的结构可简化持续的维护和管理，确保您当前的同事和未来的继任者能够轻松了解实施的内容。 |
| *测试* | 使用测试安装进行练习并确保您了解各种用户和组之间的关系。 |
| *默认用户/组* | 始终在安装后立即更新默认用户和组，以防止出现任何安全问题。 |

## 管理用户和组 {#managing-users-and-groups}

用户包括使用系统的人员和向系统发出请求的外部系统。

组是一组用户。

两者都可以使用安全控制台中的用户管理功能进行配置。

### 使用安全控制台访问用户管理 {#accessing-user-administration-with-the-security-console}

您可以使用“安全”控制台访问所有用户、组和关联的权限。 在此窗口中执行本节中介绍的所有过程。

要访问AEM WCM安全性，请执行以下操作之一：

* 在AEM的欢迎屏幕或各种位置中，单击安全图标：

![AEM WCM安全性选项卡](do-not-localize/wcmtoolbar.png)

* 直接导航到 `https://<server>:<port>/useradmin`. 确保您以管理员身份登录AEM。

将显示以下窗口：

![cqsecuritypage](assets/cqsecuritypage.png)

左边的树状结构列出了系统中当前的所有用户和组。 您可以选择要显示的列，对列内容进行排序，甚至通过将列标题拖到新位置来更改列的显示顺序。

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

通过选项卡可访问各种配置：

<!-- ??? in table below. -->

| 制表符 | 描述 |
|--- |--- |
| 筛选器框 | 用于筛选列出的用户、组或两者的机制。 请参阅 [筛选用户和组](#filtering-users-and-groups). |
| 隐藏用户 | 一种切换开关，可隐藏列出的所有用户，仅保留组。 请参阅 [隐藏用户和组](#hiding-users-and-groups). |
| 隐藏组 | 一种切换开关，可隐藏列出的所有组，仅留下用户。 请参阅 [隐藏用户和组](#hiding-users-and-groups). |
| 编辑 | 一个菜单，可让您创建和删除以及激活和停用用户或组。 请参阅 [创建用户和组](#creating-users-and-groups) 和 [删除用户和组](#deleting-users-and-groups). |
| 属性 | 列出有关用户或组的信息，其中包括电子邮件信息、说明和名称信息。 还允许您更改用户的密码。 请参阅 [创建用户和组](#creating-users-and-groups)， [修改用户和组属性](#modifying-user-and-group-properties) 和 [更改用户密码](#changing-a-user-password). |
| 组 | 列出所选用户或组所属的所有组。 您可以将选定的一个或多个用户分配给其他组，或从组中将其删除。 请参阅 [组](#adding-users-or-groups-to-a-group). |
| 成员 | 仅适用于组。 列出特定组的成员。 请参阅 [成员](#members-adding-users-or-groups-to-a-group). |
| 权限 | 您可以将权限分配给用户或组。 允许您控制以下内容：<ul><li>与特定页面/节点相关的权限。 请参阅 [设置权限](#setting-permissions). </li><li>与创建和删除页面以及层次结构修改相关的权限。???允许您 [分配权限](#settingprivileges)，例如层级修改，您可以创建和删除页面，</li><li>与相关的权限 [复制权限](#setting-replication-privileges) （通常从创作到发布）时，不会将反向链接计算两次。</li></ul> |
| 模拟者 | 允许其他用户模拟帐户。 当您需要用户代表其他用户进行操作时非常有用。 请参阅 [模拟用户](#impersonating-another-user). |
| 首选项 | 集 [组或用户的首选项](#setting-user-and-group-preferences). 例如，语言首选项。 |

### 筛选用户和组 {#filtering-users-and-groups}

您可以通过输入过滤表达式来过滤列表，该表达式将隐藏所有与表达式不匹配的用户和组。 您还可以使用隐藏用户和组 [隐藏用户和隐藏组](#hiding-users-and-groups) 按钮。

要筛选用户或组，请执行以下操作：

1. 在左侧树列表中，在提供的空白处键入您的过滤器表达式。 例如，输入 **管理员** 显示包含此字符串的所有用户和组。
1. 单击放大镜以过滤列表。

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. 单击 **x** ，以删除所有过滤器。

### 隐藏用户和组 {#hiding-users-and-groups}

隐藏用户或组是筛选系统中所有用户和组列表的另一种方法。 有两种切换机制。 单击“隐藏用户”可隐藏视图中的所有用户，单击“隐藏组”可隐藏视图中的所有组（不能同时隐藏用户和组）。 要通过使用过滤器表达式过滤列表，请参阅 [筛选用户和组](#filtering-users-and-groups).

要隐藏用户和组：

1. 在 **安全性** 控制台，单击 **隐藏用户** 或 **隐藏组**. 选定的按钮将突出显示。

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. 要重新显示用户或组，请再次单击相应的按钮。

### 创建用户和组 {#creating-users-and-groups}

要创建用户或组，请执行以下操作：

1. 在 **安全性** 控制台树列表，单击 **编辑** 然后 **创建用户** 或 **创建组**.

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. 根据您是创建用户还是创建组，输入所需的详细信息。

   * 如果您选择 **创建用户，** 输入登录ID、名字和姓氏、电子邮件地址和密码。 默认情况下，AEM会根据姓氏的第一个字母创建路径，但您可以选择其他路径。

   ![createuserdialog](assets/createuserdialog.png)

   * 如果您选择 **创建组**，您可以输入组ID和可选描述。

   ![creategroupdialog](assets/creategroupdialog.png)

1. 单击&#x200B;**创建**。您创建的用户或组将显示在树列表中。

### 删除用户和组 {#deleting-users-and-groups}

要删除用户或组，请执行以下操作：

1. 在 **安全性** 控制台中，选择要删除的用户或组。 如果要删除多个项目，请按住Shift或Ctrl并单击以选择它们。
1. 单击 **编辑，** 然后选择“删除”。 AEM WCM会询问您是否要删除用户或组。
1. 单击 **确定** 以确认或取消。

### 修改用户和组属性 {#modifying-user-and-group-properties}

要修改用户和组属性，请执行以下操作：

1. 在 **安全性** 控制台，双击要修改的用户名或组名。

1. 单击 **属性** 选项卡，进行所需的更改，然后单击 **保存**.

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>用户的路径显示在用户属性的底部。 无法修改它。

### 更改用户密码 {#changing-a-user-password}

使用以下过程可修改用户的密码。

>[!NOTE]
>
>不能使用“安全”控制台更改管理员密码。 要更改管理员帐户的密码，请使用 [用户控制台](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) Granite Operations提供的。
>
>如果您在JEE上使用AEM Forms，请不要使用以下说明来更改密码，而应使用JEEAdmin Console上的AEM Forms (/adminui)来更改密码。

1. 在 **安全性** 控制台中，双击要更改密码的用户名。
1. 单击 **属性** 选项卡（如果尚未处于活动状态）。
1. 单击 **设置密码**. 将会打开“设置密码”窗口，您可以在其中更改密码。

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. 输入新密码两次；由于新密码未以明文显示，此操作用于确认 — 如果新密码不匹配，系统将显示错误。
1. 单击 **设置** 以激活帐户的新密码。

### 将用户或组添加到组 {#adding-users-or-groups-to-a-group}

AEM提供了三种将用户或组添加到现有组的方法：

* 在组中时，可以添加成员（用户或组）。
* 在成员中时，可以将成员添加到组。
* 处理权限时，可以将成员添加到组。

### 组 — 将用户或组添加到组 {#groups-adding-users-or-groups-to-a-group}

此 **组** 选项卡显示当前帐户所属的组。 您可以使用它来将所选帐户添加到组：

1. 双击要分配给组的帐户（用户或组）的名称。
1. 单击 **组** 选项卡。 您会看到该帐户已属于的组的列表。
1. 在树列表中，单击要添加到帐户的组的名称，然后将其拖到 **组** 窗格。 （如果要添加多个用户，请按住Shift或Ctrl并单击这些名称并拖动它们。）

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. 单击 **保存** 以保存更改。

### 成员 — 将用户或组添加到组 {#members-adding-users-or-groups-to-a-group}

此 **成员** 选项卡仅适用于组，并显示哪些用户和组属于当前组。 您可以使用它向组添加帐户：

1. 双击要向其添加成员的组的名称。
1. 单击 **成员** 选项卡。 您会看到已属于此组的成员列表。
1. 在树列表中，单击要添加到组中的成员的名称，然后将其拖到 **成员** 窗格。 （如果要添加多个用户，请按住Shift或Ctrl并单击这些名称并拖动它们。）

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. 单击 **保存** 以保存更改。

### 添加权限时添加用户或组 {#adding-users-or-groups-while-adding-permissions}

要按特定路径将成员添加到所在的组，请执行以下操作：

1. 双击要向其添加用户的组或用户的名称。

1. 单击 **权限** 选项卡。

1. 导航到要将权限添加到的路径，然后单击 **详细信息**. 详细信息窗口的下半部分提供了有关谁拥有该页面的权限的信息。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 选中 **会员** 列，用于您希望对该路径拥有权限的成员。 清除要为其删除权限的成员对应的复选框。 您更改的单元格中将显示一个红色三角形。
1. 单击 **确定** 以保存更改。

### 从组中删除用户或组 {#removing-users-or-groups-from-groups}

AEM提供了三种从组中删除用户或组的不同方式：

* 在组配置文件中，您可以删除成员（用户或组）。
* 在成员配置文件中，您可以从组中删除成员。
* 处理权限时，可以从组中删除成员。

### 组 — 从组中删除用户或组 {#groups-removing-users-or-groups-from-groups}

要从组中删除用户或组帐户，请执行以下操作：

1. 双击要从组中删除的组或用户帐户的名称。
1. 单击 **组** 选项卡。 您可以看到所选帐户属于哪些组。
1. 在 **组** 窗格，单击要从组中移除的用户或组的名称，然后单击 **移除**. (如果要删除多个帐户，请按住Shift或Ctrl并单击这些名称，然后单击 **移除**.)

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. 单击 **保存** 以保存更改。

### 成员 — 从组中移除用户或组 {#members-removing-users-or-groups-from-groups}

要从组中删除帐户，请执行以下操作：

1. 双击要从中删除成员的组的名称。
1. 单击 **成员** 选项卡。 您会看到已属于此组的成员列表。
1. 在 **成员** 窗格，单击要从组中移除的成员名称，然后单击 **移除**. (如果要删除多个用户，请按住Shift或Ctrl并单击这些名称，然后单击 **移除**.)

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. 单击 **保存** 以保存更改。

### 添加权限时删除用户或组 {#removing-users-or-groups-while-adding-permissions}

要从特定路径下的组中删除成员，请执行以下操作：

1. 双击要从中删除用户的组或用户的名称。

1. 单击 **权限** 选项卡。

1. 导航到要删除权限的路径，然后单击 **详细信息**. 详细信息窗口的下半部分提供了有关谁拥有该页面的权限的信息。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 选中 **会员** 列，用于您希望对该路径拥有权限的成员。 清除要为其删除权限的成员对应的复选框。 您更改的单元格中将显示一个红色三角形。
1. 单击 **确定** 以保存更改。

### 用户同步 {#user-synchronization}

当部署是 [发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，用户和组必须在所有发布节点之间同步。

要了解用户同步以及如何启用用户同步，请参阅 [用户同步](/help/sites-administering/sync.md).

## 管理权限 {#managing-permissions}

>[!NOTE]
>
>Adobe为权限管理引入了一个新的基于触屏UI的主体视图。 有关如何使用的更多详细信息，请参阅 [此页面](/help/sites-administering/touch-ui-principal-view.md).

本节介绍如何设置权限，包括复制权限。

### 设置权限 {#setting-permissions}

权限允许用户对特定路径上的资源执行特定操作。 它还包含创建或删除页面的功能。

要添加、修改或删除权限：

1. 在 **安全性** 控制台中，双击要为其设置权限的用户或组的名称，或者 [搜索节点](#searching-for-nodes).

1. 单击 **权限** 选项卡。

   ![cquserpermissions](assets/cquserpermissions.png)

1. 在树网格中，选中复选框以允许选定的用户或组执行操作，或清除复选框以拒绝选定的用户或组执行操作。 有关详细信息，请单击 **详细信息**.

1. 完成后，单击 **保存**.

### 设置复制权限 {#setting-replication-privileges}

复制权限是发布内容的权限，可为组和用户设置此权限。

>[!NOTE]
>
>* 应用到组的任何复制权限都适用于该组中的所有用户。
>* 用户的复制权限将取代组的复制权限。
>* 允许复制权限的优先级高于拒绝复制权限。 请参阅 [AEM中的权限](#permissions-in-aem) 以了解更多信息。
>

要设置复制权限，请执行以下操作：

1. 从列表中选择用户或组，双击以打开，然后单击 **权限**.
1. 在网格中，导航到您希望用户拥有复制权限的路径，或者 [搜索节点。](#searching-for-nodes)

1. 在 **复制** 列中，选中复选框以添加该用户或组的复制权限，或清除复选框以删除复制权限。 AEM会在您所做更改但尚未保存的任何位置显示红色三角形。

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. 单击 **保存** 以保存更改。

### 搜索节点 {#searching-for-nodes}

添加或删除权限时，您可以浏览或搜索节点。

有两种不同类型的路径搜索：

* 路径搜索 — 如果搜索字符串以“/”开头，则它会搜索给定路径的直接子节点：

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

在搜索框中，可以执行以下操作：

| 操作 | 作用 |
|--- |--- |
| 向右箭头键 | 在搜索结果中选择子节点 |
| 向下箭头键 | 再次开始搜索。 |
| 输入（返回）键 | 选择子节点并将其加载到树网格中 |

* 全文搜索 — 如果搜索字符串不以“/”开头，则会在路径“/content”下的所有节点上执行全文搜索。

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

要对路径或全文执行搜索，请执行以下操作：

1. 在“安全”控制台中，选择一个用户或组，然后单击 **权限** 选项卡。

1. 在搜索框中，输入要搜索的词语。

### 模拟用户 {#impersonating-users}

您可以指定一个或多个允许模拟当前用户的用户。 这种能力意味着他们可以将其帐户设置切换到当前用户的并代表此用户执行操作。

使用此功能时请务必谨慎，因为它可能会允许用户执行其自己的用户无法执行的操作。 模拟用户时，系统会通知用户他们未以自己的身份登录。

在多种情况下，您可能希望使用此功能，包括：

* 如果你不在办公室，你可以让别人在你不在的时候模拟你。 通过使用此功能，您可以确保某人拥有您的访问权限，并且您无需修改用户配置文件或提供密码。
* 您可以将其用于调试目的。 例如，查看网站如何查找具有受限访问权限的用户。 此外，如果用户抱怨技术问题，则可以模拟该用户来诊断和修复问题。

模拟现有用户：

1. 在树列表中，选择要指定其他用户进行模拟的人员姓名。 双击以打开。
1. 单击 **模拟者** 选项卡。
1. 单击您希望能够模拟所选用户的用户。 将用户（模拟者）从列表拖到模拟窗格。 该名称将显示在列表中。

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. 单击&#x200B;**保存**。

### 设置用户和组首选项 {#setting-user-and-group-preferences}

要设置用户和组首选项，包括语言、窗口管理和工具栏首选项，请执行以下操作：

1. 在左侧树中选择要更改其首选项的用户或组。 要选择多个用户或组，请按住Ctrl或Shift并单击您的选择。
1. 单击 **偏好设置** 选项卡。

   ![cqsecuritypreferences](assets/cqsecuritypreferences.png)

1. 根据需要更改组或用户首选项，然后单击 **保存** 完成后。

### 将用户或管理员设置为具有管理其他用户的权限 {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

要将用户或管理员设置为具有删除/激活/停用其他用户的权限，请执行以下操作：

1. 将要授予管理其他用户的权限的用户添加到管理员组，并保存更改。

   ![cqsecurityaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. 在用户的 **权限** 选项卡，导航到“/”，在复制列中，选中允许在“/”处复制的复选框，然后单击 **保存**.

   ![cqsecurityreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   所选用户现在可以停用、激活、删除和创建用户。

### 在项目级别扩展权限 {#extending-privileges-on-a-project-level}

如果您计划实施特定于应用程序的权限，以下信息将描述实施自定义权限所必须了解的信息，以及如何在CQ中实施自定义权限：

jcr-privileges的组合覆盖了层次结构修改权限。 已命名复制权限 **crx：replicate** 以及jcr存储库上的其他权限一起存储/评估。 但是，它不在jcr级别强制执行。

自定义权限的定义和注册正式属于 [Jackrabbit API](https://jackrabbit.apache.org/oak/docs/security/privilege.html) 从版本2.4开始(另请参阅 [JCR-2887](https://issues.apache.org/jira/browse/JCR-2887))。 JCR访问控制管理（如定义的）涵盖了进一步的用法 [JSR 283](https://jcp.org/en/jsr/detail?id=283) （第16节）。 此外，Jackrabbit API还定义了几个扩展。

权限注册机制反映在UI中的 **存储库配置**.

新（自定义）权限的注册本身受必须在存储库级别授予的内置权限保护。 在JCR：在ac mgt api中将“null”作为“absPath”参数传递，有关详细信息，请参阅jsr 333 。 默认情况下， **管理员** 管理员的所有成员都拥有该权限。

>[!NOTE]
>
>虽然实施负责验证和评估自定义权限，但除非它们是内置权限的聚合，否则无法强制实施这些权限。
