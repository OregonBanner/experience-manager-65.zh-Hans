---
title: 使用CRXDE Lite进行开发
seo-title: 使用CRXDE Lite进行开发
description: CRXDE Lite已嵌入到AEM中，使您能够在浏览器中执行标准开发任务
seo-description: CRXDE Lite已嵌入到AEM中，使您能够在浏览器中执行标准开发任务
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: cb141914428f42a9755b5479ab1652c8ca51f640
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 5%

---


# 使用CRXDE Lite进行开发{#developing-with-crxde-lite}

本节介绍如何使用CRXDE Lite开发AEM应用程序。

请参阅概述文档，进一步了解可用的不同开发环境。

CRXDE Lite已嵌入到AEM中，允许您在浏览器中执行标准开发任务。 使用CRXDE Lite，您可以在记录时创建项目、创建和编辑文件（如。jsp和。java）、文件夹、模板、组件、对话框、节点、属性和捆绑。
当您无法直接访问AEM服务器、通过扩展或修改现成组件和Java包开发应用程序时，或者您不需要专用调试器、代码完成和语法突出显示时，建议使用CRXDE Lite。

>[!NOTE]
>
>从AEM 6.5.5.0开始，不再能够匿名访问CRXDE Lite。
>用户将被重定向到登录屏幕。


>[!NOTE]
>
>建议在项目开发 [过程中使用Eclipse的AEM](/help/sites-developing/aem-eclipse.md) Developer [Tools和AEM HTL Brackets Extension](/help/sites-developing/aem-brackets.md) 。

## CRXDE Lite快速入门 {#getting-started-with-crxde-lite}

要开始使用CRXDE Lite，请按照以下步骤继续：

1. 安装AEM。
1. 在您的浏览器中，输入 `https://<host>:<port>/crx/de`。 默认情况下为 `https://localhost:4502/crx/de`。
1. 输入您 **的用** 户名 **和密码**。 默认情况下，它为 `admin` 和 `admin`。

1. 单击&#x200B;**确定**。

CRXDE Lite用户界面在您的浏览器中如下所示：

![chlimage_1-18](assets/crx-interface.jpg)

您现在可以使用CRXDE Lite开发应用程序。

## 用户界面概述 {#overview-of-the-user-interface}

CRXDE Lite优惠以下功能：

