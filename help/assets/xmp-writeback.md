---
title: XMP 写回到演绎版
description: 了解XMP写回功能如何将资产的元数据更改传播到资产的所有或特定演绎版。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 15%

---


# XMP 写回到演绎版 {#xmp-writeback-to-renditions}

中的XMP写回功能 [!DNL Adobe Experience Manager Assets] 将资产元数据更改复制到资产的演绎版。 当您从资产内部或上传资产时， [!DNL Experience Manager Assets] 更改资产的元数据时，更改最初会存储在CRXDe的资产节点内。 XMP写回功能将元数据更改传播到资产的所有或特定演绎版。

请考虑将标题为的资 [!UICONTROL 产] “标题”属性修改 `Classic Leather` 为的情 `Nylon`况。

![元数据](assets/metadata.png)

在这种情况下， [!DNL Experience Manager Assets] 会在资产层次结构中 **[!UICONTROL 存储的资]**`dc:title` 产元数据的参数中保存对Title属性所做的更改。

![metadata_stored](assets/metadata_stored.png)

However, [!DNL Experience Manager Assets] does not automatically propagate any metadata changes to the renditions of an asset.

利用XMP写回功能，您可以将元数据更改传播到资产的所有演绎版或特定演绎版。 但是，这些更改不会存储在资产层次结构中的元数据节点下。此功能而是会将更改嵌入到演绎版的二进制文件中。

## 启用XMP写回 {#enabling-xmp-writeback}

要在上传元数据更改时将其传播到资产的演绎版，请在Configuration Manager中 **[!UICONTROL 修改Adobe CQ DAM Rendition]** Maker配置。

1. 要打开Configuration Manager，请访 `https://[aem_server]:[port]/system/console/configMgr`问。
1. 打开 **[!UICONTROL Adobe CQ DAM Rendition Maker配置]** 。
1. 选择**[!UICONTROL传播XMP[!UICONTROL **选项，然后保存更改。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 为特定再现启用XMP写回 {#enabling-xmp-writeback-for-specific-renditions}

要让XMP写回功能将元数据更改传播到选定的演绎版，请将这些演绎版指定到DAM元数据写回工作流的“XMP写 [!UICONTROL 回流程”工作流] 步骤。 默认情况下，此步骤配置为原始再现。

要使XMP写回功能将元数据传播到再现缩略图140.100.png和319.319.png，请执行这些步骤。

1. 在Experience Manager界面中，导航到工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流]** > **[!UICONTROL 模型]**。
1. 在“模型”页中，打开DAM元 **[!UICONTROL 数据写回工作流]** 模型。
1. 在“ **[!UICONTROL DAM元数据写回]** ”属性页中，打开“ **[!UICONTROL XMP写回进程”步骤]** 。
1. In the [!UICONTROL Step Properties] dialog box, click the **[!UICONTROL Process]** tab.
1. 在“参 **数** ”框中，添 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`加，然后单 **击确定**。

   ![step_properties](assets/step_properties.png)

1. 保存更改。
1. To regenerate the pyramid TIFF renditions for [!DNL Dynamic Media] images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the [!UICONTROL DAM Metadata Writeback] workflow.

   PTIFF 呈现仅在 Dynamic Media Hybrid 实施中本地创建和存储。

1. 保存工作流。

元数据更改将传播到资产的演绎版缩略图140.100.png和缩略图319.319.png，而不是其他演绎版。

>[!NOTE]
>
>有关64位Linux中的XMP写回问题，请 [参阅如何在64位RedHat Linux上启用XMP写回](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)。
>
>有关受支持平台的详细信息，请参 [阅XMP元数据回写的先决条件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)。

## 筛选XMP元数据 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 支持黑名单和白名单过滤XMP元数据的属性／节点，该元数据从资产二进制文件读取并在摄取资产时存储在JCR中。

黑名单过滤允许您导入除为排除指定的属性外的所有XMP元数据属性。 但是，对于具有大量XMP元数据（例如，1000个节点具有10,000个属性）的资产类型（如INDD文件），要筛选的节点名称并不总是预先知道的。 如果黑名单过滤允许导入大量具有大量XMP元数据的资产，则Experience Manager部署可能会遇到稳定性问题，例如阻塞的观察队列。

XMP元数据的白名单过滤功能允许您定义要导入的XMP属性，从而解决了此问题。 这样，将忽略其他／未知的XMP属性。 您可以将这些属性中的某些属性添加到黑名单筛选器，以实现向后兼容。

>[!NOTE]
>
>筛选仅适用于资产二进制文件中从XMP源派生的属性。 对于从非XMP源（如EXIF和IPTC格式）派生的属性，过滤不起作用。 例如，资产创建日期存储在以EXIF TIFF命名 `CreateDate` 的属性中。 Experience Manager将此值存储在名为的元数据字段中 `exif:DateTimeOriginal`。 由于源是非XMP源，因此过滤不适用于此属性。

1. 要打开Configuration Manager，请访 `https://[aem_server]:[port]/system/console/configMgr`问。
1. 打开 **[!UICONTROL Adobe CQ DAM XmpFilter配置]** 。
1. 要应用白名单过滤，请选择&#x200B;**[!UICONTROL 将白名单应用于 XMP 属性]**，然后在 **[!UICONTROL XMP 过滤的列入白名单的 XML 名称]**&#x200B;框中指定要导入的属性。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 要在应用白名单过滤后过滤掉列入黑名单的 XMP 属性，请在 **[!UICONTROL XMP 过滤的列入黑名单的 XML 名称]**&#x200B;框中指定。

   >[!NOTE]
   >
   >默认 **[!UICONTROL 情况下，将黑名单应用]** 到XMP属性选项处于选中状态。 换句话说，黑名单过滤默认为启用。 要禁用黑名单过滤，请取消选 **[!UICONTROL 择“将黑名单应用到XMP属性]** ”选项。

1. 保存更改。
