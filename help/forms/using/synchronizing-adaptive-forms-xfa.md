---
title: 将自适应Forms与XFA表单模板同步
seo-title: 将自适应Forms与XFA表单模板同步
description: 将自适应表单与XFA/XDP文件同步。
seo-description: 将自适应表单与XFA/XDP文件同步。
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
feature: 自适应表单
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---


# 将自适应Forms与XFA表单模板同步{#synchronizing-adaptive-forms-with-xfa-form-templates}

## 简介 {#introduction}

您可以基于XFA表单模板（`*.XDP`文件）创建自适应表单。 这种重复使用使您能够保留对现有XFA表单的投资。 有关如何使用XFA表单模板创建自适应表单的信息，请[基于模板](../../forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p)创建自适应表单。

您可以在自适应表单中重复使用XDP文件中的字段。 这些字段称为绑定字段。 绑定字段的属性（如脚本、标签和显示格式）将从XDP文件中复制。 您还可以选择覆盖其中某些属性的值。

AEM Forms提供了一种方法，帮助您使自适应表单的字段与随后对XDP文件中的相应字段所做的任何更改保持同步。 本文说明了如何启用此同步。

![您可以将字段从XFA表单拖动到自适应表单](assets/drag-drop-xfa.gif.gif)

在AEM Forms创作环境中，您可以将字段从XFA表单（左）拖动到自适应表单（右）

## 前提条件 {#prerequisites}

要使用本文中的信息，建议您熟悉以下方面：

* [创建自适应表单](../../forms/using/creating-adaptive-form.md)

* XFA(XML Forms架构)

要使用文章中的示例提供的资产，请下载示例包，如下一节[示例包](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-sample-package-p)中所述。

## 示例包{#sample-package}

文章使用一个示例演示如何将自适应表单与更新的XFA表单模板同步。 此示例中使用的资源位于包中，可从本文的[下载](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-downloads-p)部分下载。

上传包后，您可以在AEM Forms UI中视图这些资产。

使用包管理器安装包：`https://<server>:<port>/crx/packmgr/index.jsp`

该包包含以下资产：

1. `sample-form.xdp`:用作示例的XFA表单模板

1. `sample-xfa-af`:基于sample-form.xdp文件的自适应表单。但是，此自适应表单不包含任何字段。 在下一步中，我们将向此自适应表单添加内容。

### 将内容添加到自适应表单{#add-content-to-adaptive-form-br}

1. 导航到https://&lt;server>:&lt;port>/aem/forms.html。 如果询问，请输入您的凭据。
1. 打开示例af-xfa，以在创作模式下进行编辑。
1. 从侧栏中的内容浏览器中，选择“数据模型对象”选项卡。 将NumericField1和TextField1拖动到自适应表单上。
1. 将NumericField1的标题从&#x200B;**Numeric Field**&#x200B;更改为&#x200B;**AF Numeric Field。**

>[!NOTE]
>
>在前面的步骤中，我们在XDP文件中覆盖了字段的属性。 因此，如果稍后修改XDP文件中的相应属性，则不同步此属性。

## 检测XDP文件{#detecting-changes-in-xdp-file}中的更改

只要XDP文件或片段中有任何更改，AEM Forms UI就会标记所有基于XDP文件或片段的自适应表单。

更新XDP文件后，您需要在AEM Forms UI中再次上传它，以便标记更改。

例如，让我们按照以下步骤更新`sample-form.xdp`文件：

1. 导航到`https://<server>:<port>/projects.html.`如果出现提示，请输入您的凭据。
1. 单击左侧的Forms选项卡。
1. 将`sample-form.xdp`文件下载到本地计算机上。 XDP文件将下载为`.zip`文件，可使用任何文件解压缩实用程序提取该文件。

1. 打开`sample-form.xdp`文件，将字段TextField1的标题从&#x200B;**Text Field**&#x200B;更改为&#x200B;**My Text Field**。

1. 将`sample-form.xdp`文件上传回AEM Forms UI。

如果XDP文件更新，则在编辑基于XDP文件的自适应表单时，您会在编辑器中看到一个图标。 此图标表示自适应表单与XDP文件不同步。 在下图中，请参阅侧栏中旁边的图标。

![用于显示自适应表单与XDP文件不同步的图标](assets/sync-af-xfa.png)

## 将自适应表单与最新的XDP文件{#synchronizing-adaptive-forms-with-the-latest-xdp-file}同步

在下次打开与XDP文件不同步的自适应表单进行创作时，将显示以下消息：**自适应表单的模式/表单模板已更新。 `Click Here` 以使用新版本对其进行重新设计。**

单击消息会将自适应表单中的字段与XDP文件中的相应字段同步。

对于本文中使用的示例，请在创作模式下打开`sample-xfa-af`。 消息将显示在自适应表单的底部。

![提示您将自适应表单与XDP文件同步的消息](assets/sync-af-xfa-1.png)

### 更新属性{#updating-the-properties}

除了作者在自适应表单（从组件对话框中）中显式覆盖的属性外，从XDP文件复制到自适应表单的所有属性都将更新。 服务器日志中提供已更新属性的列表。

要更新示例自适应表单中的属性，请单击消息中的链接（标记为`"Click Here"`）。 TextField1的标题从&#x200B;**Text Field**&#x200B;更改为&#x200B;**My Text Field**。

![update-property](assets/update-property.png)

>[!NOTE]
>
>未更改标签AF数字字段，因为您已从组件属性对话框中覆盖了此属性，如[向自适应表单添加内容](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p)中所述。

### 将新字段从XDP文件添加到自适应表单   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

之后添加到原始XDP文件的任何字段都显示在“表单层次结构”选项卡中，您可以将这些新字段拖动到自适应表单。

您无需单击错误消息中的链接即可更新表单层次结构选项卡中的字段。

### 已删除XDP文件{#deleted-fields-in-xdp-file}中的字段

如果从XDP文件中删除了以前复制到自适应表单的字段，则在创作模式下会显示一条错误消息，指出该字段不存在于XDP文件中。 在这种情况下，请手动从自适应表单中删除字段或清除组件对话框中的`bindRef`属性。

以下步骤在本文中使用的示例中说明资产的使用流程：

1. 更新`sample-form.xdp`文件并删除NumericField1。
1. 在AEM Forms UI中上载`sample-form.xdp`文件
1. 打开`sample-xfa-af`自适应表单进行创作。 将显示以下错误消息：自适应表单的模式/表单模板已更新。 `Click Here` 以使用新版本对其进行重新设计。

1. 单击消息中的链接（标记为“`Click Here`”）。 将显示一条错误消息，指出该字段不再存在于XDP文件中。

![删除XDP文件中的元素时出现错误](assets/no-element-xdp.png)

已删除的字段还会标有一个图标，以指示该字段中存在错误。

![字段中的错误图标](assets/error-field.png)

>[!NOTE]
>
>自适应表单中绑定不正确的字段（编辑对话框中的`bindRef`值无效）也被视为已删除的字段。 如果作者未修复这些错误并发布自适应表单，则该字段将被视为普通的未绑定自适应表单字段，并包含在输出XML文件的未绑定部分中。

## 下载 {#downloads}

本文中示例的内容包

[获取文件](assets/sample-xfa-af-sync-1.0.zip)
