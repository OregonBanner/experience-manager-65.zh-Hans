---
title: XMP 写回到演绎版
description: 了解XMP写回功能如何将资产的元数据更改传播到资产的所有演绎版或特定演绎版。
contentOwner: AG
role: Business Practitioner, Administrator
feature: Metadata
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 5%

---


# XMP 写回到演绎版 {#xmp-writeback-to-renditions}

[!DNL Adobe Experience Manager Assets]中的此XMP写回功能会将元数据更改复制到原始资产的演绎版。 当您从资产中更改资产的元数据时，或在上传资产时，更改最初存储在资产层次结构的元数据节点中。

XMP写回功能允许您将元数据更改传播到资产的所有演绎版或特定演绎版。 该功能仅回写那些使用`jcr`命名空间的元数据属性，即，将回写名为`dc:title`的属性，但不写名为`mytitle`的属性。

考虑将标题为`Classic Leather`的资产的[!UICONTROL Title]属性修改为`Nylon`的方案。

![元数据](assets/metadata.png)

在这种情况下，[!DNL Experience Manager Assets]将对资产层次结构中存储的资产元数据的`dc:title`参数中的&#x200B;**[!UICONTROL Title]**&#x200B;属性进行更改。

![metadata_stored](assets/metadata_stored.png)

但是，[!DNL Experience Manager Assets]不会自动将任何元数据更改传播到资产的演绎版。 请参阅[如何启用XMP写回](#enable-xmp-writeback)。

## 启用XMP写回{#enable-xmp-writeback}

要在上传资产时启用元数据更改将传播到资产的演绎版，请在Configuration Manager中修改&#x200B;**[!UICONTROL Adobe CQ DAM Rendition Maker]**&#x200B;配置。

1. 要打开Configuration Manager，请访问`https://[aem_server]:[port]/system/console/configMgr`。
1. 打开&#x200B;**[!UICONTROL Adobe CQ DAM Rendition Maker]**&#x200B;配置。
1. 选择&#x200B;**[!UICONTROL 传播XMP]**&#x200B;选项，然后保存更改。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 为特定再现{#enabling-xmp-writeback-for-specific-renditions}启用XMP写回

要让XMP写回功能将元数据更改传播到选定的演绎版，请将这些演绎版指定到[!UICONTROL DAM元数据写回]工作流的XMP写回流程工作流步骤。 默认情况下，此步骤配置为原始再现。

要使XMP写回功能将元数据传播到演绎版缩略图140.100.png和319.319.png，请执行这些步骤。

1. 在Experience Manager界面中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在“模型”页中，打开&#x200B;**[!UICONTROL DAM元数据写回]**&#x200B;工作流模型。
1. 在“ **[!UICONTROL DAM元数据写回]** ”属性页中，打开“ **[!UICONTROL XMP写回进程”步骤]** 。
1. 在[!UICONTROL 步骤属性]对话框中，单击&#x200B;**[!UICONTROL 进程]**&#x200B;选项卡。
1. 在&#x200B;**参数**&#x200B;框中，添加`rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然后单击&#x200B;**[!UICONTROL 确定]**。

   ![step_properties](assets/step_properties.png)

1. 保存更改。
1. 要使用新属性为[!DNL Dynamic Media]图像重新生成金字塔TIFF演绎版，请将&#x200B;**[!UICONTROL Dynamic Media处理图像资产]**&#x200B;步骤添加到[!UICONTROL DAM元数据写回]工作流。

   PTIFF 呈现仅在 Dynamic Media Hybrid 实施中本地创建和存储。

1. 保存工作流。

元数据更改将传播到资产的演绎版缩略图140.100.png和缩略图319.319.png，而不是其他演绎版。

>[!NOTE]
>
>有关64位Linux中的XMP写回问题，请参阅[如何在64位RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)上启用XMP写回。
>
>有关支持的平台，请参阅[XMP元数据回写先决条件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)。

## 筛选XMP元数据{#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 支持对从资源二进制文件读取并在摄取资源时存储在JCR中的XMP元数据的属性/节点进行阻止列表和允许列表过滤。

使用阻止列表进行筛选可导入除为排除指定的属性外的所有XMP元数据属性。 但是，对于具有大量XMP元数据的资产类型（例如1000个节点，其属性为10,000个），要筛选的节点名称并不总是提前知道的。 如果使用阻止列表进行筛选可导入包含大量XMP元数据的大量资产，则[!DNL Experience Manager]部署可能会遇到稳定性问题，例如观察队列阻塞。

通过允许列表筛选XMP元数据可通过允许您定义要导入的XMP属性来解决此问题。 这样，将忽略任何其他或未知的XMP属性。 为了向后兼容性，您可以向使用阻止列表的过滤器添加其中一些属性。

>[!NOTE]
>
>筛选仅适用于资产二进制文件中从XMP源派生的属性。 对于从非XMP源（如EXIF和IPTC格式）派生的属性，过滤不起作用。 例如，资产创建日期存储在EXIF TIFF中名为`CreateDate`的属性中。 Experience Manager将此值存储在名为`exif:DateTimeOriginal`的元数据字段中。 由于源是非XMP源，因此过滤不适用于此属性。

1. 要打开Configuration Manager，请访问`https://[aem_server]:[port]/system/console/configMgr`。
1. 打开&#x200B;**[!UICONTROL Adobe CQ DAM XmpFilter]**&#x200B;配置。
1. 要通过允许列表应用过滤，请选择&#x200B;**[!UICONTROL 应允许列表用到XMP属性]**，然后在XMP过滤&#x200B;]**的**[!UICONTROL &#x200B;允许的XML名称框中指定要导入的属性。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 要在通过允许列表应用过滤后过滤出已阻止的XMP属性，请在“用于XMP过滤的已阻止的XML名称”**[!UICONTROL 框中指定这些属性。]**

   >[!NOTE]
   >
   >默认情况下，将选阻止列表择&#x200B;**[!UICONTROL 应用到XMP属性]**&#x200B;选项。 换句话说，默认情况下启用使用阻止列表的过滤。 要禁用此类过滤，请取消选择&#x200B;**[!UICONTROL 应阻止列表用到XMP属性]**&#x200B;选项。

1. 保存更改。
