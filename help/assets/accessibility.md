---
title: 中的辅助功能 [!DNL Experience Manager Assets]
description: 了解辅助功能如何 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 帮助残障用户。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 00f5a6194c8c29d358f362441c155c9c2a52cac7
workflow-type: tm+mt
source-wordcount: '1906'
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

[!DNL Adobe Experience Manager] 使内容创建者和发布者能够在Web上提供出色的体验。 Adobe致力于通过改进辅助工具来使残疾创造者参与进来 [!DNL Experience Manager]。 该软件不断得到增强，以满足所有类型用户的需求，并遵守包括具有视觉、听觉、移动或其他障碍的个人在内的全球标准。

[!DNL Experience Manager] 发布符合性信息，描述其所遵循的标准，概述产品中的辅助功能，并描述符合性级别。 辅助功能符合性报告 [!DNL Experience Manager] 可帮助用户了解各种标准的遵守程度。 中完成的增强功 [!DNL Assets] 能使所有用户都能通过键盘、屏幕阅读器、放大镜和其他辅助技术轻松使用界面。

[!DNL Experience Manager] 为以下标准提供不同级别的支持：

* [Web 内容无障碍准则 (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [修订了《康复法》第508条](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [辅助功能计划- W3C提供的可访问的富Internet应用程序(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)。

要阅读包含规范级别详细信息的报告，请参 [阅辅助功能符合性报告](https://www.adobe.com/accessibility/compliance.html) (ACR)页。

<!-- TBD: Add link after release.
To know how [!DNL Dynamic Media] is accessible, see [accessibility in [!DNL Dynamic Media]](/). -->

## 辅助技术 {#at-support}

残障用户经常依赖硬件和软件来访问Web内容和使用软件产品。 这些工具被称为辅助型技术。 [!DNL Experience Manager Assets] 在使用软件的核心功能时，可以使用下列类型的辅助技术(AT):

* 屏幕阅读器和屏幕放大镜。
* 语音识别软件。
* 键盘使用——导航和快捷键。
* 辅助硬件，包括开关控件、可刷新的盲文显示和其他计算机输入设备。
* UI放大工具。

## [!DNL Experience Manager Assets] 可访问的用例 {#accessible-assets-use-cases}

其中 [!DNL Experience Manager]，辅助功能满足了用户及其客户的两 [!DNL Experience Manager] 个关键要求。

* 对于内容设计人员和创作人员，有一些功能可用于创建和发布可供其客户和网站访客反过来使用的可访问内容。 残障人士在辅助型技术的帮助下使用内容。 有关详细信息，请参 [阅Web辅助功能指南](/help/managing/web-accessibility.md)。
* [!DNL Experience Manager] 还允许残障用户和管理员访问用户界面和控件来创建和管理内容。 残障人士可以使用辅助技术导航、使用和管理 [!DNL Assets] 功能。

中的核心功能 [!DNL Assets] 比以前更易于访问，并会定期更新以改进对全球标准的遵守。 中的CRUD操作 [!DNL Assets] 具有一定程度的辅助功能。 通过键盘快捷键、屏幕阅读器文本、颜色对比度等，可以访问添加、管理、搜索和分发资产等DAM工作流。

## 支持使用键盘 {#keyboard-use}

许多可单击或可操作指针的用户界面元素也可以使用键盘。 使用键盘，用户可以专注于UI元素并采取适当的操作。 用户无需关注UI元素并使用键盘触发命令或操作，即可直接使用键盘快捷键触发命令或操作。 例如，用户可以使用键盘和选择键盘快捷键浏览至用户界面控件，然后打开用户界面左侧资 `Return`产的时 `Alt + 2` 间轴。

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### 键盘快捷键 [!DNL Assets] {#keyboard-shortcuts}

下列操作可 [!DNL Assets] 以使用列出的键盘快捷键。 大多数应用于控制台的键 [!DNL Experience Manager] 盘快捷键也适用于 [!DNL Assets]控制台。 See [keyboard shortcuts for Consoles](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). 了解如何 [启用或禁用键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)。

| 用户界面或方案 | 键盘快捷键 | 操作 |
|---|---|---|
| 用户界面中的 [!DNL Assets] 列视图 | 向上和向下箭头键 | 导航到同一层次结构中的文件和文件夹。 |
| 用户界面中的 [!DNL Assets] 列视图 | 向左和向右箭头键 | 导航到当前文件夹上方或下方的文件和文件夹。 |
| 在 [!DNL Assets] | `/` | 通过打开Omnisearch框调用搜索。 |
| [!DNL Assets] 控制台 | ` | 切换侧边栏 |
| [!DNL Assets] 控制台 | `Alt + 1` | 打开内容树。 |
| [!DNL Assets] 控制台 | `Alt + 2` | 打开 [!UICONTROL 导航] 左边栏。 |
| [!DNL Assets] 控制台 | `Alt + 3` | 显示 [!UICONTROL 选定] 资产的时间轴。 |
| [!DNL Assets] 控制台 | `Alt + 4` | 打开选定资产的Live Copy引用。 |
| [!DNL Assets] 控制台 | `Alt + 5` | 开始在所选文件夹中搜索和搜索。 |
| 已选择资产或文件夹 | Backspace | 删除选定的资产或文件夹。 |
| 已选择资产或文件夹 | `p` | 打开选定资产的“属性”页面。 |
| 已选择资产或文件夹 | `e` | 编辑选定的资产。 |
| 已选择资产或文件夹 | `m` | 移动选定的资产。 |
| 已选择资产或文件夹 | `Ctrl + c` | 复制选定的资产。 |
| 已选择资产或文件夹 | `Esc` | 取消选择选择。 |
| 对话框打开并处于焦点中 | `Esc` | 关闭对话框。 |
| 在DAM中的文件夹中 | `Ctrl + v` | 粘贴复制的资产。 |
| [!DNL Assets] 控制台 | `Ctrl + A` | 选择所有资产。 |
| 资产属性页 | `Ctrl + S` | 保存更改。 |
| [!DNL Assets] 控制台 | `?` | 请参阅一列表键盘快捷键。 |

## 登录并导航用 [!DNL Assets] 户界面 {#login}

用户可以使用键盘导航并填写登录字段以登录。 每次出现错误时，屏幕阅读器会通知由于登录页面上的用户名和密码组合不正确而导致的错误消息。

登录后，DAM用户可以使用键盘在 [!DNL Assets] 用户界面中导航。 用户界面元素(如左边栏、菜单、用户用户档案、搜索栏、文件和文件夹)以及管理和配置设置都可以使用键盘进行导航。 键盘导航顺序为从左到右和从上到下。 使用键盘导航时，焦点时可执行的选项会以更好的颜色对比度高亮显示，并由屏幕阅读器解说。 如果适用，屏幕阅读器会宣布菜单中重点选项的状态，例如展开、折叠和混合状态。 此外，屏幕阅读器还宣布了可操作选项的用途，而不是说外观或界面位置。

如果用户从菜单中展开帮助或用户用户档案选项，屏幕阅读器将宣布相应的选项或状态。 如果用户展开用户用户档案选项，则可以使用键盘选择可用选项。 例如，管理员可以模拟其他用户。 如果用户从“帮助”选项中搜 [!UICONTROL 索字] 符串，则解说员将宣布“搜索帮助”以指示正在进行搜索。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 浏览资源并视图相关信息 {#browse}

在用户 [!DNL Assets] 界面中，用户可以使用键盘浏览DAM存储库中现有数字资产的列表、预览或下载资产、查看生成的演绎版、切换视图、查看生成的演绎版、查看时间轴和版本历史记录、查看注释和引用以及视图和管理元数据。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close button in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close button through keyboard press in version preview dialog. After fix, user can close dialog through close button using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

在浏览资产存储库时，以下功能改进了辅助功能：

* 屏幕阅读器将发布替代文本，这些替代文本描述图标的用途或功能，而不是图标的名称。
* 用户可以使用键盘键访问资产的引用列表中的交互式用户界面选项并将其集中显示。
* 列表视图中每行中的元素由屏幕阅读器作为同一行的元素进行宣布。
* 使用键导 `Tab` 航时，焦点可移至版本预览中的关闭选项。
* 使用键盘进行浏览时，突出显示的可操作用户界面选项具有更突出的视觉焦点和增强的对比度。 它使聚焦区域对用户更加可识别。
* 使用键从 `Esc` 缩略图视图删除快速操作图标不会从最后一个聚焦的项目删除键盘焦点。
* 选择资产后，选择键 `Alt + 4` 盘快捷键会打 [!UICONTROL 开左边栏] 中的引用列表。 使 `Tab` 用键，用户可以浏览非零引用条目。 仅浏览非零引用条目也省去了工作和按键。
* 资产时间轴中提供对资产的评论。 如果使用键盘或键盘快捷键访问左边栏，则可访问该边栏。
* [!UICONTROL 视图] “ [!DNL Experience Manager] 设置”可通过键盘访问。 用户可以使用箭头键浏览可用的卡大小，然后选择并跳转，以在现有视图设置视图中导航和设置其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Manage digital assets {#manage-assets}

许多资产管理任务（如CRUD操作、下载资产、添加元数据）都可以在不同程度上进行访问。 [!DNL Assets] 允许您使用屏幕阅读器和键盘等各种辅助技术完成任务。

观看一个视频演示，了解如何使用键 [盘浏览存储库和下载资产](https://youtu.be/K3dgqMRQJys)。

对于元数据操作（通常由营销人员和管理员等角色完成），以下功能可改进辅助功能：

* [!UICONTROL 现在可以使] 用键盘访 [!UICONTROL 问资产] “属性”页面上的“保存并关闭”选项。
* 屏幕阅读器会宣布删除资产属性的“基 [!UICONTROL 本] ”选项卡中选 [!UICONTROL 定标记]。
* 用户可以将“日期选取器”弹出对话框与键盘一起使用。 Datepicker用户界面元素用于设置开启时间和结束时间，以及选择日期。
* 在屏幕阅读器的浏览模式下，使用键盘的 [!UICONTROL 拖动功能在元数] 据模式编辑器中正确发挥作用。
* 用户可以使用键盘将焦点移动到文件夹属性的“权限”选项卡 [!UICONTROL 的“已关闭的用户组] ”下 [!UICONTROL 的“添加用户] ”或“ [!UICONTROL 组”字段]。

## 搜索数字资产 {#search-assets}

快速、无缝的资产搜索体验提高了内容速度。 内容速度使用案例是核心功能的一 [!DNL Assets] 部分。 要从搜索栏开始搜索，用户可以使用键盘快捷键或 `/` 与屏 `Tab` 幕阅读器一起使用以快速找到搜索选项。 当焦点在搜索选项搜索选项上时，屏幕阅读器将选项的名称解说为“搜索 ![按钮”](assets/do-not-localize/search_icon.png)。 用户可以选 `Return` 择打开“搜索”框。 屏幕阅读器不仅会讲述在搜索框中键入的关键字，还会讲述由提供的建议 [!DNL Experience Manager Assets]。 用户可以使用箭头键组合 `Return`，并 `Tab` 访问各种选项以触发搜索。

搜索功能可通过以下功能进行访问：

* 页面标题（对于屏幕阅读器可用）有助于将页面标识为资产的搜索页面。
* 用户从“全局搜索”字段中搜索资产。 用户可以使用键盘导航或键盘快捷键打开它 `/`。
* 用户可以开始键入搜索关键字，然后使用箭头键选择自动建议。 可以使用键选择突出显示的 `Return` 建议，并搜索资产以查找选定的建议。
* 在筛选搜索结果时，屏幕阅读器可以在过滤器面板中识别和宣布混合状态复选框（除非您选择所有嵌套谓词，否则不会选择并检查第一级复选框）。
* 关闭Omnisearch框后，用户焦点将移至搜索选项。

筛选搜索结果时：

* 搜索结果页面包含信息性标题，可更好地了解屏幕阅读器用户。
* 屏幕阅读器将搜索筛选器中的选项作为可扩展的折叠宣布。
* 具有混合状态选项的谓词由屏幕阅读器宣布。

## 共享资产 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共享资源时，以下功能可改进辅助功能：

* 用户可以在链接共享对话框的“搜索”和“添加电子邮件地址”字段中使用键盘移动焦点。

* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器、

   * 加载对话框时，不要解说表信息。
   * 可导航到所有列出的建议。
   * 解说显示的“添加电子邮件地址”和“搜索”字段的建议。

## 可访问的文档 {#accessible-docs}

[!DNL Experience Manager] 提供可供残障人士使用的可访问文档。 以下内容有助于使内容产品目前可访问，同时Adobe继续改进模板和内容：

* 屏幕阅读器可以阅读文本。
* 图像和插图具有可用的替代文本。
* 可进行键盘导航。
* 对比度有助于突出显示文档网站的某些部分。

## 提供反馈 {#a11y-feedback}

要提供与辅助功能相关的反馈、提出问题和请求产品增强功能，请使用以下方法：

* 请在www.adobe.com/accessibility/feedback.html填写 [表单](https://www.adobe.com/accessibility/feedback.html)。
* 请发送电子邮件至access@adobe.com。

>[!MORELIKETHIS]
>
>* [每个版本中增强功能的发行说明](/help/release-notes/new-features-latest-service-pack.md)。
>* [[!DNL Adobe Experience Manager] 辅助功能指南](/help/managing/web-accessibility.md)。
>* [Adobe解决方案的符合性报告(ACR)和VPAT列表](https://www.adobe.com/accessibility/compliance.html)。

