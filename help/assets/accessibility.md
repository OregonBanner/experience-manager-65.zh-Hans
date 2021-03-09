---
title: ' [!DNL Experience Manager Assets]中的辅助功能'
description: 了解 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] 中的辅助功能如何帮助残障用户。
contentOwner: AG
translation-type: tm+mt
source-git-commit: cf86d0c38e326766b35318e78a94a3f32e166e01
workflow-type: tm+mt
source-wordcount: '1919'
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

[!DNL Adobe Experience Manager] 使内容创建者和发布者能够在Web上提供令人惊叹的体验。Adobe努力通过改进[!DNL Experience Manager]的可访问性，使残疾创造者参与进来。 该软件不断得到增强，以满足所有类型用户的需求，并符合包括有视觉、听觉、移动或其他障碍的个人在内的全球标准。

[!DNL Experience Manager] 发布符合性信息，描述符合的标准，概述产品中的辅助功能，并描述符合性级别。辅助功能符合性报告有助于[!DNL Experience Manager]用户了解各种标准的遵守程度。 [!DNL Assets]中完成的增强功能使所有用户都能通过键盘、屏幕阅读器、放大器和其他辅助技术轻松使用界面。

[!DNL Experience Manager] 为以下标准提供不同级别的支持：

* [Web 内容无障碍准则 (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [修订了《康复法》第508条](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [辅助功能计划 — W3C提供的可访问的富Internet应用程序(WAI-ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)。

要阅读包含规范级别详细信息的报告，请参阅[辅助功能符合性报告](https://www.adobe.com/accessibility/compliance.html)(ACR)页。

要了解如何访问[!DNL Dynamic Media]，请参阅 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的[辅助功能。

## 辅助技术{#at-support}

残障用户经常依赖硬件和软件来访问Web内容和使用软件产品。 这些工具被称为辅助型技术。 [!DNL Experience Manager Assets] 使用软件的核心功能时，可以使用以下类型的辅助技术(AT):

* 屏幕阅读器和屏幕放大镜。
* 语音识别软件。
* 键盘使用 — 导航和快捷键。
* 辅助硬件，包括开关控件、可刷新的盲文显示和其他计算机输入设备。
* UI放大工具。

## [!DNL Experience Manager Assets] 可访问的用例  {#accessible-assets-use-cases}

在[!DNL Experience Manager]中，辅助功能满足了[!DNL Experience Manager]用户及其客户的两个关键要求。

* 对于内容设计人员和创作人员，有一些功能可用于创建和发布供其客户和网站访客依次使用的辅助内容。 残障人士在辅助技术的帮助下使用内容。 有关详细信息，请参阅[Web辅助功能指导原则](/help/managing/web-accessibility.md)。
* [!DNL Experience Manager] 还允许其残障用户和管理员访问用户界面和控件，以创建和管理内容。残障人士可以使用辅助技术导航、使用和管理[!DNL Assets]功能。

[!DNL Assets]中的核心功能比以前更易访问，并定期更新以改进对全球标准的遵守。 [!DNL Assets]中的CRUD操作具有一定程度的可访问性。 通过键盘快捷键、屏幕阅读器文本、颜色对比度等，可以访问添加、管理、搜索和分发资产等DAM工作流。

## 支持使用键盘{#keyboard-use}

许多可单击或可操作指针的用户界面元素也可以使用键盘。 使用键盘，用户可以专注于UI元素并采取相应的操作。 用户可以直接使用键盘快捷键触发命令或操作，而无需关注UI元素并使用键盘触发它。 例如，用户可以使用键盘浏览到用户界面控件并选择`Return`并选择`Alt + 2`键盘快捷键，打开用户界面左侧资产的时间轴。

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets] {#keyboard-shortcuts}中的键盘快捷键

[!DNL Assets]中的以下操作使用列出的键盘快捷键。 大多数应用于[!DNL Experience Manager]控制台的键盘快捷键也应用于[!DNL Assets]。 请参阅Consoles](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)的[键盘快捷键。 了解如何[启用或禁用键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)。

| 用户界面或方案 | 键盘快捷键 | 操作 |
|---|---|---|
| [!DNL Assets]用户界面中的列视图 | 向上和向下箭头键 | 导航到同一层次结构中的文件和文件夹。 |
| [!DNL Assets]用户界面中的列视图 | 向左和向右箭头键 | 导航到当前文件夹上方或下方的文件和文件夹。 |
| 在[!DNL Assets]中浏览文件夹 | `/` | 通过打开Omnisearch框调用搜索。 |
| [!DNL Assets] 控制台 | ` | 切换侧边栏 |
| [!DNL Assets] 控制台 | `Alt + 1` | 打开内容树。 |
| [!DNL Assets] 控制台 | `Alt + 2` | 打开[!UICONTROL 导航]左边栏。 |
| [!DNL Assets] 控制台 | `Alt + 3` | 显示选定资产的[!UICONTROL 时间轴]。 |
| [!DNL Assets] 控制台 | `Alt + 4` | 打开选定资产的Live Copy引用。 |
| [!DNL Assets] 控制台 | `Alt + 5` | 开始在所选文件夹中搜索和搜索。 |
| 已选择资产或文件夹 | Backspace | 删除选定的资产或文件夹。 |
| 已选择资产或文件夹 | `p` | 打开选定资产的“属性”页面。 |
| 已选择资产或文件夹 | `e` | 编辑选定的资产。 |
| 已选择资产或文件夹 | `m` | 移动选定的资产。 |
| 已选择资产或文件夹 | `Ctrl + c` | 复制选定的资产。 |
| 已选择资产或文件夹 | `Esc` | 取消选择。 |
| 对话框打开并处于焦点 | `Esc` | 的双曲余切值。 |
| 在DAM中的文件夹内 | `Ctrl + v` | 粘贴复制的资产。 |
| [!DNL Assets] 控制台 | `Ctrl + A` | 选择所有资产。 |
| 资产属性页 | `Ctrl + S` | 保存更改。 |
| [!DNL Assets] 控制台 | `?` | 请参阅列表键盘快捷键。 |

## 登录并导航[!DNL Assets]用户界面{#login}

用户可以使用键盘导航并填写登录字段以登录。 每次出现错误时，屏幕阅读器都会宣布由于登录页面上的用户名和密码组合不正确而导致的错误消息。

登录后，DAM用户可以使用键盘在[!DNL Assets]用户界面中导航。 用户界面元素(如左边栏、菜单、用户用户档案、搜索栏、文件和文件夹)以及管理和配置设置可通过键盘进行导航。 键盘导航顺序为从左到右和从上到下。 使用键盘导航时，焦点时的可操作选项会以更好的颜色对比度高亮显示，并由屏幕阅读器解说。 如果适用，屏幕阅读器会宣布菜单中重点选项的状态，例如，展开、折叠和混合状态。 此外，屏幕阅读器还宣布了可操作选项（例如外观或界面放置）的用途。

如果用户从菜单中展开帮助或用户用户档案选项，屏幕阅读器将宣布相应的选项或状态。 如果用户展开用户用户档案选项，则可以使用键盘选择可用选项。 例如，管理员可以模拟其他用户。 如果用户从[!UICONTROL Help]选项中搜索字符串，则旁白将宣布“搜索帮助”以指示正在进行搜索。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 浏览资源并视图相关信息{#browse}

在[!DNL Assets]用户界面中，用户可以使用键盘浏览DAM存储库中现有数字资产的列表、预览或下载资产、查看生成的演绎版、切换视图、查看生成的演绎版、查看时间轴和版本历史记录、查看注释和引用以及视图和管理元数据。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

在浏览资产存储库时，以下功能改进了辅助功能：

* 屏幕阅读器会发布替代文本，这些替代文本描述图标的用途或功能，而不是图标的名称。
* 用户可以使用键盘键访问资产的引用列表中的交互式用户界面选项并将其集中显示。
* 列表视图中每行中的元素都由屏幕阅读器作为同一行的元素来宣布。
* 使用`Tab`键导航时，焦点可移至版本预览中的关闭选项。
* 使用键盘浏览时，突出显示的可操作用户界面选项具有更突出的视觉焦点，并增强了对比度。 它使聚焦区域对用户更加可识别。
* 使用`Esc`键从缩览图视图中删除快速操作图标不会从最后一个聚焦项目中删除键盘焦点。
* 选择`Alt + 4`键盘快捷键后，将打开左边栏中的[!UICONTROL 引用]列表。 使用`Tab`键，用户可以浏览非零引用条目。 仅浏览非零引用条目也可节省工作和按键次数。
* 资产时间轴中会显示有关资产的注释。 如果使用键盘或键盘快捷键访问左边栏，则可访问该边栏。
* [!UICONTROL 视图] 设置 [!DNL Experience Manager] 可通过键盘访问。用户可以使用箭头键浏览可用的卡大小，并选择和跳转以在现有的视图设置视图中导航和设置其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理数字资产{#manage-assets}

许多资产管理任务（如CRUD操作、下载资产、添加元数据）都可以在不同程度上进行访问。 [!DNL Assets] 允许您使用屏幕阅读器和键盘等各种辅助技术完成任务。

观看有关如何使用键盘浏览[存储库并下载资产](https://youtu.be/K3dgqMRQJys)的视频演示。

对于元数据操作（通常由营销人员和管理员等角色完成），以下功能可改进辅助功能：

* [!UICONTROL 现在，可] 以使用键  盘访问资产属性页面上的“保存并关闭”选项。
* 屏幕阅读器会宣布删除资产[!UICONTROL 属性]的[!UICONTROL 基本]选项卡中选定标记的选项。
* 用户可以使用带键盘的“日期选择器”弹出对话框。 Datepicker用户界面元素用于设置开启时间和结束时间，并选择日期。
* 在屏幕阅读器的浏览模式下，使用键盘的拖动功能在[!UICONTROL 元数据模式编辑器]中正确工作。
* 用户可以使用键盘将焦点移动到文件夹[!UICONTROL 属性]的[!UICONTROL 权限]选项卡中[!UICONTROL 已关闭的用户组]下的“添加用户或组”字段。

## 搜索数字资产{#search-assets}

快速、无缝的资产搜索体验提升了内容速度。 内容速度用例是核心[!DNL Assets]功能的一部分。 要从搜索栏开始搜索，用户可以使用键盘快捷键`/`或与屏幕阅读器一起使用`Tab`来快速查找搜索选项。 当焦点在搜索选项![搜索选项](assets/do-not-localize/search_icon.png)时，屏幕阅读器将选项的名称解说为“搜索按钮”。 用户可选择`Return`打开“搜索”框。 屏幕阅读器不仅会讲述在搜索框中键入的关键字，还会讲述[!DNL Experience Manager Assets]提供的建议。 用户可以使用箭头键、`Return`和`Tab`的组合来访问各种选项以触发搜索。

搜索功能可通过以下功能访问：

* 页面标题（对于屏幕阅读器可用）有助于将页面识别为资产的搜索页面。
* 用户从搜索字段中搜索资产。 用户可以使用键盘导航或键盘快捷键`/`打开它。
* 用户可以开始键入搜索关键字，然后使用箭头键选择自动建议。 可以使用`Return`键选择高亮显示的建议，并搜索资产以查找选定的建议。
* 在筛选搜索结果时，屏幕阅读器可以在“过滤器”面板中标识和宣布混合状态复选框（除非您选择了所有嵌套谓词，否则不会选择并检查第一级复选框）。
* 关闭“全搜索”框后，用户焦点将移至搜索选项。

筛选搜索结果时：

* 搜索结果页面包含一个信息性标题，可以更好地了解屏幕阅读器用户。
* 屏幕阅读器将搜索过滤器中的选项作为可扩展的折叠宣布。
* 具有混合状态选项的谓词由屏幕阅读器宣布。

## 共享资产 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共享资源时，以下功能可改善辅助功能：

* 用户可以使用键盘在链接共享对话框的搜索和添加电子邮件地址字段中移动焦点。

* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器

   * 加载对话框时不要解说表信息。
   * 可导航到所有列出的建议。
   * 解说显示的“添加电子邮件地址”和“搜索”字段的建议。

## 可访问文档{#accessible-docs}

[!DNL Experience Manager] 为残障人士提供可访问的文档。以下内容有助于使内容产品暂时可访问，而Adobe则不断改进模板和内容：

* 屏幕阅读器可以阅读文本。
* 图像和插图提供替代文本。
* 可进行键盘导航。
* 对比度有助于突出显示文档网站的某些部分。

## 提供反馈{#a11y-feedback}

要提供与辅助功能相关的反馈、提出问题和请求产品增强功能，请使用以下方法：

* 在[www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)填写表单。
* 请发送电子邮件至access@adobe.com。

>[!MORELIKETHIS]
>
>* [中的辅助功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)。
>* [每个Service Pack版本中增强功能的发行说明](/help/release-notes/new-features-latest-service-pack.md)。
>* [[!DNL Adobe Experience Manager] 辅助功能指导](/help/managing/web-accessibility.md)。
>* [Adobe解决方案的符合性报告(ACR)和VPAT列表](https://www.adobe.com/accessibility/compliance.html)。

