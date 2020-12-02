---
title: 翻译资产的最佳实践
description: 有效管理资产的最佳实践，可同步各种翻译版本并简化翻译工作流。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---


# 翻译资产的最佳实践{#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] 支持多语言工作流将数字资产的二进制文件、元数据和标记翻译为多个语言环境并管理已翻译的资产。有关详细信息，请参阅[多语言资产](multilingual-assets.md)。

为了有效管理资产以确保不同的翻译版本保持同步，请在运行翻译工作流之前创建资产的[语言副本](preparing-assets-for-translation.md)。

资产或资产组的语言副本是具有相似内容层次结构的语言同级（或同一语言中资产的版本）。

每个语言副本都是独立资产。 因此，将资源翻译为多个区域设置可大幅增加CRX存储库的大小。 例如，将总大小为10 GB的资产翻译为两种语言可将存储库大小增加约20 GB（每种语言为10 GB）。

与元数据和标记相比，资源二进制文件占用的存储空间要大得多。 因此，如果转换元数据和标记只能满足您的目的，请忽略转换二进制文件。 您可以在存储库中保留二进制文件的原始副本，以便与翻译为不同区域设置的元数据和标记关联。 维护一个二进制副本（而不是多个译文版本）可最大限度地减少对存储库大小的影响。

文件数据存储和AmazonS3数据存储提供最适合这些情形的存储基础结构。 这些存储存储库存储资产二进制文件（包括演绎版）的单一副本，这些二进制文件可以在多个区域设置中由元数据和标记共享。 因此，创建资产语言副本以及翻译元数据和标记不会影响存储库大小。

您还可以对两个工作流和翻译集成框架进行一些配置更改以进一步简化该过程。

1. 执行下列操作之一：

   * [设置文件数据存储](/help/sites-deploying/data-store-config.md)
   * [设置AmazonS3数据存储](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. 启用[!UICONTROL 设置上次修改日期]工作流。

   [!UICONTROL DAM MetaData Writeback]工作流配置资产的上次修改日期。 由于您在步骤2中禁用了此工作流，[!DNL Assets]无法再让资产的上次修改日期保持最新。 因此，请启用&#x200B;*设置上次修改日期*&#x200B;工作流，以确保资产的上次修改日期是最新的。 具有过期的上次修改日期的资产可能会导致错误。

1. [配置转换集成框架](/help/sites-administering/tc-tic.md) 以停止转换资产二进制文件。取消选择[!UICONTROL 资产]选项卡下的&#x200B;**[!UICONTROL 转换资产]**&#x200B;选项，以停止转换资产二进制文件。
1. 使用[多语言资产工作流](multilingual-assets.md)转换资产元数据／标记。
