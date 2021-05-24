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
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: 安全
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '5488'
ht-degree: 2%

---

# 用户管理和安全{#user-administration-and-security}

本章介绍如何配置和维护用户授权，并介绍如何在AEM中进行身份验证和授权工作的原理。

## AEM {#users-and-groups-in-aem}中的用户和组

本节将更详细地介绍各种实体和相关概念，以帮助您配置易于维护的用户管理概念。

### 用户 {#users}

用户将使用其帐户登录AEM。 每个用户帐户都是唯一的，它包含基本帐户详细信息以及分配的权限。

用户通常是组的成员，这可以简化这些权限和/或权限的分配。

### 组 {#groups}

组是用户和/或其他组的集合；这些都称为群组成员。

其主要目的是通过减少要更新的实体数来简化维护过程，因为对组所做的更改会应用于组的所有成员。 群体通常反映：

* 在应用程序内的角色；例如，有权访问内容的人员，或有权提供内容的人员。
* 您自己的组织；当参与者被限制到内容树中的不同分支时，您可能希望扩展角色以区分不同部门的参与者。

因此，组通常保持稳定，而用户来来去的频率更高。

通过规划和清晰的结构，使用组可以反映您的结构，从而为您提供清晰的概述和高效的更新机制。

### 内置用户和组{#built-in-users-and-groups}

AEM WCM安装大量用户和组。 在安装后首次访问安全控制台时，将会看到这些内容。

下表列出了每个项目及：

* 简短的描述
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
   <td><p>具有完全访问权限的系统管理帐户。</p> <p>此帐户用于AEM WCM和CRX之间的连接。</p> <p>如果意外删除了此帐户，则在重新启动存储库（在默认设置中）时，将重新创建此帐户。</p> <p>管理员帐户是AEM平台的一项要求。 因此，无法删除此帐户。</p> </td>
   <td><p>Adobe强烈建议将此用户帐户的密码从默认值更改为。</p> <p>最好在安装时，尽管可以在安装后完成。</p> <p>注意：不要将此帐户与CQ Servlet引擎的管理员帐户混淆。</p> </td>
  </tr>
  <tr>
   <td><p>匿名</p> <p> </p> </td>
   <td>用户</td>
   <td><p>保留对实例的未经身份验证访问的默认权限。 默认情况下，此设置将保留最低访问权限。</p> <p>如果意外删除了此帐户，则会在启动时重新创建该帐户。 无法永久删除，但可以禁用。</p> </td>
   <td>请避免删除或禁用此帐户，因为这将对创作实例的功能产生负面影响。 如果存在要求您删除该文件的安全要求，请确保首先正确测试该文件对系统的影响。</td>
  </tr>
  <tr>
   <td><p>作者</p> <p>默认密码：作者</p> </td>
   <td>用户</td>
   <td><p>允许作者帐户写入/content。 包含参与者和冲浪者权限。</p> <p>可以用作Webmaster，因为它有权访问整个/content树。</p> <p>这不是内置用户，而是另一个geometrixx演示用户</p> </td>
   <td><p>Adobe建议完全删除帐户，或从默认值更改密码。</p> <p>最好在安装时，尽管可以在安装后完成。</p> </td>
  </tr>
  <tr>
   <td>管理员</td>
   <td>组</td>
   <td><p>为其所有成员授予管理员权限的组。 只允许管理员编辑此群组。</p> <p>具有完全访问权限。</p> </td>
   <td>如果您在节点上设置“deny-everyone”，则只有在再次为该组启用该属性时，管理员才具有访问权限。</td>
  </tr>
  <tr>
   <td>content-authors</td>
   <td>组</td>
   <td><p>负责内容编辑的组。 需要读取、修改、创建和删除权限。</p> </td>
   <td>您可以创建自己的内容创作组，并具有项目特定的访问权限，前提是您添加读取、修改、创建和删除权限。</td>
  </tr>
  <tr>
   <td>contributor</td>
   <td>组</td>
   <td><p>允许用户写入内容的基本权限（仅在功能中）。</p> <p>不向/content树分配任何权限 — 必须专门为各个组或用户分配这些权限。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam-users</td>
   <td>组</td>
   <td>典型AEM Assets用户的现成引用组。 此组的成员具有相应权限，可启用资产和收藏集的上传/共享。</td>
   <td> </td>
  </tr>
  <tr>
   <td>每个</td>
   <td>组</td>
   <td><p>AEM中的每个用户都是组中每个人的成员，即使您可能看不到该组或所有工具中的成员资格关系。</p> <p>此组可以被视为默认权限，因为它可用于为每个人（甚至是将来创建的用户）应用权限。</p> </td>
   <td><p>请勿修改或删除此组。</p> <p>修改此帐户会涉及其他安全问题。</p> </td>
  </tr>
  <tr>
   <td>标记管理员</td>
   <td>组</td>
   <td>允许编辑标记的组。</td>
   <td> </td>
  </tr>
  <tr>
   <td>用户管理员</td>
   <td>组</td>
   <td>授权用户管理，即创建用户和群组的权限。</td>
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
   <td><p>参与工作流的用户必须是组工作流用户的成员。 这样，他/她就可以完全访问：/etc/workflow/instances，以便他/她可以更新工作流实例。</p> <p>该组包含在标准安装中，但您必须手动将用户添加到该组。</p> </td>
  </tr>
 </tbody>
