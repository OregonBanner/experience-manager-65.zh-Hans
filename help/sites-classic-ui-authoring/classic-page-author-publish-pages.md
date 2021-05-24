---
title: 发布页面
seo-title: 发布页面
description: 在创作环境中创建并审核内容后，接下来的目标就是让内容在您的公共网站中可供使用。
seo-description: 在创作环境中创建并审核内容后，接下来的目标就是让内容在您的公共网站中可供使用。
uuid: ab5ffc59-1c41-46fe-904e-9fc67d7ead04
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 46d6bde0-8645-4cff-b79c-8e1615ba4ed4
docset: aem65
exl-id: 3f6aa06e-b5fd-4ab0-9ecc-14250cb3f55e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 79%

---

# 发布页面{#publishing-pages}

在创作环境中创建并审核内容后，接下来的目标就是让内容在您的公共网站（发布环境）中可供使用。

这称为“发布页面”。当您要从发布环境中删除页面时，此过程称为“取消发布”。在发布和取消发布时，页面会保留在创作环境中以供进一步更改，直到将其删除为止。

您还可以立即发布/取消发布页面，或者在某个预定义的未来日期/时间发布/取消发布页面。

>[!NOTE]
>
>一些与发布有关的术语可能会引起混淆：
>
>* **发布/取消发布**
   >  这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
   >
   >
* **激活／取消激活**
   >  这两个术语与发布/取消发布同义。
   >
   >
* **复制**
   >  这些是技术术语，用于描述数据（例如页面内容、文件、代码、用户评论）从一个环境移动到另一个环境（例如在发布或反向复制用户评论时）的移动。
>



>[!NOTE]
>
>如果您没有必要的权限来发布特定页面：
>
>* 将触发一个工作流，向相应的人员通知您的发布请求。
>* 将显示一条消息来通知您没有权限（仅显示很短的一段时间）。

>



## 发布页面  {#publishing-a-page}

激活页面的方法有两种：

* [从“网站”控制台激活](#activating-a-page-from-the-websites-console)
* [从页面本身中的 Sidekick 激活](#activating-a-page-from-sidekick)

>[!NOTE]
>
>您还可以使用“工具”控制台上的[激活树](#howtoactivateacompletesectiontreeofyourwebsite)来激活多个页面的子树。

### 从网站控制台激活页面 {#activating-a-page-from-the-websites-console}

您可以在网站控制台中激活页面。在您打开页面并修改其内容后，您返回至网站控制台：

1. 在网站控制台中，选择您要激活的页面。
1. 从顶部菜单或选定页面项目的下拉菜单中选择&#x200B;**激活**。

   要激活页面及其所有子页面的内容，请使用&#x200B;[**工具**&#x200B;控制台](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite)。

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >必要时，AEM 会要求您激活或取消激活与该页面链接的所有资产。您可以选中或清除用于激活这些资产的复选框。

1. 必要时，AEM 会要求您激活或取消激活与该页面链接的所有资产。您可以选中或清除用于激活这些资产的复选框。

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. AEM WCM 可激活所选的内容。发布的一个或多个页面将显示在[“网站”控制台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)中（用绿色标记），并提供有关谁激活了内容以及激活日期和时间的信息。

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### 从 Sidekick 激活页面 {#activating-a-page-from-sidekick}

您还可以在打开页面进行编辑时激活页面。

在打开页面并修改其内容后，您：

1. 选择 Sidekick 中的&#x200B;**页面**&#x200B;选项卡。
1. 单击“**激活页面**”。窗口右上方会显示一条消息，确认已激活页面。

## 取消发布页面 {#unpublishing-a-page}

要从发布环境删除页面，您需要取消激活内容。

取消激活页面：

1. 在“网站”控制台中，选择您要取消激活的页面。
1. 从顶部菜单或所选页面项目的下拉菜单中选择&#x200B;**取消激活**。将要求您确认删除。

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. 刷新[“网站”控制台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)，此时该内容会标记为红色，指示它不再处于已发布状态。

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## 以后激活/稍后取消激活 {#activate-deactivate-later}

### 以后激活 {#activate-later}

计划在以后的时间激活：

1. 在“网站”控制台中，转到&#x200B;**激活**&#x200B;菜单，然后选择&#x200B;**以后激活**。
1. 在打开的对话框中，您提供激活的日期和时间，然后单击&#x200B;**OK**。这会创建在指定时间激活的页面版本。

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

以后激活会启动在指定的时间激活此版本页面的工作流。相反，稍后取消激活则会启动在指定时间取消激活此版本页面的工作流。

如果您要撤消激活/取消激活页面，请转到[“工作流”控制台](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd)以终止相应的工作流。

### 稍后取消激活  {#deactivate-later}

计划在以后的时间取消激活：

1. 在网站控制台中，转到&#x200B;**停用**&#x200B;菜单，然后选择&#x200B;**稍后停用**。

1. 在打开的对话框中，您提供停用的日期和时间，然后单击&#x200B;**确定**。

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**稍后取消激活**&#x200B;会启动一个工作流，用于在指定时间取消激活此版本的页面。

如果您要撤消此取消激活操作，请转到[“工作流”控制台](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd)以终止相应的工作流。

## 计划激活/计划停用（开始/结束时间）  {#scheduled-activation-deactivation-on-off-time}

您可以使用&#x200B;**开始时间**&#x200B;和&#x200B;**结束时间**&#x200B;来安排页面的发布/取消发布时间，这两个设置可在[页面属性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)中进行定义。

### 确定页面发布状态 {#determining-page-publication-status-classic-ui}

状态可以从[网站](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)控制台查看。发布状态将以不同的颜色表示。

## 激活网站的完整区域（树）  {#activating-a-complete-section-tree-of-your-website}

在&#x200B;**网站**&#x200B;选项卡中，可以激活单个页面。如果输入或更新了大量内容页面（所有内容页面都位于同一根页面下），则可以更轻松地通过一个操作来激活整个树。您也可以通过执行练习来模拟激活和突出显示要激活的页面。

1. 从&#x200B;**欢迎**&#x200B;页面中选择&#x200B;**工具**&#x200B;控制台，然后双击&#x200B;**复制**&#x200B;以打开该控制台(`https://localhost:4502/etc/replication.html`)。

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. 在&#x200B;**复制**&#x200B;控制台上，单击&#x200B;**激活树**。

   将显示以下窗口(`https://localhost:4502/etc/replication/treeactivation.html`)。

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. 输入&#x200B;**开始路径**。这会指定要激活（发布）的节的根路径。 系统将考虑激活此页面及其下的所有页面（或在选择“练习”时，系统将模拟激活这些页面）。
1. 根据需要激活选择条件：

   * **仅限已修改的条目**：仅激活已修改的页面。
   * **仅限已激活的条目**：仅激活已激活的页面。作为一种重新激活形式操作。
   * **忽略已取消激活的条目**：忽略已取消激活的所有页面。

1. 选择要执行的操作：

   1. 如果要检查要激活的页面&#x200B;**，请选择&#x200B;**练习**。这只是模拟操作，不会激活任何页面。

   1. 如果要激活页面，请选择&#x200B;**激活**。