<table>
 <tbody>
  <tr>
   <td>顶部切换器栏</td>
   <td>允许您在CRXDE Lite、Package Manager和Package Share之间快速切换。</td>
  </tr>
  <tr>
   <td>节点路径构件</td>
   <td><p>显示当前选定节点的路径。</p> <p>您还可以使用它跳转至节点，方法是手工输入路径，或从其他位置粘贴路径并点击Enter。</p> <p>它还支持查找具有特定节点名称的节点。 输入要查找的节点的名称，然后等待（或点击右侧的搜索符号）。 您可以尝试输入，例如，将字符串 <em>oak</em> 输入构件中，了解其工作方式。 如果给定的节点或节点加载到资源管理器窗格中，则将显示列表，您可以选择路径并按Enter导航到该路径。 请注意，它仅适用于浏览器中当前加载到CRXDE客户端应用程序中的节点。 如果要搜索整个存储库，请使用工具，然后查询。</p> </td>
  </tr>
  <tr>
   <td>资源管理器窗格</td>
   <td><p>显示存储库中所有节点的树。</p> <p>单击某个节点以在“属性”选项卡中显 <strong>示其</strong> 属性。 单击某个节点后，您可以在工具栏中选择操作。 再次单击该节点以对其进行重命名。</p> <p>树形导航滤镜（双目图标）: 允许您过滤名称包含输入文本的存储库中的节点。 它仅适用于已本地加载的节点。<br /> </p> </td>
  </tr>
  <tr>
   <td>编辑窗格</td>
   <td><p><strong>“主页</strong> ”选项卡： 允许您搜索内容和／或文档，访问开发人员资源（文档、开发人员博客、知识库）和支持（Adobe主页和支持中心）。<br /> </p> <p>多次在“资源管理器”窗格 <strong>中单击</strong> 某个文件以显示其内容； 例如。jsp或。java文件。 然后，您可以修改它并保存更改。</p> <p>在“编辑”窗格中编辑文 <strong>件</strong> 后，工具栏中会显示以下工具：<br /> </p> -在 <strong>树中显示： </strong>显示存储库树中的文件。<br /> - <strong>搜索／替换。.</strong>. 进行搜索或替换。<br /> <br /> 多次单击“编辑”窗格的状 <strong>态行</strong> ，打开“ <strong>转到行</strong> ”对话框，以便输入要转到的特定行号。<br /> </td>
  </tr>
  <tr>
   <td>“属性”选项卡<br /> </td>
   <td>显示您选择的节点的属性。 您可以添加新属性或删除现有属性。<br /> </td>
  </tr>
  <tr>
   <td>访问控制选项卡</td>
   <td><p>根据当前路径、存储库级别或主体显示权限。</p> <p>权限被分为</p> <p>-适 <strong>用访问控制策略</strong>: 可应用于当前选择的策略。</p> <p>-本 <strong>地访问控制策略</strong>: 当前策略已本地应用于当前选择。</p> <p>-有效 <strong>的访问控制政策</strong>: 可以在本地设置或从父节点继承当前选择应用的当前策略。</p> <p>注意. 要能够查看访问控制信息，登录到CRXDE Lite的用户必须具有读取ACL条目的权限。 默认情况下，匿名用户无法看到此信息——请以管理员等身份登录以查看该信息。</p> </td>
  </tr>
  <tr>
   <td>复制选项卡</td>
   <td><p>显示当前节点的复制状态。 您可以复制和复制删除当前节点。</p> </td>
  </tr>
  <tr>
   <td>控制台选项卡<br /> </td>
   <td><p><strong>服务器日志</strong>:</p> <p>显示日志消息。 您可以配置日志级别、清除控制台、固定到所选滚动位置并启用／禁用消息显示。<br /> </p> <p><strong>版本控制</strong>:</p> <p>显示版本控制消息。<br /> </p> </td>
  </tr>
  <tr>
   <td>“生成信息”选项卡<br /> </td>
   <td>在构建捆绑时显示信息。<br /> </td>
  </tr>
  <tr>
   <td>刷新<br /> </td>
   <td>刷新当前选择。 在存储库的视图中，将更新来自其他用户的更改。 您所做的更改不会受到影响。<br /> </td>
  </tr>
  <tr>
   <td>全部保存</td>
   <td><p><strong>全部保存</strong>:<br /> </p> <p>保存您所做的所有更改。 在单击“保存”之前，这些更改是临时的，当您退出控制台时将丢失。</p> <p><strong>还原</strong>:</p> <p>放弃自上次保存操作以来在选定节点上所做的所有更改，然后重新加载选定节点的存储库的当前状态。</p> <p><strong>全部恢复</strong>:</p> <p>放弃自上次保存操作以来在整个存储库中所做的所有更改，然后重新加载存储库的当前状态。</p> </td>
  </tr>
  <tr>
   <td>创建 ...<br /> </td>
   <td><p>用于在选定节点下创建以下内容的下拉菜单：<br /> </p> <p>-节 <strong>点</strong>: 具有任意节点类型的节点<br /> </p> <p>-文 <strong>件</strong>: nt：文件节点及其nt：资源子节点</p> <p>-文 <strong>件夹</strong>: nt：文件夹节点</p> <p>-模 <strong>板</strong>: AEM模板</p> <p>-组 <strong>件</strong>: AEM组件</p> <p>-对 <strong>话框</strong>: AEM对话框</p> </td>
  </tr>
  <tr>
   <td>删除<br /> </td>
   <td>删除所选节点。<br /> </td>
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
   <td>将选定节点移动到通过对话框设置的节点。</td>
  </tr>
  <tr>
   <td>重命名 ...<br /> </td>
   <td>重命名所选节点。<br /> </td>
  </tr>
  <tr>
   <td>Mixin...<br /> </td>
   <td>允许您向节点类型添加混音类型。 混合类型主要用于向节点添加高级功能，如版本控制、访问控制、引用和锁定。</td>
  </tr>
  <tr>
   <td>工具<br /> </td>
   <td><p>下拉菜单，包含以下工具：</p> <p>-服 <strong>务器配置。.</strong>. 访问Felix控制台。</p> <p>- <strong>查询..</strong>. 查询存储库。</p> <p>- <strong>特权。.</strong>: 打开权限管理，在这里您可以视图和添加权限。</p> <p>-测 <strong>试访问控制...</strong>: 可在其中测试特定路径和／或主体权限的位置。</p> <p>-导 <strong>出节点类型</strong>: 将系统中的节点类型导出为cnd记号。</p> <p>-导 <strong>入节点类型……</strong>: 使用cnd记号导入节点类型。</p> <p>-安 <strong>装SiteCatalyst调试器……</strong>: 关于如何安装Analytics调试器的说明。</p> </td>
  </tr>
  <tr>
   <td>登录构件<br /> </td>
   <td><p>显示当前登录的用户及其登录的工作区，例如admin@crx.default。</p> <p>单击它以特定用户身份登录或重新登录。 如果未指定要登录的工作区，则将登录到默认工作区crx.default。</p> <p>如果要以匿名用户身份浏览存储库 <strong></strong> ，请使用匿名作为登录名和任何口令（例如空格或点）。<br /> </p> <p>如果您的授权不再有效（例如，该授权已过期），则登录小部件会显示“未<strong>授权——登录。.</strong>”。 单击它以重新登录。</p> </td>
  </tr>
 </tbody>