</table>

## AEM {#permissions-in-aem}中的权限

AEM使用ACL来确定用户或组可以执行哪些操作以及可以在何处执行这些操作。

### 权限和ACL {#permissions-and-acls}

权限定义允许谁对资源执行哪些操作。 权限是[访问控制](#access-control-lists-and-how-they-are-evaluated)评估的结果。

您可以通过选中或清除单个AEM [actions](security.md#actions)对应的复选框，来更改授予/拒绝给定用户的权限。 复选标记表示允许执行操作。 无复选标记表示操作被拒绝。

复选标记位于网格中的位置还指示用户在AEM中的哪些位置（即哪些路径）拥有哪些权限。

### 操作 {#actions}

可以对页面（资源）执行操作。 对于层次结构中的每个页面，您可以指定允许用户对该页面执行哪项操作。 [](#permissions-and-acls) 允许您允许或拒绝某个操作。

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
    </ul> <p>在JCR级别，用户可以通过修改资源的属性、锁定、版本控制、nt-modification来修改资源，并且他们对定义jcr:content子节点的节点（例如cq:Page、nt:file、cq:Asset）具有完全写入权限。</p> </td>
  </tr>
  <tr>
   <td>创建</td>
   <td><p>用户可以：</p>
    <ul>
     <li>创建新页面或子页面。</li>
    </ul> <p>如果拒绝<strong>modify</strong>，则明确排除jcr:content下的子树，因为创建jcr:content及其子节点被视为页面修改。 这仅适用于定义jcr:content子节点的节点。</p> </td>
  </tr>
  <tr>
   <td>删除</td>
   <td><p>用户可以：</p>
    <ul>
     <li>从页面或任何子页面中删除现有段落。</li>
     <li>删除页面或子页面。</li>
    </ul> <p>如果拒绝<strong>modify</strong>，则明确排除jcr:content下的任何子树作为删除jcr:content，其子节点将被视为页面修改。 这仅适用于定义jcr:content子节点的节点。</p> </td>
  </tr>
  <tr>
   <td>读取 ACL</td>
   <td>用户可以读取页面或子页面的访问控制列表。</td>
  </tr>
  <tr>
   <td>编辑 ACL</td>
   <td>用户可以修改页面或任何子页面的访问控制列表。</td>
  </tr>
  <tr>
   <td>复制</td>
   <td>用户可以将内容复制到其他环境（例如，发布环境）。 该权限也应用于任何子页面。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM会自动为[Collections](/help/assets/manage-collections.md)中的角色分配（所有者、编辑者、查看者）生成用户组。 但是，手动为此类组添加ACL可能会在AEM中引入安全漏洞。 Adobe建议您避免手动添加ACL。

### 访问控制列表及其评估方式{#access-control-lists-and-how-they-are-evaluated}

AEM WCM使用访问控制列表(ACL)来组织应用于各个页面的权限。

访问控制列表由各个权限组成，用于确定实际应用这些权限的顺序。 根据所考虑页面的层次结构形成列表。 然后，将从下到上扫描此列表，直到找到应用于页面的第一个适当权限为止。

>[!NOTE]
>
>示例中包含一些ACL。 建议您查看并确定适合您的应用程序的内容。 要查看包含的ACL，请转到**CRXDE **，并为以下节点选择&#x200B;**Access Control**&#x200B;选项卡：
>
>`/etc/cloudservices/facebookconnect/geometrixx-outdoorsfacebookapp`:允许每个人读取访问权限。
>`/etc/cloudservices/twitterconnect/geometrixx-outdoors-twitter-app`:允许每个人读取访问权限。
>`/home/users/geometrixx-outdoors`:允许每个人读取`*/profile*`和
>`*/social/relationships/following/*`.
>
>您的自定义应用程序可以设置对其他关系（如`*/social/relationships/friend/*`或`*/social/relationships/pending-following/*`）的访问权限。
>
>创建特定于社区的ACL时，加入这些社区的成员可能会被授予额外的权限。 例如，当用户在`/content/geometrixx-outdoors/en/community/hiking`或`/content/geometrixx-outdoors/en/community/winter-sports`处加入社区时，可能会出现这种情况。

### 权限状态{#permission-states}

>[!NOTE]
>
>对于CQ 5.3用户：
>
>与以前的CQ版本相比，如果用户只需要修改页面，则不应再授予&#x200B;**create**&#x200B;和&#x200B;**delete**。 相反，仅当您希望用户能够在现有页面上创建、修改或删除组件时，才应授予&#x200B;**modify**&#x200B;操作。
>
>出于向后兼容性的考虑，操作测试未考虑定义&#x200B;**jcr:content**&#x200B;的节点的特殊处理。

| **操作** | **描述** |
|---|---|
| 允许（复选标记） | AEM WCM允许用户在此页面或任何子页面上执行操作。 |
| 拒绝（无复选标记） | AEM WCM不允许用户在此页面上或任何子页面上执行操作。 |

权限也会应用于任何子页面。

如果权限不是从父节点继承的，但至少具有一个本地条目，则以下符号会附加到复选框中。 本地条目是在CRX 2.2接口中创建的条目（通配符ACL当前只能在CRX中创建。）

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

将鼠标悬停在星号或感叹号上时，工具提示会提供有关声明条目的更多详细信息。 工具提示分为两部分：

<table>
 <tbody>
  <tr>
   <td>上部</td>
   <td><p>列出有效条目。</p> </td>
  </tr>
  <tr>
   <td>下部</td>
   <td>列出可能在树中其他位置产生影响的无效条目（如具有相应ACE的特殊属性所表示，该属性限制了条目的范围）。 或者，这是一个条目，其效果已被在给定路径或上级节点上定义的另一个条目撤消。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>如果未为页面定义权限，则所有操作都将被拒绝。

以下是有关管理访问控制列表的建议：

* 请勿直接将权限分配给用户。 仅将其分配给组。

   这将简化维护过程，因为组数量远小于用户数量，而且波动性也较小。

* 如果您希望组/用户只能修改页面，请勿授予他们创建或拒绝权限。 仅授予他们修改和读取权限。
* 少用拒绝。 尽可能仅使用允许。

   如果按与预期顺序不同的顺序应用权限，则使用拒绝可能会导致意外影响。 如果用户是多个组的成员，则来自一个组的Deny语句可以取消来自另一个组的Allow语句，反之亦然。 发生此情况时，很难保留概览，并且很容易导致意外结果，而“允许”分配不会导致此类冲突。

   Adobe建议您使用“允许”而不是“拒绝”，请参阅[最佳实践](#best-practices)。

在修改任一权限之前，请确保您了解这些权限的工作方式和相互关系。 请参阅CRX文档，以说明AEM WCM [如何评估访问权限](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated)以及有关设置访问控制列表的示例。

### 权限 {#permissions}

通过这些权限，用户和群组有权访问AEM页面上的AEM功能。

通过展开/折叠节点按路径浏览权限，并可跟踪到根节点的权限继承。

您可以通过选中或清除相应的复选框来允许或拒绝权限。

![cqsecuritypermissionstab](assets/cqsecuritypermissionstab.png)

### 查看详细权限信息{#viewing-detailed-permission-information}

除了网格视图之外，AEM还提供给定路径下选定用户/群组权限的详细视图。 详细信息视图提供其他信息。

除了查看信息外，您还可以包含当前用户或组或将其从组中排除。 请参阅[添加权限时添加用户或组](#adding-users-or-groups-while-adding-permissions)。 此处所做的更改会立即反映在详细视图的上部。

要访问“详细信息”视图，请在&#x200B;**权限**&#x200B;选项卡中，单击任何选定组/用户和路径的&#x200B;**详细信息**。

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
   <td><p>显示执行以下操作的用户和组的网格：</p>
    <ul>
     <li>声明给定路径AND的条目</li>
     <li>给定的可授权OR是组</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 模拟其他用户{#impersonating-another-user}

借助[模拟功能](/help/sites-authoring/user-properties.md#user-settings)，用户可以代表其他用户工作。

这意味着用户帐户可以指定其他可以使用其帐户运行的帐户。 换言之，如果允许用户B模拟用户A，则用户B可以使用用户A的完整帐户详细信息执行操作。

这样，模拟员帐户就可以像使用模拟员帐户一样完成任务；例如，在缺勤期间或在短期内共享过多负载。

>[!NOTE]
>
>为了模拟为非管理员用户工作，模拟器（在上述示例中为user-B）需要在`/home/users`路径中具有READ权限。
>
>有关如何实现此操作的更多信息，请参阅AEM](/help/sites-administering/security.md#permissions-in-aem)中的[权限。

>[!CAUTION]
>
>如果一个帐户模拟另一个帐户，则很难查看。 模拟开始和结束时，审核日志中会有一个条目，但其他日志文件（如访问日志）不包含有关事件上发生模拟的事实的信息。 因此，如果用户B模拟用户A，则所有事件看起来都像是用户A个人执行的。

>[!CAUTION]
>
>模拟用户身份时可以执行页面锁定。但是，以这种方式锁定的页面随后只能由被模拟的用户或拥有管理员权限的用户解锁。
>
>不能通过模拟锁定页面的用户的身份来解锁页面。

### 最佳实践 {#best-practices}

以下介绍了使用权限和权限时的最佳实践：

| 规则 | 原因 |
|--- |--- |
| *使用群组* | 避免按用户分配访问权限。 原因有多种：<ul><li>用户比组多，因此组可以简化结构。</li><li>群组可帮助提供有关所有帐户的概述。</li> <li>对于组，继承更简单。</li><li>用户来来去。 群体是长期的。</li></ul> |
| *积极* | 始终使用Allow语句指定组的权限（尽可能）。 避免使用Deny语句。 按顺序评估组，并且顺序可以按用户不同进行定义。 换句话说：您可能对语句的实施和评估顺序几乎没有控制权。 如果仅使用Allow语句，则顺序无关紧要。 |
| *保持简单* | 在配置新安装时花一些时间和时间思考就能得到很好的回报。 应用清晰的结构将简化持续的维护和管理，确保您的当前同事和/或未来继任者都能够轻松了解正在实施的内容。 |
| *测试* | 使用测试安装来实践并确保您了解各种用户和组之间的关系。 |
| *默认用户/组* | 请始终在安装后立即更新默认用户和组，以帮助防止出现任何安全问题。 |

## 管理用户和组{#managing-users-and-groups}

用户包括使用系统的人员和向系统发出请求的外国系统。

群组是一组用户。

这两种配置都可以使用安全控制台中的用户管理功能进行配置。

### 使用安全控制台{#accessing-user-administration-with-the-security-console}访问用户管理

您可以使用安全控制台访问所有用户、组和关联的权限。 本节中描述的所有过程都将在此窗口中执行。

要访问AEM WCM安全性，请执行以下操作之一：

* 从欢迎屏幕或AEM中的各个位置，单击安全图标：

![](do-not-localize/wcmtoolbar.png)

* 直接导航到`https://<server>:<port>/useradmin`。 确保您以管理员身份登录AEM。

此时将显示以下窗口：

![cqsecuritypage](assets/cqsecuritypage.png)

左侧树列出了系统中当前的所有用户和组。 您可以选择要显示的列，对列的内容进行排序，甚至通过将列标题拖动到新位置来更改列的显示顺序。

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

通过选项卡，可以访问各种配置：

<!-- ??? in table below. -->

| 选项卡· | 描述 |
|--- |--- |
| 过滤器框 | 用于筛选列出的用户和/或组的机制。 请参阅[筛选用户和组](#filtering-users-and-groups)。 |
| 隐藏用户 | 一个切换开关，将隐藏列出的所有用户，仅保留群组。 请参阅[隐藏用户和组](#hiding-users-and-groups)。 |
| 隐藏组 | 一个切换开关，将隐藏列出的所有组，仅保留用户。 请参阅[隐藏用户和组](#hiding-users-and-groups)。 |
| 编辑 | 用于创建和删除以及激活和停用用户或组的菜单。 请参阅[创建用户和组](#creating-users-and-groups)和[删除用户和组](#deleting-users-and-groups)。 |
| 属性 | 列出有关用户或组的信息，这些信息可以包含电子邮件信息、描述和名称信息。 还允许您更改用户的密码。 请参阅[创建用户和组](#creating-users-and-groups)、[修改用户和组属性](#modifying-user-and-group-properties)和[更改用户密码](#changing-a-user-password)。 |
| 组 | 列出选定用户或组所属的所有组。 您可以将选定的用户或组分配给其他组或从组中删除它们。 请参阅[组](#adding-users-or-groups-to-a-group)。 |
| 成员 | 仅适用于组。 列出特定组的成员。 请参阅[成员](#members-adding-users-or-groups-to-a-group)。 |
| 权限 | 您可以向用户或群组分配权限。 允许您控制以下内容：<ul><li>与特定页面/节点相关的权限。 请参阅[设置权限](#setting-permissions)。 </li><li>与创建和删除页面以及层次结构修改相关的权限。???允许[分配权限](#settingprivileges)，例如层次结构修改，用于创建和删除页面，</li><li>与[复制权限相关的权限](#setting-replication-privileges)（通常从创作到发布）。</li></ul> |
| 模拟者 | 允许其他用户模拟该帐户。 当您需要用户代表其他用户执行操作时，此变量非常有用。 请参阅[模拟用户](#impersonating-another-user)。 |
| 首选项 | 设置组或用户](#setting-user-and-group-preferences)的[首选项。 例如，语言首选项。 |

### 筛选用户和组{#filtering-users-and-groups}

您可以通过输入过滤器表达式来过滤列表，该表达式会隐藏与表达式不匹配的所有用户和组。 您还可以使用[隐藏用户和隐藏群组](#hiding-users-and-groups)按钮来隐藏用户和群组。

要筛选用户或组，请执行以下操作：

1. 在左树列表中，在提供的空格中键入过滤器表达式。 例如，输入&#x200B;**admin**&#x200B;将显示包含此字符串的所有用户和组。
1. 单击放大镜以过滤列表。

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. 如果要删除所有过滤器，请单击&#x200B;**x**。

### 隐藏用户和组{#hiding-users-and-groups}

隐藏用户或组是筛选系统中所有用户和组列表的另一种方法。 有两种切换机制。 单击“隐藏用户”可隐藏视图中的所有用户，单击“隐藏组”可隐藏视图中的所有组（您不能同时隐藏用户和组）。 要使用过滤器表达式过滤列表，请参阅[过滤用户和组](#filtering-users-and-groups)。

要隐藏用户和群组，请执行以下操作：

1. 在&#x200B;**Security**&#x200B;控制台中，单击&#x200B;**隐藏用户**&#x200B;或&#x200B;**隐藏组**。 选定按钮将突出显示。

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. 要使用户或组重新显示，请再次单击相应的按钮。

### 创建用户和组{#creating-users-and-groups}

要创建新用户或群组，请执行以下操作：

1. 在&#x200B;**Security**&#x200B;控制台树列表中，单击&#x200B;**Edit**，然后单击&#x200B;**Create User**&#x200B;或&#x200B;**Create Group**。

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. 根据您是创建用户还是群组，输入所需的详细信息。

   * 如果选择&#x200B;**创建用户，** ，则输入登录ID、名字和姓氏、电子邮件地址和密码。 默认情况下，AEM会根据姓氏的第一个字母创建一个路径，但您可以选择其他路径。

   ![createuserdialog](assets/createuserdialog.png)

   * 如果选择&#x200B;**创建组**，则输入组ID和可选描述。

   ![创建组对话框](assets/creategroupdialog.png)

1. 单击&#x200B;**创建**。创建的用户或组将显示在树列表中。

### 删除用户和组{#deleting-users-and-groups}

要删除用户或组，请执行以下操作：

1. 在&#x200B;**Security**&#x200B;控制台中，选择要删除的用户或组。 如果要删除多个项目，请按住Shift并单击或按住Control并单击以选择这些项目。
1. 单击&#x200B;**编辑，**，然后选择删除。 AEM WCM会询问您是要删除用户或组。
1. 单击&#x200B;**确定**&#x200B;以确认，或单击取消以取消您的操作。

### 修改用户和组属性{#modifying-user-and-group-properties}

要修改用户和群组属性，请执行以下操作：

1. 在&#x200B;**Security**&#x200B;控制台中，双击要修改的用户或组名称。

1. 单击&#x200B;**属性**&#x200B;选项卡，进行所需的更改，然后单击&#x200B;**保存**。

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>用户的路径显示在用户属性的底部。 无法修改。

### 更改用户密码{#changing-a-user-password}

请按照以下过程修改用户的密码。

>[!NOTE]
>
>您无法使用安全控制台更改管理员密码。 要更改管理员帐户的密码，请使用Granite Operations提供的[Users console](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)。
>
>如果您在JEE上使用AEM Forms，请勿使用下面的说明更改密码，而是使用JEE管理控制台(/adminui)上的AEM Forms更改密码。

1. 在&#x200B;**Security**&#x200B;控制台中，双击要更改其密码的用户名。
1. 单击&#x200B;**属性**&#x200B;选项卡（如果尚未激活）。
1. 单击&#x200B;**设置密码**。 “Set Password（设置密码）”窗口将打开，您可以在其中更改密码。

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. 输入新密码两次；由于它们未以明文显示，因此这是为了进行确认 — 如果它们不匹配，则系统会显示错误。
1. 单击&#x200B;**设置**&#x200B;以激活帐户的新密码。

### 将用户或组添加到组{#adding-users-or-groups-to-a-group}

AEM提供了三种将用户或组添加到现有组的不同方法：

* 在群组中，可以添加成员（用户或群组）。
* 在成员中，可以向组添加成员。
* 使用“权限”时，可以将成员添加到群组。

### 组 — 将用户或组添加到组{#groups-adding-users-or-groups-to-a-group}

**组**&#x200B;选项卡显示当前帐户所属的组。 您可以使用它将所选帐户添加到群组：

1. 双击要分配给群组的帐户（用户或群组）名称。
1. 单击&#x200B;**Groups**&#x200B;选项卡。 您会看到帐户已属于的组列表。
1. 在树列表中，单击要添加到帐户的组名称，并将其拖动到&#x200B;**组**&#x200B;窗格。 （如果要添加多个用户，请按住Shift并单击或按住Control并单击这些名称并拖动它们。）

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. 单击&#x200B;**Save**&#x200B;以保存更改。

### 成员 — 将用户或组添加到组{#members-adding-users-or-groups-to-a-group}

**成员**&#x200B;选项卡仅适用于组，并显示哪些用户和组属于当前组。 您可以使用它将帐户添加到群组：

1. 双击要向其添加成员的组的名称。
1. 单击&#x200B;**Members**&#x200B;选项卡。 您会看到已属于此组的成员列表。
1. 在树列表中，单击要添加到组的成员的名称，并将其拖动到&#x200B;**Members**&#x200B;窗格。 （如果要添加多个用户，请按住Shift并单击或按住Control并单击这些名称并拖动它们。）

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. 单击&#x200B;**Save**&#x200B;以保存更改。

### 添加权限{#adding-users-or-groups-while-adding-permissions}时添加用户或组

要将成员添加到特定路径中的组，请执行以下操作：

1. 双击要将用户添加到的组或用户的名称。

1. 单击&#x200B;**权限**&#x200B;选项卡。

1. 导航到要添加权限的路径，然后单击&#x200B;**Details**。 详细信息窗口的下半部分提供有关谁具有该页面权限的信息。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 选中&#x200B;**成员**&#x200B;列中要拥有该路径权限的成员的复选框。 清除要删除其权限的成员的复选框。 在您对进行更改的单元格中，会出现一个红色三角形。
1. 单击&#x200B;**确定**&#x200B;以保存您的更改。

### 从组{#removing-users-or-groups-from-groups}中删除用户或组

AEM提供了三种从群组中删除用户或组的不同方法：

* 在群组配置文件中时，可以删除成员（用户或群组）。
* 在成员配置文件中时，可以从组中删除成员。
* 使用“权限”时，可以从组中删除成员。

### 组 — 从组{#groups-removing-users-or-groups-from-groups}中删除用户或组

要从群组中删除用户或组帐户，请执行以下操作：

1. 双击要从群组中删除的群组或用户帐户的名称。
1. 单击&#x200B;**Groups**&#x200B;选项卡。 您会看到选定帐户所属的组。
1. 在&#x200B;**组**&#x200B;窗格中，单击要从组中删除的用户或组的名称，然后单击&#x200B;**删除**。 （如果要删除多个帐户，请按住Shift键并单击或按住Control键并单击这些名称，然后单击&#x200B;**删除**。）

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. 单击&#x200B;**Save**&#x200B;以保存更改。

### 成员 — 从组{#members-removing-users-or-groups-from-groups}中删除用户或组

要从组中删除帐户，请执行以下操作：

1. 双击要从中删除成员的组名称。
1. 单击&#x200B;**Members**&#x200B;选项卡。 您会看到已属于此组的成员列表。
1. 在&#x200B;**成员**&#x200B;窗格中，单击要从组中删除的成员的名称，然后单击&#x200B;**删除**。 （如果要删除多个用户，请按住Shift并单击或按住Control并单击这些名称，然后单击&#x200B;**删除**。）

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. 单击&#x200B;**Save**&#x200B;以保存更改。

### 添加权限{#removing-users-or-groups-while-adding-permissions}时删除用户或组

要从特定路径的组中删除成员：

1. 双击要从中删除用户的组或用户的名称。

1. 单击&#x200B;**权限**&#x200B;选项卡。

1. 导航到要删除权限的路径，然后单击&#x200B;**Details**。 详细信息窗口的下半部分提供有关谁具有该页面权限的信息。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 选中&#x200B;**成员**&#x200B;列中要拥有该路径权限的成员的复选框。 清除要删除其权限的成员的复选框。 在您对进行更改的单元格中，会出现一个红色三角形。
1. 单击&#x200B;**确定**&#x200B;以保存您的更改。

### 用户同步{#user-synchronization}

当部署为[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)时，需要在所有发布节点之间同步用户和组。

要了解用户同步及其启用方法，请参阅[用户同步](/help/sites-administering/sync.md)。

## 管理权限{#managing-permissions}

>[!NOTE]
>
>Adobe引入了新的基于触屏UI的权限管理主体视图。 有关如何使用该子域的详细信息，请参阅[此页面](/help/sites-administering/touch-ui-principal-view.md)。

本节介绍如何设置权限，包括复制权限。

### 设置权限{#setting-permissions}

权限允许用户在特定路径上对资源执行特定操作。 它还包括创建或删除页面的功能。

要添加、修改或删除权限，请执行以下操作：

1. 在&#x200B;**Security**&#x200B;控制台中，双击要为或[搜索节点](#searching-for-nodes)设置权限的用户或组的名称。

1. 单击&#x200B;**权限**&#x200B;选项卡。

   ![cquserpermissions](assets/cquserpermissions.png)

1. 在树网格中，选中一个复选框，以允许选定的用户或组执行某项操作，或清除一个复选框以拒绝选定的用户或组执行某项操作。 有关详细信息，请单击&#x200B;**详细信息**。

1. 完成后，单击&#x200B;**Save**。

### 设置复制权限{#setting-replication-privileges}

复制权限是发布内容的权限，它可以为组和用户设置。

>[!NOTE]
>
>* 对组应用的任何复制权限都适用于该组中的所有用户。
>* 用户的复制权限将取代组的复制权限。
>* 允许复制权限的优先级比拒绝复制权限的优先级高。 有关更多信息，请参阅AEM](#permissions-in-aem)中的[权限。

>



要设置复制权限，请执行以下操作：

1. 从列表中选择用户或组，双击以打开，然后单击&#x200B;**权限**。
1. 在网格中，导航到希望用户具有复制权限的路径或搜索节点。](#searching-for-nodes)[

1. 在选定路径的&#x200B;**复制**&#x200B;列中，选中用于添加该用户或组的复制权限的复选框，或清除用于删除复制权限的复选框。 AEM会在您所做更改但尚未保存的位置显示一个红色三角形。

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. 单击&#x200B;**Save**&#x200B;以保存更改。

### 搜索节点{#searching-for-nodes}

添加或删除权限时，您可以浏览或搜索节点。

路径搜索有两种不同类型：

* 路径搜索 — 如果搜索字符串以“/”开头，则搜索将搜索给定路径的直接子节点：

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

在搜索框中，您可以执行以下操作：

| 操作 | 它的作用 |
|--- |--- |
| 向右箭头键 | 在搜索结果中选择子节点 |
| 向下箭头键 | 再次开始搜索。 |
| Enter(Return)键 | 选择子节点并将其加载到树状网格中 |

* 全文搜索 — 如果搜索字符串不以“/”开头，则对路径“/content”下的所有节点执行全文搜索。

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

要对路径或全文执行搜索，请执行以下操作：

1. 在“安全”控制台中，选择一个用户或组，然后单击&#x200B;**权限**&#x200B;选项卡。

1. 在搜索框中，输入要搜索的术语。

### 模拟用户{#impersonating-users}

您可以指定一个或多个允许模拟当前用户的用户。 这意味着他们可以将其帐户设置切换为当前用户的帐户设置，并代表此用户执行操作。

使用此函数时请务必谨慎，因为此函数可能允许用户执行其自己用户无法执行的操作。 模拟用户时，系统会通知用户他们未以自己的身份登录。

您可能希望使用此功能的各种情况，包括：

* 如果你不在办公室，你可以让别人在你不在的时候冒充你。 通过使用此功能，您可以确保某人拥有您的访问权限，并且您无需修改用户配置文件或提供您的密码。
* 您可以将其用于调试目的。 例如，查看网站如何查找具有受限访问权限的用户。 此外，如果用户抱怨技术问题，您可以模拟该用户来诊断和修复问题。

要模拟现有用户，请执行以下操作：

1. 在树列表中，选择要为其他用户分配模拟身份的人员的姓名。 双击以打开。
1. 单击&#x200B;**模拟器**&#x200B;选项卡。
1. 单击您希望能够模拟选定用户的用户。 将用户（将模拟的用户）从列表拖到“模拟”窗格。 该名称会显示在列表中。

   ![chlimage_1-114](assets/chlimage_1-115.png)

1. 单击&#x200B;**保存**。

### 设置用户和组首选项{#setting-user-and-group-preferences}

要设置用户和组首选项，包括语言、窗口管理和工具栏首选项：

1. 在左侧树中选择要更改其首选项的用户或组。 要选择多个用户或组，请按住Ctrl或Shift并单击您的选择。
1. 单击&#x200B;**首选项**&#x200B;选项卡。

   ![cqsecuritypreferences](assets/cqsecuritypreferences.png)

1. 根据需要对组或用户首选项进行更改，完成后单击&#x200B;**保存**。

### 将用户或管理员设置为具有管理其他用户的权限{#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

要将用户或管理员设置为具有删除/激活/取消激活其他用户的权限，请执行以下操作：

1. 将要授予权限以管理其他用户的用户添加到管理员组并保存更改。

   ![cqsecurityadmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. 在用户的&#x200B;**Permissions**&#x200B;选项卡中，导航到“/”，在“复制”列中，选中允许复制的复选框，然后单击&#x200B;**Save**。

   ![cqsecurityreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   现在，所选用户能够停用、激活、删除和创建用户。

### 扩展项目级别{#extending-privileges-on-a-project-level}的权限

如果您计划实施特定于应用程序的权限，以下信息将描述您在实施自定义权限时需要了解的信息以及如何在整个CQ中强制实施该权限：

层次结构修改权限由jcr权限的组合覆盖。 复制权限名为&#x200B;**crx:replicate**，该权限与jcr存储库的其他权限一起存储/评估。 但是，它并未在jcr级别上强制执行。

自定义权限的定义和注册正式包含在[Jackrabbit API](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/api/security/authorization/PrivilegeManager.html)版本2.4中（另请参阅[JCR-2887](https://issues.apache.org/jira/browse/JCR-2887)）。 JCR访问控制管理涵盖进一步的使用，如[JSR 283](https://jcp.org/en/jsr/detail?id=283)（第16节）定义的。 此外，Jackrabbit API还定义了几个扩展。

权限注册机制反映在&#x200B;**Repository Configuration**&#x200B;下的UI中。

新（自定义）权限的注册本身受必须在存储库级别(在JCR中：在ac mgt api中将“null”作为“absPath”参数传递，有关详细信息，请参阅jsr 333)。 默认情况下，**admin**&#x200B;和管理员的所有成员都具有该权限。

>[!NOTE]
>
>虽然实施会负责验证和评估自定义权限，但除非这些权限是内置权限的聚合，否则将无法强制执行这些权限。
