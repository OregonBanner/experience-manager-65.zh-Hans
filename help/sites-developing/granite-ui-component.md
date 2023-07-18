---
title: 创建新的Granite UI字段组件
description: Granite UI提供了一系列旨在用于表单的组件，称为字段
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# 创建新的Granite UI字段组件{#creating-a-new-granite-ui-field-component}

Granite UI提供了一系列旨在用于表单的组件；这些组件称为 *字段* 在Granite UI词汇中。 标准Granite表单组件在以下位置提供：

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>这些Granite UI表单字段特别令人感兴趣，因为它们用于 [组件对话框](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>有关字段的完整详细信息，请参阅 [Granite UI文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

使用Granite UI Foundation框架开发和/或扩展Granite组件。 这包含两个元素：

* 服务器端：

   * 基础组件的集合

      * 基础 — 模块化、可组合、可分层、可重用
      * 组件 — Sling组件

   * 帮助应用程序开发的帮助程序

* 客户端：

   * 提供一些词汇(即HTML语言的扩展)的clientlibs集合，以通过超媒体驱动的用户界面实现通用的交互模式。

通用Granite UI组件 `field` 由两个感兴趣的文件组成：

* `init.jsp`：处理常规处理；标记、描述，并提供呈现字段时所需的表单值。
* `render.jsp`：这是执行字段实际渲染的位置，并且必须为自定义字段覆盖；包含于 `init.jsp`.

参见 [Granite UI文档 — 字段](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 了解详细信息。

有关示例，请参阅：

* `cqgems/customizingfield/components/colorpicker`

   * 由 [代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>由于此机制使用JSP，因此i18n和XSS不是现成的。 这意味着您必须国际化并避开“字符串”。 以下目录包含来自标准实例的通用字段，您可以将这些字段用作引用：
>
>`/libs/granite/ui/components/foundation/form` 目录

## 创建组件的服务器端脚本 {#creating-the-server-side-script-for-the-component}

您的自定义字段应仅覆盖 `render.jsp` 脚本，您可以在其中为组件提供标记。 可以将JSP（即渲染脚本）视为标记的包装器。

1. 创建使用 `sling:resourceSuperType` 继承自以下对象的属性：

   `/libs/granite/ui/components/foundation/form/field`

1. 覆盖脚本：

   `render.jsp`

   在此脚本中，生成超媒体标记（即，包含超媒体可供性的扩充标记），以便客户端知道如何与生成的元素交互。 这应遵循Granite UI服务器端编码样式。

   在自定义时，您唯一的 *必须* fullable为读取表单值(初始化于 `init.jsp`)从请求访问：

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   有关更多详细信息，请参阅现成Granite UI字段的实施；例如， `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >目前，JSP是首选的脚本编写方法，因为在HTL中不太容易实现将信息从一个组件传递到另一个组件（在表单/字段的上下文中频繁发生）。

## 为组件创建客户端库 {#creating-the-client-library-for-the-component}

要将特定客户端行为添加到组件，请执行以下操作：

1. 创建类别的clientlib `cq.authoring.dialog`.
1. 创建类别的clientlib `cq.authoring.dialog` 并定义 `JS`/ `CSS` 里面的。

   定义 `JS`/ `CSS` clientlib内部。

   >[!NOTE]
   >
   >目前，Granite UI不提供任何可以直接用于添加JS行为的现成侦听器或挂接。 因此，要向组件添加其他JS行为，您必须实施JS挂接到自定义类，然后在标记生成期间将该自定义类分配给组件。
