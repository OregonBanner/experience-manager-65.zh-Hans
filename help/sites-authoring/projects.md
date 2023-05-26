---
title: 项目
seo-title: Projects
description: 通过项目，您可以将资源分组到一个实体中，该实体通过共享的公共环境可轻松管理项目。
seo-description: Projects let you group resources into one entity whose common, shared environment makes it easy to manage your projects
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: 85e993000c016240c0fbf398ec8192990e60eee6
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 14%

---


# 项目 {#projects}

通过项目，您可以将资源分组到一个实体中。 通过一个通用的共享环境，可轻松管理您的项目。 您可以与项目关联的资源类型在AEM中称为“图块”。 拼贴可以包含项目和团队信息、资产、工作流及其他类型的信息，如[项目拼贴](#project-tiles)中详述。

作为用户，您可以：

* 创建和删除项目
* 将内容和资产文件夹关联到项目
* 从项目中删除内容链接

## 访问要求 {#access-requirements}

项目是一项标准的AEM功能，无需任何其他设置。

但是，对于项目中的用户，要在使用项目（如创建项目、创建任务/工作流或查看和管理团队）时查看其他用户/组，这些用户需要拥有读取权限 `/home/users` 和 `/home/groups`.

最简单的方法是给出 **projects — 用户** 对的组读取访问权限 `/home/users` 和 `/home/groups`.

## 项目控制台 {#projects-console}

在项目控制台中，您可以访问和管理AEM中的项目。

![项目控制台](assets/screen-shot_2019-03-05at125110.png)

项目控制台与AEM中的其他控制台类似，允许对单个项目执行许多操作并调整项目的视图。

### 切换模式 {#modes}

您可以使用边栏选择器来更改控制台模式。

![边栏选择器](assets/projects-rail.png)

#### 仅限内容 {#content-only}

“仅内容”是打开控制台时的默认模式。 它将显示您的所有项目。

#### 时间线 {#timeline}

时间线视图允许您选择单个项目并查看其上的活动。 使用边栏选择器或热键 `alt+1` 以更改此视图。

![时间轴模式](assets/project-timeline.png)

### 切换视图 {#views}

您可以使用视图选择器，在以大图块形式查看项目（默认）、以列表形式查看项目或在日历上查看项目之间进行更改。

![视图](assets/projects-views.png)

### 筛选视图 {#filter}

您可以使用该过滤器在所有项目与仅活动项目之间进行切换。

![过滤器](assets/projects-filter.png)

### 选择和查看项目 {#selecting}

通过将鼠标悬停在项目拼贴上并单击复选标记来选择项目。

通过单击项目以深入查看其详细信息，可查看项目的详细信息。

### 创建新项目 {#creating}

单击 **创建** 以添加新项目。

## 项目拼贴 {#project-tiles}

项目由您希望一起管理的不同类型的信息组成。 此信息由不同的 **磁贴**.

您可以使以下磁贴与项目关联。

* [Assets](#assets)
* [资产收藏集](#asset-collections)
* [体验](#experiences)
* [链接](#links)
* [项目信息](#project-info)
* [团队](#team)
* [登录页面](#landing-pages)
* [电子邮件](#emails)
* [工作流](#workflows)
* [启动项](#launches)
* [任务](#tasks)

单击任何图块右上角的下拉菜单，向图块中添加更多数据。

单击任何图块右下方的省略号按钮，以在其关联控制台中打开图块的数据。

### 资产 {#assets}

在 **资产** 图块，您可以收集用于特定项目的所有资源。

![“资产”拼贴](assets/project-tile-assets.png)

您可以直接在图块中上传资产。

### 资产收藏集 {#asset-collections}

与资源类似，您可以添加 [资产收藏集](/help/assets/manage-collections.md) 直接转到您的项目。 您可以在Assets中定义收藏集。

![资产收藏集拼贴](assets/project-tile-asset-collection.png)

通过单击&#x200B;**添加收藏集**&#x200B;并从列表中选择相应的收藏集来添加收藏集。

### 体验 {#experiences}

此 **体验** 通过图块，您可以将移动应用程序、网站或发布添加到项目中。

![“体验”拼贴](assets/project-tile-experiences.png)

这些图标指示表示的体验类型。

* 网站
* 移动应用程序

### 链接 {#links}

此 **链接** 利用图块，可将外部链接与项目相关联。

![“链接”拼贴](assets/project-tile-links.png)

您可以使用易于识别的名称来命名链接并更改其缩略图。

### 项目信息 {#project-info}

此 **项目信息** 拼贴提供有关项目的一般信息，包括描述、项目状态（非活动或活动）、截止日期和成员。 此外，您还可以添加项目缩略图，该缩略图显示在主项目页面上。

![“项目信息”拼贴](assets/project-tile-info.png)

### 翻译作业 {#translation-job}

此 **翻译作业** 图块是开始翻译的位置，也是查看翻译状态的位置。

![翻译作业拼贴](assets/project-tile-translation.png)

要设置翻译，请参阅文档 [正在创建翻译项目。](/help/assets/translation-projects.md)

### 团队 {#team}

在此图块中，您可以指定项目团队的成员。 编辑时，您可以输入团队成员的名称并分配用户角色。

![“团队”拼贴](assets/project-tile-team.png)

您可以在团队中添加和删除团队成员。此外，您还可以编辑向团队成员分配的[用户角色](#userroles)。

### 登录页面 {#landing-pages}

此 **登陆页面** 通过图块，可请求新的登陆页面。

![登陆页面拼贴](assets/project-tile-landing.png)

文档中介绍了此工作流[创建登陆页面工作流。](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)

### 电子邮件 {#emails}

此 **电子邮件** 图块帮助您管理电子邮件请求。 它会启动 **电子邮件请求** 工作流。

![“电子邮件”拼贴](assets/project-tile-email.png)

欲知更多信息，请参见 [请求电子邮件工作流。](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)

### 工作流 {#workflows}

您可以启动项目的工作流。 如果有任何工作流正在运行，其状态会显示在 **工作流** 图块。

![“工作流”拼贴](assets/project-tile-workflows.png)

根据您创建的项目，有不同的可用工作流。

有关这些功能的说明，请参见 [使用项目工作流。](/help/sites-authoring/projects-with-workflows.md)

### 启动项 {#launches}

此 **启动次数** 图块显示已请求的任何启动项 [请求启动工作流。](/help/sites-authoring/projects-with-workflows.md)

![“启动项”拼贴](assets/project-tile-launches.png)

### 任务 {#tasks}

任务允许您监控任何与项目相关的任务（包括工作流）的状态。 [处理任务](/help/sites-authoring/task-content.md)中详细介绍了任务。

![“任务”拼贴](assets/project-tile-tasks.png)

## 项目模板 {#project-templates}

模板是启动项目的基础。 AEM提供这些标准项目模板。

* **媒体项目**  — 这是一个与媒体相关活动的参考示例项目。 它包括多个与媒体相关的项目角色，还包括与媒体内容相关的工作流。
* **[产品照片拍摄项目](/help/sites-authoring/managing-product-information.md)**  — 这是用于管理电子商务相关产品摄影的参考示例。
* **[翻译项目](/help/sites-administering/translation.md)**  — 这是用于管理翻译相关活动的参考示例。 它包括基本角色和用于管理翻译的工作流。
* **简单项目**  — 这是任何不适合其他类别的项目的参考示例。 它包括三个基本角色和四个常规AEM工作流。

根据您选择的模板，您在项目中有不同的可用选项，例如提供的用户角色和工作流。

## 项目中的用户角色 {#user-roles-in-a-project}

不同的用户角色在项目模板中定义，主要原因有二：

1. 权限：用户角色属于列出的三个类别之一：观察者、编辑者、所有者。 例如，摄影师或撰稿人将拥有与编辑者相同的权限。 这些权限决定用户可以对项目中的内容执行的操作。
1. 工作流：工作流确定在项目中向谁分配任务。 任务可以与项目角色关联。例如，可以将任务分配给摄影师，以便具有摄影师角色的所有团队成员都能获得该任务。

所有项目都支持以下默认角色，以便您管理安全和控制权限。

| 角色 | 描述 | 权限 | 组成员资格 |
|---|---|---|---|
| 观察者 | 具有此角色的用户可以查看项目详细信息，包括项目状态。 | 项目的只读权限 | `workflow-users` 组 |
| 编辑器 | 此角色中的用户可以上传和编辑项目的内容。 | 对项目、关联的元数据和相关资源的读写访问权限<br>上传拍摄列表、照片拍摄以及查看和批准资源的权限<br>写入权限 `/etc/commerce`<br>修改特定项目的权限 | `workflow-users` 组 |
| 所有者 | 具有此角色的用户可以创建项目、在项目中启动工作，并将批准的资产移动到生产文件夹。 所有者还可以查看和执行项目中的所有其他任务。 | `/etc/commerce` 的写入权限 | `dam-users` 组才能创建项目<br>`project-administrators` 组才能创建项目和移动资产 |

对于创意项目，还提供了其他角色，例如摄影师。 您可以使用这些角色为特定项目派生自定义角色。

### 自动组创建 {#auto-group-creation}

在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。

例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。

如果删除了项目，则只有在选择适当的选项时，才会删除这些组 [删除项目时。](/help/sites-authoring/touch-ui-managing-projects.md#deleting-a-project) 管理员还可以手动删除中的组 **工具** > **安全性** > **组**.

## 其他资源 {#additional-resources}

有关使用项目的更多详细信息，请参阅以下附加文档：

* [管理项目](/help/sites-authoring/touch-ui-managing-projects.md)
* [处理任务](/help/sites-authoring/task-content.md)
* [使用项目工作流](/help/sites-authoring/projects-with-workflows.md)
* [Creative Project与PIM集成](/help/sites-authoring/managing-product-information.md)
