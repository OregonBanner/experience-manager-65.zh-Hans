---
title: 使用CRXDE Lite进行开发
seo-title: Developing with CRXDE Lite
description: CRXDE Lite已嵌入到AEM中，可让您在浏览器中执行标准开发任务
seo-description: CRXDE Lite is embedded into AEM and enables you to perform standard development tasks in the browser
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 2%

---

# 使用CRXDE Lite进行开发{#developing-with-crxde-lite}

本节介绍如何使用CRXDE Lite开发AEM应用程序。

有关可用的不同开发环境的更多信息，请参阅概述文档。

CRXDE Lite会嵌入到AEM中，使您能够在该浏览器中执行标准开发任务。 使用CRXDE Lite，您可以在日志记录时创建项目、创建和编辑文件(如.jsp和.java)、文件夹、模板、组件、对话框、节点、属性和捆绑包。
在以下情况下建议使用CRXDE Lite：无法直接访问AEM服务器，通过扩展或修改现成的组件和Java捆绑包来开发应用程序，或者不需要专门的Debugger、代码完成和语法突出显示。

>[!NOTE]
>
>从AEM 6.5.5.0开始，无法再匿名访问CRXDE Lite。
>用户将被重定向到登录屏幕。


>[!NOTE]
>
>建议使用 [适用于Eclipse的AEM开发人员工具](/help/sites-developing/aem-eclipse.md) 和 [AEM HTL Brackets扩展](/help/sites-developing/aem-brackets.md) 在项目开发期间。

## CRXDE Lite快速入门 {#getting-started-with-crxde-lite}

要开始使用CRXDE Lite，请按照以下步骤操作：

1. 安装AEM。
1. 在浏览器中，输入 `https://<host>:<port>/crx/de`. 默认情况下，这是 `https://localhost:4502/crx/de`。
1. 输入您的 **用户名** 和 **密码**. 默认情况下，它为 `admin` 和 `admin`.

1. 单击&#x200B;**确定**。

CRXDE Lite用户界面在浏览器中如下所示：

![chlimage_1-18](assets/crx-interface.jpg)

您现在可以使用CRXDE Lite来开发应用程序。

## 用户界面概述 {#overview-of-the-user-interface}

CRXDE Lite提供以下功能：

