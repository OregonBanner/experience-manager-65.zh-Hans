---
title: CIF产品和类别选取器的用法
description: 了解如何在客户商务组件中使用CIF产品和类别选取器，以支持作者和营销人员高效地处理商务产品和目录数据。
sub-product: 商务
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: 商务集成框架
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# AEM Content &amp; Commerce创作选取器{#cif-pickers}

AEM Content &amp; Commerce Authoring提供了一套创作工具，可帮助AEM作者和营销人员高效地处理商务产品数据和目录。 产品选取器和类别选取器是CIF附加组件的一部分，供CIF核心组件使用。 项目可以在任何组件对话框中使用这些选取器来选择产品或类别。

## 产品选取器 {#product-picker}

要在项目组件中使用产品选取器，开发人员必须将`commerce/gui/components/common/cifproductfield`添加到组件对话框。 例如，对cq:dialog使用以下内容：

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

产品字段允许通过不同视图导航到用户要选择的产品。 默认情况下，product字段会返回产品的ID，但可以使用`selectionId`属性对其进行配置。

产品选取器字段支持以下可选属性：

- selectionId(id、uid、sku、sug、combinedSlug、combinedSku) — 允许选择选取器返回的产品属性（默认= id）。 使用sku可返回选定产品的SKU，使用combinedSku时，将返回诸如base#variant之类的字符串（其中包含基本产品和所选变体的SKU）；或者，如果选择了基本产品，则返回单个SKU。
- filter(folderOrProduct、folderOrProductOrVariant) — 在导航产品树时筛选器要呈现的内容。 folderOrProduct — 渲染文件夹和产品。 folderOrProductOrVariant — 渲染文件夹、产品和产品变体。 如果某个产品或产品变体已呈现，则它也会在选取器中变为可选。 （默认值= folderOrProduct）
- 多个(true， false) — 启用对一个或多个产品的选择(default = false)
- emptyText — 配置选取器字段的空文本值

此外，还支持标准图表字段属性，如`name`、`fieldLabel`或`fieldDescription`。

`cifproductfield`组件需要cif.shell.picker clientlib。 要向对话框中添加clientlib，您可以使用extraClientlibs属性。

`cifproductfield`的完整工作示例可在[CIF核心组件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)项目中找到。 另请参阅AEM核心组件文档的[自定义对话框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs)。

## 类别选取器{#category-picker}

类别选取器也可在组件对话框中使用，其方式与产品选取器类似。

以下代码片段可在cq:dialog配置中使用：

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

类别选取器字段支持以下可选属性：

- selectionId(id， uid， sulg， idAndUrlPath， uidAndUrlPath) — 允许选择选取器返回的类别属性（默认值= id）。 idAndUrlPath &amp; uidAndUrlPath是一些特殊选项，用于存储以 |字符，例如1|men/tops。
- 多个(true， false) — 启用一个或多个类别的选择(default = false)

此外，还支持标准图表字段属性，如`name`、`fieldLabel`或`fieldDescription`。

与`cifproductfield`组件相同，`cifcategoryfield`组件还需要cif.shell.picker clientlib。 要向对话框中添加clientlib，可以使用`extraClientlibs`属性。 请参阅AEM核心组件文档的[自定义对话框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) 。

`cifcategoryfield`的完整工作示例可在[CIF核心组件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)项目中找到。
