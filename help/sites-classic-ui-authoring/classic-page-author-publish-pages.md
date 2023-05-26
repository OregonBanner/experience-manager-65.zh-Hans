---
title: 发布页面
description: 在创作环境中创建并查看内容后，将其发布到公共网站上。
uuid: ab5ffc59-1c41-46fe-904e-9fc67d7ead04
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 46d6bde0-8645-4cff-b79c-8e1615ba4ed4
docset: aem65
exl-id: 3f6aa06e-b5fd-4ab0-9ecc-14250cb3f55e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 3%

---

# 发布页面{#publishing-pages}

在创作环境中创建并查看内容后，将其发布到公共网站（您的发布环境）上。

这称为发布页面。 要从发布环境中删除页面时，将称为取消发布。 在发布和取消发布页面时，该页面在删除之前仍可在创作环境中进行进一步更改。

您还可以立即发布/取消发布页面，或者在预定义的未来日期/时间发布/取消发布页面。

>[!NOTE]
>
>某些与发布相关的术语可能会混淆：
>
>* **发布/取消发布**
   >  这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
>
>* **激活／取消激活**
   >  这两个术语与发布/取消发布同义。
>
>* **复制**
   >  这些是技术术语，用于描述数据（例如页面内容、文件、代码、用户注释）从一个环境移动到另一个环境，例如发布或反向复制用户注释时。
>


>[!NOTE]
>
>如果您没有发布特定页面所需的权限，请执行以下操作：
>
>* 将触发一个工作流，通知相应人员您的发布请求。
>* 此时将显示一条消息（短时间内）通知您。
>


## 发布页面 {#publishing-a-page}

激活页面的方法有两种：

* [从网站控制台中](#activating-a-page-from-the-websites-console)
* [从页面的副手手手手里](#activating-a-page-from-sidekick)

>[!NOTE]
>
>您还可以使用激活多个页面的子树 [激活树](#howtoactivateacompletesectiontreeofyourwebsite) 工具控制台上的。

### 从网站控制台激活页面 {#activating-a-page-from-the-websites-console}

您可以在网站控制台中激活页面。 打开页面并修改其内容后，您将返回到网站控制台：

1. 在网站控制台中，选择要激活的页面。
1. 选择 **激活**，或从顶部菜单或所选页面项目上的下拉菜单中。

   要激活页面及其所有子页面的内容，请使用 [**工具** 控制台](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite).

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >如有必要，AEM会请求您激活或重新激活任何链接到页面的资源。 您可以选中或清除复选框以激活这些资产。

1. 如有必要，AEM会请求您激活或重新激活任何链接到页面的资源。 您可以选中或清除复选框以激活这些资产。

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. AEM WCM会激活选定的内容。 已发布的页面将显示在 [网站控制台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) （标记为绿色），其中包含有关谁激活了内容的信息以及激活日期和时间。

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### 从Sidekick激活页面 {#activating-a-page-from-sidekick}

在打开页面进行编辑时，您还可以激活该页面。

打开页面并修改其内容后，您可以：

1. 选择 **页面** 在Sidekick中翻页。
1. 单击 **激活页面**.
窗口右上角会显示一条消息，确认页面已激活。

## 取消发布页面 {#unpublishing-a-page}

要从发布环境中删除页面，请取消激活该内容。

要取消激活页面，请执行以下操作：

1. 在网站控制台中，选择要取消激活的页面。
1. 选择 **取消激活**，或从顶部菜单或所选页面项目上的下拉菜单中。 系统会要求您确认删除。

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. 刷新 [网站控制台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) 并且内容以红色标记，表示它不再发布。

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## 稍后激活/取消激活 {#activate-deactivate-later}

### 以后激活 {#activate-later}

要安排稍后激活，请执行以下操作：

1. 在“网站”控制台中，转到 **激活** 菜单，然后选择 **稍后激活**.
1. 在打开的对话框中，提供激活的日期和时间，然后单击 **确定**. 这将创建在指定时间激活的页面版本。

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

稍后激活会启动一个工作流，以在指定时间激活此版本的页面。 相反，稍后取消激活会启动一个工作流，以在特定时间取消激活此版本的页面。

如果要取消此激活/停用，请转到 [工作流控制台](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) 以终止相应的工作流。

### 稍后取消激活 {#deactivate-later}

要安排稍后再停用，请执行以下操作：

1. 在网站控制台中，转到 **取消激活** 菜单，然后选择 **稍后取消激活**.

1. 在打开的对话框中，提供取消激活的日期和时间，然后单击 **确定**.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**延迟停用** r会启动一个工作流，以在特定时间取消激活此版本的页面。

如果要取消此停用，请转到 [工作流控制台](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) 以终止相应的工作流。

## 计划的激活/停用（开启/关闭时间） {#scheduled-activation-deactivation-on-off-time}

您可以使用计划发布/取消发布页面的时间 **准时** 和 **关闭时间** 中定义的属性 [页面属性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

### 确定页面发布状态 {#determining-page-publication-status-classic-ui}

可以从以下位置查看状态 [网站控制台](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). 颜色指示出版状态。

## 激活网站的完整部分（树） {#activating-a-complete-section-tree-of-your-website}

从 **网站** 选项卡，您可以激活各个页面。 当您输入或更新了大量内容页面（所有这些页面都驻留在同一根页面下）时，可以更轻松地在一次操作中激活整个树。 您还可以执行模拟激活并突出显示要激活的页面。

1. 打开 **工具** 控制台，方法是从 **欢迎** 页面，然后双击 **复制** 以打开控制台( `https://localhost:4502/etc/replication.html`)。

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. 在 **复制** 控制台，单击 **激活树**.

   以下窗口( `https://localhost:4502/etc/replication/treeactivation.html`)将显示。

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. 输入 **起始路径**. 这会指定要激活（发布）的节的根路径。 此页面及其下的所有页面均被视为待激活（如果选择了试运行，则用于模拟）。
1. 根据需要激活选择标准：

   * **仅已修改**：仅激活已修改的页面。
   * **仅已激活**：仅激活（已）已激活的页面。 作为重新激活的一种形式。
   * **忽略已停用的项目**：忽略任何已停用的页面。

1. 选择要执行的操作：

   1. 选择 **练习** 如果您要检查哪些页面 *会* 被激活。 这只是一个模拟，不会激活任何页面。

   1. 选择 **激活** 如果要激活页面，请执行以下操作。
