---
title: 翻译资产的最佳实践
description: 高效管理资产的最佳实践，以同步各种翻译版本并简化翻译工作流。
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 翻译资产的最佳实践 {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] 支持多语言工作流将数字资源的二进制文件、元数据和标记翻译成多个区域设置并管理已翻译的资源。 有关详细信息，请参阅 [多语言资产](multilingual-assets.md).

为了高效管理资产以确保不同的翻译版本保持同步，请创建 [语言副本](preparing-assets-for-translation.md) 之前的所有资产。

资产或资产组的语言副本是具有相似内容层次结构的语言同级（或相同语言的资产版本）。

每个语言副本都是一个独立的资产。 因此，将资产转换为多个区域设置可以显着增加CRX存储库的大小。 例如，将总大小为10 GB的资产翻译为两种语言可将存储库大小增加约20 GB（每种语言增加10 GB）。

与元数据和标记相比，资产二进制文件占用的存储空间要大得多。 因此，如果翻译元数据和标记仅符合您的目的，请忽略以翻译二进制文件。 您可以在资料档案库中保留二进制文件的原始副本，以便与翻译成不同区域设置的元数据和标记相关联。 维护二进制文件的单个副本而不是多个已翻译版本，可最大限度地减少对存储库大小的影响。

File Data Store和Amazon S3 Data Store提供了最适合这些情况的存储基础架构。 这些存储库存储着资产二进制文件（包括演绎版）的单一副本，这些副本可由元数据和标记在多个区域设置中共享。 因此，创建资源语言副本并翻译元数据和标记不会影响存储库大小。

您还可以对几个工作流和翻译集成框架进行一些配置更改，以进一步简化该过程。

1. 执行下列操作之一：

   * [设置文件数据存储](/help/sites-deploying/data-store-config.md)
   * [设置Amazon S3数据存储](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. 启用 [!UICONTROL 设置上次修改日期] 工作流。

   此 [!UICONTROL DAM元数据写回] 工作流配置资产的上次修改日期。 由于您在步骤2中禁用了此工作流， [!DNL Assets] 无法再使资源的上次修改日期保持最新。 因此，请启用 *设置上次修改日期* 此工作流用于确保资产的上次修改日期是最新的。 如果资源具有过时的上次修改日期，则可能会导致错误。

1. [配置翻译集成框架](/help/sites-administering/tc-tic.md) 以停止翻译资产二进制文件。 取消选择 **[!UICONTROL 翻译资产]** 下的选项 [!UICONTROL 资产] 制表符，以停止翻译资产二进制文件。
1. 翻译资源元数据/标记，使用 [多语言资源工作流](multilingual-assets.md).
