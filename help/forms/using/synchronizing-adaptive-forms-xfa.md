---
title: 将自适应Forms与XFA表单模板同步
seo-title: Synchronizing Adaptive Forms with XFA Form Templates
description: 将自适应表单与XFA/XDP文件同步。
seo-description: Synchronizing Adaptive forms with XFA/XDP files.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
feature: Adaptive Forms
exl-id: fed67c23-a9b7-403e-9199-dfd527d5f209
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 0%

---

# 将自适应Forms与XFA表单模板同步{#synchronizing-adaptive-forms-with-xfa-form-templates}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

## 简介 {#introduction}

您可以基于XFA表单模板创建自适应表单( `*.XDP` 文件)。 通过重复使用，您可以保留在现有XFA表单中的投资。 有关如何使用XFA表单模板创建自适应表单的信息， [基于模板创建自适应表单](../../forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p).

您可以在自适应表单中重用XDP文件中的字段。 这些字段称为绑定字段。 从XDP文件复制绑定字段的属性（如脚本、标签和显示格式）。 您还可以选择覆盖其中某些属性的值。

AEM Forms提供了一种方法，帮助您将自适应表单的字段与稍后对XDP文件中的相应字段所做的任何更改保持同步。 本文介绍如何启用此同步。

![您可以将字段从XFA表单拖到自适应表单中](assets/drag-drop-xfa.gif.gif)

在AEM Forms创作环境中，您可以将字段从XFA表单（左）拖到自适应表单（右）中

## 前提条件 {#prerequisites}

若要使用本文中的信息，建议熟悉以下方面：

* [创建自适应表单](../../forms/using/creating-adaptive-form.md)

* XFA(XML Forms架构)

要使用文章中提供的资源作为示例，请下载示例包，如下一节中所述， [示例包](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## 示例包 {#sample-package}

文章通过一个示例演示了如何将自适应表单与更新后的XFA表单模板同步。 该示例中使用的资产位于一个包中，该包可从以下位置下载： [下载](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-downloads-p) 章节。

上传包后，您可以在AEM Forms UI中查看这些资源。

使用包管理器安装包： `https://<server>:<port>/crx/packmgr/index.jsp`

该资源包包含以下资源：

1. `sample-form.xdp`：用作示例的XFA表单模板

1. `sample-xfa-af`：基于sample-form.xdp文件的自适应表单。 但是，此自适应表单不包括任何字段。 在下一步中，我们将向此自适应表单添加内容。

### 将内容添加到自适应表单 {#add-content-to-adaptive-form-br}

1. 导航到https://&lt;server>：&lt;port>/aem/forms.html. 如果询问，请输入您的凭据。
1. 打开sample-af-xfa以在创作模式下进行编辑。
1. 从侧栏中的内容浏览器中，选择数据模型对象选项卡。 将NumericField1和TextField1拖动到自适应表单上。
1. 将NumericField1的标题从 **数值字段** 到 **AF数字字段。**

>[!NOTE]
>
>在前面的步骤中，我们覆盖了XDP文件中字段的属性。 因此，如果稍后修改XDP文件中的相应属性，则不会同步此属性。

## 检测XDP文件中的更改 {#detecting-changes-in-xdp-file}

每当XDP文件或片段中的任何更改时，AEM Forms UI都会标记所有基于XDP文件或片段的自适应表单。

更新XDP文件后，您需要在AEM Forms UI中再次上传该文件，以便标记更改。

例如，让我们更新 `sample-form.xdp` 文件，请执行以下步骤：

1. 导航到 `https://<server>:<port>/projects.html.` 如果出现提示，请输入您的凭据。
1. 单击左侧的Forms选项卡。
1. 下载 `sample-form.xdp` 文件。 XDP文件下载为 `.zip` 文件，可使用任何文件解压缩实用程序提取该文件。

1. 打开 `sample-form.xdp` 文件，并将TextField1字段的标题从 **文本字段** 到 **我的文本字段**.

1. 上传 `sample-form.xdp` 文件返回到AEM Forms UI。

如果更新了XDP文件，当您编辑基于XDP文件的自适应表单时，会在编辑器中看到一个图标。 此图标表示自适应表单与XDP文件不同步。 在下图中，查看侧栏中的下一个图标。

![用于显示自适应表单与XDP文件不同步的图标](assets/sync-af-xfa.png)

## 将自适应表单与最新的XDP文件同步 {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

下次打开与XDP文件不同步的自适应表单进行创作时，会显示以下消息： **自适应表单的架构/表单模板已更新。 `Click Here` 以使用新版本进行重新定位。**

单击消息可将自适应表单中的字段与XDP文件中的相应字段同步。

对于本文中使用的示例，请打开 `sample-xfa-af` 处于创作模式。 消息会显示在自适应表单的底部。

![消息提示您将自适应表单与XDP文件同步](assets/sync-af-xfa-1.png)

### 更新属性 {#updating-the-properties}

从XDP文件复制到自适应表单的所有属性都将更新，但作者在自适应表单中（从“组件”对话框）显式覆盖的属性除外。 服务器日志中提供了已更新的属性列表。

要更新自适应表单示例中的属性，请单击链接(标签为 `"Click Here"`)。 TextField1的标题从 **文本字段** 到 **我的文本字段**.

![update — 属性](assets/update-property.png)

>[!NOTE]
>
>标签AF数值字段未发生更改，因为您已从组件属性对话框中覆盖了此属性，如中所述 [将内容添加到自适应表单](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### 将XDP文件中的新字段添加到自适应表单   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

稍后添加到原始XDP文件中的任何字段都会显示在“表单层次结构”选项卡中，您可以将这些新字段拖到自适应表单中。

您无需单击错误消息中的链接即可更新“表单层次结构”选项卡中的字段。

### XDP文件中已删除字段 {#deleted-fields-in-xdp-file}

如果从XDP文件中删除了之前复制到自适应表单的字段，则会以创作模式显示错误消息，声明该字段在XDP文件中不存在。 在这种情况下，请从自适应表单中手动删除字段或清除 `bindRef` 属性。

以下步骤说明了本文中所用示例中资产的此使用流程：

1. 更新 `sample-form.xdp` 文件并删除NumericField1。
1. 上传 `sample-form.xdp` AEM Forms UI中的文件
1. 打开 `sample-xfa-af` 用于创作的自适应表单。 显示以下错误消息：自适应表单的架构/表单模板已更新。 `Click Here` 以使用新版本进行重新定位。

1. 单击链接(标记为“ ” `Click Here`“)中。 此时会显示一条错误消息，指出该字段在XDP文件中不再存在。

![删除XDP文件中的元素时看到的错误](assets/no-element-xdp.png)

已删除的字段还会标记一个图标，以指示字段中存在错误。

![字段中的错误图标](assets/error-field.png)

>[!NOTE]
>
>自适应表单中的字段具有不正确的绑定（无效） `bindRef` （例如，编辑对话框中的值）也视为已删除的字段。 如果作者未修复这些错误并发布自适应表单，则该字段将被视为普通未绑定的自适应表单字段，并包含在输出XML文件的未绑定部分中。

## 下载 {#downloads}

内容包（适用于本文中的示例）

[获取文件](assets/sample-xfa-af-sync-1.0.zip)
