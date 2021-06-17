---
title: ' [!DNL Experience Manager Assets]的可访问功能和接口'
description: 了解 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 中的辅助功能如何帮助残障用户。
contentOwner: AG
feature: 资产管理
role: Business Practitioner, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '1926'
ht-degree: 2%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}中的辅助功能

[!DNL Adobe Experience Manager] 允许内容创建者和发布者在Web上提供令人惊叹的体验。Adobe努力通过改进[!DNL Experience Manager]的无障碍功能，将残障创建者也包括在内。 该软件不断得到增强，以满足所有类型用户的需求，并遵守包括视力、听觉、移动性或其他残障人士在内的全球标准。

[!DNL Experience Manager] 发布符合性信息，其中描述了符合的标准，概述了产品中的无障碍功能，并描述了符合性级别。无障碍合规性报告可帮助[!DNL Experience Manager]用户了解各种标准的遵守程度。 [!DNL Assets]中的增强功能使所有用户都可以通过键盘、屏幕阅读器、放大镜和其他辅助技术轻松使用界面。

[!DNL Experience Manager] 对以下标准提供不同级别的支持：

* [Web 内容无障碍准则 (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [修订了《康复法》第508条](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [无障碍计划 — 由W3C提供的无障碍富互联网应用程序(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)。

要阅读包含合规性级别详细信息的报告，请参阅[无障碍合规性报告](https://www.adobe.com/accessibility/compliance.html)(ACR)页面。

要了解如何访问[!DNL Dynamic Media]，请参阅 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的[辅助功能。

## 辅助技术{#at-support}

残障用户经常依赖硬件和软件来访问Web内容并使用软件产品。 这些工具被称为辅助技术。 [!DNL Experience Manager Assets] 使用软件的核心功能时，可以使用以下类型的辅助技术(AT):

* 屏幕阅读器和屏幕放大镜。
* 语音识别软件。
* 键盘使用情况 — 导航和快捷键。
* 辅助硬件，包括开关控件、可刷新的盲文显示屏和其他计算机输入设备。
* UI放大工具。

## [!DNL Experience Manager Assets] 可访问的用例  {#accessible-assets-use-cases}

在[!DNL Experience Manager]中，辅助功能满足[!DNL Experience Manager]用户及其客户的两个关键要求。

* 对于内容设计人员和创建者，有一些功能可用于创建和发布客户和网站访客反过来使用的无障碍内容。 残障人士在辅助技术的帮助下使用内容。 有关详细信息，请参阅[Web无障碍准则](/help/managing/web-accessibility.md)。
* [!DNL Experience Manager] 还允许残障用户和管理员访问用于创建和管理内容的用户界面和控件。残障人士可以使用辅助技术来导航、使用和管理[!DNL Assets]功能。

[!DNL Assets]中的核心功能比以前更易访问，并且会定期更新以提高对全球标准的遵从性。 [!DNL Assets]中的CRUD操作在这些操作中具有一定程度的辅助功能。 可通过键盘快捷键、屏幕阅读器文本、颜色对比度等方式，访问添加、管理、搜索和分发资产等DAM工作流。

## 支持使用键盘{#keyboard-use}

许多可单击或可通过指针操作的用户界面元素也可以使用键盘参与。 使用键盘，用户可以专注于UI元素并执行适当的操作。 用户可以使用键盘快捷键直接触发命令或操作，而无需重点关注UI元素并使用键盘触发。 例如，用户可以通过使用键盘浏览到用户界面控件，选择`Return`，然后选择`Alt + 2`键盘快捷键，来打开用户界面左侧资产的时间轴。

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets] {#keyboard-shortcuts}中的键盘快捷键

[!DNL Assets]中的以下操作可使用列出的键盘快捷键。 大多数应用于[!DNL Experience Manager]控制台的键盘快捷键也适用于[!DNL Assets]。 请参阅Console](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)的[键盘快捷键。 请参阅如何[启用或禁用键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)。

| 用户界面或方案 | 键盘快捷键 | 操作 |
|---|---|---|
| [!DNL Assets]用户界面中的列视图 | 向上和向下箭头键 | 导航到同一层次结构中的文件和文件夹。 |
| [!DNL Assets]用户界面中的列视图 | 向左和向右箭头键 | 导航到当前文件夹上方或下方的文件和文件夹。 |
| 在[!DNL Assets]中浏览文件夹 | `/` | 通过打开Omnisearch框来调用搜索。 |
| [!DNL Assets] 控制台 | &amp;grave; | 切换侧边栏 |
| [!DNL Assets] 控制台 | `Alt + 1` | 打开内容树。 |
| [!DNL Assets] 控制台 | `Alt + 2` | 打开[!UICONTROL Navigation]左边栏。 |
| [!DNL Assets] 控制台 | `Alt + 3` | 显示选定资产的[!UICONTROL 时间轴]。 |
| [!DNL Assets] 控制台 | `Alt + 4` | 打开选定资产的Live Copy引用。 |
| [!DNL Assets] 控制台 | `Alt + 5` | 在选定的文件夹中开始搜索和搜索。 |
| 已选择资产或文件夹 | Backspace | 删除选定的资产或文件夹。 |
| 已选择资产或文件夹 | `p` | 打开选定资产的属性页面。 |
| 已选择资产或文件夹 | `e` | 编辑选定的资产。 |
| 已选择资产或文件夹 | `m` | 移动选定的资产。 |
| 已选择资产或文件夹 | `Ctrl + c` | 复制选定的资产。 |
| 已选择资产或文件夹 | `Esc` | 取消选择。 |
| 对话框打开且处于焦点中 | `Esc` | 关闭对话框。 |
| 在DAM的文件夹内 | `Ctrl + v` | 粘贴复制的资产。 |
| [!DNL Assets] 控制台 | `Ctrl + A` | 选择所有资产。 |
| 资产属性页面 | `Ctrl + S` | 保存更改。 |
| [!DNL Assets] 控制台 | `?` | 请参阅键盘快捷键列表。 |

## 登录并导航[!DNL Assets]用户界面 {#login}

用户可以使用键盘导航到并填写登录字段以登录。 每次发生错误时，屏幕阅读器都会显示由于登录页面上用户名和密码组合不正确导致的错误消息。

登录后，DAM用户可以使用键盘在[!DNL Assets]用户界面中导航。 用户界面元素（如左边栏、菜单、用户配置文件、搜索栏、文件和文件夹）以及管理和配置设置均可使用键盘进行导航。 键盘导航顺序为从左到右和从上到下。 使用键盘导航时，焦点时的可操作选项会以更好的颜色对比度突出显示，并由屏幕阅读器讲述。 在适当情况下，屏幕阅读器会宣布菜单中重点选项的状态（例如，展开、折叠和混合状态）。 此外，屏幕阅读器还会朗读可操作选项（而不是外观或界面放置）的用途。

如果用户从菜单中展开帮助或用户配置文件选项，屏幕阅读器会朗读相应的选项或状态。 如果用户扩展了用户配置文件选项，则可以使用键盘选择可用选项。 例如，管理员可以模拟其他用户。 如果用户从[!UICONTROL Help]选项中搜索字符串，则讲述人会宣布“搜索帮助”，以指示正在搜索。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 浏览资产并查看相关信息 {#browse}

在[!DNL Assets]用户界面中，用户可以使用键盘浏览DAM存储库中的现有数字资产列表，预览或下载资产，查看生成的演绎版，切换视图，查看生成的演绎版，查看时间轴和版本历史记录，查看注释和引用，以及查看和管理元数据。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

浏览资产存储库时，以下功能可改进辅助功能：

* 屏幕阅读器会朗读描述图标用途或功能的替换文本，而不是其名称。
* 用户可以使用键盘键访问资产引用列表中的交互式用户界面选项，并将其集中显示。
* 列表视图中每行的元素会由屏幕阅读器作为同一行的元素来宣布。
* 使用`Tab`键导航时，焦点可移至版本预览中的关闭选项。
* 使用键盘浏览时，突出显示的可操作用户界面选项具有更突出的视觉焦点，且对比度增强。 它使得焦点区域对用户更加可识别。
* 使用`Esc`键从缩略图视图中删除快速操作图标不会从最后一个焦点项目中删除键盘焦点。
* 选择资产后，选择`Alt + 4`键盘快捷键会打开左边栏中的[!UICONTROL 引用]列表。 使用`Tab`键，用户可以浏览非零引用条目。 仅浏览非零引用条目也可节省工作和击键。
* 资产时间轴中提供了对资产的评论。 如果使用键盘或键盘快捷键访问左边栏，则可以访问该边栏。
* [!UICONTROL 可使] 用键 [!DNL Experience Manager] 盘访问视图设置。用户可以使用箭头键浏览可用的卡片大小，然后选择并选中选项卡以在现有的“视图设置”视图中导航并设置其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理数字资产{#manage-assets}

许多资产管理任务（如CRUD操作、下载资产、添加元数据）都可以按不同程度进行访问。 [!DNL Assets] 允许您使用各种辅助技术（如屏幕阅读器和键盘）完成任务。

请观看视频演示，了解如何使用键盘浏览[存储库并下载资产](https://youtu.be/K3dgqMRQJys)。

对于元数据操作（通常由营销人员和管理员等角色完成），以下功能可改进辅助功能：

* [!UICONTROL 现在，可以] 使用键盘访问  资产属性页面上的“保存并关闭”选项。
* 屏幕阅读器会朗读资产[!UICONTROL 属性]的[!UICONTROL Basic]选项卡中用于删除所选标记的选项。
* 用户可以使用带键盘的日期选取器弹出对话框。 日期选取器用户界面元素用于设置开启时间和关闭时间，并选择日期。
* 在屏幕阅读器的浏览模式下，使用键盘的拖动功能在[!UICONTROL 元数据架构编辑器]中正确运行。
* 用户可以使用键盘将焦点移动到文件夹[!UICONTROL 属性]的[!UICONTROL 权限]选项卡中[!UICONTROL 已关闭的用户组]下的添加用户或组字段。

## 搜索数字资产{#search-assets}

快速、无缝的资产搜索体验可提高内容速度。 内容周转率用例是核心[!DNL Assets]功能的一部分。 要从Omnisearch栏开始搜索，用户可以使用键盘快捷键`/`或将`Tab`与屏幕阅读器一起使用，以快速找到搜索选项。 当焦点位于搜索选项![搜索选项](assets/do-not-localize/search_icon.png)时，屏幕阅读器会将选项的名称讲述为“搜索按钮”。 用户可以选择`Return`以打开Omnisearch框。 屏幕阅读器不仅讲述在搜索框中键入的关键词，还讲述[!DNL Experience Manager Assets]提供的建议。 用户可以使用箭头键、`Return`和`Tab`的组合来访问各种选项以触发搜索。

搜索功能可通过以下功能访问：

* 页面标题（可供屏幕阅读器使用）有助于将页面识别为资产的搜索页面。
* 用户从Omnisearch字段中搜索资产。 用户可以使用键盘导航或键盘快捷键`/`将其打开。
* 用户可以开始键入搜索关键词，然后使用箭头键选择自动建议。 可以使用`Return`键选择高亮显示的建议，并且会搜索资产以查找选定的建议。
* 筛选搜索结果时，屏幕阅读器可以在“筛选器”面板中识别并读出混合状态复选框（除非您选择所有嵌套谓词，否则未选择并遍历第一级复选框）。
* 在Omnisearch框关闭后，用户焦点将移至搜索选项。

过滤搜索结果时：

* 搜索结果页面提供了一个信息性标题，以便更好地了解屏幕阅读器用户。
* 屏幕阅读器将搜索筛选器中的选项作为可扩展的折叠项来宣布。
* 具有混合状态选项的谓词由屏幕阅读器发布。

## 共享资产 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共享资产时，以下功能可改进辅助功能：

* 用户可以使用键盘在链接共享对话框的搜索和添加电子邮件地址字段中移动焦点。

* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器会显示

   * 加载对话框时，请勿讲述表信息。
   * 可以导航到所有列出的建议。
   * 讲述有关添加电子邮件地址和搜索字段的显示建议。

## 辅助文档{#accessible-docs}

[!DNL Experience Manager] 提供供残障人士使用的辅助文档。在Adobe不断改进模板和内容的同时，以下内容有助于使内容产品当前可访问：

* 屏幕阅读器可以读取文本。
* 图像和插图具有可用的替换文本。
* 可以使用键盘导航。
* 对比度有助于突出文档网站的某些部分。

## 提供反馈{#a11y-feedback}

要提供与辅助功能相关的反馈、提出问题并请求产品增强功能，请使用以下方法：

* 在[www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)填写表单。
* 发送电子邮件至access@adobe.com。

>[!MORELIKETHIS]
>
>* [ [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的辅助功能。
>* [每个Service Pack版本中所做增强功能的发行说明](/help/release-notes/new-features-latest-service-pack.md)。
>* [[!DNL Adobe Experience Manager] 辅助功能指南](/help/managing/web-accessibility.md)。
>* [Adobe解决方案的合规性报告(ACR)和VPAT列表](https://www.adobe.com/accessibility/compliance.html)。

