---
title: 编辑内容页面时进行注释
description: 许多与内容直接相关的组件允许您添加注释。
uuid: 157be55c-8ab8-472e-be32-0dcc02bfa41d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: aa89326a-ad33-4b0b-8d09-c68c5a5c790a
exl-id: de1ae7e3-db3a-4b5e-8a4f-ae111227181f
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 40%

---

# 编辑页面时的注释{#annotations-when-editing-a-page}

向网站的页面添加内容通常需要经过实际发布之前的讨论。 为了帮助实现此目的，许多与内容直接相关的组件（例如，与布局相反的组件）都允许您添加注释。

页面上的注释以彩色标记/便签显示。 您（或其他用户）可以通过注释给其他作者/审阅人留下意见和/或问题。

>[!NOTE]
>
>单个组件类型的定义决定是否可在该组件的实例中添加注释。

>[!NOTE]
>
>经典UI中创建的注释将显示在触屏UI中。 但是，草图是特定于UI的，并且只会在创建草图的UI中显示。

>[!CAUTION]
>
>删除资源（例如，段落）会删除附加到该资源的所有注释和草图，无论这些注释和草图处于整个页面的什么位置，均将如此。

>[!NOTE]
>
>根据您的要求，您还可以开发一个工作流，用于在添加、更新或删除注释时发送通知。

## 注释 {#annotations}

这是一种特殊的[模式](/help/sites-authoring/author-environment-tools.md#page-modes)，可用于创建和查看注释。

>[!NOTE]
>
>请不要忘记，[评论](/help/sites-authoring/basic-handling.md#timeline)也可用于在页面中提供反馈。

>[!NOTE]
>
>您可以对各种资源添加注释：
>
>* [对资产添加注释](/help/assets/manage-assets.md#annotating)
>* [对视频资产添加注释](/help/assets/managing-video-assets.md#annotate-video-assets)
>


### 对组件添加注释 {#annotating-a-component}

在“注释”模式中，您可以创建、编辑、移动或删除内容的注释：

1. 编辑页面时，您可以使用工具栏（右上方）中的图标进入注释模式：

   ![](do-not-localize/screen_shot_2018-03-22at110414.png)

   此时，您可以查看任何现有的注释。

   >[!NOTE]
   >
   >要退出注释模式，请点按/单击顶部工具栏右侧的注释图标（x符号）。

1. 单击/点按“添加注释”图标（工具栏左侧的加号）以开始添加注释。

   >[!NOTE]
   >
   >要停止添加注释（并返回到查看状态），请点按/单击顶部工具栏左侧的取消图标（白色圆圈中的x符号）。

1. 单击/点按所需的组件（可添加注释的组件将以蓝色边框突出显示）以添加注释并打开对话框：

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   在此，您可以使用相应的字段和/或图标：

   * 输入注释文本。
   * 创建草图（线和形状）以突出显示组件的某个区域。


      创建草图时，光标将变为十字线。 您可以绘制多条不同的线。草图线反映注释颜色，可为箭头、圆环或椭圆环。
   ![](do-not-localize/screen_shot_2018-03-22at110640.png)

   * 选择/更改颜色：

   ![](do-not-localize/chlimage_1-19.png)

   * 删除注释。

   ![](do-not-localize/screen_shot_2018-03-22at110647.png)

1. 单击/点按对话框外部可关闭注释对话框。 将显示注释的截断视图（第一个词）以及任何草图：

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. 完成特定注释编辑之后，您可以：

   * 单击/点按文本标记以打开注释。打开后，您可以查看全文，进行更改或删除注释。

      * 无法独立于注释删除草图。
   * 调整文本标记位置。
   * 单击/点按草图线以选择该草图，然后将其拖动到所需位置。
   * 移动或复制组件

      * 此外，还将移动或复制任何相关注释及其草图，并且它们相对于段落的位置将保持不变。


1. 要退出“注释”模式，并返回之前使用的模式，请点按/单击顶部工具栏右侧的“注释”图标（x符号）。

>[!NOTE]
>
>无法将注释添加到其他用户已锁定的页面。

### 注释指示器 {#annotation-indicator}

在“编辑”模式下不会显示注释，但工具栏右上方的徽章会显示当前页面存在的注释数。该徽章取代了默认的“注释”图标，但还可用作打开/关闭“注释”模式的快速链接：

![chlimage_1-242](assets/chlimage_1-242.png)
