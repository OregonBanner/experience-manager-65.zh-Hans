---
title: 对话框编辑器
seo-title: 对话框编辑器
description: 对话框编辑器提供了一个图形界面，用于轻松创建和编辑对话框和基架
seo-description: 对话框编辑器提供了一个图形界面，用于轻松创建和编辑对话框和基架
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 对话框编辑器{#dialog-editor}

对话框编辑器提供了一个图形界面，用于轻松创建和编辑对话框和基架。

要了解其工作方式，请转到CRXDE Lite，打开资源管理器树，然 `/libs/foundation/components/chart` 后双击该节点 `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

对话框节点将在对话框编辑 **器中打开**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## 用户界面概述 {#user-interface-overview}

对话框编辑器界面由四个窗格组成：

* 调 **色板**，位于左上角。 此窗格包含可用于构建对话框的构件，如选项卡面板、文本字段、选择列表和按钮。 单击所需的分隔条可展开调色板中的不同类别。
* 结构 **窗格** ，位于左下角。 此窗格显示构成对话框定义的节点的层次结构。 通过在CRXDE lite或CRX内容资源管理器中展开对话框节点，可以看到相同的结构。
* 渲 **染窗格** ，位于窗口的中心。 此窗格显示在结构窗格中定义的对话框定义如何呈现为实际对话框。
* 属性 **窗格** 。 此窗格显示结构窗格中当前高亮显示的节点的属性。

### 使用对话框编辑器 {#using-the-dialog-editor}

要构建对话框，用户将元素从调色板拖放到结构窗格中的对话框定义层次结构中的位置。

完成所需结构后，用户单击渲染窗 **格顶部的**“保存”。

>[!CAUTION]
>
>请注意，对话框编辑器用于创建相对简单的对话框，可能无法编辑更复杂的对话框定义。 如果对话框编辑器不允许编辑对话框结构，则必须通过使用CRXDE Lite或CRX内容浏览器直接编辑节点结构来手动创建和／或编辑对话框定义。

### 创建新对话框 {#creating-a-new-dialog}

****&#x200B;要创建新对话框，您需要选择所需的组件，请单击“ **创建……”然后，**&#x200B;创建对话框…….

输入所需的详细信息，然 **后单击全部保存** -现在，您可以双击对话框以使用编辑器打开它。

### 使用基架的对话框编辑器 {#using-the-dialog-editor-for-scaffolds}

A scaffold是包含表单的特殊页面，该表单可以一步填写和提交。 这允许您使用输入的内容快速创建页面。

组成scaffold的表单由对话框定义，就像正常对话框一样，但它显示在不同表单的scaffolding页面上。 由于对话框定义用于定义基架，因此可以使用对话框编辑器来设计基架。 请注意，以这种方式使用对话框编辑器时，渲染窗格仍将以对话框的形式显示对话框定义，而不是以scaffold的形式显示。

有关使 [用对话框编辑器创建基架的更多信息](/help/sites-authoring/scaffolding.md) ，请参阅基架。
