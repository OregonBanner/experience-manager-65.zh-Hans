---
title: 经典UI标记控制台
seo-title: 经典UI标记控制台
description: 了解经典UI标记控制台。
seo-description: 了解经典UI标记控制台。
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 37%

---


# 经典UI标记控制台{#classic-ui-tagging-console}

此部分用于经典UI标记控制台。

触屏优化UI标记控制台位于[此处](/help/sites-administering/tags.md#tagging-console)。

要访问经典UI标记控制台，请执行以下操作：

* 在作者
* 以管理权限登录
* 浏览到控制台
例如[https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## 创建标记和名称空间 {#creating-tags-and-namespaces}

1. 根据您的起始级别，您可以使用“**新建**”创建标记或命名空间：

   如果选择“**标记**”，则可以创建一个命名空间：

   ![](assets/creating_tags_andnamespaces.png)

   如果选择一个命名空间（例如&#x200B;**演示**），则可以在该命名空间内创建一个标记：

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 在两种情况下，输入

   * **标题**
(
*必需*)标记的显示标题。虽然可以输入任何字符，
建议不要使用这些特殊字符：

      * `colon (:)` -命名空间分隔符
      * `forward slash (/)` -子标签分隔符

      如果输入这些字符，则不会显示这些字符。

   * **名称**
(
*必需*)标记的节点名称。

   * **描述**
(
*可选*)标记的说明。

   * 选择&#x200B;**创建**


## 编辑标记 {#editing-tags}

1. 在右侧窗格中，选择要编辑的标记。
1. 单击&#x200B;**编辑**。
1. 您可以修改&#x200B;**标题**&#x200B;和&#x200B;**说明**。
1. 单击&#x200B;**保存**&#x200B;以关闭对话框。

## 删除标记  {#deleting-tags}

1. 在右侧窗格中，选择要删除的标记。
1. 单击&#x200B;**删除**。
1. 单击&#x200B;**是**&#x200B;以关闭对话框。

   标记不应再列出。

## 激活和取消激活标记 {#activating-and-deactivating-tags}

1. 在右侧窗格中，选择要激活（发布）或取消激活（取消发布）的命名空间或标记。
1. 根据需要单击“**激活**”或“**取消激活**”。

## 列表 - 显示引用标记的位置  {#list-showing-where-tags-are-referenced}

**列表**&#x200B;会打开一个新窗口，使用突出显示的标记显示所有页面的路径：

![](assets/list_showing_wheretagsarereferenced.png)

## 移动标记 {#moving-tags}

要帮助标记管理员和开发人员清理分类或重命名标记ID，可以将标记移动到新位置：

1. 打开 **Tagging** 控制台。
1. 选择标记并在顶部工具栏（或上下文菜单）中单击“**移动...**”。
1. 在“**移动标记**”对话框中，定义：

   * **目标位置**，目标节点。
   * **重命名为**，新的节点名称。

1. 单击“**移动**”。

“**移动标记**”对话框如下所示：

![](assets/move_tag.png)

>[!NOTE]
>
>作者不应移动标记或重命名标记ID。 必要时，作者只应[更改标记标题](#editing-tags)。

## 合并标记 {#merging-tags}

当有重复的分类时，可以使用合并标记。当标记 A 合并到标记 B 时，所有使用标记 A 标记的页面都将使用标记 B 标记，并且标记 A 不再可供作者使用。

将一个标记合并到另一个标记：

1. 打开 **Tagging** 控制台。
1. 选择标记并在顶部工具栏（或上下文菜单）中单击“**合并...**”。
1. 在“**合并标记**”对话框中，定义：

   * **目标标记**，目标节点。

1. 单击“**合并**”。

**合并标记**&#x200B;对话框如下所示：

![](assets/mergetag.png)

## 对标记的使用进行计数 {#counting-usage-of-tags}

查看标记的已使用次数：

1. 打开 **Tagging** 控制台。
1. 在顶部工具栏中单击“**计数用法**”：“计数”列会显示结果。

## 管理不同语言的标记  {#managing-tags-in-different-languages}

标记的可选`title`属性可以翻译为多种语言。 然后，可以根据用户语言或页面语言显示标记`titles`。

### 用多种语言定义标记标题 {#defining-tag-titles-in-multiple-languages}

以下过程说明如何将标签&#x200B;**Animals**&#x200B;的`title`翻译为英语、德语和法语：

1. 转到&#x200B;**Tagging**&#x200B;控制台。
1. 编辑&#x200B;**Tags**>**Stock Photography**&#x200B;下面的&#x200B;**Animals**&#x200B;标签。
1. 添加以下语言的翻译：

   * **英语**：Animals
   * **德语**：Tiere
   * **法语**：Animaux

1. 保存更改。

对话框如下所示：

![](assets/edit_tag.png)

Tagging控制台使用用户语言设置，因此对于Animal标记，将为用户属性中将语言设置为法语的用户显示“Animaux”。

要向对话框添加新语言，请参阅&#x200B;**开发人员标记**&#x200B;部分中的[向编辑标记对话框添加新语言](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)部分。

### 以指定语言{#displaying-tag-titles-in-page-properties-in-a-specified-language}在页面属性中显示标记标题

默认情况下，页面属性中的标记`titles`以页面语言显示。 页面属性中的标记对话框有一个语言字段，用于以其他语言显示标记`titles`。 以下过程介绍如何以法语显示标记`titles`:

1. 请参阅上一节，将法语翻译添加到&#x200B;**Tags** > **Stock Photography**&#x200B;下的&#x200B;**Animals**。
1. 打开英语分支的 **Geometrixx** 站点中的&#x200B;**产品**&#x200B;页面的页面属性。
1. 打开&#x200B;**标记／关键字**&#x200B;对话框（通过选择“标记／关键字”显示区域右侧的下拉菜单），并从右下角的下拉菜单中选择&#x200B;**法语**&#x200B;语言。
1. 使用左右箭头滚动，直到能够选择&#x200B;**图片库**&#x200B;选项卡

   选择&#x200B;**Animals**(**Animaux**)标签，在对话框外进行选择以关闭它，然后将标签添加到页面属性。

   ![](assets/french_tag.png)

默认情况下，页面属性对话框根据页面语言显示标记`titles`。

通常，如果页面语言可用，则标记的语言会从页面语言中获取。 当在其他情况下（例如在表单或对话框中）使用[ `tag`构件](/help/sites-developing/building.md#tagging-on-the-client-side)时，标记语言取决于上下文。

>[!NOTE]
>
>标准页面组件中的标记云和元关键字根据页面语言使用本地化的标记`titles`（如果可用）。