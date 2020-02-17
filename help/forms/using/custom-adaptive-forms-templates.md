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

---


# 创建自定义自适应表单模板{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms已引入动态模板。 您可以使用AEM Sites模板编辑器创建 [或编辑动态模板](../../forms/using/template-editor.md)。 下面文章中提到的模板是静态模板。 默认安装中不提供这些组件。 [安装兼容性包](../../forms/using/compatibility-package.md) ，在您的环境中获取这些模板。

## 前提条件 {#prerequisites}

* 了解AEM页面 [模板和自适应](/help/sites-authoring/templates.md) 表 [单创作](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* 了解AEM客 [户端库](/help/sites-developing/clientlibs.md)

## Adaptive form template {#adaptive-form-template}

自适应表单模板是专用的AEM页面模板，具有用于创建自适应表单的某些属性和内容结构。 模板具有预配置的布局、样式和基本的初始内容结构。

创建表单后，对原始模板内容结构的任何更改都不会反映在表单中。

## 默认自适应表单模板 {#default-adaptive-form-templates}

AEM quickStart提供以下自适应表单模板：

* 调查模板：允许您使用已配置多列的响应式布局创建单页自适应表单。 布局会根据要显示表单的各种屏幕的尺寸自动调整。
* 简单登记模板：允许您使用向导布局创建多步自适应表单。 在此布局中，您可以为每个步骤指定一个步骤完成表达式，该表达式在向导继续执行下一步之前经过验证。
* 选项卡式登记模板：允许您使用左侧选项卡布局创建多选项卡自适应表单，您可以按任意顺序访问选项卡。
* 高级登记模板：允许您创建包含多个选项卡和向导的表单。 它使用左侧选项卡的布局，允许您按任意顺序访问选项卡。 它使用Adobe Document cloud设计服务进行签名和验证。
* 空白模板：允许您创建不含任何页眉、页脚和初始内容的表单。 您可以添加文本框、按钮和图像等组件。 空白模板允许您创建可嵌入AEM站 [点页面的表单](/help/forms/using/embed-adaptive-form-aem-sites.md)。

这些模板的属 `sling:resourceType` 性设置为相应的页面组件。 页面组件呈现CQ页面，其中包含自适应表单容器，而自适应表单容器则呈现自适应表单。

下表枚举了模板与页面组件之间的关联：

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
   <td><p>/libs/fd/af/templates/simpleEnmortyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnmortmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnmortmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advanced-relloment</p> </td>
  </tr>
 </tbody>
</table>

## 使用模板编辑器创建自适应表单模板 {#creating-an-adaptive-form-template-using-template-editor}

您可以使用模板编辑器指定自适应表单的结构和初始内容。 例如，您希望所有表单作者在登记表单中都具有几个文本框、导航按钮和提交按钮。 您可以创建一个模板，作者可以使用该模板创建与其他注册表单一致的表单。 AEM模板编辑器允许您：

* 在结构层中添加表单的页眉和页脚组件
* 为表单提供初始内容。
* 指定主题。
* 指定提交、重置和导航等操作。

有关详细信息，请参阅模 [板编辑器](../../forms/using/template-editor.md)。

## 从CRXDE创建自适应表单模板 {#creating-an-adaptive-form-template-from-crxde}

您可以创建模板并使用它创建自适应表单，而不是使用可用的模板。 自定义模板基于引用自适应表单容器和页面元素（如页眉和页脚）的各种页面组件。

您可以使用网站的基本页面组件创建这些组件。 或者，您也可以扩展自适应表单的页面组件（现成模板使用）。

执行以下步骤以创建自定义模板，如simpleEngromentTemplate。

1. 在创作实例上导航到CRXDE Lite。

1. 在/apps目录下，为应用程序创建文件夹结构。 例如，如果应用程序名称是mycompany，则创建一个具有此名称的文件夹。 通常，应用程序文件夹包含组件、配置、模板、src和安装目录。 在此示例中，创建组件、配置和模板文件夹。

1. 导览至文件夹/libs/fd/af/templates。
1. 复制节 `simpleEnrollmentTemplate` 点。
1. 导览至文件夹/apps/mycompany/templates。 右键单击它并选择“粘 **[!UICONTROL 贴”]**。
1. 如有必要，请重命名您复制的模板节点。 例如，将其重命名为登记模板。

1. 导航到位置/apps/mycompany/templates/engroment-template。

1. 修改节 `jcr:title` 点的 `jcr:description` 和属性 `jcr:content` ，以区分模板和您复制的模板。

1. 修 `jcr:content` 改后的模板的节点包含 `guideContainer` 和组 `guideformtitle` 件。 `guideContainer` 是保存自适应表单的容器。 组 `guideformtitle` 件显示应用程序名称、说明等。

   您可以包 `guideformtitle`含自定义组件或组件，而不是 `parsys` 包含。 例如，删除 `guideformtitle`并添加自定义组件或组 `parsys` 件节点。 确保组件 `sling:resourceType` 的属性引用组件，并且该属性在页面文件中也进行了定 `component.jsp` 义。

1. 导航到位置/apps/mycompany/templates/engroment-template/jcr:content。

1. 打开“ **[!UICONTROL 属性]** ”选项卡，将属性的值 `cq:designPath` 更改为/etc/designs/mycompany。

1. 现在，为类型创建一个/etc/designs/mycompany节 `cq:Page` 点。

## 创建自适应表单页面组件 {#create-an-adaptive-form-page-component}

自定义模板的样式与默认模板相同，因为模板引用页面组件/libs/fd/af/components/page/base。 您可以查找组件引用，它是在节 `sling:resourceType` 点/apps/mycompany/templates/engroment-template/jcr:content中定义的属性。 由于基础是核心产品组件，因此请勿修改此组件。

1. 导航到节点/apps/mycompany/templates/enjorment-template/jcr:content，并将属性的值修改为/apps/mycompany/components/page/enromentpage `sling:resourceType`
1. 将节点/libs/fd/af/components/page/base复制到文件夹/apps/mycompany/components/page。

1. 将复制的组件重命名为 `enrollmentpage`。

1. **（仅当您已有内容页面时）** ，如果您有网站的现有组件，请执行以下 `contentpage`步骤(a-d)。 如果您没有网站的现 `contentpage`有组件，则可以保留 `resourceSuperType`该属性以指向OOTB基页。

   1. 对于节 `enrollmentpage` 点，将属性的值设置为 `sling:resourceSuperType` mycompany/components/page/contentpage。 组 `contentpage` 件是站点的基本页面组件。 其他页面组件可以扩展它。 删除脚本文 `enrollmentpage`件，除 `head.jsp`、 `content.jsp`和之外 `library.jsp`。 在本 `sling:resourceSuperType` 例中，该组件 `contentpage` 包括所有此类脚本。 页眉（包括导航栏和页脚）是从组件继承 `contentpage` 的。

   1. Open the file `head.jsp`.

      JSP文件包含该行 `<cq.include script="library.jsp"/>`。

      该文 `library.jsp` 件包含客 `guide.theme.simpleEnrollment` 户端库，它包含自适应表单的样式。

      页面组件 `enrollmentpage` 有一个专用 `head.jsp` 文件，它覆盖 `head.jsp` 了组件的文 `contentpage` 件。

   1. 将组件的所有脚 `head.jsp` 本包含在该 `contentpage` 组件的文件 `head.jsp` 中到该组件的文 `enrollmentpage` 件中。
   1. 在脚本 `content.jsp` 中，您可以添加其他页面内容或对页面呈现时包含的其他组件的引用。 例如，如果添加自定义组件， `applicationformheader`请确保在JSP文件中为该组件添加以下引用：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同样，如果在模板节点结 `parsys` 构中添加组件，也应包括自定义组件。

## 创建自适应表单客户端库 {#creating-an-adaptive-form-client-library}

新模 `head.jsp` 板的组 `enrollmentpage` 件文件包括客户端库 `guide.theme.simpleEnrollment`。 默认模板还使用此客户端库。 使用以下方法更改新模板中的样式：

* 定义自定义主题，并将默认主题替 `guide.theme.simpleEnrollment` 换为自定义主题。
* 在/etc/designs/mycompany下定义新的客户端库。 在jsp页中的默认主题条目后加入客户端库。 在此客户端库中包含所有被覆盖的样式和其他Java Script文件。

>[!NOTE]
>
>主题是指包含在用于渲染自适应表单的页面组件中的客户端库。 客户端库主要控制自适应表单的外观。

