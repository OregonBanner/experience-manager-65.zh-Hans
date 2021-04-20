---
title: 翻译资产的最佳实践
description: 有效管理资产的最佳实践，可同步各种翻译版本并简化翻译工作流。
contentOwner: AG
role: Administrator
feature: Asset Management
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---


# 翻译资产的最佳实践{#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] 支持多语言工作流，将数字资产的二进制文件、元数据和标记翻译为多个区域设置并管理已翻译的资产。有关详细信息，请参阅[多语言资产](multilingual-assets.md)。

为了有效管理资产以确保不同的翻译版本保持同步，请在运行翻译工作流之前创建资产的[语言副本](preparing-assets-for-translation.md)。

资产或资产组的语言副本是具有类似内容层次结构的语言同级（或同一语言中资产的版本）。

每个语言副本都是独立的资产。 因此，将资源翻译为多个区域设置会大大增加CRX存储库的大小。 例如，将总大小为10 GB的资产翻译为两种语言可以将存储库大小增加约20 GB（每种语言为10 GB）。

与元数据和标记相比，资源二进制文件占用的存储空间要大得多。 因此，如果翻译元数据和标记只有您的用途，请省略翻译二进制文件。 您可以在存储库中保留二进制文件的原始副本，以便与翻译为不同区域设置的元数据和标记关联。 维护一个二进制文件副本，而不是多个转换版本，可最大限度地减少对存储库大小的影响。

文件存储存储和Amazon S3数据存储提供最适合这些场景的文件基础架构。 这些存储存储库存储资产二进制文件（包括演绎版）的单个副本，这些二进制文件可由元数据和标记在多个区域设置中共享。 因此，创建资产语言副本以及翻译元数据和标记不会影响存储库大小。

您还可以对两个工作流和翻译集成框架进行一些配置更改，以进一步简化该过程。

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

1. 启用[!UICONTROL 设置上次修改日期]工作流。

   [!UICONTROL DAM MetaData Writeback]工作流配置资产的上次修改日期。 由于您在步骤2中禁用了此工作流，[!DNL Assets]无法再让资产的上次修改日期保持最新。 因此，请启用&#x200B;*设置上次修改日期*&#x200B;工作流，以确保资产的上次修改日期为最新状态。 具有过期的上次修改日期的资产可能会导致错误。

1. [配置翻译集成框](/help/sites-administering/tc-tic.md) 架以停止翻译资产二进制文件。取消选择[!UICONTROL 资产]选项卡下的&#x200B;**[!UICONTROL 转换资产]**&#x200B;选项，以停止资产二进制文件的转换。
1. 使用[多语言资产工作流](multilingual-assets.md)翻译资产元数据/标记。
