---
title: 如何编辑或添加元数据
description: 了解AEM资产中的资产元数据以及编辑资产元数据的各种方式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91818198032de0580fe04d09fdd567dc470c021d

---


# 如何编辑或添加元数据 {#how-to-edit-or-add-metadata}

元数据是有关可搜索资产的其他信息。 上传图像时，会自动提取该图像。 您可以编辑现有元数据或向现有字段添加新的元数据属性（例如，当元数据字段为空时）。

由于公司需要可控且可靠的元数据词汇表，因此AEM资产不允许临时添加新的元数据属性。 尽管作者无法为资产添加新的元数据字段，但开发人员可以。 请参 [阅为资产创建新的元数据属性](meta-edit.md#editing-metadata-schema)。

## 编辑资产的元数据 {#editing-metadata-for-an-asset}

要编辑元数据，请执行以下操作：

1. 执行下列操作之一：

   * 在资产UI中，选择资产，然后单击／点按工具栏中 **[!UICONTROL 的查看属]** 性图标。
   * 从资产缩略图中，选择查 **[!UICONTROL 看属性]** 快速操作。
   * 在资产页面中，单击／点按工具 **[!UICONTROL 栏中的查看]** 属性图标。
      ![chlimage_1-168](assets/chlimage_1-168.png)
      *图：属性图标*
   资产页面会显示资产的所有元数据。 此元数据在上传（摄取）到AEM资产时会自动提取。

   ![选择资产属性以查看元数据](assets/asset-metadata.png)


   *图：在资产属性页面上编辑或添加元数据*

1. 根据需要，在各个选项卡下对元数据进行编辑，完成后，单击／点按工具栏中的 **[!UICONTROL 保存]** ，以保存更改。 单击／点 **[!UICONTROL 按关闭]** ，以返回到资产Web界面。

   >[!NOTE]
   >
   >如果文本字段为空，则没有现有的元数据集。 您可以在字段中输入值并保存它以添加该元数据属性。

对资产元数据所做的任何更改都会作为XMP数据的一部分写回原始二进制文件。 这是通过AEM元数据回写工作流完成的。 对现有属性(如 `dc:title`)所做的更改会被覆盖，新创建的属性(包括自定义属性 `cq:tags`等)会与架构一起添加。

支持并支持XMP写回功能，支持技术要求中描述的平台和文 [件格式。](/help/sites-deploying/technical-requirements.md)

## 编辑元数据架构 {#editing-metadata-schema}

有关如何编辑元数据架构的详细信息，请参阅编 [辑元数据架构表单](metadata-schemas.md#edit-metadata-schema-forms)。

## 在AEM中注册自定义命名空间 {#registering-a-custom-namespace-within-aem}

您可以在AEM中添加您自己的命名空间。 正如存在预定义的命名空间（如cq、jcr和sling）一样，您也可以为存储库元数据和xml处理提供一个命名空间。

1. 转到节点类型管理页 `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`。
1. 单击或点 **[!UICONTROL 按页面顶部]** 的命名空间。 命名空间管理页面显示在窗口中。

1. 要添加命名空间，请单击或点 **[!UICONTROL 按底部]** 的“新建”。
1. 在XML命名空间约定中指定自定义命名空间（以URI形式指定id，并为id指定关联的前缀），然后单击或点按保 **[!UICONTROL 存]**。
