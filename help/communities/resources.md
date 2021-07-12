---
title: 启用资源控制台
seo-title: 启用资源控制台
description: 在“资源”控制台中，启用管理器可以创建、管理和将资源分配给启用社区站点的成员
seo-description: 在“资源”控制台中，启用管理器可以创建、管理和将资源分配给启用社区站点的成员
uuid: 52445b39-c339-4b39-8004-eb36de99bced
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1ef15e76-fe7c-4ced-a20d-c0a9385e3ee4
role: Admin
exl-id: 15e16572-c692-41fc-86e4-c1d475afa63c
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2979'
ht-degree: 5%

---

# 启用资源控制台 {#enablement-resources-console}

对于AEM Communities，在资源控制台中， [启用管理器](users.md)可创建资源，并管理资源并将其分配给启用社区站点的成员。

## 要求 {#requirements}

在添加社区站点的启用资源之前，必须正确配置AEM实例，包括：

* SCORM
* FFmpeg

有关详细信息，请参阅[配置启用](enablement.md)。

>[!CAUTION]
>
>如果在社区站点创建后安装了SCORM，则必须重新创建在安装SCORM之前存在的任何支持资源。

>[!NOTE]
>
>随着[AEM 6.3](deploy-communities.md#latestfeaturepack)和等效的社区功能包[AEM 6.2 FP3](deploy-communities.md#latestfeaturepack)和[AEM 6.1 FP7](https://docs.adobe.com/content/docs/en/aem/6-1/deploy/communities.html#Latest功能包)的发布，启用功能不再需要[MySQL数据库](mysql.md)。

## 术语 {#terminology}

### 资源 {#resource}

资源对于[启用社区](overview.md#enablement-community)至关重要。 这些是分配给成员的材料，使他们能够提高技能。

资源的特性：

* 可能为：
   * 图像(JPG、PNG、GIF、BMP)
   * 视频(MP4)
   * Flash(SWF)
   * 文档(PDF)
   * 测验(SCORM)
* 可以从一个或多个学习路径引用。

### 学习路径 {#learning-path}

学习路径是一组分组在一起的支持资源的逻辑集合，用于轻松分配给成员。

### 成员组 {#members-group}

创建社区站点时，在创建为[站点特定用户组](users.md)（为各种角色配置了各种权限）时，会使用为URL指定的站点名称。 所有这些自动创建的组都带有`Community <site-name>`前缀。

其中一个此类用户组是`Community <site-name> Members`组，用于将发布环境中的注册用户标识为社区成员。 有关Enablement](getting-started-enablement.md)的教程[AEM Communities快速入门的示例，请参阅。

对于[参与社区](overview.md#egagementcommunity)，允许站点访客自行注册或使用社交登录是合理的，此时，他们会自动添加到成员组。

对于[启用社区](overview.md#enablement-community)，建议将站点设为私有，然后需要管理员将用户添加到成员组。

## 访问社区站点的支持资源 {#accessing-a-community-site-s-enablement-resources}

### 导航到Communities Resources {#navigate-to-communities-resources}

在创作环境中，访问资源控制台

* 从全局导航：**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 资源]**

   ![启用站点](assets/enablement-sites.png)

### 选择社区站点 {#select-a-community-site}

“社区资源”控制台将显示所有社区站点。

从“资源”控制台中选择特定社区站点后，即会为该站点创建启用资源。

选择特定的社区站点后，可以访问任何现有的支持资源和学习路径以进行管理和修改，并且可以创建新的支持资源和学习路径。

![社区资源](assets/community-resources.png)

#### 搜索 {#search-features}

![searchsite](assets/searchsite.png)

选择侧面板切换图标以搜索启用资源或学习路径。 选择后，控制台左侧将打开一个搜索面板，并提供一个可在其中输入搜索词的文本框。

![搜索结果](assets/search-result.png)

#### 选择模式 {#selection-mode}

要选择多个启用资源，请将鼠标悬停在卡片上并选择复选标记图标，以选择第一个启用资源。 选择卡片后，选择任何其他卡片会将其添加到选择组。 再次选择时，将取消选择卡。

![选择模式](assets/selection-mode.png)

## 创建资源 {#create-a-resource}

![创建资源](assets/create-resource1.png)

向社区站点添加新的支持资源

* 选择`Create`图标。
* 从显示的子菜单中，选择&#x200B;**[!UICONTROL 资源]**。

此操作将启动以下分步流程：

* 描述资源（名称、卡片图像和文本）。
* 选择资源内容。
* 为资源选择封面图像。
* 识别资源联系人。
* 将资源分配给成员。

当资源是课程（学习路径）的一部分时，应仅将成员分配到学习路径。 在创建启用资源后，可以添加分配。

### 1基本信息 {#basic-info}

![resource-basicinfo](assets/resource-basicinfo.png)

* **[!UICONTROL 添加]**

   （*可选*）要在成员的分配页面以及资源控制台中用于启用资源的卡片上显示的图像。 从服务器的本地文件系统中选择映像。 如果未提供图像，则会为上传的资源生成缩略图。

   ***注意***:建议的图像大小不仅为480 x 480像素。由于卡片对各种浏览器尺寸的响应式设计，因此显示大小将因220 X 165像素到400 x 165像素而异。

* **[!UICONTROL 网站名称]**

   (*readonly*)添加资源的社区站点。

* **[!UICONTROL 资源名称]**

   （*必需*）资源的显示名称。 根据显示名称创建有效的节点名称。

* **[!UICONTROL 标记]**

   （*可选*）可以选择一个或多个标记，这些标记将启用资源与一个或多个目录相关联。 请参阅[标记支持资源](tag-resources.md)。

* **[!UICONTROL 在目录中显示]**

   取消选中后，启用资源将不会显示在任何目录中。 如果选中此项，则启用资源将显示在所有目录中，除非[预过滤的](catalog-developer-essentials.md#pre-filters)或UI中的成员过滤器。 默认为未选中。

* **[!UICONTROL 描述]**

   （*可选*）要为启用资源显示的描述。

* **[!UICONTROL 较小的资产]**

   （*可选*）从AEM Assets中选择。 用于在发布环境中（如在目录中）表示资源的缩略图。

* **[!UICONTROL 较大的资产]**

   （*可选*）从AEM Assets中选择。 用于在发布环境中表示资源的大图像，例如在资源的主页上。

* **[!UICONTROL 内容片段资产]**

   （*可选*）从AEM Assets中选择。 可在发布环境中引用但默认未使用的内容片段。

* 选择&#x200B;**[!UICONTROL Next]**

### 2添加内容 {#add-content}

![resource-addcontent](assets/resource-addcontent.png)

虽然它看起来好像可能选择了多个启用资源，但只允许使用一个。

选择右上角的`'+' icon`以通过标识源开始选择资源的过程。

![上载资源](assets/upload-resource1.png)

* **[!UICONTROL 从我的本地文件上传]**

   从本地文件系统上传将使用本机文件浏览器选择并上传文件。 支持的文件类型包括SCORM.zip（HTML5或SWF）、MP4视频、SWF、PDF和图像类型(JPG、PNG、GIF、BMP)。 文件名将变为添加到资产库的资产名称。

* **[!UICONTROL 浏览资产库]**

   从资产库中选择。 选择范围仅限于社区站点中可见的内容。

* **[!UICONTROL 添加外部 URL]**

   输入学习内容的链接。

   在打开的对话框中，输入：

   * **[!UICONTROL 标题]**

      启用资源的资产名称。

   * **[!UICONTROL URL]**

      资产的URL。

* **[!UICONTROL 添加 Adobe Connect URL]**

   输入指向Adobe Connect会话的链接。

   在打开的对话框中，输入：

   * **[!UICONTROL 标题]**

      启用资源的资产名称。

   * **[!UICONTROL URL]**

      指向Adobe Connect会话的URL。

* **[!UICONTROL 定义外部资源]**

   输入要显示物料的位置。 成功状态和分数的值是手动输入的（请参阅[Reports](reports.md)）。 上传的封面图像可用于提供其他信息。

   在打开的对话框中，输入：

   * **[!UICONTROL 标题]**

      启用资源的资产名称。

   * **[!UICONTROL 位置]**

      物理站点的位置，如教室。

#### 添加的视频资源示例 {#example-of-an-added-video-resource}

![add-video](assets/add-video.png)

* **[!UICONTROL 资源封面图像]**

   封面图像是首次查看启用资源时要显示的图像。 例如，当视频资源尚未播放时，会显示封面图像。 如果未上传自定义图像，则会显示默认图像。 对于视频资源，[可能会生成缩略图](enablement.md#ffmpeg)，但只有在上传时才会生成缩略图，而在将视频引用为URL时则不会生成缩略图。 对于位置资源，图像可用于提供其他信息。

   封面图像的建议大小为640 x 360像素。

* 选择&#x200B;**[!UICONTROL 下一步]**。

### 3设置 {#settings}

![资源设置](assets/resource-settings.png)

>[!NOTE]
>
>不应直接在要从学习路径引用的支持资源中注册学习者。 学习者只需在学习路径中注册即可。
>
>如果成员同时注册了资源和引用该资源的学习路径，则其分配将同时显示学习路径中的单个资源和资源。

* **[!UICONTROL 社交设置]**

   这些设置控制学习者是否能够提供有关启用资源的输入。 [审核设置](sites-console.md#moderation)是父社区站点的设置。

   * **[!UICONTROL 允许评论]**

      如果选中，则允许成员对资源进行评论。 默认选中。

   * **[!UICONTROL 允许评级]**

      如果选中，则允许成员对资源进行评级。 默认选中。

   * **[!UICONTROL 允许匿名访问]**

      如果选中此项，则当社区站点还允许匿名访问时，允许匿名站点访客查看目录中的资源。 默认为未选中。

* **[!UICONTROL 到期日期]**

   *（可选）* 可以选择完成分配的日期。

* **[!UICONTROL 资源作者]**

   *（可选）* 启用资源的作者。使用下拉菜单从[成员组](#members-group)的成员中进行选择。

* **[!UICONTROL 资源联系人(&amp;A);]**

   *（必需）* 成员可以联系的与启用资源有关的人员。使用下拉菜单从[成员组](#members-group)的成员中进行选择。

* **[!UICONTROL 资源专家]**

   *（可选）* 会员可以联系对支持资源具有专业知识的人员。使用下拉菜单从[成员组](#members-group)的成员中进行选择。

### 4项任务 {#assignments}

![资源分配](assets/resource-assignments.png)

* **[!UICONTROL 添加被分派人]**

   使用下拉菜单从[members](#members-group) — 用户和用户组（以粗体字列出） — 将作为学习者注册的用户和用户组。 当成员登录社区网站时，其[Assignments](functions.md#assignments-function)页面上将显示他们注册的支持资源（和学习路径）。

* 选择&#x200B;**[!UICONTROL 创建]**。

   ![resourceinfo](assets/resourceinfo.png)

成功创建启用资源后，将返回到资源控制台，并选中新创建的资源。 从此控制台中，可以[管理资源](#managing-a-resource)。

## 创建学习路径 {#create-a-learning-path}

![add-learning-path](assets/add-learning-path.png)

向社区站点添加新的学习路径

* 选择`Create`图标
* 从显示的子菜单中，选择&#x200B;**[!UICONTROL 学习路径]**。

此操作将启动以下分步流程：

* 识别学习路径。
* 提供用于表示学习者的学习路径的卡片图像。
* 引用要包含在学习路径中的支持资源。
* （可选）对资源进行排序。
* （可选）识别先决条件学习路径。
* 识别学习路径联系人。
* 注册成员。

对于学习路径中包含的支持资源，应仅为学习路径进行分配，而不应为单个资源进行分配。

### 基本信息 {#basic-info-1}

![学习路径基本](assets/learningpath-basic1.png)

* **[!UICONTROL 添加]**

   （*可选*）要在成员分配页面和资源控制台中学习路径的卡片上显示的图像。 从服务器的本地文件系统中选择映像。 如果未提供图像，则会为上传的资源生成缩略图。

   ***注意***:建议的图像大小不再只是480 x 480像素。由于卡片对各种浏览器尺寸的响应式设计，因此显示大小将因220 X 165像素到400 x 165像素而异。

* **[!UICONTROL 网站名称]**

   （*只读*）添加资源的社区站点。

* **[!UICONTROL 学习路径名称]**

   （*必需*）学习路径的显示名称。 根据显示名称创建有效的节点名称。

* **[!UICONTROL 标记]**

   （*可选*）可以选择一个或多个标记，这些标记将学习路径与一个或多个目录相关联。 请参阅[标记支持资源](tag-resources.md)。

* **[!UICONTROL 在目录中显示]**

   如果未选中此选项，则学习路径将不会显示在任何目录中。 如果选中此项，则学习路径将显示在所有目录中，除非[预过滤的](catalog-developer-essentials.md#pre-filters)或UI中的成员过滤器。 在目录中显示学习路径将间接授予对其所有包含资源的读取权限。 默认为未选中。

* **[!UICONTROL 描述]**

   （*可选*）要为启用资源显示的描述。

* **[!UICONTROL 较小的资产]**

   （*可选*）从AEM Assets中选择。 用于在发布环境中（如在目录中）表示资源的缩略图。

* **[!UICONTROL 较大的资产]**

   （*可选*）从AEM Assets中选择。 用于在发布环境中表示资源的大图像，例如在资源的主页上。

* **[!UICONTROL 内容片段资产]**

   （*可选*）从AEM Assets中选择。 可在发布环境中引用但默认未使用的内容片段。

* 选择&#x200B;**[!UICONTROL 下一步]**。

### 添加必备项 {#add-prerequisites}

![学习路径先决条件](assets/learningpath-prerequisites.png)

* **[!UICONTROL 必要的学习路径]**

   （*可选*）选择其他已发布的学习路径后，必须先完成这些路径，学员才能选择此学习路径。

* 选择&#x200B;**[!UICONTROL 下一步]**。

### 添加资源 {#add-resources}

![learningpath-addresource](assets/learningpath-addresource.png)

* **[!UICONTROL 强制执行学习路径中的排序]**

   （*可选*）如果设置为“开”，则添加启用资源的顺序是学习者继续完成学习路径的顺序。 默认为“关”。

* **[!UICONTROL 资源]**

   从为当前社区站点创建的&#x200B;*已发布*&#x200B;启用资源中选择的一个或多个资源。

>[!NOTE]
>
>您只能选择与学习路径处于同一级别的可用资源。 例如，对于在组中创建的学习路径，只有组级别资源可用；对于在社区站点中创建的学习路径，该站点中的资源可用于添加到学习路径中。

* 选择&#x200B;**[!UICONTROL 下一步]**。

### 设置 {#settings-1}

![learningpath-settings1](assets/learningpath-settings1.png)

* **[!UICONTROL 添加注册]**

   使用下拉菜单从社区站点的[成员组](#members-group)的成员组（以粗体字列出）中进行选择。 首次创建学习路径时，无需添加分配。 可以修改学习路径属性以在以后添加学习者。

* **[!UICONTROL 学习路径联系方式(&amp;A);]**

   *（必需）* 成员可以联系的有关学习路径的人员。使用下拉菜单从社区站点的[成员组](#members-group)的成员中进行选择。

* 选择&#x200B;**[!UICONTROL 创建]**

>[!NOTE]
>
>从学习路径引用的支持资源不应列出相同的受分配者（学习者）（如果有）。
>
>如果成员同时注册了启用资源和引用该资源的学习路径，则其分配将显示学习路径中的单个资源和资源。

## 管理资源 {#managing-a-resource}

要管理单个启用资源，请执行以下操作：

* 从&#x200B;**[!UICONTROL 资源]**&#x200B;控制台中，选择包含该资源的社区站点。
* 选择资源。

对于选定的启用资源，可以：

* 查看属性（默认）
* 编辑属性
* 删除
* 发布
* 取消发布

要上传支持资源的新版本，建议创建新资源，然后从旧版本中取消注册成员，并将他们注册到新版本中。

### 编辑资源 {#edit-resource}

![edit-resource](assets/edit-resource.png)

通过选择铅笔图标，可以使用显示的用于创建启用资源的步骤，以便可以修改提供的任何信息。

如果唯一的更改是修改“设置”步骤中的分配，则保存更改会导致修改被发布。 如果进行了任何其他更改，则必须在保存后明确发布资源。

### 删除资源 {#delete-resource}

![delete-resource](assets/delete-resource.png)

通过选择垃圾桶图标，确认后启用资源将为`Deleted`。

### 发布 {#publish}

![publish-resource](assets/publish-resource1.png)

在学习者能够看到已分配的支持资源之前，必须先发布该资源：

* 选择`Publish`的世界图标。
* 在弹出的对话框中，再次选择&#x200B;**[!UICONTROL 发布]**。
* 选择&#x200B;**[!UICONTROL 关闭]**。

即使对话框声明该操作已排入队列，它通常也会立即发布。

### 取消发布 {#unpublish}

![取消发布](assets/unpublish.png)

要临时使发布环境中的成员无法访问启用资源，而不删除该资源，请使用`Unpublish`资源的世界图标。

### 报告 {#report}

![资源报表](assets/resource-reports.png)

通过“报表”图标，可访问学员在发布环境中与分配的支持资源交互时生成的报表。 报表因资源类型而异。

对于所有学习路径，都可以根据资源或学习者查看报告(`User Report`)。

![learningpath-info](assets/learningpath-info1.png)

此报表专门针对当前支持资源或学习路径。 提供的报告深度取决于是否为社区站点许可和启用了[Adobe Analytics](analytics.md)。 [时间轴](#timeline)、[查看者参与度](#viewer-engagement)和[按设备参与度](#engagement-by-device)报告根据[轮询间隔](analytics.md#report-importer)从Adobe Analytics导入。

对于所有启用资源，无论是否启用了Adobe Analytics，都有关于[被分派人状态](#assignee-status)和[评级](#ratings)的报告以及[报表摘要](#report-summary)表。

![资源报告](assets/resource-report1.png)

#### 时间轴 {#timeline}

Analytics时间轴报表显示此启用资源的事件在一段时间内发生的时间：

* **视图**

   查看是指学习者访问资源详细信息页面时。

* **播放**

   播放是指alLearner与资源交互（如播放视频或打开PDF）时。

* **评级**

   评分是指学习者为资源分配星级评分时。

* **评论**

   评论是alLearner添加评论时。

纵轴是事件数。

水平轴是日历时间。

[需要Adobe Analytics](sites-console.md#analytics)。

#### 查看器参与度 {#viewer-engagement}

Analytics查看者参与度报表会针对视频资源显示已查看该资源的学习者数量，如果没有播放到最后，则学习者会在什么时间点停止播放该资源。

纵轴是查看了此资源的学习者数量。

水平轴是此资源的持续时间。

[Marketing Cloud组织ID为必填项](sites-console.md#enablement)。

#### 按设备划分的参与 {#engagement-by-device}

对于视频资源，“按设备划分的Analytics参与度”报表描述了从桌面和移动设备播放的查看次数百分比。

[Marketing Cloud组织ID为必填项](sites-console.md#enablement)。

#### 被分派人状态 {#assignee-status}

“被分派人状态”报告基于学习者数量，描述有多少人

* **未启动**
* **进行中**
* **已完成**

#### 评级 {#ratings}

评级报表基于已对启用资源进行评级的学习者数量，显示每个星级评级的数量，然后是总评级数和平均评级的摘要。

#### 报表摘要 {#report-summary}

有关启用资源，报表摘要是一个表格列表。

* 与资源进行交互的每个学员
   * 他们的状态
   * 是否为他们分配了资源
      * 与他们在目录中查找资源不同
      * 已发布的评论数
      * 给定的评级（如果有）

对于学习路径资源报表，报表摘要是一个列出

* 学习路径中包含的每个资源
   * 发布状态
   * 查看次数
   * 播放次数
   * 平均评分
   * 格式
   * 大小
   * 社区站点名称

对于学习路径用户报表，报表摘要是一个表格列表。

* 分配到学习路径的每个学习者：
   * 已完成的资源数。
   * 他们的身份。

可以通过使用`Show / hide columns`选择器选择列来调整表的显示。

#### 以CSV格式下载报表 {#download-report-as-csv}

可以使用控制台顶部的按钮，以CSV格式下载报表摘要表。

* 对于启用资源：`Download Resource Report as CSV`按钮。
* 对于学习路径：`Download Learning Path Report as CSV`按钮。

无论选择何种列进行显示，都会下载完整的报表摘要。
