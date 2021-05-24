---
title: 对话框编辑器
seo-title: 对话框编辑器
description: 对话框编辑器提供了一个图形界面，用于轻松创建和编辑对话框和支架
seo-description: 对话框编辑器提供了一个图形界面，用于轻松创建和编辑对话框和支架
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# 对话框编辑器{#dialog-editor}

对话框编辑器提供了一个图形界面，用于轻松创建和编辑对话框和支架。

要查看其工作方式，请转到CRXDE Lite，打开资源管理器树以访问`/libs/foundation/components/chart`，然后双击节点`dialog`:

![chlimage_1-248](assets/chlimage_1-247.png)

对话框节点将在&#x200B;**对话框编辑器**&#x200B;中打开：

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## 用户界面概述{#user-interface-overview}

对话框编辑器界面由四个窗格组成：

* 左上角的&#x200B;**面板**。 此窗格包含可用于构建对话框的小部件，如选项卡面板、文本字段、选择列表和按钮。 您可以通过单击所需的分隔条来展开面板中的不同类别。
* 左下角的&#x200B;**结构**&#x200B;窗格。 此窗格显示构成对话框定义的节点的层次结构。 通过在“CRXDE Lite”或“CRX内容资源管理器”中展开对话框节点，可以看到相同的结构。
* 窗口中心的&#x200B;**render**&#x200B;窗格。 此窗格显示结构窗格中定义的对话框定义如何作为实际对话框呈现。
* **属性**&#x200B;窗格。 此窗格显示结构窗格中当前突出显示的节点的属性。

### 使用对话框编辑器{#using-the-dialog-editor}

要构建对话框，用户将元素从面板拖放到结构窗格中，以在对话框定义层次结构中的位置。

完成所需的结构后，用户单击呈现窗格顶部的&#x200B;**Save**。

>[!CAUTION]
>
>请注意，对话框编辑器是用于创建的相对简单的对话框，可能无法编辑更复杂的对话框定义。 如果对话框编辑器不允许编辑对话框结构，则必须通过使用(例如，CRXDE Lite或CRX内容资源管理器)直接编辑节点结构来手动创建和/或编辑对话框定义。

### 创建新对话框{#creating-a-new-dialog}

要创建新对话框，您需要选择所需的组件，请单击&#x200B;**创建……**，然后&#x200B;**创建对话框……**。

输入所需的详细信息，然后单击&#x200B;**全部保存** — 现在，您可以双击对话框以使用编辑器将其打开。

### 使用基架{#using-the-dialog-editor-for-scaffolds}的对话框编辑器

基架是一个特殊页面，其中包含可在一个步骤中填写和提交的表单。 这允许您使用输入的内容快速创建页面。

构成基架的表单由对话框定义定义，与普通对话框一样，只是它以其他表单显示在基架页面上。 由于对话框定义用于定义基架，因此可以使用对话框编辑器来设计基架。 请注意，以这种方式使用对话框编辑器时，呈现窗格仍将以对话框的形式显示对话框定义，而不是以基架的形式显示。

有关使用对话框编辑器创建基架的详细信息，请参阅[基架](/help/sites-authoring/scaffolding.md)。
