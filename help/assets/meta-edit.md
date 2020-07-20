---
title: 如何编辑或添加元数据
description: 了解通过各种方 [!DNL Adobe Experience Manager Assets] 式编辑资产元数据的资产元数据。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 4748eed3ce484e8446b641ccbc7b5d76cb66f428
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---


# 如何编辑或添加元数据 {#how-to-edit-or-add-metadata}

元数据是有关可搜索资产的其他信息。 上传图像时会自动提取图像。 您可以编辑现有元数据或向现有字段添加新的元数据属性，例如，当元数据字段为空时。

组织需要可控、可靠的元数据词汇。 因 [!DNL Experience Manager Assets] 此不允许按需添加新元数据属性。 开发人员（而非作者）可以为资产添加新的元数据字段。 请参 [阅为资产创建元数据属性](meta-edit.md#editing-metadata-schema)。

## 编辑资产的元数据 {#editing-metadata-for-an-asset}

要编辑元数据，请执行以下步骤：

1. 执行下列操作之一：

   * 从界面 [!DNL Assets] 中，选择资产，然后单击工 **[!UICONTROL 具栏中的]** 视图“属性”。
   * 从资产缩略图中，选择 **[!UICONTROL 视图属性]** 快速操作。
   * 在资产页面中，单击工 **[!UICONTROL 具栏中]**![的视图](assets/do-not-localize/info-circle-icon.png) 属性资产信息图标。

   资产页面会显示资产的所有元数据。 将资产上传（摄取）到时，会提取元数据 [!DNL Experience Manager]。

   ![选择资产的属性以视图其元数据](assets/asset-metadata.png)

   *图： 在资产属性页面上编辑或添[!UICONTROL 加元]数据。*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >如果文本字段为空，则没有现有元数据集。 您可以在字段中输入一个值并保存它以添加该元数据属性。

对资产元数据所做的任何更改都会作为其XMP数据的一部分写回原始二进制文件。 元数据回写工作流会将元数据添加到原始二进制文件中。 对现有属性（如）所做的更 `dc:title`改将被覆盖，新属性(包括自定义属 `cq:tags`性，如)将随模式添加。

支持XMP写回，并支持技术要求中描述的平台和文 [件格式。](/help/sites-deploying/technical-requirements.md)

## 编辑元数据模式 {#editing-metadata-schema}

有关详细信息，请参 [阅编辑元数据模式表单](metadata-schemas.md#edit-metadata-schema-forms)。

## 在 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

您可以在中添加您自己的命名空间 [!DNL Experience Manager]。 正如存在预定义的命名空间 `cq`, `jcr`如、 `sling`和，您可以为存储库元数据和XML处理创建命名空间。

1. 访问节点类型管理页 `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`面。
1. 要访问命名空间管理页面，请 **[!UICONTROL 单击]** 页面顶部的命名空间。
1. 要添加命名空间, **[!UICONTROL 请单]** 击页面底部的“新建”。
1. 在XML命名空间约定中指定自定义命名空间。 以URI的形式指定ID，并为ID指定关联前缀。 单击&#x200B;**[!UICONTROL 保存]**。

>[!MORELIKETHIS]
>
>* [关于元数据及其在资产中的需求](metadata.md)
>* [XMP 元数据](xmp.md)
>* [元数据架构参考](meta-ref.md)

