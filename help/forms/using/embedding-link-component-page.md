---
title: 在页面中嵌入链接组件
seo-title: Embedding link component in a page
description: 您可以使用链接组件从任何页面链接自适应文档或自适应表单。
seo-description: You can use the link component to link an adaptive document or an adaptive form from any page.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 在页面中嵌入链接组件{#embedding-link-component-in-a-page}

## 前提条件 {#prerequisites}

链接组件是Document Services类别的成员。 确保Document Services类别在AEM组件浏览器中可见。 如果未列出该类别，请按照 [启用Forms Portal组件](/help/forms/using/enabling-forms-portal-components.md).

## 链接组件 {#link-component}

利用链接组件，表单门户作者可在页面上的任何位置创建指向自适应表单的链接。 链接组件在组件浏览器的“文档服务”部分中提供。

执行以下步骤以将链接组件添加到页面：

1. 拖动 **链接** 组件。 选择组件并选择 ![cmppr](assets/cmppr.png). 这将打开编辑链接组件对话框。

   ![edit-link-component](assets/edit-link-component.png)

1. 在 **显示** 选项卡中，指定以下内容：

   * **链接标题**：链接的文本或标题。
   * **链接工具提示**：链接的工具提示。
   * **布局模板**：链接组件布局模板。

1. 打开 **资源信息** 选项卡，并指定资源的类型。 资产可以是 **表单**. 根据所选资产类型，将显示以下选项：

   * **资产路径**：存储资产的存储库路径。

   * **渲染类型**：渲染格式 — “PDF”、“HTML”或“自动”。 自动渲染类型会检测用户环境，并相应地将表单渲染为HTML或PDF。 例如，如果从移动设备访问表单，则自动渲染类型以HTML渲染表单。
   * **提交URL：**  指向提交表单数据的servlet的URL。
   * **HTML配置文件**：用于将表单渲染为HTML的配置文件。
   * **PDF配置文件**：用于将表单渲染为PDF文档的配置文件。

1. 打开 **高级** 选项卡。 可用键值对格式指定其他参数。 单击链接时，这些附加参数将与表单一起传递。

   选择 **完成** 以保存配置。

## 使用链接组件的最佳实践 {#best-practices-for-using-link-component-br}

* 如果在“表单路径”中指定的PDF指向文档(该文档的PDF作为其允许的渲染格式)，请确保选择“路径”作为渲染类型。
* 可以在多个位置指定表单的提交URL，其优先顺序如下：

   1. 表单中嵌入的提交URL（在提交按钮中）具有最高优先级。
   1. Forms Manager中提到的提交URL具有中优先级。
   1. Forms Portal中提到的提交URL的优先级最低。
