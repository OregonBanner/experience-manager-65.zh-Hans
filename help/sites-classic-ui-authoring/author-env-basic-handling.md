---
title: 基本操作
seo-title: 基本操作
description: 概述使用 AEM 创作环境时的基本操作。它使用站点控制台作为基础。
seo-description: 概述使用 AEM 创作环境时的基本操作。它使用站点控制台作为基础。
uuid: ab488d7c-7b7f-4a23-a80c-99d37ac84246
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9737ead9-e324-43c9-9780-7abd292f4e5b
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 基本操作{#basic-handling}

>[!NOTE]
>
>* 此页面旨在概述使用 AEM 创作环境时的基本操作。它使用&#x200B;**站点**&#x200B;控制台作为基础。
   >
   >
* 某些功能并不是在所有控制台中均可用，并且/或者某些控制台会提供额外功能。其他页面中会更详细地介绍有关具体控制台及其相关功能的特定信息。
>* 用户在整个 AEM 环境中都可以使用各种键盘快捷键，尤其是在[使用控制台](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md)和[编辑页面](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)时。
>



## 欢迎屏幕 {#the-welcome-screen}

经典 UI 提供了一系列控制台选项，它使用大家熟知的机制进行导航和启动操作，包括单击、双击和[上下文菜单](#context-menus)。

登录后，将会显示欢迎屏幕，其中提供指向控制台和服务的链接列表：

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## 控制台 {#consoles}

主要的控制台有：

<table>
 <tbody>
  <tr>
   <td><strong>控制台</strong></td>
   <td><strong>用途</strong></td>
  </tr>
  <tr>
   <td><strong>欢迎</strong></td>
   <td>提供 AEM 主要功能的概述和直接访问（通过链接）。</td>
  </tr>
  <tr>
   <td><strong>数字资产</strong><br /> </td>
   <td>通过这些控制台，您可以导入和<a href="/help/sites-classic-ui-authoring/classicui-assets.md">管理数字资产</a>，如图像、视频、文档和音频文件。随后，这些资产便可由同一 AEM 实例上运行的任何网站使用。 </td>
  </tr>
  <tr>
   <td><strong>启动项</strong></td>
   <td>此控制台可帮助管理您的<a href="/help/sites-classic-ui-authoring/classic-launches.md">启动项</a>；通过这些启动项，可以为一个或多个已激活网页的将来版本开发内容。
<br /> 注 <i>意：在触屏优化UI中，“站点”控制台中提供了大量相同的功能，同时还提供了“引用”边栏。</i><i>如果需要，可以从“工具”控制台中访问此控制台；选择“操作”，然后选择“启动项”。</i></td>
  </tr>
  <tr>
   <td><strong>收件箱 </strong></td>
   <td>在很多情况下，工作流的子任务中会涉及很多人员，每人必须完成自己的步骤，才能将工作转交给下一个人。“收件箱”允许您查看与此类任务相关的通知。请参阅<a href="/help/sites-administering/workflows.md">使用工作流</a>。<br /> </td>
  </tr>
  <tr>
   <td><strong>标记</strong></td>
   <td>“标记”控制台让您可以管理标记。标记是一些短名称或短语，可用于对某些内容片段进行分类和添加注释，以便更容易查找和组织。有关进一步的信息，请参阅<a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">使用和管理标记</a>。</td>
  </tr>
  <tr>
   <td><strong>工具</strong></td>
   <td><a href="/help/sites-administering/tools-consoles.md">“工具”控制台</a>让您可以访问一些专用工具和控制台，帮助您管理网站、数字资产及内容存储库的其他方面。</td>
  </tr>
  <tr>
   <td><strong>用户</strong></td>
   <td>这些控制台让您可以管理用户和组的访问权限。有关完整的详细信息，请参阅<a href="/help/sites-administering/security.md">用户管理和安全</a>。<br />
 </td>
  </tr>
  <tr>
   <td><strong>网站</strong></td>
   <td>“站点”/“网站”控制台让您可以<a href="/help/sites-classic-ui-authoring/classic-page-author.md">创建、查看和管理</a>在 AEM 实例上运行的网站。通过这些控制台，可以创建、复制、移动和删除网站页面、启动工作流和激活（发布）页面。还可以打开页面进行编辑。<br /> </td>
  </tr>
  <tr>
   <td><strong>工作流</strong></td>
   <td>工作流是定义的一系列步骤，用于描述完成某些任务的过程。在许多情况下，任务中会涉及很多人员，每人必须完成自己的步骤，才能将工作转交给下一个人。“工作流”控制台可让您构建工作流模型和管理正在运行的工作流实例。请参阅<a href="/help/sites-administering/workflows.md">使用工作流</a>。<br /> </td>
  </tr>
 </tbody>
</table>

**站点**&#x200B;控制台提供了两个窗格，用于导航和管理页面：

* 左窗格

   这显示了网站的树结构以及这些网站中的页面。

   还显示有关其他方面或 AEM 的信息，包括项目、Blueprint 和资产。

* 右窗格

   这将显示页面（在左侧窗格中选定的位置），并可用于执行操作。

从此处，可以使用工具栏、上下文菜单，或通过打开页面以执行进一步操作，来[管理您的页面](/help/sites-authoring/managing-pages.md)。

>[!NOTE]
>
>在所有控制台上，基本操作都是一样的。此部分侧重于“**网站**”控制台，因为该控制台是创作时使用的主控制台。

![chlimage_1-9](assets/chlimage_1-9a.png)

## 访问帮助 {#accessing-help}

各个控制台（例如，“网站”）上也提供了&#x200B;**帮助**&#x200B;按钮，用于打开包共享或文档站点。

![chlimage_1-10](assets/chlimage_1-10a.png)

编辑页面时，[Sidekick 也有一个用于获取帮助的按钮](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help)。

## 利用“网站”控制台进行导航 {#navigating-with-the-websites-console}

**网站**&#x200B;控制台以树状结构列出您的内容页面（左侧窗格）。为了方便导航，可以根据需要展开 (+) 或折叠 (-) 树状结构的各个部分。

* 只需单击一下页面名称（左侧窗格中），即可：

   * 在右侧窗格中列出子页面
   * 同时在左侧窗格中展开结构。

      因为性能原因，此操作取决于子节点的数量。在标准安装下，此展开方法在子节点数少于或等于 `30` 时有效。

* 双击页面名称（左窗格）也将展开树，但因为同时会打开页面，所以此效果不是很明显。

>[!NOTE]
>
>可以在 siteadmin 小部件特定于应用程序的配置中针对控制台更改此默认值 (`30`)：
>
>在 siteadmin 节点上：
>
>设置以下属性的值：
>`treeAutoExpandMax`
>on:
>`/apps/wcm/core/content/siteadmin`
>
>或者在主题中全局应用：
>设置下面的值：
>`TREE_AUTOEXPAND_MAX`
>in:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>有关更多详细信息，请参阅 [CQ 小部件 API 中的 SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)。

## “网站”控制台上的页面信息{#page-information-on-the-websites-console}

**网站**&#x200B;控制台的右侧窗格中提供了一个包含页面相关信息的列表视图：

![page-info](assets/page-info.png)

以下为可用字段；默认将显示这些字段的子集：

<table>
 <tbody>
  <tr>
   <td><strong>列</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>缩略图</td>
   <td>显示页面的缩略图。</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>在页面上显示的标题</td>
  </tr>
  <tr>
   <td>名称</td>
   <td>AEM 用来表示该页面的名称</td>
  </tr>
  <tr>
   <td>发布时间</td>
   <td>指示页面是否已发布，并提供发布日期和时间。</td>
  </tr>
  <tr>
   <td>修改时间</td>
   <td>指示页面是否已修改，并提供修改日期和时间。要保存任何修改，必须激活页面。</td>
  </tr>
  <tr>
   <td>Scene7 发布状态</td>
   <td>指示该页面是否已发布到 Scene7。<br /> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td>指示页面的当前状态，如页面是否属于工作流或 Live Copy 的一部分，或者页面当前是否已锁定。</td>
  </tr>
  <tr>
   <td>展示次数</td>
   <td>以点击数显示页面上的活动。</td>
  </tr>
  <tr>
   <td>模板</td>
   <td>指示页面所基于的模板。</td>
  </tr>
  <tr>
   <td>在工作流中</td>
   <td>指示页面是否位于工作流中。</td>
  </tr>
  <tr>
   <td>锁定者</td>
   <td>显示页面是否被锁定以及锁定该页面的用户帐户。</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>指示页面是否是 Live Copy 的一部分。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>要选择可见的列，请将鼠标悬停在列标题上。将显示一个下拉菜单，通过该菜单可以使用&#x200B;**列**&#x200B;选项。

**发布时间**&#x200B;和&#x200B;**修改时间**&#x200B;列旁边的颜色指示发布状态：

| **列** | **颜色** | **描述** |
|---|---|---|
| 发布时间 | 绿色 | 发布成功。内容已发布。 |
| 发布时间 | 黄色 | 正在等待发布。系统未收到发布确认。 |
| 发布时间 | 红色 | 发布失败。与发布实例之间没有连接。这还可能意味着内容已取消激活。 |
| 发布时间 | *空* | 此页面从未发布过。 |
| 修改时间 | 蓝色 | 页面自上次发布后已被修改。 |
| 修改时间 | *空* | 此页面从未被修改，或者自上次发布后未被修改。 |

## 上下文菜单 {#context-menus}

经典 UI 使用大家熟知的机制进行导航和启动操作，包括单击和双击。根据当前位置，还将显示一系列上下文菜单（通常使用鼠标右键打开）：

![chlimage_1-11](assets/chlimage_1-11a.png)

