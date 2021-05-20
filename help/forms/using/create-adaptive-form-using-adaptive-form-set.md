---
title: 使用一组自适应表单创建自适应表单
seo-title: 使用一组自适应表单创建自适应表单
description: '借助AEM Forms，将自适应表单整合在一起，创作单个大型自适应表单，并了解其功能。 '
seo-description: '借助AEM Forms，将自适应表单整合在一起，创作单个大型自适应表单，并了解其功能。 '
uuid: e52e4f90-8821-49ec-89ff-fbf07db69bd2
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 264aa8c0-ba64-4768-b3d1-1b9baa6b4d72
docset: aem65
feature: 自适应表单
exl-id: 4254c2cb-66cc-4a46-b447-bc5e32def7a0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# 使用一组自适应表单创建自适应表单{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## 概述 {#overview}

在工作流（如开立银行帐户的应用程序）中，您的用户会填写多个表单。 您可以将表单堆叠在一起并构建一个大型表单（父表单），而不是要求他们填写一组表单。 向较大的表单添加自适应表单时，它将添加为面板（子表单）。 添加一组子表单以创建父表单。 您可以根据用户输入显示或隐藏面板。 父表单的按钮（如提交和重置）会覆盖子表单的按钮。 要在父表单中添加自适应表单，您可以从资产浏览器中拖放自适应表单（如自适应表单片段）。

可用功能包括：

* 独立创作
* 显示/隐藏适当的表单
* 延迟加载

与使用单个组件创建父表单相比，独立创作和延迟加载等功能可提供更佳的性能。

>[!NOTE]
>
>不能将基于XFA的自适应表单/片段用作子表单或父表单。

## 幕后{#behind-the-scenes}

您可以在父表单中添加基于XSD的自适应表单和片段。 父表单的结构与[任何自适应表单](../../forms/using/prepopulate-adaptive-form-fields.md)的结构相同。 将自适应表单添加为子表单时，它将作为面板添加到父表单中。 绑定子表单的数据存储在父表单XML架构`afBoundData`部分的`data`根下。

例如，您的客户会填写申请表。 表单的前两个字段是名称和标识。 其XML为：

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

您可以在应用程序中添加其他表格，以让客户填写其办公地址。 子表单的架构根为`officeAddress`。 应用`bindref` `/application/officeAddress`或`/officeAddress`。 如果未提供`bindref`，则将子表单添加为`officeAddress`子树。 请参阅下面表单的XML:

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

如果插入另一个允许客户提供住宅地址的表单，请应用`bindref` `/application/houseAddress or /houseAddress.` XML如下所示：

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

如果要保留与架构根（本示例中为`Address`）相同的子根名称，请使用已索引的bindrefs。

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

您可以使用`bindRef`属性更改自适应表单/片段的默认子树。 使用`bindRef`属性可指定指向XML架构树结构中某个位置的路径。

如果子表单未绑定，则其数据将存储在父表单XML架构的`afUnboundData`部分的`data`根下。

您可以多次将自适应表单添加为子表单。 确保正确修改了`bindRef`，以便自适应表单的每个使用实例都指向数据根目录下的不同子根目录。

>[!NOTE]
>
>如果不同的表单/片段映射到同一子根，则数据会被覆盖。

## 使用资产浏览器{#adding-an-adaptive-form-as-a-child-form-using-asset-browser}将自适应表单添加为子表单

执行以下步骤，使用资产浏览器将自适应表单添加为子表单。

1. 在编辑模式下打开父表单。
1. 在侧栏中，单击&#x200B;**Assets** ![assets-browser](assets/assets-browser.png)。 在“资产”下，从下拉菜单中选择&#x200B;**自适应表单**。
   [ ![在资产下选择自适应表单](assets/asset.png)](assets/asset-1.png)

1. 拖放要作为子表单添加的自适应表单。
   [ ![将自适应表单拖放到您的网站中。](assets/drag-drop.png)](assets/drag-drop-1.png)您拖放的自适应表单将添加为子表单。
