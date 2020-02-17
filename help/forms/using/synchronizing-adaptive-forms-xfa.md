---
title: 将自适应表单与XFA表单模板同步
seo-title: 将自适应表单与XFA表单模板同步
description: 将自适应表单与XFA/XDP文件同步。
seo-description: 将自适应表单与XFA/XDP文件同步。
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 将自适应表单与XFA表单模板同步{#synchronizing-adaptive-forms-with-xfa-form-templates}

## 简介 {#introduction}

您可以基于XFA表单模板（文件）创建自适 `*.XDP` 应表单。 这种重复使用使您能够保留对现有XFA表单的投资。 有关如何使用XFA表单模板创建自适应表单的信息，请 [基于模板创建自适应表单](../../forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p)。

您可以在自适应表单中重复使用XDP文件中的字段。 这些字段称为绑定字段。 绑定字段的属性（如脚本、标签和显示格式）是从XDP文件中复制的。 您还可以选择覆盖其中某些属性的值。

AEM Forms提供了一种方法，帮助您使自适应表单的字段与随后对XDP文件中的相应字段所做的任何更改保持同步。 本文介绍如何启用此同步。

![您可以将字段从XFA表单拖动到自适应表单](assets/drag-drop-xfa.gif.gif)

在AEM表单创作环境中，您可以将字段从XFA表单（左）拖动到自适应表单（右）

## 前提条件 {#prerequisites}

要使用本文中的信息，建议您熟悉以下方面：

* [创建自适应表单](../../forms/using/creating-adaptive-form.md)

* XFA（XML表单体系结构）

要使用资产提供的示例作为文章中的示例，请下载示例包，如下一节示例包中 [所述](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-sample-package-p)。

## 示例包 {#sample-package}

文章使用示例演示如何将自适应表单与更新的XFA表单模板同步。 示例中使用的资源位于包中，可从本文的“下载”部分 [下载](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-downloads-p) 。

上传包后，您可以在AEM Forms UI中查看这些资产。

使用包管理器安装包： `https://<server>:<port>/crx/packmgr/index.jsp`

该包包含以下资产：

1. `sample-form.xdp`:用作示例的XFA表单模板

1. `sample-xfa-af`:基于sample-form.xdp文件的自适应表单。 但是，此自适应表单不包含任何字段。 在下一步中，我们将向此自适应表单添加内容。

### 向自适应表单添加内容 {#add-content-to-adaptive-form-br}

1. 导航到https://&lt;server>:&lt;port>/aem/forms.html。 如果询问，请输入您的凭据。
1. 打开示例af-xfa，以在创作模式下进行编辑。
1. 从提要栏的内容浏览器中，选择“数据模型对象”选项卡。 将NumericField1和TextField1拖到自适应表单上。
1. 将NumericField1的标题从“数字字段” **更改为** “ **AF数字字段”。**

>[!NOTE]
>
>在前面的步骤中，我们在XDP文件中覆盖了字段的属性。 因此，如果稍后修改XDP文件中的相应属性，则不同步此属性。

## 检测XDP文件中的更改 {#detecting-changes-in-xdp-file}

每当XDP文件或片段中发生任何更改时，AEM表单UI都会标记所有基于XDP文件或片段的自适应表单。

更新XDP文件后，您需要在AEM Forms UI中再次上传该文件，以便标记更改。

例如，让我们使用以下步骤 `sample-form.xdp` 更新文件：

1. 如果出现提 `https://<server>:<port>/projects.html.` 示，导览至输入凭据。
1. 单击左侧的“表单”选项卡。
1. 将文件下 `sample-form.xdp` 载到本地计算机上。 XDP文件下载为文件， `.zip` 可使用任何文件解压缩实用程序解压该文件。

1. 打开文 `sample-form.xdp` 件，将字段TextField1的标题从“文本字段” **更改为** “我 **的文本字段”**。

1. 将文 `sample-form.xdp` 件上传回AEM Forms UI。

如果XDP文件更新，则在编辑基于XDP文件的自适应表单时，您会在编辑器中看到一个图标。 此图标表示自适应表单与XDP文件不同步。 在下图中，请参阅提要栏中旁边的图标。

![显示自适应表单与XDP文件不同步的图标](assets/sync-af-xfa.png)

## 将自适应表单与最新的XDP文件同步 {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

下次打开与XDP文件不同步的自适应表单进行创作时，将显示以下消息：自 **适应表单的架构／表单模板已更新。`Click Here`以使用新版本重新构建基础。**

单击消息可将自适应表单中的字段与XDP文件中的相应字段同步。

对于本文中使用的示例，请在创作模 `sample-xfa-af` 式下打开。 消息将显示在自适应表单的底部。

![提示您将自适应表单与XDP文件同步的消息](assets/sync-af-xfa-1.png)

### 更新属性 {#updating-the-properties}

从XDP文件复制到自适应表单的所有属性都会更新，但作者在自适应表单（从组件对话框）中显式覆盖的属性除外。 服务器日志中提供已更新的属性列表。

要更新示例自适应表单中的属性，请单击消息中的链接( `"Click Here"`已标记)。 TextField1的标题从“文本字段” **更改为** “我 **的文本字段”**。

![update-property](assets/update-property.png)

>[!NOTE]
>
>未更改AF数字字段标签，因为您已从组件属性对话框中覆盖了此属性，如向自适应表单添 [加内容中所述](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p)。

### 将XDP文件中的新字段添加到自适应表单 {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

以后添加到原始XDP文件的任何字段都显示在“表单层次结构”选项卡中，您可以将这些新字段拖动到自适应表单中。

您无需单击错误消息中的链接即可更新表单层次结构选项卡中的字段。

### XDP文件中已删除的字段 {#deleted-fields-in-xdp-file}

如果之前复制到自适应表单的字段从XDP文件中删除，则在创作模式下将显示一条错误消息，指明该字段在XDP文件中不存在。 在这种情况下，从自适应表单中手动删除字段或在组件对 `bindRef` 话框中清除属性。

以下步骤说明了本文所用示例中资产的使用流程：

1. 更新文 `sample-form.xdp` 件并删除NumericField1。
1. 在AEM Forms UI `sample-form.xdp` 中上传文件
1. 打开自适 `sample-xfa-af` 应表单进行创作。 此时将显示以下错误消息：自适应表单的架构／表单模板已更新。 `Click Here` 以使用新版本重新构建基础。

1. 单击消息中的链 `Click Here`接（标记为“”）。 将显示一条错误消息，指出该字段在XDP文件中已不存在。

![删除XDP文件中的元素时出现的错误](assets/no-element-xdp.png)

已删除的字段也会标有一个图标，以指示该字段中出现错误。

![字段中的错误图标](assets/error-field.png)

>[!NOTE]
>
>自适应表单中绑定错误(编辑对话框中的 `bindRef` 值无效)的字段也被视为已删除的字段。 如果作者未修复这些错误并发布自适应表单，则该字段将被视为普通的未绑定自适应表单字段，并包含在输出XML文件的未绑定部分中。

## 下载 {#downloads}

本文示例的内容包

[获取文件](assets/sample-xfa-af-sync-1.0.zip)
