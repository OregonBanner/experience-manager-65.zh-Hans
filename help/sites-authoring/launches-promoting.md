---
title: 提升启动项
seo-title: 提升启动项
description: '您需要提升启动页面以将内容移回源（生产）中，然后才能进行发布。 '
seo-description: '您需要提升启动页面以将内容移回源（生产）中，然后才能进行发布。 '
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 92%

---


# 提升启动项{#promoting-launches}

您需要提升启动页面以将内容移回源（生产）中，然后才能进行发布。提升启动页面时，源页面的对应页面会被替换为提升页面的内容。提升启动页面时可以做出以下选择：

* 是只提升当前页面还是提升整个启动项。
* 是否提升当前页面的子页面。
* 是提升整个启动项还是只提升已更改的页面。
* 是否在提升后删除启动项。

>[!NOTE]
>
>在将启动页面提升到目标（**生产**）后，您可以将&#x200B;**生产**&#x200B;页面作为实体进行激活（以加快进程）。向工作流包添加页面，然后在激活页面包的工作流中将其用作有效负荷。您需要先创建工作流包，然后才能提升启动项。请参阅[使用 AEM 工作流处理提升的页面](#processing-promoted-pages-using-aem-workflow)。

>[!CAUTION]
>
>不能并行提升单个启动项。这意味着，在同一次启动中同时执行两个提升操作可能会导致错误- `Launch could not be promoted`（以及日志中的冲突错误）。

>[!CAUTION]
>
>在对&#x200B;*修改过的*&#x200B;页面提升启动项时，会考虑源和启动项分支中的修改。

## 提升启动页面 {#promoting-launch-pages}

>[!NOTE]
>
>此处介绍的是只有一个启动项级别时提升启动页面的手动操作。请参阅：
>
>* [提升嵌套启动项](#promoting-a-nested-launch)，当结构中有多个启动项时。
>* [启动项 - 事件的顺序](/help/sites-authoring/launches.md#launches-the-order-of-events)，包含有关自动提升和发布的更多详细信息。

>



您可以从&#x200B;**站点**&#x200B;控制台或&#x200B;**启动项**&#x200B;控制台提升启动项：

1. 打开：

   * **站点**&#x200B;控制台：

      1. 打开[引用边栏](/help/sites-authoring/author-environment-tools.md#showingpagereferences)，然后使用[选择模式](/help/sites-authoring/basic-handling.md)选择所需的源页面（或选择并打开引用边栏，顺序不重要）。 此时将显示所有引用。

      1. 选择&#x200B;**启动项**（例如“启动项 (1)”）以显示特定启动项的列表。
      1. 选择特定的启动项以显示可用的操作。
      1. 选择&#x200B;**提升启动项**&#x200B;以打开向导。
   * **启动项**&#x200B;控制台：

      1. 选择您的启动项（点按/单击缩略图）。
      1. 选择&#x200B;**提升**。


1. 在第一步中，您可以指定：

   * **目标**

      * **提升后删除启动项**
   * **范围**

      * **提升整个启动项**
      * **提升已修改的页面**
      * **提升当前页面**
      * **提升当前页面和子页面**

   例如，当选择仅提升已修改的页面时：

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >此处介绍的是单个启动项的情况，如果您具有嵌套启动项，请参阅[提升嵌套启动项](#promoting-a-nested-launch)。

1. 选择&#x200B;**下一步**&#x200B;以继续。
1. 您可以查看要提升的页面，具体页面取决于您选择的页面范围：

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. 选择&#x200B;**提升**。

## 编辑时提升启动页面  {#promoting-launch-pages-when-editing}

在编辑启动页面时，也可以从&#x200B;**页面信息**&#x200B;中执行&#x200B;**提升启动项**&#x200B;操作。这将打开相应向导来收集所需的信息。

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>此操作适用于单个启动项和[嵌套启动项](#promoting-a-nested-launch)。

## 提升嵌套启动项  {#promoting-a-nested-launch}

创建嵌套启动项后，您可以将其提升回任意源，包括根目录源（生产）。

![chlimage_1-104](assets/chlimage_1-104.png)

1. 与[创建嵌套启动项](#creatinganestedlaunchlaunchwithinalaunch)一样，在&#x200B;**启动项**&#x200B;控制台或&#x200B;**引用**&#x200B;边栏中导航到所需的启动项并将其选中。
1. 选择&#x200B;**提升启动项**&#x200B;以打开向导。

1. 输入所需的详细信息：

   * **目标**

      * **提升目标**&#x200B;您可以提升到任意源。

      * **提升后删除启动项**&#x200B;提升后，将删除所选启动项以及嵌套在其中的所有启动项。
   * **范围**&#x200B;在此处，您可以选择是提升整个启动项，还是仅提升已实际编辑的页面。如果选择后者，则还可以选择包括/排除子页面。默认配置是仅提升当前页面的页面更改：

      * **提升整个启动项**
      * **提升已修改的页面**
      * **提升当前页面**
      * **提升当前页面和子页面**

   ![chlimage_1-105](assets/chlimage_1-105.png)

1. 选择&#x200B;**下一步**。
1. 在选择&#x200B;**提升**&#x200B;之前查看提升详细信息：

   ![chlimage_1-105](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >列出的页面将取决于定义的&#x200B;**范围**，并且可能还取决于您已实际编辑的页面。

1. 您所做的更改将会被提升并反映在&#x200B;**启动项**&#x200B;控制台中：

   ![chlimage_1-107](assets/chlimage_1-107.png)

## 使用 AEM 工作流处理提升的页面 {#processing-promoted-pages-using-aem-workflow}

使用工作流模型批处理提升的启动页面：

1. 创建工作流包。
1. 当作者提升启动页面时，他们会将其存储在工作流包中。
1. 将包作为有效负荷，以启动工作流模型。

要在提升页面时自动启动工作流，请为包节点[配置工作流启动器](/help/sites-administering/workflows-starting.md#workflows-launchers)。

例如，您可以在作者提升启动页面时自动生成页面激活请求。配置工作流启动器，以在包节点被修改时启动请求激活工作流。

![chlimage_1-108](assets/chlimage_1-108.png)
