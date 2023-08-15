---
title: 基本操作
description: 有关使用Adobe Experience Manager创作环境时基本处理的概述。 它使用 Sites 控制台作为基础。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 6%

---

# 基本处理{#basic-handling}

>[!NOTE]
>
>* 本页旨在概述使用Adobe Experience Manager (AEM)创作环境时的基本处理。 它使用&#x200B;**Sites**&#x200B;控制台作为基础。
>
>* 某些功能并非在所有控制台中均可用，而其他功能在某些控制台中可用。 有关各个控制台及其相关功能的特定信息，将在其他页面上详细介绍。
>* 用户在整个 AEM 环境中都可以使用各种键盘快捷键，尤其是在[使用控制台](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md)和[编辑页面](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)时。
>

## 欢迎屏幕 {#the-welcome-screen}

经典UI使用众所周知的导航和启动操作(包括单击、双击和 [上下文菜单](#context-menus).

登录后，将显示欢迎屏幕。 它提供控制台和服务链接列表：

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## 控制台 {#consoles}

主要控制台包括：

<table>
 <tbody>
  <tr>
   <td><strong>控制台</strong></td>
   <td><strong>用途</strong></td>
  </tr>
  <tr>
   <td><strong>欢迎</strong></td>
   <td>提供对AEM主要功能的概述和直接访问（通过链接）。</td>
  </tr>
  <tr>
   <td><strong>数字资产</strong><br /> </td>
   <td>这些控制台允许您导入和 <a href="/help/sites-classic-ui-authoring/classicui-assets.md">管理数字资产</a> 如图像、视频、文档和音频文件。 随后，这些资产便可由同一AEM实例上运行的任何网站使用。 </td>
  </tr>
  <tr>
   <td><strong>启动项</strong></td>
   <td>这有助于您管理 <a href="/help/sites-classic-ui-authoring/classic-launches.md">启动项</a>；利用这些功能，可为一个或多个激活网页的未来版本开发内容。<br /> <i>注意：在触屏优化UI中，站点控制台与引用边栏提供了许多相同的功能。</i> <i>如有必要，可以从“工具”控制台中使用此控制台；依次选择操作和启动项。</i></td>
  </tr>
  <tr>
   <td><strong>收件箱 </strong></td>
   <td>通常，工作流的子任务涉及不同的人，每个人必须先完成自己的步骤，然后才能将工作移交给下一个人。 收件箱允许您查看与此类任务相关的通知。 请参阅 <a href="/help/sites-administering/workflows.md">使用工作流</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>标记</strong></td>
   <td>“标记”控制台允许您管理标记。 标记是简短名称或短语，可用于对内容片段进行分类和注释，使其更易于查找和整理。 有关更多信息，请参阅 <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">使用和管理标记</a>.</td>
  </tr>
  <tr>
   <td><strong>工具</strong></td>
   <td>此 <a href="/help/sites-administering/tools-consoles.md">工具控制台</a> 提供对几个专用工具和控制台的访问权限，这些工具和控制台可帮助您管理网站、数字资产及内容存储库的其他方面。</td>
  </tr>
  <tr>
   <td><strong>用户</strong></td>
   <td>通过这些控制台，您可以管理用户和组的访问权限。 有关完整的详细信息，请参阅 <a href="/help/sites-administering/security.md">用户管理和安全性</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>网站</strong></td>
   <td>站点/网站控制台允许您 <a href="/help/sites-classic-ui-authoring/classic-page-author.md">创建、查看和管理网站</a> 在您的AEM实例上运行。 通过这些控制台，您可以创建、复制、移动和删除网站页面、启动工作流以及激活（发布）页面。 您还可以打开一个页面进行编辑。<br /> </td>
  </tr>
  <tr>
   <td><strong>工作流</strong></td>
   <td>工作流是定义的一系列步骤，用于描述完成某些任务的过程。 通常，有几个人参与一项任务，每个人必须先完成自己的步骤，然后才能将工作交给下一个人。 通过“工作流”控制台，可构建工作流模型并管理正在运行的工作流实例。 请参阅 <a href="/help/sites-administering/workflows.md">使用工作流</a>.<br /> </td>
  </tr>
 </tbody>
</table>

此 **网站** 控制台为您提供两个窗格来导航和管理页面：

* 左窗格

  这显示了您网站的树结构以及这些网站中的页面。

  它还显示有关其他方面或AEM的信息，包括项目、Blueprint和资源。

* 右窗格

  这将显示页面（位于左窗格中所选的位置），并可用于执行操作。

从这里，您可以 [管理您的页面](/help/sites-authoring/managing-pages.md) 使用工具栏、上下文菜单或通过打开页面执行进一步操作。

>[!NOTE]
>
>所有控制台的基本处理方式都相同。 本节将重点介绍 **网站** 控制台，因为它是创作时使用的主要控制台。

![chlimage_1-9](assets/chlimage_1-9a.png)

## 访问帮助 {#accessing-help}

在各种控制台（例如，网站）上， **帮助** 按钮可用。 点击 **帮助** 打开包共享或文档站点。

![chlimage_1-10](assets/chlimage_1-10a.png)

编辑页面时， [sidekick还有一个按钮用于访问帮助](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## 使用网站控制台导航 {#navigating-with-the-websites-console}

此 **网站** 控制台以树形结构（左侧窗格）列出您的内容页面。 为便于导航，可以根据需要展开树结构的各个部分(+)或折叠(-)：

* 单击左窗格中的页面名称会执行以下操作：

   * 在右侧窗格中列出子页面
   * 展开左窗格中的结构。

     出于性能原因，此操作取决于子节点的数量。 在标准安装中，此扩展方法适用于 `30` 或更少的子节点。

* 双击页面名称（左窗格）可展开树，不过由于该页面同时打开，因此这种效果并不明显。

>[!NOTE]
>
>此默认值( `30`)可以在特定于应用程序的siteadmin小组件配置中每个控制台进行更改：
>
>在站点管理员节点上：
>
>设置属性的值：
>`treeAutoExpandMax`
>开启:
>`/apps/wcm/core/content/siteadmin`
>
>或者，在主题中全局查找：
>设置值：
>`TREE_AUTOEXPAND_MAX`
>in:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>请参阅 [CQ小组件API中的SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteAdmin) 以了解更多详细信息。

## 网站控制台上的页面信息 {#page-information-on-the-websites-console}

的右窗格 **网站** 控制台提供包含有关页面信息的列表视图：

![page-info](assets/page-info.png)

以下各项可用；这些字段的子集显示为默认字段：

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
   <td>页面上显示的标题</td>
  </tr>
  <tr>
   <td>名称</td>
   <td>AEM引用的页面名称</td>
  </tr>
  <tr>
   <td>发布时间</td>
   <td>指示页面是否已发布并提供发布日期和时间。</td>
  </tr>
  <tr>
   <td>修改时间</td>
   <td>指示页面是否已修改并提供修改日期和时间。 要保存任何修改，必须激活页面。</td>
  </tr>
  <tr>
   <td>Scene7发布</td>
   <td>指示页面是否已发布到Scene7。<br /> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td>指示页面的状态，如页面是工作流的一部分还是LiveCopy的一部分，或者页面是否已锁定。</td>
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
   <td>指示页面在工作流中的时间。</td>
  </tr>
  <tr>
   <td>锁定者</td>
   <td>显示页面何时被锁定以及已锁定页面的用户帐户。</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>指示页面何时是Live Copy的一部分。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>要选择可见的列，请将鼠标悬停在列标题上。 随后将显示一个下拉菜单，您可以从此处使用 **列** 选项。

中页面旁边的颜色 **已发布** 和 **修改时间** 列指示发布状态：

| **列** | **颜色** | **描述** |
|---|---|---|
| 发布时间 | 绿色 | 发布成功。 内容已发布。 |
| 发布时间 | 黄色 | 正在等待发布。 系统尚未收到发布确认。 |
| 发布时间 | 红色 | 发布失败. 未与发布实例建立连接。 这还意味着该内容已被停用。 |
| 发布时间 | *blank* | 此页面从未发布。 |
| 修改时间 | 蓝色 | 自上次发布后，页面已被修改。 |
| 修改时间 | *blank* | 此页面从未被修改，或者自上次发布以来从未被修改。 |

## 上下文菜单 {#context-menus}

经典UI使用众所周知的机制来导航和启动操作，包括单击和双击。 根据当前情况，还会提供一系列上下文菜单（以鼠标右键打开）：

![chlimage_1-11](assets/chlimage_1-11a.png)
