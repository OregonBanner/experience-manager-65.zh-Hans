---
title: 如何编辑或添加元数据
description: 了解通过各种方 [!DNL Adobe Experience Manager Assets] 式编辑资产元数据的资产元数据。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 99ce6e0572797b7bccf755aede93623be6bd5698
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---


# 如何编辑或添加元数据 {#how-to-edit-or-add-metadata}

元数据是有关可搜索资产的其他信息。 上传图像时会自动提取图像。 您可以编辑现有元数据或向现有字段添加新的元数据属性（例如，当元数据字段为空时）。

由于组织需要可控、可靠的元数 [!DNL Experience Manager Assets] 据词汇，因此不允许临时添加新的元数据属性。 尽管作者无法为资产添加新的元数据字段，但开发人员可以。 请参 [阅为资产创建新的元数据属性](meta-edit.md#editing-metadata-schema)。

## 编辑资产的元数据 {#editing-metadata-for-an-asset}

要编辑元数据，请执行以下操作：

1. 执行下列操作之一：

   * 从界面 [!DNL Assets] 中，选择资产，然后单击工 **[!UICONTROL 具栏中的]** 视图“属性”。
   * 从资产缩略图中，选择 **[!UICONTROL 视图属性]** 快速操作。
   * 在资产页面中，单 **[!UICONTROL 击工具栏]**![中的视图](assets/chlimage_1-168.png) 属性chlimage_1-168。
   资产页面会显示资产的所有元数据。 将资产上传（摄取）到时，会提取元数据 [!DNL Experience Manager]。

   ![选择资产属性以视图元数据](assets/asset-metadata.png)

   *图： 在资产属性页面上编辑或添[!UICONTROL 加元]数据。*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the Assets web interface.

   >[!NOTE]
   >
   >如果文本字段为空，则没有现有元数据集。 您可以在字段中输入一个值并保存它以添加该元数据属性。

对资产元数据所做的任何更改都会作为其XMP数据的一部分写回原始二进制文件。 这是通过元数 [!DNL Experience Manager] 据回写工作流完成的。 对现有属性（如）所做的更 `dc:title`改会被覆盖，新创建的属性(包括自定义属 `cq:tags`性等)会与模式一起添加。

支持XMP写回，并支持技术要求中描述的平台和文 [件格式。](/help/sites-deploying/technical-requirements.md)

## 编辑元数据模式 {#editing-metadata-schema}

有关详细信息，请参 [阅编辑元数据模式表单](metadata-schemas.md#edit-metadata-schema-forms)。

## 在 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

您可以在中添加您自己的命名空间 [!DNL Experience Manager]。 正如存在预定义的命名空间 `cq`, `jcr`如、 `sling`和，您可以为存储库元数据和XML处理创建命名空间。

1. 转到节点类型管理页 `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`面。
1. 单 **[!UICONTROL 击页]** 面顶部的命名空间。 命名空间管理页面显示在窗口中。

1. 要添加命名空间，请单 **[!UICONTROL 击]** 底部的“新建”。
1. 在XML命名空间约定中指定自定义命名空间。 以URI的形式指定ID，并为ID指定关联前缀。 单击&#x200B;**[!UICONTROL 保存]**。
