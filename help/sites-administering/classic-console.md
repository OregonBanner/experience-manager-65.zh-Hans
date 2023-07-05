---
title: 经典UI标记控制台
seo-title: Classic UI Tagging Console
description: 了解经典UI标记控制台。
seo-description: Learn about the Classic UI Tagging Console.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
source-git-commit: 21330d460d1080ab1dee3e82bc3c3877677c1420
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 1%

---


# 经典UI标记控制台{#classic-ui-tagging-console}

本节适用于经典UI标记控制台。

触屏优化UI标记控制台是 [此处](/help/sites-administering/tags.md#tagging-console).

要访问经典UI标记控制台，请执行以下操作：

* 在作者上
* 使用管理权限登录
* 浏览到控制台，例如， [https://localhost:4502/tagging](https://localhost:4502/tagging)

![经典控制台窗口](assets/managing_tags_usingthetagasministrationconsole.png)

## 创建标记和命名空间 {#creating-tags-and-namespaces}

1. 根据您从开始的级别，您可以使用以下方式创建标记或命名空间 **新**：

   如果您选择 **标记** 您可以创建命名空间：

   ![创建命名空间对话框](assets/creating_tags_andnamespaces.png)

   如果您选择命名空间(例如 **演示**)您可以在该命名空间中创建标记：

   ![创建标记对话框](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 在这两种情况下，请输入

   * **标题**
(*必需*)标记的显示标题。 虽然可以输入任何字符，但建议不要使用以下特殊字符：

      * `colon (:)`  — 命名空间分隔符
      * `forward slash (/)`  — 子标记分隔符

     如果输入，将不显示这些字符。

   * **名称**
(*必需*)标记的节点名称。

   * **描述**
(*可选*)标记的描述。

   * 选择 **创建**

## 编辑标记 {#editing-tags}

1. 在右侧窗格中，选择要编辑的标记。
1. 单击 **编辑**.
1. 您可以修改 **标题** 和 **描述**.
1. 单击 **保存** 以关闭对话框。

## 正在删除标记 {#deleting-tags}

1. 在右侧窗格中，选择要删除的标记。
1. 单击&#x200B;**删除**。
1. 单击 **是** 以关闭对话框。

   标记不应再列出。

## 激活和停用标记 {#activating-and-deactivating-tags}

1. 在右侧窗格中，选择要激活（发布）或停用（取消发布）的命名空间或标记。
1. 单击 **激活** 或 **取消激活** 根据需要。

## 列表 — 显示引用标记的位置 {#list-showing-where-tags-are-referenced}

**列表** 打开一个新窗口，其中显示使用高亮显示的标记的所有页面的路径：

![查找引用标记的位置](assets/list_showing_wheretagsarereferenced.png)

## 移动标记 {#moving-tags}

为帮助标记管理员和开发人员清理分类或重命名标记ID，可以将标记移动到新位置：

1. 打开 **标记** 控制台。
1. 选择标记并单击 **移动……** 在顶部工具栏（或上下文菜单）中。
1. 在 **移动标记** 对话框，定义：

   * **到**，即目标节点。
   * **重命名为**，即新节点名称。

1. 单击 **移动**.

此 **移动标记** 对话框如下所示：

![移动标记](assets/move_tag.png)

>[!NOTE]
>
>作者不应移动标记或重命名标记ID。 必要时，作者只应 [更改标记标题](#editing-tags).

## 合并标记 {#merging-tags}

当分类包含重复项时，可以使用合并标记。 当标记A合并到标记B中时，所有使用标记A标记的页面都将使用标记B标记，并且标记A不再对作者可用。

要将标记合并到另一个标记中，请执行以下操作：

1. 打开 **标记** 控制台。
1. 选择标记并单击 **合并……** 在顶部工具栏（或上下文菜单）中。
1. 在 **合并标记** 对话框，定义：

   * **到**，即目标节点。

1. 单击 **Merge**.

此 **合并标记** 对话框如下所示：

![合并标记](assets/mergetag.png)

## 对标记的使用进行计数 {#counting-usage-of-tags}

要查看标记的使用次数，请执行以下操作：

1. 打开 **标记** 控制台。
1. 单击 **计数用法** 在顶部工具栏中：“计数”列显示结果。

## 管理不同语言的标记 {#managing-tags-in-different-languages}

可选 `title`标记属性可以翻译成多种语言。 标记 `titles` 然后可以根据用户语言或页面语言进行显示。

### 定义多种语言的标记标题 {#defining-tag-titles-in-multiple-languages}

以下过程说明如何翻译 `title`标记的 **动物** 英语、德语和法语：

1. 转到 **标记** 控制台。
1. 编辑标记 **动物** 以下 **标记** > **Stock摄影**.
1. 添加以下语言的翻译：

   * **英语**：动物
   * **德语**：蒂耶尔
   * **法语**：阿尼莫

1. 保存更改。

该对话框如下所示：

![编辑标记](assets/edit_tag.png)

“标记”控制台使用用户语言设置，因此对于Animal标记，对于在用户属性中将语言设置为“法语”的用户，将显示“Animaux”。

要向对话框添加新语言，请参阅一节 [向“编辑标记”对话框添加新语言](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) 在 **为开发人员添加标记** 部分。

### 以指定语言在页面属性中显示标记标题 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

默认情况下，标记 `titles`在中，页面属性以页面语言显示。 页面属性中的标记对话框有一个可显示标记的语言字段 `titles`换了语言。 以下过程介绍了如何显示标记 `titles`法语：

1. 请参阅上一节以将法语翻译添加到 **动物** 以下 **标记** > **Stock摄影**.
1. 打开 **产品** 的英文分支中的页面 **Geometrixx** 站点。
1. 打开 **标记/关键字** 对话框（通过选择“标记”/“关键字”显示区域右侧的下拉菜单），然后选择 **法语** 从右下角的下拉菜单中选取语言。
1. 使用左右箭头滚动，直到能够选择 **Stock摄影** 选项卡

   选择 **动物** (**阿尼莫**)，然后选择对话框外部以将其关闭并将标记添加到页面属性。

   ![编辑其他标记](assets/french_tag.png)

默认情况下，“页面属性”对话框会显示标记 `titles`根据页面语言。

通常，如果页面语言可用，则从页面语言中获取标记的语言。 当 [`tag` 构件](/help/sites-developing/building.md#tagging-on-the-client-side) 在其他情况下（例如在表单或对话框中）使用，标记语言取决于上下文。

>[!NOTE]
>
>标准页面组件中的标记云和元关键字使用本地化的标记 `titles`基于页面语言（如果可用）。
