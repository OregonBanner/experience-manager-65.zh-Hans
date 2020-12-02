---
title: 创建自定义自适应表单模板
seo-title: 创建自定义自适应表单模板
description: 本文介绍如何创建自定义自适应表单模板。
seo-description: 本文介绍如何创建自定义自适应表单模板。
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---


# 创建自定义自适应表单模板{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms推出了动态模板。 您可以使用AEM Sites模板编辑器[创建或编辑动态模板](../../forms/using/template-editor.md)。 以下文章中提到的模板是静态模板。 默认安装中不提供这些设置。 [安装兼容](../../forms/using/compatibility-package.md) 性包，在您的环境中获取这些模板。

## 前提条件 {#prerequisites}

* 了解AEM [页面模板](/help/sites-authoring/templates.md)和[自适应表单创作](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* 了解AEM [客户端库](/help/sites-developing/clientlibs.md)

## 自适应表单模板{#adaptive-form-template}

自适应表单模板是专用的AEM页面模板，具有用于创建自适应表单的某些属性和内容结构。 模板具有预配置的布局、样式和基本的初始内容结构。

创建表单后，对原始模板内容结构的任何更改不会反映在表单中。

## 默认自适应表单模板{#default-adaptive-form-templates}

AEM快速入门提供以下自适应表单模板：

* 调查模板:允许您使用已配置多列的响应式布局创建单页自适应表单。 布局会根据要显示表单的各种屏幕的尺寸自动调整。
* 简单登记模板：允许您使用向导布局创建多步自适应表单。 在此布局中，您可以为每个步骤指定一个步骤完成表达式，该完成在向导继续执行下一步之前经过验证。
* 标签登记模板：允许您使用左侧的选项卡布局创建多选项卡自适应表单，在该布局中，您可以按任意顺序访问选项卡。
* 高级登记模板：允许您创建包含多个选项卡和向导的表单。 它使用左侧选项卡布局，允许您按任意顺序访问选项卡。 它使用Adobe Document Cloud设计服务进行签名和验证。
* 空白模板：允许您创建不带任何页眉、页脚和初始内容的表单。 您可以添加文本框、按钮和图像等组件。 空白模板允许您创建一个表单，该表单可以[嵌入AEM站点页面](/help/forms/using/embed-adaptive-form-aem-sites.md)。

这些模板将`sling:resourceType`属性设置为相应的页面组件。 页面组件呈现CQ页面，其中包含自适应表单容器，而自适应表单则呈现自适应表单。

下表枚举了模板与页面组件之间的关联：

<table>
 <tbody>
  <tr>
   <td><p><strong>模板</strong></p> </td>
   <td><p><strong>页面组件</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/调查</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrommentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrommentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedrent</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrommentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## 使用模板编辑器{#creating-an-adaptive-form-template-using-template-editor}创建自适应表单模板

您可以使用模板编辑器指定自适应表单的结构和初始内容。 例如，您希望所有表单作者在登记表单中都有几个文本框、导航按钮和提交按钮。 您可以创建一个模板，作者可以使用该模板创建与其他登记表单一致的表单。 AEM模板编辑器允许您：

* 在结构层中添加表单的页眉和页脚组件
* 提供表单的初始内容。
* 指定主题。
* 指定提交、重置和导航等操作。

有关详细信息，请参阅[模板编辑器](../../forms/using/template-editor.md)。

## 从CRXDE {#creating-an-adaptive-form-template-from-crxde}创建自适应表单模板

您可以创建模板并使用它创建自适应表单，而不是使用可用的模板。 自定义模板基于引用自适应表单容器和页面元素（如页眉和页脚）的各种页面组件。

您可以使用网站的基本页面组件创建这些组件。 或者，您也可以扩展现成模板所使用的自适应表单的页面组件。

请执行以下步骤以创建自定义模板，如simpleEngrolmentTemplate。

1. 导航到创作实例上的CRXDE Lite。

1. 在/apps目录下，为应用程序创建文件夹结构。 例如，如果应用程序名称为mycompany，则创建一个具有此名称的文件夹。 通常，应用程序文件夹包含组件、配置、模板、src和安装目录。 在此示例中，创建组件、配置和模板文件夹。

1. 导览至文件夹/libs/fd/af/templates。
1. 复制`simpleEnrollmentTemplate`节点。
1. 导航到文件夹/apps/mycompany/templates。 右键单击它并选择&#x200B;**[!UICONTROL 粘贴]**。
1. 如有必要，请重命名您复制的模板节点。 例如，将其重命名为登记模板。

1. 导航到位置/apps/mycompany/templates/engrolment-template。

1. 修改`jcr:content`节点的`jcr:title`和`jcr:description`属性，将模板与您复制的模板区分开来。

1. 已修改模板的`jcr:content`节点包含`guideContainer`和`guideformtitle`组件。 `guideContainer` 是包含自适应表单的容器。`guideformtitle`组件显示应用程序名称、说明等。

   您可以包含自定义组件或`parsys`组件，而不是`guideformtitle`。 例如，删除`guideformtitle`，并添加自定义组件或`parsys`组件节点。 确保组件的`sling:resourceType`属性引用组件，并且在页面`component.jsp`文件中定义相同的属性。

1. 导航到位置/apps/mycompany/templates/engrolment-template/jcr:content。

1. 打开&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡，将`cq:designPath`属性的值更改为/etc/designs/mycompany。

1. 现在为`cq:Page`类型创建/etc/designs/mycompany节点。

## 创建自适应表单页面组件{#create-an-adaptive-form-page-component}

自定义模板的样式与默认模板的样式相同，因为模板引用页面组件/libs/fd/af/components/page/base。 您可以在节点/apps/mycompany/templates/enromment-template/jcr:content中找到作为属性`sling:resourceType`定义的组件引用。 由于基础是核心产品组件，请不要修改此组件。

1. 导航到节点/apps/mycompany/templates/enromment-template/jcr:content，将属性`sling:resourceType`的值修改为/apps/mycompany/components/page/enrmontpage
1. 将节点/libs/fd/af/components/page/base复制到文件夹/apps/mycompany/components/page。

1. 将复制的组件重命名为`enrollmentpage`。

1. **(仅当您已有内容页面** 时)如果您有网站的现有组件，请执行以 `contentpage`下步骤(a-d)。如果您的网站没有现有的`contentpage`组件，您可以保留`resourceSuperType`属性以指向OOTB基页。

   1. 对于`enrollmentpage`节点，将属性`sling:resourceSuperType`的值设置为mycompany/components/page/contentpage。 `contentpage`组件是站点的基本页面组件。 其他页面组件可以扩展它。 删除`enrollmentpage`下的脚本文件，但`head.jsp`、`content.jsp`和`library.jsp`除外。 `sling:resourceSuperType`组件（本例中为`contentpage`）包括所有此类脚本。 页眉（包括导航栏和页脚）是从`contentpage`组件继承的。

   1. 打开文件`head.jsp`。

      JSP文件包含行`<cq.include script="library.jsp"/>`。

      `library.jsp`文件包含`guide.theme.simpleEnrollment`客户端库，它包含自适应表单的样式。

      页面组件`enrollmentpage`有一个专用的`head.jsp`文件，它覆盖`contentpage`组件的`head.jsp`文件。

   1. 将`contentpage`组件的`head.jsp`文件包含到`enrollmentpage`组件的`head.jsp`文件中的所有脚本。
   1. 在`content.jsp`脚本中，可以添加其他页面内容或对页面呈现时包含的其他组件的引用。 例如，如果添加自定义组件`applicationformheader`，请确保在JSP文件中添加对该组件的以下引用：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同样，如果在模板节点结构中添加`parsys`组件，也应包含自定义组件。

## 创建自适应表单客户端库{#creating-an-adaptive-form-client-library}

新模板的`enrollmentpage`组件的`head.jsp`文件包括客户端库`guide.theme.simpleEnrollment`。 默认模板还使用此客户端库。 使用以下方法更改新模板中的样式：

* 定义自定义主题，并将默认主题`guide.theme.simpleEnrollment`替换为自定义主题。
* 在/etc/designs/mycompany下定义新的客户端库。 在jsp页中的默认主题条目后加入客户端库。 在此客户端库中包含所有被覆盖的样式和其他Java Script文件。

>[!NOTE]
>
>主题是指包含在用于渲染自适应表单的页面组件中的客户端库。 客户端库主要控制自适应表单的外观。

