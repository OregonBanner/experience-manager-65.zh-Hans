---
title: Enablement Resources Console
seo-title: Enablement Resources Console
description: “资源”控制台是Enablement Managers创建、管理资源并将资源分配给Enablement社区站点成员的位置
seo-description: “资源”控制台是Enablement Managers创建、管理资源并将资源分配给Enablement社区站点成员的位置
uuid: 52445b39-c339-4b39-8004-eb36de99bced
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1ef15e76-fe7c-4ced-a20d-c0a9385e3ee4
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Enablement Resources Console {#enablement-resources-console}

对于AEM Communities,“资源”控制台是 [Enablement Managers](users.md) 创建、管理资源并将资源分配给Enablement Community站点成员的位置。

## 要求 {#requirements}

在为社区站点添加启用资源之前，必须正确配置AEM实例，包括：

* SCORM
* FFmpeg

有关详细信息，请参阅 [配置启用](enablement.md)。

>[!CAUTION]
>
>如果在社区站点创建后安装了SCORM，则必须重新创建安装SCORM之前存在的任何启用资源。



>[!NOTE]
>
>随着 [AEM 6.3](deploy-communities.md#latestfeaturepack) 版本和同等的Communities功能包 [AEM 6.2 FP3](deploy-communities.md#latestfeaturepack) 和 [AEM 6.1 FP](https://docs.adobe.com/content/docs/en/aem/6-1/deploy/communities.html#Latest Feature Pack)的推出，启用功能不再需要 [](mysql.md)MySQL数据库fp7。


## 术语 {#terminology}

### 资源 {#resource}

资源对于支持社区 [至关重要](overview.md#enablement-community)。 它们是分配给成员的材料，使他们能够提高技能。

资源的特性：

* 可能为：
   * 图像(JPG、PNG、GIF、BMP)
   * 视频(MP4)
   * Flash(SWF)
   * 文档(PDF)
   * 测验(SCORM)
* 可以从一个或多个学习路径中引用。

### 学习路径 {#learning-path}

学习路径是一组分组在一起的支持资源的逻辑集合，便于分配给成员。

### 成员组 {#members-group}

创建社区站点时，为URL给定的站点名称用于创建为不同角色配置了各种权限的站 [点特定用户组](users.md) 。 所有这些自动创建的用户组都带有前缀 `Community <site-name>`。

此类用户组是组， `Community <site-name> Members` 该组将发布环境中的注册用户标识为社区成员。 有关示例，请 [参阅教程AEM Communities快速入门](getting-started-enablement.md) 。

对于 [参与社区](overview.md#egagementcommunity)，允许站点访客自行注册或使用社交登录是合理的，在此时，他们会自动添加到成员组。

对于 [启用社区](overview.md#enablement-community)，建议将站点设为私有，然后需要管理员将用户添加到成员组。

## 访问社区站点的Enablement Resources {#accessing-a-community-site-s-enablement-resources}

### 导航到社区资源 {#navigate-to-communities-resources}

在创作环境中，要访问“资源”控制台

* 从全局导航：“导 **[!UICONTROL 航]** ”>“社 **[!UICONTROL 区”]** >“资 **[!UICONTROL 源”]**

   ![chlimage_1-163](assets/chlimage_1-163.png)

### 选择社区站点 {#select-a-community-site}

“社区资源”控制台将显示所有社区站点。

从“资源”控制台中选择站点后，将为特定社区站点创建启用资源。

选择特定社区站点后，可访问任何现有的支持资源和学习路径以进行管理和修改，并可创建新的支持资源和学习路径。

![chlimage_1-164](assets/chlimage_1-164.png)

#### 搜索 {#search-features}

![chlimage_1-165](assets/chlimage_1-165.png)

选择侧面板切换图标以搜索启用资源或学习路径。 选择后，控制台左侧的搜索面板将打开，并提供一个文本框，可在其中输入搜索词。

![chlimage_1-166](assets/chlimage_1-166.png)

#### 选择模式 {#selection-mode}

要选择多个启用资源，请将指针悬停在卡上并选择复选标记图标，以选择第一个启用资源。 选择卡后，选择任何其他卡片会将其添加到选择组。 再次选择卡将取消选择。

![chlimage_1-167](assets/chlimage_1-167.png)

## 创建资源 {#create-a-resource}

![chlimage_1-168](assets/chlimage_1-168.png)

向社区站点添加新的启用资源

* Select the `Create` icon.
* 从显示的子菜单中，选择“资 **[!UICONTROL 源”]**。

此操作将启动以下步骤的分步过程：

* 描述资源（名称、卡图像和文本）。
* 选择资源内容。
* 为资源选择封面图像。
* 识别资源联系人。
* 将资源分配给成员。

当资源是课程的一部分（即学习路径）时，只应将成员分配到学习路径。 在创建启用资源后，可以添加分配。

### 1 Basic Info {#basic-info}

![chlimage_1-169](assets/chlimage_1-169.png)

* **[!UICONTROL 添加]**

   (可&#x200B;*选*)要在成员的分配页面和资源控制台中的启用资源卡片上显示的图像。 从服务器的本地文件系统中选择该图像。 如果未提供图像，则将为上传的资源生成缩略图。

   ***注意***:建议的图像大小不仅为480 x 480像素。 由于卡的响应式设计具有不同的浏览器尺寸，因此显示大小将从220 X 165像素变为400 x 165像素。

* **[!UICONTROL 网站名称]**

   (*只读*)要添加资源的社区站点。

* **[!UICONTROL 资源名称]**

   (必&#x200B;*需*)资源的显示名称。 根据显示名称创建有效的节点名称。

* **[!UICONTROL 标记]**

   (可&#x200B;*选*)可以选择一个或多个标记，将启用资源与一个或多个目录相关联。 请参阅 [标记启用资源](tag-resources.md)。

* **[!UICONTROL 在目录中显示]**

   取消选中后，启用资源将不会显示在任何目录中。 如果选中此项，则启用资源将显示在所有目录中，除 [非已预过滤](catalog-developer-essentials.md#pre-filters) ，或UI中的成员过滤器。 默认为未选中。

* **[!UICONTROL 描述]**

   (可&#x200B;*选*)要显示的启用资源说明。

* **[!UICONTROL 较小的资产]**

   (可&#x200B;*选*)从AEM资产中选择。 用于表示发布环境（如在目录中）中的资源的缩略图。

* **[!UICONTROL 较大的资产]**

   (可&#x200B;*选*)从AEM资产中选择。 在发布环境中表示资源的大图像，例如在资源的主页上。

* **[!UICONTROL 内容片段资产]**

   (可&#x200B;*选*)从AEM资产中选择。 可能在发布环境中引用但默认未使用的内容片段。

* Select **[!UICONTROL Next]**

### 2 Add Content {#add-content}

![chlimage_1-170](assets/chlimage_1-170.png)

虽然它看起来好像可能选择了多个启用资源，但只允许一个。

选择 `'+' icon`右上角的，以通过标识源开始选择资源的过程。

![chlimage_1-171](assets/chlimage_1-171.png)

* **[!UICONTROL 从我的本地文件上传]**

   从本地文件系统上传将使用本机文件浏览器选择并上传文件。 支持的文件类型有SCORM.zip（HTML5或SWF）、MP4视频、SWF、PDF和图像类型(JPG、PNG、GIF、BMP)。 文件名将变为添加到资产库的资产名称。

* **[!UICONTROL 浏览资产库]**

   从资产库中进行选择。 选择仅限于社区站点中可见的选项。

* **[!UICONTROL 添加外部 URL]**

   输入指向学习内容的链接。

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

      Adobe Connect会话的URL。

* **[!UICONTROL 定义外部资源]**

   输入要展示物料的位置。 成功状态和得分的值是手动输入的(请参阅 [报告](reports.md))。 上传的封面图像可用于提供其他信息。

   在打开的对话框中，输入：

   * **[!UICONTROL 标题]**

      启用资源的资产名称。

   * **[!UICONTROL 位置]**

      物理站点（如教室）的位置。

#### 已添加视频资源的示例 {#example-of-an-added-video-resource}

![chlimage_1-172](assets/chlimage_1-172.png)

* **[!UICONTROL 资源封面图像]**

   封面图像是在首次查看启用资源时要显示的图像。 例如，当视频资源尚未播放时，将显示封面图像。 如果未上传自定义图像，则显示默认图像。 对于视频资源，可能会生成缩 [略图](enablement.md#ffmpeg)，但只有在上传时，而不是在视频作为URL引用时。 对于位置资源，图像可用于提供其他信息。

   封面图像的建议大小为640 x 360 px。

* 选择&#x200B;**[!UICONTROL 下一步]**。

### 3 Settings {#settings}

![chlimage_1-173](assets/chlimage_1-173.png)

>[!NOTE]
>
>不应直接在要从学习路径引用的启用资源中登记学员。 学员只需在学习路径中登记即可。
>
>如果某个会员同时登记了引用该资源的资源和学习路径，则其分配将同时显示学习路径中的单一资源和资源。


* **[!UICONTROL 社交设置]**

   这些设置控制学员是否能够提供有关启用资源的输入。 审核 [设置](sites-console.md#moderation) ，是父社区站点的设置。

   * **[!UICONTROL 允许评论]**

      如果选中此项，则允许成员对资源进行评论。 选中默认值。

   * **[!UICONTROL 允许评级]**

      如果选中此项，则允许成员对资源进行评级。 选中默认值。

   * **[!UICONTROL 允许匿名访问]**

      如果选中此项，则允许匿名站点访客在社区站点也允许匿名访问时视图目录中的资源。 默认为未选中。

* **[!UICONTROL 到期日期]**

   *（可选）* A date which the assignment should be completed by the signment.

* **[!UICONTROL 资源作者]**

   *（可选）* Enablement Resource的作者。 使用下拉菜单从成员组的成员用户中进 [行选择](#members-group)。

* **[!UICONTROL 资源联系和映射；ast;]**

   *（必需）* ，会员可以联系的与启用资源相关的人员。 使用下拉菜单从成员组的成员用户中进 [行选择](#members-group)。

* **[!UICONTROL 资源专家]**

   *（可选）* ，会员可以联系的人员，他们具有与启用资源相关的专业知识。 使用下拉菜单从成员组的成员用户中进 [行选择](#members-group)。

### 4 Assignments {#assignments}

![chlimage_1-174](assets/chlimage_1-174.png)

* **[!UICONTROL 添加代理人]**

   使用下拉菜单从会员 [中进行选择](#members-group) -用户和用户组（以粗体列出）-将作为学员登记的用户和用户组。 当会员登录社区站点时，其登记的启用资源（和学习路径）将显示在其“任务分配”页 [面上](functions.md#assignments-function) 。

* 选择&#x200B;**[!UICONTROL 创建]**。

   ![chlimage_1-175](assets/chlimage_1-175.png)

成功创建启用资源会返回到“资源”控制台，并且新创建的资源处于选中状态。 在此控制台中，可以管 [理资源](#managing-a-resource)。

## Create a Learning Path {#create-a-learning-path}

![chlimage_1-176](assets/chlimage_1-176.png)

向社区站点添加新的学习路径

* 选择图 `Create` 标
* 从显示的子菜单中，选择“学习 **[!UICONTROL 路径”]**。

此操作将启动以下步骤的分步过程：

* 识别学习路径。
* 提供卡图像以表示学员的学习路径。
* 引用启用资源以包含在学习路径中。
* （可选）对资源进行排序。
* （可选）确定入门项目学习路径。
* 识别学习路径联系人。
* 登记会员。

对于包含在学习路径中的启用资源，应仅为学习路径分配任务，而不为单个资源分配任务。

### 基本信息 {#basic-info-1}

![chlimage_1-177](assets/chlimage_1-177.png)

* **[!UICONTROL 添加]**

   (可&#x200B;*选*)要在成员的分配页面以及“资源”控制台中学习路径的卡片上显示的图像。 从服务器的本地文件系统中选择该图像。 如果未提供图像，则将为上传的资源生成缩略图。

   ***注意***:建议的图像大小不再只是480 x 480像素。 由于卡的响应式设计具有不同的浏览器尺寸，因此显示大小将从220 X 165像素变为400 x 165像素。

* **[!UICONTROL 网站名称]**

   (*只读*)要添加资源的社区站点。

* **[!UICONTROL 学习路径名称]**

   (必&#x200B;*需*)学习路径的显示名称。 根据显示名称创建有效的节点名称。

* **[!UICONTROL 标记]**

   (可&#x200B;*选*)可以选择一个或多个标记，将学习路径与一个或多个目录相关联。 请参阅 [标记启用资源](tag-resources.md)。

* **[!UICONTROL 在目录中显示]**

   取消选中后，学习路径将不会显示在任何目录中。 如果选中此项，则除非已预过滤或UI中 [的成员过滤器](catalog-developer-essentials.md#pre-filters) ，否则学习路径将显示在所有目录中。 在目录中显示学习路径将间接授予对其所有包含资源的READ访问权。 默认为未选中。

* **[!UICONTROL 描述]**

   (可&#x200B;*选*)要显示的启用资源说明。

* **[!UICONTROL 较小的资产]**

   (可&#x200B;*选*)从AEM资产中选择。 用于表示发布环境（如在目录中）中的资源的缩略图。

* **[!UICONTROL 较大的资产]**

   (可&#x200B;*选*)从AEM资产中选择。 在发布环境中表示资源的大图像，例如在资源的主页上。

* **[!UICONTROL 内容片段资产]**

   (可&#x200B;*选*)从AEM资产中选择。 可能在发布环境中引用但默认未使用的内容片段。

* 选择&#x200B;**[!UICONTROL 下一步]**。

### 添加必备项 {#add-prerequisites}

![chlimage_1-178](assets/chlimage_1-178.png)

* **[!UICONTROL 必要的学习路径]**

   (可&#x200B;*选*)选择其他已发布的学习路径后，学员必须完成这些路径，才能选择此学习路径。

* 选择&#x200B;**[!UICONTROL 下一步]**。

### 添加资源 {#add-resources}

![chlimage_1-179](assets/chlimage_1-179.png)

* **[!UICONTROL 强制执行学习路径中的排序]**

   (可&#x200B;*选*)如果设置为“开”，则添加启用资源的顺序是学员在学习路径中继续学习的顺序。 默认为关闭。

* **[!UICONTROL 资源]**

   从为当前社区站点创建的已发布 *启用资源* 中选择的一个或多个资源。

>[!NOTE]
>
>您只能选择与学习路径处于同一级别的可用资源。 例如，对于在组中创建的学习路径，只有组级别资源可用；对于在社区站点中创建的学习路径，该站点中的资源可用于添加到学习路径。


* 选择&#x200B;**[!UICONTROL 下一步]**。

### 设置 {#settings-1}

![chlimage_1-180](assets/chlimage_1-180.png)

* **[!UICONTROL 添加注册]**

   使用下拉菜单从社区站点的成员组和成员组（以粗体列出）中进行 [选择](#members-group)。 在首次创建学习路径时，无需添加任务。 可以修改学习路径属性以在以后添加学员。

* **[!UICONTROL Learning Path Contact&amp;ast;]**

   *（必需）* ，会员可以联系的与学习路径相关的人员。 使用下拉菜单从社区站点的成员组中的用户中进行 [选择](#members-group)。

* Select **[!UICONTROL Create]**

>[!NOTE]
>
>从学习路径引用的启用资源不应列表同一个被分派人（学员）（如果有）。
>
>如果某个会员同时登记了启用资源和引用该资源的学习路径，则其分配将同时显示学习路径中的单一资源和资源。


## 管理资源 {#managing-a-resource}

要管理单个启用资源，请执行以下操作：

* 从“资 **[!UICONTROL 源]** ”控制台中，选择包含该资源的社区站点。
* 选择资源。

对于选定的启用资源，可以：

* 视图属性（默认）
* 编辑属性
* 删除
* 发布
* 取消发布

要上传启用资源的新版本，建议创建新资源，然后从旧版本中取消登记成员并将他们登记到新版本中。

### 编辑资源 {#edit-resource}

![chlimage_1-181](assets/chlimage_1-181.png)

通过选择铅笔图标，显示用于创建启用资源的步骤变得可用，以便可以修改提供的任何信息。

如果唯一的更改是修改设置步骤中的分配，则保存更改将导致修改被发布。 如果进行了任何其他更改，则在保存后必须显式发布资源。

### 删除资源 {#delete-resource}

![chlimage_1-182](assets/chlimage_1-182.png)

通过选择垃圾桶图标，启用资源将在确认 `Deleted` 后显示。

### 发布 {#publish}

![chlimage_1-183](assets/chlimage_1-183.png)

在学员能够查看分配的支持资源之前，必须先发布该资源：

* 选择要显示的全球图标 `Publish`。
* 在弹出的对话框中，再次选择 **[!UICONTROL 发布]** 。
* 选择 **[!UICONTROL 关闭]**。

即使对话框声明操作已排队，它通常也会立即发布。

### 取消发布 {#unpublish}

![chlimage_1-184](assets/chlimage_1-184.png)

要临时使发布环境中的成员无法访问启用资源，但不删除它，请使用资源的“世界” `Unpublish` 图标。

### 报告 {#report}

![chlimage_1-185](assets/chlimage_1-185.png)

通过“报告”图标，学员可以访问在发布环境中与分配的启用资源交互时生成的报告。 报告因资源类型而异。

对于所有学习路径，可以基于资源或学员视图报告( `User Report`.)

![chlimage_1-186](assets/chlimage_1-186.png)

此报告专门针对当前支持资源或学习路径。 提供的报告深度取决于 [Adobe Analytics](analytics.md) 是否为社区站点授权和启用。 “时 [间轴](#timeline)”、“查 [看者参与情况](#viewer-engagement)”和“按参与情况”报 [表会基于轮询间隔设备从Adobe Analytics](#engagement-by-device)[](analytics.md#report-importer)导入。

对于所有启用资源，无论是否启用Adobe Analytics，都会显示“被分派人状态 [”和“](#assignee-status) 评级 [”以及“报](#ratings) 告摘要 [](#report-summary) ”表。

![chlimage_1-187](assets/chlimage_1-187.png)

#### 时间轴 {#timeline}

分析时间线报告显示此启用资源在一段时间内发生事件的时间：

* **视图**

   视图是指学员访问资源详细信息页面时。

* **播放**

   播放是学习者与资源交互时播放的内容，如播放视频或打开PDF。

* **评级**

   评级是指学员为资源分配星级时。

* **评论**

   评论是alLearner添加评论时。

垂直轴是事件数。

水平轴是日历时间。

[需要Adobe Analytics](sites-console.md#analytics)。

#### 查看器参与度 {#viewer-engagement}

“Analytics查看器参与”报告显示视频资源的已查看该资源的学员数，如果未播放到最后，学员在什么时候停止播放该资源。

垂直轴是已查看此资源的学员数。

水平轴是此资源的持续时间。

[需要Marketing Cloud组织ID](sites-console.md#enablement)。

#### 按设备划分的参与 {#engagement-by-device}

“按设备分析参与情况”报告（针对视频资源）描述了从桌面和移动设备播放的视图百分比。

[需要Marketing Cloud组织ID](sites-console.md#enablement)。

#### 代理人状态 {#assignee-status}

“被分派人状态”报告根据学员数说明有多少学员

* **未开始**
* **进行中**
* **已完成**

#### 评级 {#ratings}

“评级”报告基于已对启用资源进行评级的学员数，显示每个星级的数量，后跟总评级数和平均评级的摘要。

#### 报告摘要 {#report-summary}

对于启用资源，“报告摘要”是表列表。

* 已与资源交互的每个学员
   * 他们的状态
   * 是否为他们分配了资源
      * 与其在目录中查找资源相反
      * 已发布的评论数
      * 给定的评级（如果有）

对于学习路径资源报告，报告摘要是一个表列表

* 学习路径中包含的每个资源
   * 发布状态
   * 视图数
   * 播放次数
   * 平均评级
   * 格式
   * 大小
   * 社区站点名称

对于学习路径用户报告，报告摘要是一个表列表。

* 分配给学习路径的每个学员：
   * 已完成的资源数。
   * 他们的身份。

使用选择器选择列，可以调整表的显 `Show / hide columns` 示。

#### Download Report as CSV {#download-report-as-csv}

“报告摘要”(Reports Summary)表格可使用控制台顶部的按钮以CSV格式下载。

* 对于启用资源：按钮的 `Download Resource Report as CSV` 子菜单。
* 对于学习路径：按钮的 `Download Learning Path Report as CSV` 子菜单。

将下载完整的“报告摘要”，而不管选择哪些列显示。
