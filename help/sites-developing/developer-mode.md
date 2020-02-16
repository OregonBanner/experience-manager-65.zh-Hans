---
title: 开发人员模式
seo-title: 开发人员模式
description: “开发人员”模式打开一个侧面板，其中包含多个选项卡，这些选项卡为开发人员提供有关当前页面的信息
seo-description: “开发人员”模式打开一个侧面板，其中包含多个选项卡，这些选项卡为开发人员提供有关当前页面的信息
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 开发人员模式{#developer-mode}

在AEM中编辑页面时，可以使用多 [种模式](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) ，包括开发人员模式。 这将打开一个侧面板，其中包含多个选项卡，这些选项卡为开发人员提供有关当前页面的信息。 这三个选项卡是：

* **[用于查看结构](#components)**和性能信息的组件。
* **[运行测试](#tests)**，并分析测试结果。
* **[出现错误](#errors)**，以查看发生的任何问题。

这些帮助开发人员：

* 发现：由哪些页面组成。
* 调试：发生在何处和何时，这反过来有助于解决问题。
* 测试：应用程序是否按预期运行。

>[!CAUTION]
>
>开发人员模式：
>
>* 仅在触屏优化UI中可用（编辑页面时）。
>* 移动设备或桌面上的小窗口不可用（因为空间限制）。
   >
   >    
   * 当宽度小于1024px时，会发生这种情况。
>
* 需要相应的权限／权限：

   * 对开发者模式的访问权限授予具有写访问权限的用户 `/apps`。




>[!CAUTION]
>
>开发人员模式仅适用于未使用nosamplecontent运行模式的标准作者实例。
>
>如果需要，可以将其配置为使用：
>
>* 在使用nosamplecontent运行模式的创作实例上
>* 发布实例
>
>
应在使用后再次禁用它。

>[!NOTE]
>
>请参阅：
>
>* 知识库文章， [AEM TouchUI问题疑难解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以获取更多提示和工具。
>* AEM Gems会话关于 [AEM 6.0开发人员模式](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。
>



## 打开开发人员模式 {#opening-developer-mode}

开发人员模式作为页面编辑器的侧面板实现。 要打开面板，请从页面编辑 **器工具栏中** ，从模式选择器中选择“开发人员”:

![chlimage_1-11](assets/chlimage_1-11.png)

该面板分为两个选项卡：

* **[组件](/help/sites-developing/developer-mode.md#components)**-显示一个组件树，类似于作者的[内容树](/help/sites-authoring/author-environment-tools.md#content-tree)。

* **[错误](/help/sites-developing/developer-mode.md#errors)**-出现问题时，将显示每个组件的详细信息。

### 组件 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

这会显示一个组件树，它：

* 概述页面上呈现的组件和模板链（SLY、JSP等）。 树可以展开以在层次中显示上下文。
* 显示渲染组件所需的服务器端计算时间。
* 允许您展开树并在树中选择特定组件。 通过选择，可访问组件详细信息；例如：

   * 存储库路径
   * 指向脚本的链接（在CRXDE lite中访问）

* 所选组件（在内容流中，由蓝色边框指示）将在内容树中高亮显示（反之亦然）。

这有助于：

* 确定并比较每个组件的渲染时间。
* 查看并了解层次结构。
* 通过查找慢速组件，了解并缩短页面加载时间。

每个组件条目都可以显示（例如）:

![chlimage_1-13](assets/chlimage_1-13.png)

* **查看详细信息**:一个指向列表的链接，其中显示：

   * 用于呈现组件的所有组件脚本。
   * 此特定组件的存储库内容路径。
   ![chlimage_1-14](assets/chlimage_1-14.png)

* **编辑脚本**:链接：

   * 在CRXDE lite中打开组件脚本。

* 扩展组件条目（箭头）也可显示：

   * 所选组件中的层次。
   * 单独呈现选定组件的时间、嵌套在其中的任何单个组件以及合并的总时间。
   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>某些链接指向下的脚本 `/libs`。 但是，这些只供参考，您不 **得编辑** ，因为您所做的任何更改 `/libs`都可能丢失。 这是由于当您升级或应用修补程序／功能包时，此分支可能会受到更改的影响。 您需要的任何更改都应在下进行， `/apps`请参阅 [叠加和覆盖](/help/sites-developing/overlays.md)。

### 错误 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

希望“错 **误** ”选项卡始终为空（如上所示），但出现问题时，会为每个组件显示以下详细信息：

* 如果组件将一个条目写入错误日志，并包含错误的详细信息，并直接链接到CRXDE Lite中的相应代码，则会发出警告。
* 组件打开管理会话时显示警告。

例如，在调用未定义方法的情况下，“错误”选项卡中将显示导致的错误 **** :

![chlimage_1-17](assets/chlimage_1-17.png)

出现错误时，“组件”选项卡树中的组件条目也将标有指示符。

### 测试 {#tests}

>[!CAUTION]
>
>在AEM 6.2中，开发人员模式的测试功能已作为独立工具应用程序重新实施。
>
>有关完整详细信息，请 [参阅测试您的UI](/help/sites-developing/hobbes.md)。

