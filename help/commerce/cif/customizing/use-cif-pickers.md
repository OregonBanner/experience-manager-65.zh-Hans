---
title: CIF产品和类别选取器的用法
description: 了解如何在客户商务组件中使用CIF产品和类别选取器，以支持作者和营销人员高效地使用商务产品和目录数据。
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: dceb187ba28ad7c377e98d29d6c815fe37e23077
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# AEM Content &amp; Commerce创作选取器 {#cif-pickers}

AEM Content &amp; Commerce Authoring提供了一组创作工具，以帮助AEM作者和营销人员有效地使用商业产品数据和目录。 产品选取器和类别选取器是CIF加载项的一部分，并由CIF核心组件使用。 项目可以在任何组件对话框中使用这些选取器来选择产品或类别。

## 产品选取器 {#product-picker}

要在项目组件中使用产品选取器，开发人员必须添加 `commerce/gui/components/common/cifproductfield` 到组件对话框。 例如，对cq使用以下内容:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

利用product字段，可导航到用户希望通过不同视图选择的产品。 默认情况下， product字段会返回产品的ID，但可使用进行配置 `selectionId` 属性。

产品选取器字段支持以下可选属性：

- selectionId(id、uid、sku、slug、combinedSlug、combinedSku) — 允许选择选择器返回的产品属性（默认为id）。 使用sku可返回所选产品的sku，而使用combinedSku时可返回诸如base#variant之类的字符串以及基础产品和所选变体的sku，如果选择基础产品，则返回单个sku。
- 过滤器(folderOrProduct、folderOrProductOrVariant) — 过滤要在导航产品树时由选取器呈现的内容。 folderOrProduct — 渲染文件夹和产品。 folderOrProductOrVariant — 渲染文件夹、产品和产品变体。 如果呈现了产品或产品变体，它也会在选取器中处于可选状态。 （默认为folderOrProduct）
- 多个(true， false) — 启用选择一个或多个产品的功能（默认值= false）
- emptyText — 配置选取器字段的空文本值

此外，标准diaglog字段属性如 `name`， `fieldLabel`，或 `fieldDescription` 支持。

>[!CAUTION]
>
>此 `cifproductfield` 组件需要 `cif.shell.picker` clientlib。 要将clientlib添加到对话框，您可以使用extraClientlibs属性。
>[!CAUTION]
>
>从CIF核心组件版本2.0.0开始，支持 `id` 已被移除并替换为 `uid`. 我们强烈建议使用 `sku` 或 `slug` 作为产品标识符。 我们将继续支持 `id` 仅适用于使用CIF核心组件1.x版的项目。

的完整工作示例 `cifproductfield` 可在以下位置找到： [CIF核心组件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) 项目。 另请参阅 [自定义对话框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) AEM核心组件文档的。

## 类别选取器 {#category-picker}

类别选取器也可在组件对话框中使用，其方式与产品选取器类似。

以下代码片段可以在cq：dialog配置中使用：

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

类别选取器字段支持以下可选属性：

- selectionId(id， uid， slug， urlPath， idAndUrlPath _（已弃用）_， uidAndUrlPath _（已弃用）_) — 允许选择选择器返回的类别属性（默认为id）。
- multiple (true， false) — 启用选择一个或多个类别（默认值= false）

此外，标准diaglog字段属性如 `name`， `fieldLabel`，或 `fieldDescription` 支持。

>[!CAUTION]
>
>与 `cifproductfield` 组成 `cifcategoryfield` 组件还需要 `cif.shell.picker` clientlib。 要将clientlib添加到对话框，您可以使用 `extraClientlibs` 属性。 参见 [自定义对话框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) AEM核心组件文档的。
>[!CAUTION]
>
>从CIF核心组件版本2.0.0开始，支持 `id` 已被移除并替换为 `uid`. 我们强烈建议使用 `uid` 或 `urlPath` 作为类别标识符。 我们将继续支持 `id` 和 `idAndUrlPath` 仅适用于使用CIF核心组件1.x版的项目。

的完整工作示例 `cifcategoryfield` 可在以下位置找到： [CIF核心组件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) 项目。