<table>
 <tbody>
  <tr>
   <td>顶部切换器栏</td>
   <td>允许您在CRXDE Lite、包管理器和包共享之间快速切换。</td>
  </tr>
  <tr>
   <td>节点路径小组件</td>
   <td><p>显示当前选定节点的路径。</p> <p>也可以使用它跳转到节点，方法是手动输入路径，或从其他位置粘贴路径，然后按回车键。</p> <p>它还支持查找具有特定节点名称的节点。 输入要查找的节点的名称，然后等待（或点击右侧的搜索符号）。 您可以尝试输入，例如，字符串 <em>Oak</em> 嵌入到构件中，以了解其工作原理。 如果将给定节点加载到资源管理器窗格中，将显示列表，您可以选择路径并按Enter导航到它。 请注意，它仅适用于浏览器中当前加载到CRXDE客户端应用程序的节点。 如果要搜索整个存储库，请使用工具，然后使用查询。</p> </td>
  </tr>
  <tr>
   <td>资源管理器窗格</td>
   <td><p>显示存储库中所有节点的树。</p> <p>单击某个节点，将其属性显示在 <strong>属性</strong> 选项卡。 单击节点后，您可以在工具栏中选择操作。 再次单击该节点可对其进行重命名。</p> <p>树导航过滤器（双目图标）：用于过滤存储库中名称包含输入文本的节点。 它仅适用于已在本地加载的节点。<br /> </p> </td>
  </tr>
  <tr>
   <td>编辑窗格</td>
   <td><p><strong>主页</strong> 选项卡：允许您搜索内容和/或文档，并访问开发人员资源（文档、开发人员博客、知识库）和支持(Adobe主页和支持中心)。<br /> </p> <p>双击 <strong>资源管理器</strong> 窗格以显示其内容；例如.jsp或.java文件。 然后，您可以修改它并保存更改。</p> <p>在中编辑文件后 <strong>编辑</strong> 工具栏上提供了以下工具：<br /> </p> - <strong>在树中显示： </strong>在存储库树中显示文件。<br /> - <strong>搜索/替换……</strong>：执行搜索或替换。<br /> <br /> 双击的状态行 <strong>编辑</strong> 窗格打开 <strong>转到行</strong> 对话框，以便您可以输入要转至的特定行号。<br /> </td>
  </tr>
  <tr>
   <td>“属性”选项卡<br /> </td>
   <td>显示所选节点的属性。 您可以添加新属性或删除现有属性。<br /> </td>
  </tr>
  <tr>
   <td>“访问控制”选项卡</td>
   <td><p>根据当前路径、存储库级别或主体显示权限。</p> <p>权限划分为</p> <p>- <strong>适用的访问控制策略</strong>：可应用于当前选择的策略。</p> <p>- <strong>本地访问控制策略</strong>：当前策略在本地应用于当前选择。</p> <p>- <strong>有效的访问控制策略</strong>：应用于当前选择的当前策略，可以在本地设置或从父节点继承。</p> <p>注意. 为了能够查看访问控制信息，登录到CRXDE Lite的用户必须有权读取ACL条目。 匿名用户默认看不到此信息 — 请以管理员身份登录以查看此信息。</p> </td>
  </tr>
  <tr>
   <td>“复制”选项卡</td>
   <td><p>显示当前节点的复制状态。 您可以复制和复制删除当前节点。</p> </td>
  </tr>
  <tr>
   <td>控制台选项卡<br /> </td>
   <td><p><strong>服务器日志</strong>:</p> <p>显示日志消息。 您可以配置日志级别、清除控制台、固定到选定的滚动位置，以及启用/禁用消息的显示。<br /> </p> <p><strong>版本控制</strong>:</p> <p>显示版本控制消息。<br /> </p> </td>
  </tr>
  <tr>
   <td>“生成信息”选项卡<br /> </td>
   <td>在生成捆绑包时显示信息。<br /> </td>
  </tr>
  <tr>
   <td>刷新<br /> </td>
   <td>刷新当前选择。 来自其他用户的更改将在您存储库的视图中更新。 您所做的更改不会受到影响。<br /> </td>
  </tr>
  <tr>
   <td>全部保存</td>
   <td><p><strong>全部保存</strong>:<br /> </p> <p>保存所做的所有更改。 在单击“保存”之前，更改是临时的，当您退出控制台时，这些更改将丢失。</p> <p><strong>还原</strong>:</p> <p>丢弃自上次保存操作以来在选定节点上所做的所有更改，然后重新加载选定节点的存储库的当前状态。</p> <p><strong>全部恢复</strong>:</p> <p>丢弃自上次保存操作以来在整个存储库中所做的所有更改，然后重新加载存储库的当前状态。</p> </td>
  </tr>
  <tr>
   <td>创建 ...<br /> </td>
   <td><p>下拉菜单，用于在所选节点下创建以下内容：<br /> </p> <p>- <strong>节点</strong>：具有任意节点类型的节点<br /> </p> <p>- <strong>文件</strong>： nt：file节点及其nt：resource子节点</p> <p>- <strong>文件夹</strong>： nt：folder节点</p> <p>- <strong>模板</strong>： AEM模板</p> <p>- <strong>组件</strong>： AEM组件</p> <p>- <strong>对话框</strong>：AEM对话框</p> </td>
  </tr>
  <tr>
   <td>删除<br /> </td>
   <td>删除选定的节点。<br /> </td>
  </tr>
  <tr>
   <td>复制</td>
   <td>复制所选节点。<br /> </td>
  </tr>
  <tr>
   <td>粘贴<br /> </td>
   <td>将复制的节点粘贴到所选节点下。<br /> </td>
  </tr>
  <tr>
   <td>移动 ...<br /> </td>
   <td>将所选节点移动到通过对话框设置的节点。</td>
  </tr>
  <tr>
   <td>重命名 ...<br /> </td>
   <td>重命名选定的节点。<br /> </td>
  </tr>
  <tr>
   <td>Mixin...<br /> </td>
   <td>用于向节点类型添加mixin类型。 mixin类型主要用于向节点添加高级功能，例如版本控制、访问控制、引用和锁定。</td>
  </tr>
  <tr>
   <td>工具<br /> </td>
   <td><p>下拉菜单包含以下工具：</p> <p>- <strong>服务器配置……</strong>：用于访问Felix控制台。</p> <p>- <strong>查询……</strong>：查询存储库。</p> <p>- <strong>权限……</strong>：打开权限管理，您可以在其中查看和添加权限。</p> <p>- <strong>测试访问控制……</strong>：您可以在此处测试特定路径和/或主体的权限。</p> <p>- <strong>导出节点类型</strong>：将系统中的节点类型导出为cnd表示法。</p> <p>- <strong>导入节点类型……</strong>：使用cnd表示法导入节点类型。</p> <p>- <strong>安装SiteCatalyst调试器……</strong>：有关如何安装Analytics Debugger的说明。</p> </td>
  </tr>
  <tr>
   <td>登录构件<br /> </td>
   <td><p>显示当前登录的用户及其登录的工作区，例如admin@crx.default。</p> <p>单击以登录或以特定用户身份重新登录。 如果您没有指定要登录的工作区，则将登录到默认工作区crx.default。</p> <p>如果要以匿名用户身份浏览存储库，请使用 <strong>匿名</strong> ，以及任何密码（例如，空格或点）。<br /> </p> <p>如果您的授权不再有效（例如，已过期），则登录构件会显示"<strong>未授权 — 登录……</strong>“。 单击以再次登录。</p> </td>
  </tr>
 </tbody>
