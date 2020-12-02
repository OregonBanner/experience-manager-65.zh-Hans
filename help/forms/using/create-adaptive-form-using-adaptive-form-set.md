---
title: 使用一组自适应表单创建自适应表单
seo-title: 使用一组自适应表单创建自适应表单
description: '与AEM Forms合作，将自适应表单整合在一起，创作单个大型自适应表单并了解其功能。 '
seo-description: '与AEM Forms合作，将自适应表单整合在一起，创作单个大型自适应表单并了解其功能。 '
uuid: e52e4f90-8821-49ec-89ff-fbf07db69bd2
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 264aa8c0-ba64-4768-b3d1-1b9baa6b4d72
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---


# 使用一组自适应表单创建自适应表单{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## 概述 {#overview}

在工作流程（如用于开立银行帐户的应用程序）中，您的用户会填写多个表单。 您可以将表单堆叠在一起并构建一个大型表单（父表单），而不是要求他们填写一组表单。 向较大表单添加自适应表单时，它将添加为面板（子表单）。 您可以添加一组子表单来创建父表单。 您可以根据用户输入显示或隐藏面板。 父表单的按钮（如提交和重置）将覆盖子表单的按钮。 要在父表单中添加自适应表单，您可以从资产浏览器中拖放自适应表单（如自适应表单片段）。

可用功能包括：

* 独立创作
* 显示／隐藏适当的表单
* 延迟加载

独立创作和延迟加载等功能比使用单个组件创建父表单提高了性能。

>[!NOTE]
>
>不能将基于XFA的自适应表单／片段用作子表单或父表单。

## 幕后花絮{#behind-the-scenes}

您可以在父表单中添加基于XSD的自适应表单和片段。 父表单的结构与任何自适应表单[相同。 ](../../forms/using/prepopulate-adaptive-form-fields.md)当您将自适应表单添加为子表单时，它会作为面板添加到父表单中。 绑定子表单的数据存储在父表单的XML模式的`afBoundData`部分的`data`根下。

例如，您的客户填写申请表。 表单的前两个字段是名称和标识。 其XML为：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

您可以在应用程序中添加另一个表单，让客户填写其办公地址。 子表单的模式根为`officeAddress`。 应用`bindref` `/application/officeAddress`或`/officeAddress`。 如果未提供`bindref`，则将子表单添加为`officeAddress`子树。 请参阅下面表单的XML:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

如果插入另一个允许客户提供房地址的表单，则应用`bindref` `/application/houseAddress or /houseAddress.` XML如下：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

如果要保留与模式根（本例中为`Address`）相同的子根名称，请使用索引bindrefs。

例如，应用bindrefs `/application/address[1]`或`/address[1]`和`/application/address[2]`或`/address[2]`。 表单的XML为：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

您可以使用`bindRef`属性更改自适应表单／片段的默认子树。 通过`bindRef`属性，可指定指向XML模式树结构中某个位置的路径。

如果子表单未绑定，则其数据存储在父表单的XML模式的`afUnboundData`部分的`data`根下。

您可以多次将自适应表单添加为子表单。 确保正确修改`bindRef`，以便自适应表单的每个已使用实例指向数据根下的不同子根。

>[!NOTE]
>
>如果不同的表单／片段被映射到同一子根，则数据将被覆盖。

## 使用资产浏览器{#adding-an-adaptive-form-as-a-child-form-using-asset-browser}将自适应表单添加为子表单

请执行以下步骤，使用资产浏览器将自适应表单添加为子表单。

1. 在编辑模式下打开父表单。
1. 在提要栏中，单击&#x200B;**资产** ![资产——浏览器](assets/assets-browser.png)。 在“资产”下，从下拉列表中选择&#x200B;**自适应表单**。
   [ ![在资产下选择自适应表单](assets/asset.png)](assets/asset-1.png)

1. 拖放要作为子表单添加的自适应表单。
   [ ![将自适应表单拖放到站点](assets/drag-drop.png)](assets/drag-drop-1.png)中拖放的自适应表单将添加为子表单。

