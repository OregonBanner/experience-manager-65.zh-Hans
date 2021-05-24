---
title: 开发人员模式
seo-title: 开发人员模式
description: 开发人员模式会打开包含多个选项卡的侧面板，这些选项卡为开发人员提供有关当前页面的信息
seo-description: 开发人员模式会打开包含多个选项卡的侧面板，这些选项卡为开发人员提供有关当前页面的信息
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# 开发人员模式{#developer-mode}

在AEM中编辑页面时，可以使用多个[模式](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui)，包括开发人员模式。 这会打开一个侧面板，其中包含多个选项卡，用于向开发人员提供有关当前页面的信息。 这三个选项卡是：

* **[](#components)** 用于查看结构和性能信息的组件。
* **[](#tests)** 测试运行并分析结果。
* **[](#errors)** 错误，无法看到发生的任何问题。

这些帮助开发人员：

* 发现：页面由什么组成。
* 调试：发生在何处和何时的事件，这反过来有助于解决问题。
* 测试：应用程序是否按预期运行。

>[!CAUTION]
>
>开发人员模式：
>
>* 仅在触屏UI中可用（编辑页面时）。
>* 在移动设备上或桌面上的小窗口上不可用（由于空间限制）。

   >
   >   
   * 当宽度小于1024像素时，会发生这种情况。
>* 仅适用于属于`administrators`组成员的用户。


>[!CAUTION]
>
>开发人员模式仅在未使用nosamplecontent运行模式的标准创作实例上可用。
>
>如果需要，可将其配置为使用：
>
>* 在使用nosamplecontent run-mode的创作实例上
>* 发布实例

>
>
在使用后应再次禁用该功能。

>[!NOTE]
>
>请参阅：
>
>* 知识库文章[AEM TouchUI问题疑难解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以获取更多提示和工具。
>* AEM Gem会话关于[AEM 6.0开发人员模式](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。

>



## 打开开发人员模式{#opening-developer-mode}

开发人员模式作为页面编辑器的侧面板来实施。 要打开面板，请从页面编辑器工具栏的模式选择器中选择&#x200B;**Developer**:

![chlimage_1-11](assets/chlimage_1-11.png)

该面板分为两个选项卡：

* **[组件](/help/sites-developing/developer-mode.md#components)**  — 此时会显示一个组件树，与作者的内 [容](/help/sites-authoring/author-environment-tools.md#content-tree) 树类似

* **[错误](/help/sites-developing/developer-mode.md#errors)**  — 出现问题时，将显示每个组件的详细信息。

### 组件 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

此时将显示一个组件树，该组件树：

* 概述在页面上呈现的组件和模板链（SLY、JSP等）。 可以展开树以显示层次结构中的上下文。
* 显示呈现组件所需的服务器端计算时间。
* 用于展开树并选择树中的特定组件。 通过选择组件，可以访问组件详细信息；例如：

   * 存储库路径
   * 指向脚本的链接(在CRXDE Lite中访问)

* 选定的组件（在内容流中，由蓝色边框指示）将在内容树中突出显示（反之亦然）。

这有助于：

* 确定并比较每个组件的渲染时间。
* 查看并了解层级。
* 通过查找慢速组件，了解并改进页面加载时间。

每个组件条目可显示（例如）：

![chlimage_1-13](assets/chlimage_1-13.png)

* **查看详细信息**:指向列表的链接，其中显示：

   * 用于呈现组件的所有组件脚本。
   * 此特定组件的存储库内容路径。

   ![chlimage_1-14](assets/chlimage_1-14.png)

* **编辑脚本**:链接：

   * 在CRXDE Lite中打开组件脚本。

* 展开组件条目（箭头）也可显示：

   * 所选组件中的层次结构。
   * 单独呈现选定组件的呈现时间、嵌套在其中的任何单个组件以及组合的总计。

   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>某些链接指向`/libs`下的脚本。 但是，这些参数仅供参考，您&#x200B;**不得**&#x200B;编辑`/libs`下的任何内容，因为您所做的任何更改都可能丢失。 这是因为当您升级或应用修补程序/功能包时，此分支可能会发生更改。 您所需的任何更改都应在`/apps`下进行，请参阅[叠加和覆盖](/help/sites-developing/overlays.md)。

### 错误 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

希望&#x200B;**Errors**&#x200B;选项卡将始终为空（如上所示），但是当出现问题时，将为每个组件显示以下详细信息：

* 当组件将条目写入错误日志、错误详细信息以及指向CRXDE Lite中相应代码的链接时，会出现警告。
* 组件打开管理员会话时出现警告。

例如，在调用了未定义方法的情况下，导致的错误将显示在&#x200B;**Errors**&#x200B;选项卡中：

![chlimage_1-17](assets/chlimage_1-17.png)

在发生错误时，“组件”选项卡树中的组件条目还会使用指示器进行标记。

### 测试 {#tests}

>[!CAUTION]
>
>在AEM 6.2中，作为独立的工具应用程序重新实施了开发人员模式的测试功能。
>
>有关完整的详细信息，请参阅[测试UI](/help/sites-developing/hobbes.md)。