</table>

## 创建文件夹 {#creating-a-folder}

要创建具有CRXDE Lite的文件夹，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要在其下创建新文件夹的文件夹，然后选择 **创建……**，则 **创建文件夹……**.

1. 输入文件夹 **名称** 并单击 **确定**.

1. 单击 **全部保存** 以保存服务器上的更改。

## 创建模板 {#creating-a-template}

要创建具有CRXDE Lite的模板，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建模板的文件夹，然后选择 **创建……**，则 **创建模板……**.

1. 输入 **标签**， **标题**， **描述**， **资源类型** 和 **排名** 模板的。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置 **允许的路径**. 单击 **下一个**

1. 此步骤是可选的：设置 **允许的父项**. 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置 **允许的子项**. 单击&#x200B;**确定**。

1. 单击 **全部保存** 以保存服务器上的更改。

它会创建：

* 类型的节点 `cq:Template` 具有模板属性

* 类型的子节点 `cq:PageContent` 具有页面内容属性

您可以将属性添加到模板中：请参阅 [创建资产](#creating-a-property) 部分。

## 创建组件 {#creating-a-component}

此处介绍的功能仅在安装了CQ5时可用，即节点类型时 `cq:Component` 在存储库中可用。

要创建具有CRXDE Lite的组件，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建该组件的文件夹，然后选择 **创建……**，则 **创建组件……**.

1. 输入 **标签**， **标题**， **描述**， **超级资源类型** 和 **组** 组件的。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性 **是容器，** **无修饰**， **单元格名称** 和 **对话框路径**. 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性 **允许的父项**. 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性 **允许的子项**. 单击&#x200B;**确定**。

1. 单击 **全部保存** 以保存服务器上的更改。

它会创建：

* 类型的节点 `cq:Component`
* 组件属性
* 组件.jsp脚本

## 创建对话框 {#creating-a-dialog}

要创建带有CRXDE Lite的对话框，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建对话框的组件，然后选择 **创建……**，则 **创建对话框……**.

1. 输入 **标签** 和 **标题**. 单击&#x200B;**确定**。

1. 单击 **全部保存** l将更改保存到服务器上。

它创建一个具有以下结构的对话框：

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

您现在可以通过修改属性或创建新节点来调整对话框，以符合您的需求。

也可以使用对话框编辑器编辑对话框。 双击CRXDE Lite中的对话框节点将打开编辑器。 可以找到有关对话框编辑器的更多信息 [此处](/help/sites-developing/dialog-editor.md).

## 创建节点 {#creating-a-node}

要创建具有CRXDE Lite的节点，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建新节点的节点，然后选择 **创建……**，则 **创建节点……**.
1. 输入 **名称** 和 **类型**. 单击&#x200B;**确定**。
1. 单击 **全部保存** 以保存服务器上的更改。

您现在可以通过修改属性或创建新节点来调整节点，以满足您的需求。

>[!NOTE]
>
>大多数编辑操作（包括“创建节点”）会将所有更改保存在内存中，并且仅在保存时将其存储在存储库中（通过“全部保存”按钮）。 但是，某些操作（如移动）会自动保留。
>
>在保存更改时，JCR存储库还会首先执行关于父节点的节点类型是否允许新创建的节点的验证。 如果在保存节点时收到错误消息，请检查内容结构是否有效(例如，您无法创建 `nt:unstructured` 作为子节点的节点 `nt:folder` 节点)。

## 创建资产 {#creating-a-property}

要创建具有CRXDE Lite的资产，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在“导航”窗格中，选择要添加新属性的节点。
1. 在 **属性** 选项卡，输入 **名称**，则 **类型** 和 **值**. 单击 **添加**.

1. 单击 **全部保存** 以保存服务器上的更改。

## 创建脚本 {#creating-a-script}

要创建新脚本，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 在导航窗格中，右键单击要创建脚本的组件，选择 **创建……**，则 **创建文件……**.

1. 输入文件 **名称** 包括其扩展。 单击&#x200B;**确定**。

1. 新文件在“编辑”窗格中作为选项卡打开。
1. 编辑文件。
1. 单击 **全部保存** 以保存更改。

## 导出和导入节点类型 {#exporting-and-importing-node-types}

利用CRXDE Lite，您可以在中导入和/或导出节点类型定义 [CND（压缩命名空间和节点类型定义）表示法](https://jackrabbit.apache.org/jcr/node-type-notation.html).

要导出节点类型定义，请执行以下操作：

1. 在浏览器中打开CRXDE Lite。
1. 选择所需的节点。
1. 选择 **工具** 则 **导出节点类型**.

1. 以符号表示的定义将显示在浏览器中。 如果需要，请保存信息。

导入节点类型定义：

1. 在浏览器中打开CRXDE Lite。
1. 选择 **工具** 则 **导入节点类型……**.

1. 在文本框中输入定义的CND表示法。
1. Check **允许更新** 如果要更新现有定义，请执行以下操作。
1. 单击 **导入**.

## 日志记录 {#logging}

通过CRXDE Lite，您可以显示文件 `error.log` 位于以下位置的文件系统上的 `<crx-install-dir>/crx-quickstart/server/logs` 并使用适当的日志级别进行筛选。 按照以下步骤操作：

1. 在浏览器中打开CRXDE Lite。
1. 在 **控制台** 选项卡，在窗口底部的下拉菜单中，选择 **服务器日志**.

1. 单击 **停止** 图标来显示消息。

您可以：

* 在Felix控制台中通过单击 **日志记录配置** 图标。
* 通过单击 **画笔** 图标。
* 通过单击 **固定** 图标。
* 通过单击 **停止** 图标。

## 访问控制 {#access-control}

>[!NOTE]
>
>参见 [用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md) 了解更多信息。
