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
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 1%

---

# 在页面{#embedding-link-component-in-a-page}中嵌入链接组件

## 前提条件 {#prerequisites}

链接组件是“文档服务”类别的成员。 确保“文档服务”类别在AEM组件浏览器中可见。 如果未列出类别，请按照[启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)中列出的步骤操作。

## 链接组件{#link-component}

链接组件允许表单门户作者从页面上的任意位置创建指向自适应表单的链接。 链接组件位于组件浏览器的文档服务部分中。

执行以下步骤以将链接组件添加到页面：

1. 在页面上拖动&#x200B;**Link**&#x200B;组件。 选择组件并点按![cmppr](assets/cmppr.png)。 将打开编辑链接组件对话框。

   ![edit-link-component](assets/edit-link-component.png)

1. 在&#x200B;**Display**&#x200B;选项卡中，指定以下内容：

   * **链接标题**:链接文本或描述。
   * **链接工具提示**:链接的工具提示。
   * **布局模板**:链接组件布局的模板。

1. 打开&#x200B;**资产信息**&#x200B;选项卡，并指定资产类型。 资产可以是&#x200B;**窗体**。 根据所选资产的类型，将显示以下列出的选项：

   * **资产路径**:存储资产的存储库路径。

   * **呈现类型**:渲染格式 — PDF、HTML或自动。自动渲染类型会检测用户环境，并相应地将表单渲染为HTML或PDF。 例如，如果从移动设备访问表单，则自动渲染类型会以HTML形式渲染表单。
   * **提交URL:**  将URL提交到从中提交表单数据的Servlet。
   * **HTML配置文件**:用于将表单渲染为HTML的配置文件。
   * **PDF配置文件**:用于将表单渲染为PDF文档的配置文件。

1. 打开&#x200B;**高级**&#x200B;选项卡。您可以以键值对格式指定其他参数。 单击链接后，这些附加参数将随表单一起传递。

   点按&#x200B;**完成**&#x200B;以保存配置。

## 使用链接组件{#best-practices-for-using-link-component-br}的最佳实践

* 如果在“表单路径”中指定的路径指向文档，且该文档包含PDF作为其允许的渲染格式，请确保选择PDF作为渲染类型。
* 表单的提交URL可以在多处指定，其优先顺序如下：

   1. 表单中嵌入的提交URL（在提交按钮中）具有最高优先级。
   1. 在Forms Manager中提及的提交URL具有中等优先级。
   1. 在Forms Portal中提及的提交URL优先级最低。
