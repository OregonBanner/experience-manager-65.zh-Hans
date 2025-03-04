---
title: 用户、组和访问权限管理
description: 了解Adobe Experience Manager中的用户、组和访问权限管理。
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 5808b8f9-9b37-4970-b5c1-4d33404d3a8b
feature: Security
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '3101'
ht-degree: 0%

---

# 用户、组和访问权限管理{#user-group-and-access-rights-administration}

启用对CRX存储库的访问涉及几个主题：

* [访问权限](#how-access-rights-are-evaluated)  — 有关如何定义和评估这些指标的概念
* [用户管理](#user-administration)  — 管理用于访问的单个帐户
* [组管理](#group-administration)  — 通过分组简化用户管理
* [访问权限管理](#access-right-management)  — 定义策略来控制这些用户和组访问资源的方式

基本元素包括：

**用户帐户** - CRX通过根据用户帐户中保留的详细信息识别并验证用户（由该人员或其他应用程序）来验证访问权限。

在CRX中，每个用户帐户都是工作区中的一个节点。 CRX用户帐户具有以下属性：

* 它表示CRX的一个用户。
* 它包含用户名和密码。
* 适用于该工作区。
* 不能有子用户。 要获得分层访问权限，您应使用组。

* 您可以指定用户帐户的访问权限。

  但是，为了简化管理，Adobe建议（在大多数情况下）为组帐户分配访问权限。 为每个用户分配访问权限会很快变得难以管理（当仅存在一两个实例时，某些系统用户例外）。

**组帐户**  — 组帐户是用户和/或其他组的集合。 这些权限用于简化管理，因为分配给组的访问权限更改会自动应用于该组中的所有用户。 用户不必属于任何组，但通常属于多个组。

在CRX中，组具有以下属性：

* 它表示一组具有共同访问权限的用户。 例如，作者或开发人员。
* 适用于该工作区。
* 它可以有成员；这些成员可以是个人用户或其他组。
* 可通过成员关系实现分层分组。 不能将组直接放在存储库中另一个组的下方。
* 您可以定义所有组成员的访问权限。

**访问权限** - CRX使用访问权限来控制对存储库特定区域的访问。

这是通过将权限分配给允许或拒绝对存储库中的资源（节点或路径）的访问来完成的。 由于可以分配各种权限，因此必须评估这些权限以确定哪个组合适用于当前请求。

CRX允许您配置用户和组帐户的访问权限。 然后将同样的基本评估原则应用于两者。

## 如何评估访问权限 {#how-access-rights-are-evaluated}

>[!NOTE]
>
>CRX实施 [JSR-283定义的访问控制](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).
>
>CRX存储库的标准安装配置为使用基于资源的访问控制列表。 这是JSR-283访问控制的一种可能实现以及Jackrabbit提供的实现之一。

### 主体和主体 {#subjects-and-principals}

CRX在评估访问权限时使用两个关键概念：

* A **主体** 是一个具有访问权限的实体。 承担者包括：

   * 用户帐户
   * 组帐户

     如果用户帐户属于一个或多个组，则它也会与每个组承担者相关联。

* A **主题** 用于表示请求的源。

  它用于合并适用于该请求的访问权限。 这些源自：

   * 用户主体

     您直接分配给用户帐户的权限。

   * 与该用户关联的所有组主体

     所有权限都会分配给用户所属的任何组。

  然后使用结果来允许或拒绝对请求资源的访问。

#### 编译主体的访问权限列表 {#compiling-the-list-of-access-rights-for-a-subject}

在CRX中，主题取决于：

* 用户主体
* 与该用户关联的所有组主体

适用于该主题的访问权限列表由以下内容构成：

* 您直接分配给用户帐户的权限
* 加上分配给用户所属任何组的所有权限

![chlimage_1-56](assets/chlimage_1-56.png)

>[!NOTE]
>
>* CRX在编译列表时不考虑任何用户层次结构。
>* 仅当您包括某个组作为另一个组的成员，CRX才使用组层次结构。 组权限没有自动继承。
>* 指定组的顺序不会影响访问权限。
>

### 解决请求和访问权限 {#resolving-request-and-access-rights}

CRX在处理请求时，会将来自主体的访问请求与存储库节点上的访问控制列表进行比较：

如果Linda请求更新 `/features` 节点：

![chlimage_1-57](assets/chlimage_1-57.png)

### 优先顺序 {#order-of-precedence}

CRX中的访问权限评估如下：

* 用户主体始终优先于组主体，不论如何：

   * 在访问控制列表中的顺序
   * 它们在节点层次结构中的位置

* 对于给定的主体，给定节点上最多有一个deny和1 allow条目。 该实施始终会清除冗余条目，并确保允许条目和拒绝条目中未列出相同的权限。

>[!NOTE]
>
>此评估过程适用于标准CRX安装的基于资源的访问控制。

举两个例子，用户 `aUser` 是组的成员 `aGroup`：

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
       + grandChildNode
```

在上例中：

* `aUser` 未授予对的写入权限 `grandChildNode`.

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
         + ace: aUser - deny - write
       + grandChildNode
```

在本例中：

* `aUser` 未授予对的写入权限 `grandChildNode`.
* 第二个ACE `aUser` 冗余。

来自多个组主体的访问权限根据其顺序进行评估，无论是在层次结构中还是在单个访问控制列表中。

### 最佳实践 {#best-practices}

下表列出了一些建议和最佳实践：

<table>
 <tbody>
  <tr>
   <td>推荐……</td>
   <td>原因...</td>
  </tr>
  <tr>
   <td><i>使用组</i></td>
   <td><p>避免逐个用户分配访问权限。 原因有多种：</p>
    <ul>
     <li>用户数多于组数，因此组简化了结构。</li>
     <li>组可帮助提供所有帐户的概述。</li>
     <li>对组进行继承更简单。</li>
     <li>用户来来去去。 组是长期的。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><i>积极的</i></td>
   <td><p>始终使用Allow语句指定组主体的访问权限（如果可能）。 避免使用Deny语句。</p> <p>在单个访问控制列表中，按层次和顺序对组主体进行评估。</p> </td>
  </tr>
  <tr>
   <td><i>保持简单</i></td>
   <td><p>在配置新安装时花费一些时间和思考是值得的。</p> <p>应用清晰的结构可简化持续的维护和管理，确保您当前的同事和/或未来的继任者能够轻松了解正在实施的内容。</p> </td>
  </tr>
  <tr>
   <td><i>测试</i></td>
   <td>使用测试安装进行练习并确保您了解各种用户和组之间的关系。</td>
  </tr>
  <tr>
   <td><i>默认用户/组</i></td>
   <td>始终在安装后立即更新默认用户和组，以防止出现任何安全问题。</td>
  </tr>
 </tbody>
</table>

## 用户管理 {#user-administration}

标准对话框用于 **用户管理**.

您必须登录到相应的工作区，然后才可以从以下两个位置访问该对话框：

* 该 **用户管理** CRX主控制台上的链接
* 该 **安全性** CRX Explorer的菜单

![chlimage_1-58](assets/chlimage_1-58.png)

**属性**

* **用户ID**

  访问CRX时使用帐户的短名称。

* **主体名称**

  帐户的全文名称。

* **密码**

  使用此帐户访问CRX时需要。

* **ntlmhash**

  自动为每个新帐户分配，并在密码更改时更新。

* 您可以通过定义名称、类型和值来添加新属性。 单击每个新属性的“保存”（绿色勾号符号）。

**组成员资格**

这将显示帐户所属的所有组。 “已继承”列指示由于另一个组的成员资格而继承的成员资格。

单击GroupID（如果可用）打开 [组管理](#group-administration) 为那个组别准备的。

**模拟者**

借助模拟功能，用户可以代表其他用户工作。

这意味着用户帐户可以指定可以与其帐户一起操作的其他帐户（用户或组）。 换言之，如果允许用户B模拟用户A，则用户B可以使用用户A的完整帐户详细信息（包括ID、名称和访问权限）进行操作。

这允许模拟者帐户完成任务，就像他们使用自己所模拟的帐户一样；例如，在缺勤期间，或者在短期共享过多负载。

如果帐户模拟其他帐户，则很难查看。 日志文件不包含有关事件上已发生模拟的事实的信息。 因此，如果用户B模拟用户A，则所有事件看起来都像是用户A亲自执行的。

### 创建用户帐户 {#creating-a-user-account}

1. 打开 **用户管理** 对话框。
1. 单击 **创建用户**.
1. 然后，您可以输入属性：

   * **用户ID** 用作帐户名称。
   * **密码** 登录时需要。
   * **主体名称** 以提供完整的文本名称。
   * **中间路径** 可用来形成树状结构。

1. 单击“保存”（绿色勾号）。
1. 该对话框将展开，这样您便可以执行以下操作：

   1. 配置 **属性**.
   1. 请参阅 **组成员资格**.
   1. 定义 **模拟者**.

>[!NOTE]
>
>在同时拥有大量新用户的安装中注册新用户时，有时可能会出现性能损失：
>
>* 用户
>* 拥有许多成员的组
>

### 更新用户帐户 {#updating-a-user-account}

1. 使用 **用户管理** 对话框，打开所有帐户的列表视图。
1. 在树结构中导航。
1. 单击所需的帐户，以便您可以打开它进行编辑。
1. 进行更改，然后单击该条目的“保存”（绿色勾号符号）。
1. 单击 **关闭** 完成，或 **列表……** 以返回到所有用户帐户的列表。

### 删除用户帐户 {#removing-a-user-account}

1. 使用 **用户管理** 对话框，打开所有帐户的列表视图。
1. 在树结构中导航。
1. 选择所需的帐户并单击 **删除用户**；立即删除帐户。

>[!NOTE]
>
>这将从存储库中删除此主体的节点。
>
>访问权限条目不会被删除。 这可以确保历史完整性。

### 定义属性 {#defining-properties}

您可以定义 **属性** 对于新帐户或现有帐户：

1. 打开 **用户管理** 对话框中的相应帐户。
1. 定义 **属性** 名称。
1. 选择 **类型** 下拉列表中。
1. 定义 **值**.
1. 单击新属性的“保存”(Save) （绿色单击符号）。

现有属性可使用垃圾桶符号删除。

除“密码”外，属性无法编辑，必须删除并重新创建。

#### 更改密码 {#changing-the-password}

此 **密码** 是一个特殊属性，通过单击 **更改密码** 链接。

您还可以将密码更改为您自己的用户帐户，其网址为 **安全性** CRX资源管理器中的菜单。

### 定义模拟者 {#defining-an-impersonator}

您可以为新帐户或现有帐户定义模拟者：

1. 打开 **用户管理** 对话框中的相应帐户。
1. 指定要允许模拟该帐户的帐户。

   您可以使用“浏览……”选择现有帐户。

1. 单击新属性的“保存”（绿色勾号符号）。

## 组管理 {#group-administration}

标准对话框用于 **组管理**.

您必须登录到相应的工作区，然后才可以从以下两个位置访问该对话框：

* 该 **组管理** CRX主控制台上的链接
* 该 **安全性** CRX Explorer的菜单

![chlimage_1-8](assets/chlimage_1-8.jpeg)

**属性**

* **组ID**

  组帐户的简短名称。

* **主体名称**

  组帐户的全文名称。

* 您可以通过定义名称、类型和值来添加新属性。 单击每个新属性的“保存”（绿色勾号符号）。

* **成员**

  您可以将用户或其他组添加为此组的成员。

**组成员资格**

这将显示当前组帐户所属的所有组。 “已继承”列指示由于另一个组的成员资格而继承的成员资格。

单击GroupID可打开该组的对话框。

**成员**

列出属于当前组的所有帐户（用户和/或组）。

此 **已继承** 列指示作为另一个组的成员身份继承的成员身份。

>[!NOTE]
>
>将所有者、编辑者或查看者角色分配给任何Asset文件夹中的用户后，将创建新组。 组名称的格式为 `mac-default-<foldername>` 用于定义角色的每个文件夹。

### 创建组帐户 {#creating-a-group-account}

1. 打开 **组管理** 对话框。
1. 单击 **创建组**.
1. 然后，您可以输入属性：

   * **主体名称** 以提供完整的文本名称。
   * **中间路径** 可用来形成树状结构。

1. 单击“保存”（绿色勾号）。
1. 该对话框将展开，以便您可以：

   1. 配置 **属性**.
   1. 请参阅 **组成员资格**.
   1. 管理 **成员**.

### 更新组帐户 {#updating-a-group-account}

1. 使用 **组管理** 对话框，打开所有帐户的列表视图。
1. 在树结构中导航。
1. 单击所需的帐户，以便您可以打开它进行编辑。
1. 进行更改，然后单击该条目的“保存”（绿色勾号符号）。
1. 单击 **关闭** 完成，或 **列表……** 以返回所有组帐户的列表。

### 删除组帐户 {#removing-a-group-account}

1. 使用 **组管理** 对话框，打开所有帐户的列表视图。
1. 在树结构中导航。
1. 选择所需的帐户并单击 **删除组**；立即删除帐户。

>[!NOTE]
>
>这将从存储库中删除此主体的节点。
>
>访问权限条目不会被删除。 这可以确保历史完整性。

### 定义属性 {#defining-properties-1}

您可以为新帐户或现有帐户定义属性：

1. 打开 **组管理** 对话框中的相应帐户。
1. 定义 **属性** 名称。
1. 选择 **类型** 下拉列表中。
1. 定义 **值**.
1. 单击新属性的“保存”（绿色勾号符号）。

现有属性可使用垃圾桶符号删除。

### 成员 {#members}

可以将成员添加到当前组：

1. 打开 **组管理** 对话框中的相应帐户。
1. 可以任选其一：

   * 输入所需成员的名称（用户或组帐户）。
   * 或使用 **浏览……** 搜索并选择要添加的主体（用户或组帐户）。

1. 单击新属性的“保存”（绿色勾号符号）。

或删除具有垃圾桶符号的现有成员。

## 访问权限管理 {#access-right-management}

使用 **访问控制** 选项卡中，您可以定义访问控制CRXDE Lite并分配相关权限。

例如，对于 **当前路径** 在左窗格（右下窗格中的“访问控制”选项卡）中选择所需的资源：

![crx_accesscontrol_tab](assets/crx_accesscontrol_tab.png)

这些策略根据以下条件进行分类：

* **适用的访问控制策略**

  可以应用这些策略。

  这些策略可用于创建本地策略。 选择并添加适用的策略后，该策略将成为本地策略。

* **本地访问控制策略**

  这些是您已应用的访问控制策略。 然后，您可以更新、排序或移除它们。

  本地策略会覆盖从父策略继承的任何策略。

* **有效的访问控制策略**

  这些是现在对任何访问请求都有效的访问控制策略。 它们显示从本地策略以及从父级继承的任何策略派生而来的聚合策略。

### 策略选择 {#policy-selection}

可以为以下对象选择策略：

* **当前路径**

  如上面的示例所示，选择存储库中的资源。 此时将显示此“当前路径”的策略。

* **存储库**

  选择存储库级别的访问控制。 例如，在设置 `jcr:namespaceManagement` 权限，它只与存储库相关，与节点无关。

* **主体**

  在存储库中注册的主体。

  您可以键入 **主体** 命名或单击字段右侧的图标以打开 **选择主体** 对话框。

  这允许您 **Search** 对于 **用户** 或 **组**. 从结果列表中选择所需的主体，然后单击 **确定** 将值带回上一个对话框。

![crx_accesscontrol_selectprincipal](assets/crx_accesscontrol_selectprincipal.png)

>[!NOTE]
>
>要简化管理Adobe，建议您为组帐户分配访问权限，而不是为单个用户帐户分配访问权限。
>
>管理几个组比管理多个用户帐户更容易。

### 特权 {#privileges}

添加访问控制条目时，可以选择以下权限(请参阅 [安全API](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/security/Privilege.html) 以了解全部详细信息)：

<table>
 <tbody>
  <tr>
   <th><strong>权限名称</strong></th>
   <th><strong>控制权限的……</strong></th>
  </tr>
  <tr>
   <td><code>jcr:read</code></td>
   <td>检索节点并读取其属性及其值。</td>
  </tr>
  <tr>
   <td><code>rep:write</code></td>
   <td>这是jcr：write和jcr：nodeTypeManagement的特定于Jackrabbit的聚合权限。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:all</code></td>
   <td>这是包含所有其他预定义权限的聚合权限。</td>
  </tr>
  <tr>
   <td><strong>高级</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>crx:replicate</code></td>
   <td>执行节点的复制。</td>
  </tr>
  <tr>
   <td><code>jcr:addChildNodes</code></td>
   <td>创建节点的子节点。</td>
  </tr>
  <tr>
   <td><code>jcr:lifecycleManagement</code></td>
   <td>在节点上执行生命周期操作。</td>
  </tr>
  <tr>
   <td><code>jcr:lockManagement</code></td>
   <td>锁定并解锁节点；刷新锁定。</td>
  </tr>
  <tr>
   <td><code>jcr:modifyAccessControl</code></td>
   <td>修改节点的访问控制策略。</td>
  </tr>
  <tr>
   <td><code>jcr:modifyProperties</code></td>
   <td>创建、修改和删除节点的属性。</td>
  </tr>
  <tr>
   <td><code>jcr:namespaceManagement</code></td>
   <td>注册、注销和修改命名空间定义。</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeDefinitionManagement</code></td>
   <td>将节点类型定义导入存储库。</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeManagement</code></td>
   <td>添加和删除mixin节点类型并更改节点的主节点类型。 这还包括对Node.addNode和XML导入方法的任何调用，其中显式指定了新节点的mixin或主要类型。</td>
  </tr>
  <tr>
   <td><code>jcr:readAccessControl</code></td>
   <td>读取节点的访问控制策略。</td>
  </tr>
  <tr>
   <td><code>jcr:removeChildNodes</code></td>
   <td>删除节点的子节点。</td>
  </tr>
  <tr>
   <td><code>jcr:removeNode</code></td>
   <td>删除节点。</td>
  </tr>
  <tr>
   <td><code>jcr:retentionManagement</code></td>
   <td>在节点上执行保留管理操作。</td>
  </tr>
  <tr>
   <td><code>jcr:versionManagement</code></td>
   <td>在节点上执行版本控制操作。</td>
  </tr>
  <tr>
   <td><code>jcr:workspaceManagement</code></td>
   <td>通过JCR API创建和删除工作区。</td>
  </tr>
  <tr>
   <td><code>jcr:write</code></td>
   <td>这是一个聚合权限，其中包含：<br /> - jcr：modifyProperties<br /> - jcr：addChildNodes<br /> - jcr：removeNode<br /> - jcr：removeChildNodes</td>
  </tr>
  <tr>
   <td><code>rep:privilegeManagement</code></td>
   <td>注册新权限。</td>
  </tr>
 </tbody>
</table>

### 注册新权限 {#registering-new-privileges}

您还可以注册新权限：

1. 在工具栏中，选择 **工具**，则 **权限** 显示当前注册的权限。

   ![ac_privileges](assets/ac_privileges.png)

1. 使用 **注册权限** 图标(**+**)，以便您可以定义权限：

   ![ac_privilegeregister](assets/ac_privilegeregister.png)

1. 单击 **确定** 以保存。 该权限现在可供选择。

### 添加访问控制条目 {#adding-an-access-control-entry}

1. 选择您的资源并打开 **访问控制** 选项卡。

1. 添加新的 **本地访问控制策略**，单击 **+** 图标（位于右侧） **适用的访问控制策略** 列表：

   ![crx_accesscontrol_applicable](assets/crx_accesscontrol_applicable.png)

1. 新条目将显示在 **本地访问控制策略：**

   ![crx_accesscontrol_newlocal](assets/crx_accesscontrol_newlocal.png)

1. 单击 **+** 图标，以添加条目：

   ![crx_accesscontrol_addentry](assets/crx_accesscontrol_addentry.png)

   >[!NOTE]
   >
   >当前需要一种解决方法来指定空字符串。
   >
   >为此，您必须使用 `""`.

1. 定义您的访问控制策略，然后单击 **确定** 以保存。 您的新策略为：

   * 列在 **本地访问控制策略**
   * 更改反映在 **有效的访问控制策略**.

CRX将验证您的选择；对于给定主体，给定节点上最多（一个）存在拒绝和一个允许条目。 该实施始终会清除冗余条目，并确保允许条目和拒绝条目中未列出相同的权限。

### 订购本地访问控制策略 {#ordering-local-access-control-policies}

列表中的顺序指示应用策略的顺序。

1. 在表中 **本地访问控制策略**，选择所需的条目并将其拖动到表中的新位置。

   ![crx_accesscontrol_reorder](assets/crx_accesscontrol_reorder.png)

1. 这些更改会显示在以下两个表中： **本地** 和 **有效的访问控制策略**.

### 删除访问控制策略 {#removing-an-access-control-policy}

1. 在表中 **本地访问控制策略**，单击条目右侧的红色图标(-)。
1. 该条目将从以下两个表中删除 **本地** 和 **有效的访问控制策略**.

### 测试访问控制策略 {#testing-an-access-control-policy}

1. 从CRXDE Lite工具栏中，选择 **工具**，则 **测试访问控制……**.
1. 将在右上角窗格中打开一个新对话框。 选择 **路径** 和/或 **主体** 要测试的对象。
1. 单击 **测试** 要查看所选内容的结果，请执行以下操作：

   ![crx_accesscontrol_test](assets/crx_accesscontrol_test.png)
