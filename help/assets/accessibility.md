---
title: 的辅助功能和界面 [!DNL Experience Manager Assets]
description: 了解中的辅助功能 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 帮助残障用户。
contentOwner: AG
feature: Asset Management
role: User, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: 399ae241593b5cc14ef1c2efd090f0d1fae7c2df
workflow-type: tm+mt
source-wordcount: '1924'
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

# 中的辅助功能 [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] 允许内容创建者和发布者在Web上提供出色的体验。 Adobe致力于通过提高的辅助功能，将残障人士包括进来 [!DNL Experience Manager]. 该软件不断得到增强，以满足所有类型的用户的需求，并遵守包括视觉、听觉、行动能力或其他残疾人士在内的全球标准。

[!DNL Experience Manager] 发布一致性信息，描述它遵循的标准，概述产品中的辅助功能，并描述一致性级别。 无障碍合规性报告帮助 [!DNL Experience Manager] 用户了解对各种标准的遵守程度。 在中完成的增强功能 [!DNL Assets] 允许所有用户通过键盘、屏幕阅读器、放大镜和其他辅助技术轻松使用界面。

[!DNL Experience Manager] 为以下标准提供不同级别的支持：

* [Web 内容无障碍准则 (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [修订《康复法》第508条](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [无障碍倡议 — 由W3C提供的无障碍富互联网应用程序(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

要阅读包含合规性级别详细信息的报告，请参阅 [无障碍合规性报告](https://www.adobe.com/cn/accessibility/compliance.html) (ACR)页面。

了解如何 [!DNL Dynamic Media] 可访问，请参见 [中的辅助功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## 辅助技术 {#at-support}

残障用户经常依赖硬件和软件来访问Web内容和使用软件产品。 这些工具被称为辅助技术。 [!DNL Experience Manager Assets] 在使用软件的核心功能时，可以使用以下类型的辅助技术(AT)：

* 屏幕阅读器和屏幕放大镜。
* 语音识别软件。
* 键盘用法 — 导航和快捷键。
* 辅助硬件，包括开关控制、可刷新的盲文显示器和其他计算机输入设备。
* UI放大工具。

## [!DNL Experience Manager Assets] 可访问的用例 {#accessible-assets-use-cases}

In [!DNL Experience Manager]，辅助功能满足的两个关键要求 [!DNL Experience Manager] 用户及其客户。

* 对于内容设计人员和创建者，提供了创建和发布无障碍内容的功能，这些内容依次由他们的客户和网站访客使用。 残障人士在辅助技术的帮助下使用内容。 有关详细信息，请参阅 [Web无障碍准则](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] 还允许残障用户和管理员访问用户界面和控制以创建和管理内容。 残障人士可以使用辅助技术导航、使用和管理 [!DNL Assets] 功能。

中的核心功能 [!DNL Assets] 比以往更容易访问，并且定期更新以更好地符合全球标准。 中的CRUD操作 [!DNL Assets] 在这些功能中内置一定程度的辅助功能。 可通过键盘快捷键、屏幕阅读器文本、颜色对比度等帮助来访问DAM工作流，如添加、管理、搜索和分发资产。

## 支持使用键盘 {#keyboard-use}

许多可以使用指针点击或操作的用户界面元素也可以使用键盘进行接合。 使用键盘，用户可以专注于UI元素并采取适当的操作。 用户可直接使用键盘快捷键来触发命令或操作，而无需专注于UI元素并使用键盘来触发它。 例如，用户可以使用键盘浏览到用户界面控件并选择 `Return`，并选择 `Alt + 2` 键盘快捷键。

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### 中的键盘快捷键 [!DNL Assets] {#keyboard-shortcuts}

中的以下操作 [!DNL Assets] 使用列出的键盘快捷键。 大多数适用于的键盘快捷键 [!DNL Experience Manager] 控制台还适用于 [!DNL Assets]. 参见 [控制台的键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). 了解如何 [启用或禁用键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| 用户界面或方案 | 键盘快捷键 | 操作 |
|---|---|---|
| 中的列视图 [!DNL Assets] 用户界面 | 向上键和向下键 | 导航到同一层次结构中的文件和文件夹。 |
| 中的列视图 [!DNL Assets] 用户界面 | 左右方向键 | 导航到当前文件夹上方或下方的文件和文件夹。 |
| 在中浏览文件夹 [!DNL Assets] | `/` | 通过打开Omnisearch框调用搜索。 |
| [!DNL Assets] 控制台 | 抑音符(&amp;G)； | 切换侧边栏 |
| [!DNL Assets] 控制台 | `Alt + 1` | 打开内容树。 |
| [!DNL Assets] 控制台 | `Alt + 2` | 打开 [!UICONTROL 导航] 左边栏。 |
| [!DNL Assets] 控制台 | `Alt + 3` | 显示 [!UICONTROL 时间线] 选定资源的ID。 |
| [!DNL Assets] 控制台 | `Alt + 4` | 打开所选资产的Live Copy引用。 |
| [!DNL Assets] 控制台 | `Alt + 5` | 在选定的文件夹中开始搜索和搜索。 |
| 已选择资源或文件夹 | 退格符 | 删除选定的资源或文件夹。 |
| 已选择资源或文件夹 | `p` | 打开选定资产的“属性”页面。 |
| 已选择资源或文件夹 | `e` | 编辑所选资源。 |
| 已选择资源或文件夹 | `m` | 移动选定的资源。 |
| 已选择资源或文件夹 | `Ctrl + c` | 复制选定的资源。 |
| 已选择资源或文件夹 | `Esc` | 取消选择。 |
| 对话框打开，并位于焦点中 | `Esc` | 关闭对话框。 |
| 在DAM的文件夹内 | `Ctrl + v` | 粘贴复制的资产。 |
| [!DNL Assets] 控制台 | `Ctrl + A` | 选择所有资源。 |
| 资产属性页面 | `Ctrl + S` | 保存更改。 |
| [!DNL Assets] 控制台 | `?` | 请参阅键盘快捷键列表。 |

## 登录和导航 [!DNL Assets] 用户界面 {#login}

用户可以使用键盘导航并填写登录字段进行登录。 每次发生错误时，屏幕阅读器都会通知由于登录页面上的用户名和密码组合不正确而导致的错误消息。

登录后，DAM用户可以在以下位置导航： [!DNL Assets] 使用键盘的用户界面。 可以使用键盘导航用户界面元素，如左边栏、菜单、用户配置文件、搜索栏、文件和文件夹以及管理和配置设置。 键盘导航顺序为从左至右、从上至下。 使用键盘导航时，聚焦时的一个可操作选项会以更好的颜色对比度突出显示，并由屏幕阅读器朗读。 适当时，屏幕阅读器会宣布菜单中聚焦选项的状态（例如，展开、折叠和混合状态）。 此外，屏幕阅读器会朗读可操作选项的用途，而不是外观或界面放置。

如果用户从菜单中展开帮助或用户配置文件选项，屏幕阅读器将朗读相应的选项或状态。 如果用户展开用户配置文件选项，则可以使用键盘选择可用选项。 例如，管理员可以模拟其他用户。 如果用户从 [!UICONTROL 帮助] 选项，讲述人会朗读“Searching Help”以指示正在搜索。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 浏览资源并查看相关信息 {#browse}

在 [!DNL Assets] 用户界面中，用户可以使用键盘浏览DAM存储库中现有数字资产列表、预览或下载资产、查看生成的演绎版、切换视图、查看生成的演绎版、查看时间轴和版本历史记录、查看注释和引用，以及查看和管理元数据。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

在浏览资产存储库时，以下功能可提高可访问性：

* 屏幕阅读器会朗读描述图标用途或功能的替换文本，而不是图标名称。
* 用户可以使用键盘键访问和焦点资源引用列表中的交互式用户界面选项。
* 列表视图中每行的元素均由屏幕阅读器声明为同一行的元素。
* 使用导航时 `Tab` 键，则焦点可以移动到版本预览中的关闭选项。
* 使用键盘浏览时，突出显示的可操作用户界面选项具有更突出的视觉焦点以及增强的对比度。 它使焦点区域对用户更易于识别。
* 使用 `Esc` 从缩略图视图中删除快速操作图标的键不会从最后一个聚焦项目中删除键盘焦点。
* 选择某个资源后，选择 `Alt + 4` 键盘快捷键打开 [!UICONTROL 引用] 左侧边栏中的列表。 使用 `Tab` 键，用户可在非零引用条目中导航。 仅浏览非零参照条目也节省了工作量和键击次数。
* 资产时间轴中提供了有关资产的注释。 如果使用键盘或键盘快捷键访问左边栏，则可以访问它。
* [!UICONTROL 查看设置] 在 [!DNL Experience Manager] 可使用键盘访问。 用户可以使用箭头键浏览可用卡片大小，选择和Tab键浏览浏览浏览并设置现有“视图设置”视图中的其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理数字资产 {#manage-assets}

许多资源管理任务（如CRUD操作、下载资源、添加元数据）都可不同程度的访问。 [!DNL Assets] 可让您使用各种辅助技术（如屏幕阅读器和键盘）完成任务。

观看视频演示，了解如何使用键盘 [浏览存储库并下载资源](https://youtu.be/K3dgqMRQJys).

对于通常由营销人员和管理员等角色执行的元数据操作，以下功能可提高可访问性：

* [!UICONTROL 保存并关闭] 资产选项 [!UICONTROL 属性] 现在可以使用键盘访问页面。
* 屏幕阅读器会朗读用于删除所选标记的选项 [!UICONTROL 基本] 资产的选项卡 [!UICONTROL 属性].
* 用户可以使用键盘的“日期选取器”弹出对话框。 Datepicker用户界面元素用于设置开启时间和关闭时间，并选择日期。
* 使用键盘的拖动功能在中正常工作 [!UICONTROL 元数据架构编辑器] 在屏幕阅读器的浏览模式下。
* 用户可以使用键盘将焦点移动到下的添加用户或组字段 [!UICONTROL 已关闭的用户组] 在 [!UICONTROL 权限] 文件夹选项卡 [!UICONTROL 属性].

## 搜索数字资产 {#search-assets}

快速、无缝的资产搜索体验可提高内容速度。 内容周转率用例是核心的一部分 [!DNL Assets] 功能。 要从Omnisearch栏开始搜索，用户可以使用键盘快捷键 `/` 或使用 `Tab` 以及屏幕阅读器，以快速找到搜索选项。 当焦点位于搜索选项上时，屏幕阅读器将选项名称叙述为“搜索按钮” ![搜索选项](assets/do-not-localize/search_icon.png). 用户可以选择 `Return` 打开Omnisearch盒。 屏幕阅读器不仅讲述在搜索框中键入的关键字，而且讲述所提供的建议 [!DNL Experience Manager Assets]. 用户可以使用箭头键的组合， `Return`、和 `Tab` 以访问各种选项来触发搜索。

搜索功能可通过以下功能访问：

* 屏幕阅读器可用的页面标题有助于将页面标识为资产的搜索页面。
* 用户在Omnisearch字段中搜索资产。 用户可以使用键盘导航或键盘快捷键打开它 `/`.
* 用户可以开始键入搜索关键词，然后使用箭头键选择自动建议。 高亮显示的建议可使用 `Return` 为所选建议搜索键和资产。
* 在筛选搜索结果时，屏幕阅读器可以识别和朗读混合状态复选框（其中除非您选择所有嵌套谓词，否则不会选择第一级复选框并清除这些复选框）。
* 关闭Omnisearch框后，用户焦点将移动到搜索选项。

筛选搜索结果时：

* 搜索结果页面有一个信息性的标题，以便更好地了解屏幕阅读器用户。
* 屏幕阅读器将搜索筛选器中的选项作为可扩展折叠项发布。
* 屏幕阅读器会声明包含混合状态选项的谓词。

## 共享资源 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

在共享资产时，以下功能可提高可访问性：

* 用户可以使用键盘在链接共享对话框的搜索和添加电子邮件地址字段中移动焦点。

* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器将：

   * 加载对话框时不要讲述表信息。
   * 可以导航到列出的所有建议。
   * 讲述为添加电子邮件地址和搜索字段显示的建议。

## 无障碍文档 {#accessible-docs}

[!DNL Experience Manager] 提供无障碍文档供残障人士使用。 Adobe以下内容有助于在模板和内容持续改进的同时，立即访问所提供的内容：

* 屏幕阅读器可以阅读文本。
* 图像和插图具有可用的替换文本。
* 可以使用键盘导航。
* 对比度有助于突出显示文档网站的某些部分。

## 提供反馈 {#a11y-feedback}

要提供与辅助功能相关的反馈、询问问题和请求产品增强功能，请使用以下方法：

* 填写表单： [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* 请发送电子邮件至access@adobe.com。

>[!MORELIKETHIS]
>
>* [中的辅助功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [每个Service Pack版本中完成的增强功能的发行说明](/help/release-notes/release-notes.md).
>* [[!DNL Adobe Experience Manager] 辅助功能指南](/help/managing/web-accessibility.md).
>* [Adobe解决方案的一致性报告(ACR)和VPAT列表](https://www.adobe.com/cn/accessibility/compliance.html).

