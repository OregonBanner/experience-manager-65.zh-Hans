---
title: 创建自定义自适应表单模板
seo-title: Creating a custom adaptive form template
description: 本文介绍了如何创建自定义自适应表单模板。
seo-description: This article describes how to create custom adaptive form templates.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# 创建自定义自适应表单模板{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms引入了动态模板。 您可以使用AEM Sites模板编辑器来 [创建或编辑动态模板](../../forms/using/template-editor.md). 下文中提到的模板是静态模板。 这些选项在默认安装中不可用。 [安装兼容包](../../forms/using/compatibility-package.md) 以便在您的环境中获取这些模板。

## 前提条件 {#prerequisites}

* 了解AEM [页面模板](/help/sites-authoring/templates.md) 和 [自适应表单创作](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* 了解AEM [客户端库](/help/sites-developing/clientlibs.md)

## 自适应表单模板 {#adaptive-form-template}

自适应表单模板是专用的AEM页面模板，具有某些用于创建自适应表单的属性和内容结构。 模板具有预配置的布局、样式和基本初始内容结构。

创建表单后，对原始模板内容结构所做的任何更改都不会反映在表单中。

## 默认自适应表单模板 {#default-adaptive-form-templates}

AEM QuickStart提供了以下自适应表单模板：

* 调查模板：允许您使用配置了多个列的响应式布局创建单页自适应表单。 布局会根据要在其上显示表单的各种屏幕的尺寸自动进行调整。
* 简单注册模板：允许您使用向导布局创建多步骤自适应表单。 在此布局中，您可以为每个步骤指定步骤完成表达式，该表达式在向导继续下一步之前经过验证。
* 选项卡式注册模板：允许您使用左侧的选项卡式布局创建多选项卡式自适应表单，您可以在其中按任意顺序访问选项卡。
* 高级注册模板：允许您创建具有多个选项卡和向导的表单。 它使用左侧的选项卡布局，允许您按任意顺序访问选项卡。 它使用Adobe Document Cloud设计服务进行签名和验证。
* 空白模板：允许您创建没有任何页眉、页脚和初始内容的表单。 可以添加文本框、按钮和图像等组件。 使用空白模板可创建表单，您可以 [嵌入到AEM网站页面](/help/forms/using/embed-adaptive-form-aem-sites.md).

这些模板具有 `sling:resourceType` 属性设置为相应的页面组件。 页面组件渲染CQ页面（包含自适应表单容器），进而渲染自适应表单。

下表枚举模板与页面组件之间的关联：

<table>
 <tbody>
  <tr>
   <td><p><strong>模板</strong></p> </td>
   <td><p><strong>页面组件</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## 使用模板编辑器创建自适应表单模板 {#creating-an-adaptive-form-template-using-template-editor}

您可以使用模板编辑器指定自适应表单的结构和初始内容。 例如，您希望所有表单作者在注册表单中都只有几个文本框、导航按钮和提交按钮。 您可以创建一个模板，供作者创建与其他注册表单一致的表单。 通过AEM模板编辑器，您可以：

* 在结构层中添加表单的页眉和页脚组件
* 提供表单的初始内容。
* 指定主题。
* 指定提交、重置和导航等操作。

有关更多信息，请参阅 [模板编辑器](../../forms/using/template-editor.md).

## 从CRXDE创建自适应表单模板 {#creating-an-adaptive-form-template-from-crxde}

您可以创建模板并使用它来创建自适应表单，而不是使用可用的模板。 自定义模板基于引用自适应表单容器和页面元素（如页眉和页脚）的各种页面组件。

您可以使用网站的基础页面组件创建这些组件。 或者，您也可以扩展现成模板使用的自适应表单的页面组件。

执行以下步骤可创建自定义模板，如simpleEnrollmentTemplate。

1. 在创作实例上导航到CRXDE Lite。

1. 在/apps目录下，为应用程序创建文件夹结构。 例如，如果应用程序名称为mycompany，请使用此名称创建一个文件夹。 通常，应用程序文件夹包含组件、配置、模板、src和安装目录。 在本例中，创建“组件”、“配置”和“模板”文件夹。

1. 导航到文件夹/libs/fd/af/templates。
1. 复制 `simpleEnrollmentTemplate` 节点。
1. 导航到/apps/mycompany/templates文件夹。 右键单击并选择 **[!UICONTROL 粘贴]**.
1. 如有必要，请重命名复制的模板节点。 例如，将其重命名为注册模板。

1. 导航到位置/apps/mycompany/templates/enrollment-template。

1. 修改 `jcr:title` 和 `jcr:description` 的属性 `jcr:content` 节点，以区分模板和复制的模板。

1. 此 `jcr:content` 修改模板的节点包含 `guideContainer` 和 `guideformtitle` 组件。 `guideContainer` 是保存自适应表单的容器。 此 `guideformtitle` 组件显示应用程序名称、描述等。

   而不是 `guideformtitle`中，您可以包含自定义组件或 `parsys` 组件。 例如，删除 `guideformtitle`，并添加自定义组件或 `parsys` 组件节点。 确保 `sling:resourceType` 组件的属性引用组件，并在页面中定义该组件 `component.jsp` 文件。

1. 导航到位置/apps/mycompany/templates/enrollment-template/jcr：content。

1. 打开 **[!UICONTROL 属性]** 制表符并更改 `cq:designPath` 属性到/etc/designs/mycompany。

1. 现在为创建一个/etc/designs/mycompany节点 `cq:Page` 类型。

## 创建自适应表单页面组件 {#create-an-adaptive-form-page-component}

自定义模板的样式与默认模板相同，因为模板引用页面组件/libs/fd/af/components/page/base。 您可以找到作为属性的组件引用 `sling:resourceType` 在节点/apps/mycompany/templates/enrollment-template/jcr：content中定义。 由于基础是核心产品组件，因此请勿修改此组件。

1. 导航到节点/apps/mycompany/templates/enrollment-template/jcr：content并修改属性的值 `sling:resourceType` 到/apps/mycompany/components/page/enrollmentpage
1. 将节点/libs/fd/af/components/page/base复制到文件夹/apps/mycompany/components/page中。

1. 将复制的组件重命名为 `enrollmentpage`.

1. **（仅当您已有内容页面时）** 如果现有，请执行以下步骤(a-d) `contentpage`网站组件。 如果您不存在 `contentpage`组件时，您可以将 `resourceSuperType`属性指向OOTB基本页。

   1. 对于 `enrollmentpage` 节点，设置属性的值 `sling:resourceSuperType` 到mycompany/components/page/contentpage。 此 `contentpage` 组件是站点的基本页面组件。 其他页面组件可以对其进行扩展。 删除下的脚本文件 `enrollmentpage`，除 `head.jsp`， `content.jsp`、和 `library.jsp`. 此 `sling:resourceSuperType` 组件，即 `contentpage` 在这种情况下，包括所有此类脚本。 标题（包括导航栏和页脚）继承自 `contentpage` 组件。

   1. 打开文件 `head.jsp`.

      JSP文件包含行 `<cq.include script="library.jsp"/>`.

      此 `library.jsp` 文件包含 `guide.theme.simpleEnrollment` 客户端库，其中包含自适应表单的样式。

      页面组件 `enrollmentpage` 具有独占 `head.jsp` 覆盖 `head.jsp` 的文件 `contentpage` 组件。

   1. 将所有脚本包含在 `head.jsp` 的文件 `contentpage` 组件到 `head.jsp` 的文件 `enrollmentpage` 组件。
   1. 在 `content.jsp` 脚本，您可以添加其他页面内容或对页面渲染时包含的其他组件的引用。 例如，如果添加自定义组件 `applicationformheader`，请确保在JSP文件中添加对组件的以下引用：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同样，如果添加 `parsys` 组件在模板节点结构中，还包括自定义组件。

## 创建自适应表单客户端库 {#creating-an-adaptive-form-client-library}

此 `head.jsp` 的文件 `enrollmentpage` 新模板的组件包括一个客户端库 `guide.theme.simpleEnrollment`. 默认模板也使用此客户端库。 使用以下方法之一更改新模板中的样式：

* 定义自定义主题并替换默认主题 `guide.theme.simpleEnrollment` 使用自定义主题。
* 在/etc/designs/mycompany下定义新的客户端库。 在jsp页中的默认主题条目之后包含客户端库。 在此客户端库中包含所有覆盖的样式和其他Java脚本文件。

>[!NOTE]
>
>主题是指用于呈现自适应表单的页面组件中包含的客户端库。 客户端库主要控制自适应表单的外观。
