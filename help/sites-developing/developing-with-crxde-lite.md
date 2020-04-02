---
title: 使用CRXDE Lite进行开发
seo-title: 使用CRXDE Lite进行开发
description: CRXDE Lite嵌入到AEM中，使您能在浏览器中执行标准开发任务
seo-description: CRXDE Lite嵌入到AEM中，使您能在浏览器中执行标准开发任务
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: 78133b41e1c99f8f86f4c0d51961287735423fe2

---


# 使用CRXDE Lite进行开发{#developing-with-crxde-lite}

本节介绍如何使用CRXDE Lite开发AEM应用程序。

请参阅概述文档，以了解有关可用的不同开发环境的更多信息。

CRXDE Lite嵌入到AEM中，允许您在浏览器中执行标准开发任务。 使用CRXDE Lite，您可以在登录和集成SVN时创建项目、创建和编辑文件（如。jsp和。java）、文件夹、模板、组件、对话框、节点、属性和捆绑包。
当您无法直接访问AEM服务器、通过扩展或修改现成组件和Java包来开发应用程序时，或者您不需要专用调试器、代码完成和语法高亮显示时，建议使用CRXDE Lite。

>[!NOTE]
>
>默认情况下，所有AEM用户都可以访问CRXDE Lite。 如果需要， [请为以下节点配置ACL](/help/sites-administering/security.md#permissions-and-acls) ，以便只有开发人员可以访问CRX DE Lite:
>
>`/libs/granite/crxde`

>[!NOTE]
>
>建议在项目开发 [过程中使用Eclipse的AEM Developer Tools](/help/sites-developing/aem-eclipse.md) 和 [AEM HTL Brackets Extension](/help/sites-developing/aem-brackets.md) 。

## CRXDE Lite快速入门 {#getting-started-with-crxde-lite}

要开始使用CRXDE Lite，请按如下步骤继续：

1. 安装AEM。
1. 在您的浏览器中，输入 `https://<host>:<port>/crx/de`。 默认情况下为 `https://localhost:4502/crx/de`。
1. 输入您的 **用户名** 和 **密码**。 默认情况下，它为 `admin` 和 `admin`。

1. 单击&#x200B;**确定**。

CRXDE Lite用户界面在您的浏览器中如下所示：

![chlimage_1-18](assets/chlimage_1-18.png)

您现在可以使用CRXDE Lite开发应用程序。

## 用户界面概述 {#overview-of-the-user-interface}

CRXDE Lite优惠了以下功能：

<table>
 <tbody>
  <tr>
   <td>顶部切换器栏</td>
   <td>允许您在CRXDE Lite、包管理器和包共享之间快速切换。</td>
  </tr>
  <tr>
   <td>节点路径构件</td>
   <td><p>显示当前选定节点的路径。</p> <p>您还可以使用它跳转至节点，方法是手动输入路径，或从其他位置粘贴路径，然后点击Enter。</p> <p>它还支持查找具有特定节点名称的节点。 输入要查找的节点的名称，然后等待（或点击右侧的搜索符号）。 您可以尝试在构件中输入字符串 <em>oak</em> ，以查看其工作方式。 如果给定节点或节点加载到资源管理器窗格中，则会显示列表，您可以选择路径并按Enter可导航到该路径。 请注意，它仅适用于浏览器中当前加载到CRXDE客户端应用程序中的节点。 如果要搜索整个存储库，请依次使用工具和查询。</p> </td>
  </tr>
  <tr>
   <td>资源管理器窗格</td>
   <td><p>显示存储库中所有节点的树。</p> <p>单击某个节点以在“属性”选项卡中显示其 <strong>属性</strong> 。 单击节点后，您可以在工具栏中选择操作。 再次单击该节点以将其重命名。</p> <p>树形导航滤镜（双目图标）:允许您过滤存储库中名称包含输入文本的节点。 它仅适用于已本地加载的节点。<br /> </p> </td>
  </tr>
  <tr>
   <td>编辑窗格</td>
   <td><p><strong>“主页</strong> ”选项卡：允许您搜索内容和／或文档，并访问开发人员资源（文档、开发人员博客、知识库）和支持（Adobe主页和支持中心）。<br /> </p> <p>多次在“资源管理器”( <strong>Explorer</strong> )窗格中单击文件以显示其内容；例如。jsp或。java文件。 然后，您可以修改它并保存更改。</p> <p>在“编辑”窗格中编辑文 <strong>件后</strong> ，工具栏上会显示以下工具：<br /> </p> -在 <strong>树中显示：显 </strong>示存储库树中的文件。<br /> -搜 <strong>索／替换……</strong>:执行搜索或替换。<br /> <br /> 多次单击“编辑 <strong></strong> ”窗格的状态行，打开“转到行 <strong></strong> ”对话框，以便输入要转到的特定行号。<br /> </td>
  </tr>
  <tr>
   <td>“属性”选项卡<br /> </td>
   <td>显示您选择的节点的属性。 您可以添加新属性或删除现有属性。<br /> </td>
  </tr>
  <tr>
   <td>访问控制选项卡</td>
   <td><p>根据当前路径、存储库级别或主体显示权限。</p> <p>权限分为</p> <p>-适用 <strong>的访问控制政策</strong>:可应用于当前选择的策略。</p> <p>-本 <strong>地访问控制政策</strong>:当前策略已本地应用于当前选择。</p> <p>-有效 <strong>的访问控制政策</strong>:可以在本地设置或从父节点继承当前选择应用的当前策略。</p> <p>注意. 要查看访问控制信息，登录到CRXDE Lite的用户必须具有读取ACL条目的权限。 默认情况下，匿名用户无法看到此信息——请以（例如，admin）身份登录以查看该信息。</p> </td>
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
   <td>“构建信息”选项卡<br /> </td>
   <td>在构建捆绑时显示信息。<br /> </td>
  </tr>
  <tr>
   <td>刷新<br /> </td>
   <td>刷新当前选择。 在存储库的视图中，将更新来自其他用户的更改。 您所做的更改不会受到影响。<br /> </td>
  </tr>
  <tr>
   <td>全部保存</td>
   <td><p><strong>全部保存</strong>:<br /> </p> <p>保存您所做的所有更改。 在单击“保存”之前，更改是临时的，当您退出控制台时，这些更改将丢失。</p> <p><strong>还原</strong>:</p> <p>放弃自上次保存操作以来对选定节点所做的所有更改，然后重新加载选定节点的存储库的当前状态。</p> <p><strong>全部恢复</strong>:</p> <p>放弃自上次保存操作以来在整个存储库中所做的所有更改，然后重新加载存储库的当前状态。</p> </td>
  </tr>
  <tr>
   <td>创建 ...<br /> </td>
   <td><p>用于在选定节点下创建以下内容的下拉菜单：<br /> </p> <p>-节 <strong>点</strong>:具有任意节点类型的节点<br /> </p> <p>-文 <strong>件</strong>:nt：文件节点及其nt：资源子节点</p> <p>-文 <strong>件夹</strong>:nt：文件夹节点</p> <p>-模 <strong>板</strong>:AEM模板</p> <p>-组 <strong>件</strong>:AEM组件</p> <p>-对 <strong>话框</strong>:AEM对话框</p> </td>
  </tr>
  <tr>
   <td>删除<br /> </td>
   <td>删除选定节点。<br /> </td>
  </tr>
  <tr>
   <td>复制</td>
   <td>复制选定节点。<br /> </td>
  </tr>
  <tr>
   <td>粘贴<br /> </td>
   <td>将复制的节点粘贴到选定节点下。<br /> </td>
  </tr>
  <tr>
   <td>移动 ...<br /> </td>
   <td>将选定节点移动到通过对话框设置的节点。</td>
  </tr>
  <tr>
   <td>重命名 ...<br /> </td>
   <td>重命名选定的节点。<br /> </td>
  </tr>
  <tr>
   <td>Mixin...<br /> </td>
   <td>允许您向节点类型添加混音类型。 混音类型主要用于向节点添加高级功能，如版本控制、访问控制、引用和锁定。</td>
  </tr>
  <tr>
   <td>团队<br /> </td>
   <td><p>执行标准版本控制任务的下拉菜单：</p> <p>-从 <strong>SVN服务器</strong> 更新存储库</p> <p>-将本 <strong>地更改</strong> 提交到SVN服务器</p> <p>-视图 <strong>当前节点</strong> 的状态</p> <p>-视图 <strong>当前节点的子树的递归状态</strong> 。</p> <p>-从 <strong>SVN服务器</strong> “签出”工作副本</p> <p>-从 <strong>SVN服务器</strong> （无需创建工作副本）导出项目</p> <p>-将 <strong>项目从存储库</strong> 导入到SVN服务器<br /> </p> <p>注意，您需要以具有足够权限的用户身份登录才能执行某些任务（特别是写入本地存储库的用户）。<br /> </p> </td>
  </tr>
  <tr>
   <td>工具<br /> </td>
   <td><p>下拉菜单中包含以下工具：</p> <p>-服 <strong>务器配置……</strong>:访问Felix控制台。</p> <p>- <strong>查询...</strong>:查询存储库。</p> <p>-权 <strong>限……</strong>:要打开权限管理，您可以在其中视图和添加权限。</p> <p>-测 <strong>试访问控制...</strong>:您可以在其中测试特定路径和／或主体权限的位置。</p> <p>-导 <strong>出节点类型</strong>:将系统中的节点类型作为cnd表示法导出。</p> <p>-导 <strong>入节点类型……</strong>:使用cnd记号导入节点类型。</p> <p>-安 <strong>装SiteCatalyst调试器……</strong>:有关如何安装Analytics Debugger的说明。</p> </td>
  </tr>
  <tr>
   <td>登录构件<br /> </td>
   <td><p>显示当前登录的用户及其登录的工作区，例如admin@crx.default。</p> <p>单击它以特定用户身份登录或重新登录。 如果未指定要登录的工作区，则将登录到默认工作区crx.default。</p> <p>如果要以匿名用户的身份浏览存储库，请使 <strong>用匿名</strong> ，作为登录名和任何密码（例如空格或点）。<br /> </p> <p>如果您的授权不再有效（例如，该授权已过期），则登录小部件会显示“未授<strong>权——登录。.</strong>”。 单击它以再次登录。</p> </td>
  </tr>
 </tbody>
</table>

## 创建项目 {#creating-a-project}

使用CRXDE Lite，只需单击三下即可创建工作项目。 项目向导将在以下位置创建新项 `/apps`目：t下的某些内 `/conten`容以及将所有项目内容打包在下的包 `/etc/packages`。 该项目可立即用于渲染示例页面，该示例页面显示 **Hello World**，该示例页面基于jsp脚本，该脚本从存储库中渲染属性并调用Java类来渲染某些文本。

使用CRXDE Lite创建项目：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击某个节点，选择创 **建……**，然后 **选择创建项目……**.
注意：您可以右键单击树导航中的任意节点，因为新项目节点是按设计在下面和下面创建 `/apps,` 的 `/content``/etc/packages`。

1. 定义：

   * **项目名称** -项目名称用于创建新节点和捆绑，例如 `myproject`.

   * **Java包** - Java包名前缀，例如 `com.mycompany`.

1. 单击&#x200B;**创建**。
1. 单击 **全部保存** ，以在服务器上保存更改。

要访问显示 **Hello World的示例页**&#x200B;面，请将您的浏览器指向：

`https://localhost:4502/content/<project-name>.html`

“ **Hello World** ”页面基于内容节点，该节点通过属性调用jsp脚 `sling:resourceType` 本。 该脚本从存储库 `jcr:title` 中读取该属性，并通过调用项目包中可用的SampleUtil类的方法获取正文内容。

将创建以下节点：

* `/apps/<project-name>`:应用程序容器。
* `/apps/<project-name>/components`:组件容器，包含用于呈现页面的示例html.jsp文件。

* `/apps/<project-name>/src`:包容器，包含示例项目包。

* `/apps/<project-name>/install`:编译的包容器，包含编译的示例项目包。
* `/content/<project-name>`:内容容器。
* /etc/packages/&lt;java-suffix>/&lt;project-name>.zip，包含所有项目应用程序和内容的包。 您可以使用它重新构建项目以进一步部署(例如，到其他环境)或通过包共享进行共享。

在CRXDE Lite中，该结构如下所示，其项目名为 **myproject** ，而java包后缀名为 **mycompany**:

![chlimage_1-19](assets/chlimage_1-19.png)

![chlimage_1-20](assets/chlimage_1-20.png)

## Creating a Folder {#creating-a-folder}

要使用CRXDE Lite创建文件夹，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要在其下创建新文件夹的文件夹，选择创建…… **，然后****选择创建文件夹……**.

1. 输入文件夹 **名称** ，然后单 **击确定**。

1. 单击 **全部保存** ，以在服务器上保存更改。

## Creating a Template {#creating-a-template}

要使用CRXDE Lite创建模板，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建模板的文件夹，选择创建…… **，然后****选择创建模板……**.

1. 输入 **Title**, Title **, Description**, **Resource of the Type Label and********** Ringing Of the The Label模板。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置“允 **许的路径”**。 Click **Next**

1. 此步骤是可选的：设置“允 **许的父母”**。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置“允 **许的子项”**。 单击&#x200B;**确定**。

1. 单击 **全部保存** ，以在服务器上保存更改。

它创建：

* 具有“模板”属性 `cq:Template` 的类型节点

* 具有页面内容属性的类 `cq:PageContent` 型的子节点

您可以向模板中添加属性：请参阅创 [建属性部分](#creating-a-property) 。

## 创建组件 {#creating-a-component}

此处描述的功能仅在安装了CQ5（即，如果节点类型在存储库中可用） `cq:Component` 时可用。

要使用CRXDE Lite创建组件，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要创建组件的文件夹，选择创 **建……**，然后 **选择创建组件……**.

1. 输入Label **、Title**、Description **、** Super Resources of the Label **、Title**、Description ******** 、Super Type Group Component。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性 **Is容器、** No Decoration **、** Name **和Dialog Path** (对 ****&#x200B;话路径)。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性“允 **许的父项**”。 单击&#x200B;**下一步**。

1. 此步骤是可选的：设置组件属性“允 **许的子项**”。 单击&#x200B;**确定**。

1. 单击 **全部保存** ，以在服务器上保存更改。

它创建：

* 类型的节点 `cq:Component`
* 组件属性
* 组件。jsp脚本

## 创建对话框 {#creating-a-dialog}

要使用CRXDE Lite创建对话框，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要创建对话框的组件，选择创 **建……**，然后 **选择创建对话框……**.

1. 输入标 **签** 和标 **题**。 单击&#x200B;**确定**。

1. 单击 **“**&#x200B;全部保存”以在服务器上保存更改。

它创建一个具有以下结构的对话框：

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

您现在可以通过修改属性或创建新节点来调整对话框以满足您的需求。

您还可以使用对话框编辑器编辑对话框。 多次在CRXDE Lite中单击对话框节点将显示编辑器。 有关对话框编辑器的更多信息，请访 [问](/help/sites-developing/dialog-editor.md)。

## 创建节点 {#creating-a-node}

要使用CRXDE Lite创建节点，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在导航窗格中，右键单击要创建新节点的节点，选择创建…… **，然后****选择创建节点……**.
1. 输入名 **称** 和类 **型**。 单击&#x200B;**确定**。
1. 单击 **全部保存** ，以在服务器上保存更改。

您现在可以通过修改属性或创建新节点来调整节点以满足您的需求。

>[!NOTE]
>
>大多数编辑操作（包括创建节点）都会保留内存中的所有更改，并且只会在保存后将其存储到存储库中（通过“全部保存”按钮）。 但是，某些操作（如移动）会自动保留。
>
>在保存更改时，JCR存储库还首先执行关于新创建的节点是否被父节点的节点类型允许的验证。 如果在保存节点时收到错误消息，请检查内容结构是否有效(例如，您不能将节点创建为节 `nt:unstructured` 点的子节 `nt:folder` 点)。

## 创建属性 {#creating-a-property}

使用CRXDE Lite创建属性：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在“导航”窗格中，选择要添加新属性的节点。
1. 在底部窗 **格的** “属性”选项卡中，输入名 **称**、类 **型和******&#x200B;值。 单击&#x200B;**添加**。

1. 单击 **全部保存** ，以在服务器上保存更改。

## 创建脚本 {#creating-a-script}

要创建新脚本，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在“导航”窗格中，右键单击要创建脚本的组件，选择“创建……” **，然后选择“****创建文件……”**.

1. 输入“文件 **名** ”（包括其扩展名）。 单击&#x200B;**确定**。

1. 新文件将作为选项卡在“编辑”窗格中打开。
1. 编辑文件。
1. Click **Save All** to save the changes.

## 管理捆绑 {#managing-a-bundle}

使用CRXDE Lite，创建OSGI包、向其添加Java类和构建它非常简单。 然后，该捆绑自动安装并在OSGI容器中启动。

本节介绍如何使用显 `Test` 示Hello World！的 `HelloWorld` Java类创建 **捆绑包** 在您的浏览器中。

### 创建捆绑 {#creating-a-bundle}

要使用CRXDE Lite创建Test捆绑，请执行以下操作：

1. 在CRXDE Lite中，使用 `myapp` 项目向导创 [建项目](#creating-a-project)。 创建了以下节点：

   * `/apps/myapp/src`
   * `/apps/myapp/install`

1. 右键单击将包 `/apps/myapp/src` 含捆绑包的文 `Test` 件夹，选择 **创建……**，然后 **创建捆绑包……**.

1. 按如下方式设置捆绑属性：

   * 符号包名称： `com.mycompany.test.TestBundle`

   * 包名称: `Test Bundle`
   * 捆绑说明：

      ```
      This is my Test Bundle
      ```

   * 包:

      ```
      com.mycompany.test
      ```
   单击&#x200B;**确定**。

1. 单击 **全部保存** ，以在服务器上保存更改。

向导将创建以下元素：

* 类型为 `com.mycompany.test.TestBundle` It的节 `nt:folder.` 点是捆绑容器节点。

* 文件 `com.mycompany.test.TestBundle.bnd`。 它充当捆绑包的部署描述符，由一组标头组成。

* 文件夹结构：

   * `src/main/java/com/mycompany/test`. 它将包含包和Java类。

   * `src/main/resources`. 它将包含捆绑中使用的资源。

* 文 `Activator.java` 件。 它是可选的监听器类，用于通知绑定开始和停止事件。

下表列表了。bnd文件的所有属性及其值和说明：

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>值（创建捆绑时）<br /> </strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>导出包：</td>
   <td><p>*</p> <p>注意：需要调整此值以反映包的特异性。</p> </td>
   <td>Export-Package头定义从包中导出的包(包的列表以逗号分隔)。 导出的包构成包的公共视图<br /> 。<br /> </td>
  </tr>
  <tr>
   <td>导入包：</td>
   <td><p>*</p> <p>注意：需要调整此值以反映包的特异性。</p> </td>
   <td>Import-Package头为包定义导入的包(包的逗号分隔列表)</td>
  </tr>
  <tr>
   <td>私有包：</td>
   <td><p>*</p> <p>注意：需要调整此值以反映包的特异性。</p> </td>
   <td>私有包头为包定义私有包(包的列表以逗号分隔)。 私人一揽子方案构成内部执行。<br /> </td>
  </tr>
  <tr>
   <td>Bundle-Name:</td>
   <td>测试套件</td>
   <td>为包定义一个简短的、可读的名称</td>
  </tr>
  <tr>
   <td>Bundle-Description:</td>
   <td>这是我的测试套件</td>
   <td>为包定义简短的、可读的描述</td>
  </tr>
  <tr>
   <td>Bundle-SymbolicName:</td>
   <td>com.mycompany.test.TestBundle</td>
   <td>为包指定唯一、不可本地化的名称</td>
  </tr>
  <tr>
   <td>捆绑版本：</td>
   <td>1.0.0-SNAPSHOT</td>
   <td>指定捆绑的版本</td>
  </tr>
  <tr>
   <td>Bundle-Activator:</td>
   <td>com.mycompany.test.Activator</td>
   <td>指定要通知捆绑开始和停止事件的可选监听器类的名称</td>
  </tr>
 </tbody>
</table>

有关bnd格式的详细信息，请参阅CRXDE用 [于创建OSGI包的bnd实用程序](https://bndtools.org/) 。

### 创建Java类 {#creating-a-java-class}

要在测试 `HelloWorld` 包中创建Java类，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在“导航”窗格中，右键单击包含文件( `Activator.java` )的节点，选择“ `/apps/myapp/src/com.mycompany.test.TestBundle/src/main/java`创建…… **”，然后****选择“创建文件……”**.

1. 命名文件 `HelloWorld.java`。 单击&#x200B;**确定**。

1. 文件 `HelloWorld.java` 将在“编辑”窗格中打开。
1. 在中添加以下行 `HelloWorld.java`:

   ```
     package com.mycompany.test;
   
     public class HelloWorld {
     public String getString(){
     return "Hello World!";
     }
     }
   ```

1. 单击 **全部保存** ，以在服务器上保存更改。

### 构建捆绑 {#building-a-bundle}

构建测试包：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在“导航”窗格中，右键单击。bnd文件，选择“工具”, **然后选择**“捆绑&#x200B;**”**。

构建包向导：

* 编译Java类。
* 创建包含编译的Java类和资源的。jar文件，并将其放入文件 `myapp/install` 夹。
* 在OSGI容器中安装和开始捆绑包。

要查看测试包的效果，请创建一个使用Java方法HelloWorld.getString()的组件和由此组件呈现的资源：

1. 在下面创建 `mycomp` 组件 `myapp/components`。

1. 编 `mycomp.jsp` 辑代码并将其替换为以下行：

   ```
     <%@ page import="com.mycompany.test.HelloWorld"%><%
     %><%@ include file="/libs/foundation/global.jsp"%><%
     %><% HelloWorld hello = new HelloWorld();%><%
     %>
     <html>
     <body>
     <b><%= hello.getString() %></b><br>
     </body>
     </html>
   ```

1. 在下创建类 `test_node` 型的 `nt:unstructured` 资源 `/content`。

1. 对 `test_node`于，创建以下属性：名称= `sling:resourceType`，类型= `String`，值= `myapp/components/mycomp`。

1. 单击 **全部保存** ，以在服务器上保存更改。

1. 在您的浏览器中，请求 `test_node`: `https://<hostname>:<port>/content/test_node.html`.

1. 将显示一个包含 **Hello World！的页面** message.

## 导出和导入节点类型 {#exporting-and-importing-node-types}

使用CRXDE Lite，您可以导入和／或导出 [CND(压缩命名空间和节点类型定义)记号中的节点类型定义](https://jackrabbit.apache.org/jcr/node-type-notation.html)。

要导出节点类型定义，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 选择所需的节点。
1. 选择工 **具** ，然后选择 **导出节点类型**。

1. 定义（以代码表示）将显示在浏览器中。 根据需要保存信息。

要导入节点类型定义，请执行以下操作：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 选择 **工具** , **然后选择导入节点类型……**.

1. 在文本框中输入定义的CND记号。
1. 如果 **要更新现有定义** ，请选中“允许更新”。
1. 单击&#x200B;**导入**。

## 记录 {#logging}

使用CRXDE Lite，您可以显示位于文 `error.log` 件系统中的文件，并使用相 `<crx-install-dir>/crx-quickstart/server/logs` 应的日志级别对其进行过滤。 按如下步骤继续：

1. 在您的 浏览器中打开 CRXDE Lite。
1. 在窗 **口底部的** “控制台”选项卡中，在右侧的下拉菜单中，选择“服务器日 **志”**。

1. Click the **Stop** icon to display the messages.

您可以：

* 单击“记录配置”图标，在Felix控制台中调整 **日志参数** 。
* 单击“画笔”图标以清除 **消息** 。
* 单击“固定”图标，将消息固定到当前选 **择** 。
* 通过单击“停止”图标启用或禁用消 **息显** 示。

## 访问控制 {#access-control}

>[!NOTE]
>
>有关 [详细信息，请参阅用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md) 。
