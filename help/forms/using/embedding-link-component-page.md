---
title: 在页面中嵌入链接组件
seo-title: 在页面中嵌入链接组件
description: 您可以使用链接组件从任何页面链接自适应文档或自适应表单。
seo-description: 您可以使用链接组件从任何页面链接自适应文档或自适应表单。
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# 在页面中嵌入链接组件{#embedding-link-component-in-a-page}

## 前提条件 {#prerequisites}

链接组件是“文档服务”类别的成员。 确保“文档服务”类别在AEM组件浏览器中可见。 如果未列出该类别，请按照启用表单门户组件 [中列出的步骤操作](/help/forms/using/enabling-forms-portal-components.md)。

## 链接组件 {#link-component}

链接组件允许表单门户作者从页面上的任意位置创建指向自适应表单的链接。 链接组件位于组件浏览器的“文档服务”部分。

执行以下步骤将链接组件添加到页面：

1. 将链 **接组件** 拖到页面上。 选择组件并点按 ![cmppr](assets/cmppr.png)。 此时将打开编辑链接组件对话框。

   ![edit-link-component](assets/edit-link-component.png)

1. 在“显 **示** ”选项卡中，指定以下内容：

   * **链接题注**:链接文本或题注。
   * **链接工具提示**:链接的工具提示。
   * **布局模板**:链接组件的布局模板。

1. 打开资 **产信息选项卡** ，然后指定资产的类型。 资产可以是表 **单**。 根据所选资产的类型，将显示以下列出的选项：

   * **资产路径**:存储资产的存储库路径。

   * **渲染类型**:渲染格式- PDF、HTML或自动。 “自动”渲染类型会检测用户环境，并相应地将表单渲染为HTML或PDF。 例如，如果从移动设备访问表单，则“自动”渲染类型将以HTML格式渲染表单。
   * **** 提交URL: 提交表单数据的servlet的URL。
   * **HTML配置文件**:用于将表单呈现为HTML的配置文件。
   * **PDF简介**:将表单渲染为PDF文档的配置文件。

1. 打开&#x200B;**高级**&#x200B;选项卡。您可以以键值对格式指定其他参数。 单击链接时，这些附加参数会随表单一起传递。

   点按 **完成** ，以保存配置。

## 使用链接组件的最佳实践 {#best-practices-for-using-link-component-br}

* 如果在“表单路径”中指定的路径指向以PDF为允许的渲染格式的文档，请确保选择PDF作为渲染类型。
* 表单的提交URL可在多个位置指定，其优先级顺序如下：

   1. 嵌入在表单中的提交URL（在提交按钮中）具有最高优先级。
   1. 在Forms manager中提及的提交URL具有中等优先级。
   1. 表单门户中提及的提交URL的优先级最低。
