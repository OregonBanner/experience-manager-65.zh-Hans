---
title: 翻譯資產的最佳實務
description: 有效管理資產的最佳實務，以同步各種翻譯版本並簡化翻譯工作流程。
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 翻譯資產的最佳實務 {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] 支援多語言工作流程，將數位資產的二進位檔案、中繼資料和標籤翻譯成多個區域設定，並管理已翻譯的資產。 如需詳細資訊，請參閱 [多語言資產](multilingual-assets.md).

為了有效管理資產，以確保不同翻譯版本保持同步，請建立 [語言副本](preparing-assets-for-translation.md) 執行翻譯工作流程之前的所有資產。

資產或資產群組的語言副本是具有類似內容階層的語言同層級（或相同語言的資產版本）。

每個語言副本都是獨立的資產。 因此，將資產轉換為多個地區設定可大幅增加CRX存放庫的大小。 例如，將合併大小為10 GB的資產翻譯為兩種語言可將存放庫大小增加約20 GB （每種語言增加10 GB）。

和中繼資料和標籤相比，資產二進位檔佔用的儲存空間大得多。 因此，如果轉譯中繼資料和標籤只符合您的用途，請省略轉譯二進位檔案。 您可以將二進位檔的原始復本保留在儲存區域中，以便與翻譯成不同地區設定的中繼資料和標籤相關聯。 維護二進位檔的單一復本，而不是多個翻譯版本，可將對存放庫大小的影響降至最低。

File Data Store和Amazon S3 Data Store提供最適合這些情況的儲存基礎架構。 這些存放庫會儲存單一的資產二進位檔復本（包括轉譯），可供多個地區設定的中繼資料和標籤共用。 因此，建立資產語言副本並翻譯中繼資料和標籤不會影響存放庫大小。

您也可以對幾個工作流程和翻譯整合框架進行一些設定變更，以進一步簡化程式。

1. 执行下列操作之一：

   * [設定檔案資料存放區](/help/sites-deploying/data-store-config.md)
   * [設定Amazon S3資料存放區](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. 啟用 [!UICONTROL 設定上次修改日期] 工作流程。

   此 [!UICONTROL DAM中繼資料回寫] 工作流程會設定資產的上次修改日期。 由於您已在步驟2中停用此工作流程， [!DNL Assets] 無法再將資產的上次修改日期保持在最新狀態。 因此，啟用 *設定上次修改日期* 工作流程，確保資產的上次修改日期為最新。 如果資產具有過時的上次修改日期，可能會導致錯誤。

1. [設定翻譯整合框架](/help/sites-administering/tc-tic.md) 以停止翻譯資產二進位檔。 取消選取 **[!UICONTROL 翻譯資產]** 下的選項 [!UICONTROL 資產] 索引標籤以停止翻譯資產二進位檔。
1. 翻譯資產中繼資料/標籤，使用 [多語言資產工作流程](multilingual-assets.md).
