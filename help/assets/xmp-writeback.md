---
title: XMP写回到演绎版
description: 了解XMP写回功能如何将资源的元数据更改传播到资源的所有或特定演绎版。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# XMP写回到演绎版 {#xmp-writeback-to-renditions}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | 本文 |

中的此XMP写回功能 [!DNL Adobe Experience Manager Assets] 将元数据更改复制到原始资源的演绎版。 当您从Assets中更改资源的元数据或上传资源时，所做的更改最初存储在资源层次结构中的元数据节点中。

XMP写回功能允许您将元数据更改传播到资源的所有或特定演绎版。 该功能仅回写那些使用的元数据属性 `jcr` namespace，即名为的属性 `dc:title` 写回，但有一个名为 `mytitle` 不是。

考虑一个方案，在其中修改了 [!UICONTROL 标题] 标题为的资产属性 `Classic Leather` 到 `Nylon`.

![元数据](assets/metadata.png)

在本例中， [!DNL Experience Manager Assets] 将更改保存到 **[!UICONTROL 标题]** 中的属性 `dc:title` 资源层次结构中存储的资源元数据的参数。

![metadata_stored](assets/metadata_stored.png)

但是， [!DNL Experience Manager Assets] 不会自动将任何元数据更改传播到资源的演绎版。 参见 [如何启用XMP写回](#enable-xmp-writeback).

## 启用XMP写回 {#enable-xmp-writeback}

要允许元数据更改在上传资产时传播到资产的演绎版，请修改 **[!UICONTROL Adobe CQ DAM演绎版生成器]** 配置。

1. 要打开配置管理器，请访问 `https://[aem_server]:[port]/system/console/configMgr`.
1. 打开 **[!UICONTROL Adobe CQ DAM演绎版生成器]** 配置。
1. 选择 **[!UICONTROL 传播XMP]** 选项，然后保存更改。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 为特定呈现版本启用XMP写回 {#enabling-xmp-writeback-for-specific-renditions}

要让XMP写回功能将元数据更改传播到所选格式副本，请在XMP写回进程工作流步骤中指定这些格式副本 [!UICONTROL DAM元数据回写] 工作流。 默认情况下，此步骤使用原始演绎版进行配置。

对于XMP写回功能要将元数据传播到演绎版缩略图140.100.png和319.319.png，请执行以下步骤。

1. 在Experience Manager界面中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 在“模型”页面中，打开 **[!UICONTROL DAM元数据写回]** 工作流模型。
1. 在“ **[!UICONTROL DAM元数据写回]** ”属性页中，打开“ **[!UICONTROL XMP写回进程”步骤]** 。
1. 在 [!UICONTROL 步骤属性] 对话框中，单击 **[!UICONTROL 进程]** 选项卡。
1. 在 **参数** 框，添加 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然后单击 **[!UICONTROL 确定]**.

   ![step_properties](assets/step_properties.png)

1. 保存更改。
1. 要重新生成金字塔TIFF演绎版，请执行以下操作 [!DNL Dynamic Media] 具有新属性的图像，添加 **[!UICONTROL Dynamic Media流程图像资源]** 步骤至 [!UICONTROL DAM元数据写回] 工作流。

   PTIFF 呈现仅在 Dynamic Media Hybrid 实施中本地创建和存储。

1. 保存工作流。

元数据更改将传播到资源的演绎版thumbnail.140.100.png和thumbnail.319.319.png ，而不是其他演绎版。

>[!NOTE]
>
>有关64位Linux中的XMP写回问题，请参见 [如何在64位RedHat Linux上启用XMP回写](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>有关支持的平台，请参阅 [XMP元数据回写先决条件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## 筛选XMP元数据 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 支持对从资源二进制文件读取并在引入资源时存储在JCR中的XMP元数据的属性/节点进行阻止列表和允许列表筛选。

使用阻止列表过滤允许您导入所有XMP元数据属性，但为排除项指定的属性除外。 但是，对于具有大量XMP元数据的资源类型（例如，具有10,000个属性的1000个节点），要过滤的节点的名称并不总是事先知道的。 如果使用阻止列表进行筛选，则可以导入大量包含许多XMP元数据的资源， [!DNL Experience Manager] 部署可能会遇到稳定性问题，例如观察队列阻塞。

通过允许列表筛选XMP元数据通过允许您定义要导入的XMP属性来解决此问题。 这样，任何其他或未知的XMP属性都将被忽略。 为了保持向后兼容性，您可以将其中某些属性添加到使用阻止列表的过滤器中。

>[!NOTE]
>
>筛选仅适用于从资产二进制文件中的XMP源派生的属性。 对于从非XMP源（如EXIF和IPTC格式）派生的属性，筛选不起作用。 例如，资产创建日期存储在名为的属性中 `CreateDate` 在EXIFTIFF中。 Experience Manager将此值存储在名为的元数据字段中 `exif:DateTimeOriginal`. 由于源是非XMP源，因此无法筛选此属性。

1. 要打开配置管理器，请访问 `https://[aem_server]:[port]/system/console/configMgr`.
1. 打开 **[!UICONTROL Adobe CQ DAM XmpFilter]** 配置。
1. 要通过允许列表应用筛选，请选择 **[!UICONTROL 将允许列表应用于XMP属性]**，并指定要在中导入的属性 **[!UICONTROL 允许用于XMP筛选的XML名称]** 盒子。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 要在通过允许列表应用筛选后筛选掉阻止的XMP属性，请在 **[!UICONTROL XMP筛选的已阻止XML名称]** 盒子。

   >[!NOTE]
   >
   >此 **[!UICONTROL 将阻止列表应用于XMP属性]** 选项默认处于选中状态。 换言之，默认情况下启用使用阻止列表进行筛选。 要禁用此类筛选，请取消选择 **[!UICONTROL 将阻止列表应用于XMP属性]** 选项。

1. 保存更改。