</table>

## Creating a Folder {#creating-a-folder}

使用CRXDE Lite创建文件夹：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要在其下创建新文件夹的文件夹，选 **择创建……**，然后 **选择创建文件夹……**.

1. 输入文件夹 **名称** ，然后单 **击确定**。

1. 单击 **“全部保** 存”以在服务器上保存更改。

## Creating a Template {#creating-a-template}

要使用CRXDE Lite创建模板，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要创建模板的文件夹，选择创 **建……**，然后 **选择创建模板……**.

1. 输入标 **签**、标 **题**、说 **明**、资 **源类型和****** 类型模板。 单击&#x200B;**下一步**。

1. 此步骤是可选的： 设置允 **许路径**。 Click **Next**

1. 此步骤是可选的： 设置“允 **许的父项**”。 单击&#x200B;**下一步**。

1. 此步骤是可选的： 设置“允 **许的子项**”。 单击&#x200B;**确定**。

1. 单击 **“全部保** 存”以在服务器上保存更改。

它创建：

* 具有模板属性 `cq:Template` 的节点类型

* 具有页面内容属性 `cq:PageContent` 的子节点

您可以向模板添加属性： 请参阅创 [建属性部分](#creating-a-property) 。

## 创建组件 {#creating-a-component}

此处描述的功能仅在安装了CQ5(即，节点类型在存储库中 `cq:Component` 可用)时可用。

要使用CRXDE Lite创建组件，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要创建组件的文件夹，选择创 **建……,**&#x200B;然后 **选择创建组件……**.

1. 输入 **Label**、Title **、Description**、 **Super Type** Resource **of the****** Super Type Group组件。 单击&#x200B;**下一步**。

1. 此步骤是可选的： 设置组件属性 **为容器、无** 装饰 **、单**&#x200B;元格名 **称** 和对 **话路径**。 单击&#x200B;**下一步**。

1. 此步骤是可选的： 设置组件属性“允 **许父项”**。 单击&#x200B;**下一步**。

1. 此步骤是可选的： 设置组件属性“允 **许子项”**。 单击&#x200B;**确定**。

1. 单击 **“全部保** 存”以在服务器上保存更改。

它创建：

* 类型的节点 `cq:Component`
* 组件属性
* 组件。jsp脚本

## 创建对话框 {#creating-a-dialog}

要使用CRXDE Lite创建对话框，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要创建对话框的组件，选择创 **建……**，然 **后选择创建对话框……**.

1. 输入 **标签** 和标 **题**。 单击&#x200B;**确定**。

1. 单击 **“**&#x200B;全部保存”以在服务器上保存更改。

它创建具有以下结构的对话框：

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

您现在可以修改属性或创建新节点，从而根据您的需要调整对话框。

还可以使用对话框编辑器编辑对话框。 多次单击CRXDE Lite中的对话框节点将显示编辑器。 有关对话框编辑器的更多信息，请 [访问](/help/sites-developing/dialog-editor.md)。

## 创建节点 {#creating-a-node}

要使用CRXDE Lite创建节点，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要创建新节点的节点，选择创 **建……**，然后 **选择创建节点……**.
1. 输入 **名称** 和类 **型**。 单击&#x200B;**确定**。
1. 单击 **“全部保** 存”以在服务器上保存更改。

您现在可以修改属性或创建新节点，从而根据您的需要调整节点。

>[!NOTE]
>
>大多数编辑操作（包括创建节点）都保留内存中的所有更改，并且只在保存后（通过“全部保存”按钮）将其存储到存储库中。 但是，某些操作（如移动）会自动保留。
>
>在保存更改时，JCR存储库还首先执行有关新创建的节点是否允许父节点的节点类型的验证。 如果您在保存节点时收到错误消息，请检查内容结构是否有效(例如，您不能将节 `nt:unstructured` 点创建为节点的子 `nt:folder` 节点)。

## 创建属性 {#creating-a-property}

要使用CRXDE Lite创建属性，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，选择要添加新属性的节点。
1. 在底部窗 **格的** “属性”选项卡中，输 **入名称**、类 **型****和**&#x200B;值。 单击&#x200B;**添加**。

1. 单击 **“全部保** 存”以在服务器上保存更改。

## 创建脚本 {#creating-a-script}

要创建新脚本，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要创建脚本的组件，选择创 **建……**，然后 **选择创建文件……**.

1. 输入“文件 **名** ”（包括其扩展名）。 单击&#x200B;**确定**。

1. 新文件将作为选项卡在“编辑”窗格中打开。
1. 编辑文件。
1. Click **Save All** to save the changes.

## 导出和导入节点类型 {#exporting-and-importing-node-types}

使用CRXDE Lite，您可以导入和／或导出CND(紧凑命名空间和节 [点类型定义)记号中的节点类型定](https://jackrabbit.apache.org/jcr/node-type-notation.html)义。

要导出节点类型定义，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 选择所需节点。
1. 选择 **工具** , **然后选择导出节点类型**。

1. 定义（以cnd表示法）将显示在浏览器中。 根据需要保存信息。

要导入节点类型定义，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 选择 **工具** , **然后选择导入节点类型……**.

1. 在文本框中输入定义的CND记号。
1. 如果 **要更新** 现有定义，请选中“允许更新”。
1. 单击&#x200B;**导入**。

## 记录 {#logging}

使用CRXDE Lite，您可以显示文 `error.log` 件系统上的文件，并 `<crx-install-dir>/crx-quickstart/server/logs` 使用适当的日志级别对其进行筛选。 按如下方式继续：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在窗 **口底部** 的“控制台”选项卡中，在右侧的下拉菜单中，选择“服务器 **日志”**。

1. Click the **Stop** icon to display the messages.

您可以：

* 单击“日志记录配置”图标，在Felix控制台中调 **整日志参** 数。
* 单击“画笔”图标以清 **除消息** 。
* 通过单击“固定”图标将消息固定在当前 **选** 择中。
* 通过单击“停止”图标启用或禁用消息 **的显** 示。

## 访问控制 {#access-control}

>[!NOTE]
>
>有关 [详细信息，请参阅用户、组](/help/sites-administering/user-group-ac-admin.md) 和访问权限管理。
