---
title: 設定遞補字型
seo-title: Configuring fallback fonts
description: 瞭解如何設定後援字型。
seo-description: Learn how to configure fallback fonts.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# 設定遞補字型 {#configuring-fallback-fonts}

您可以手動設定FontManagerResources.properties檔案，將預設AEM Forms字型對應到備援（或替代），如果預設字型在伺服器上無法使用。 此屬性檔案位於adobe-fontmanager.jar檔案中。

>[!NOTE]
>
>後援字型設定也適用於組合器服務。

1. 導覽至adobe-livecycle-*`[appserver]`*&#x200B;中的.ear檔案 *`[aem-forms root]`*/configurationManager/export目錄，製作備份復本，然後取消封裝原始檔案。
1. 找到adobe-fontmanager.jar檔案並將其取消封裝。
1. 找到FontManagerResources.properties檔案，然後在文字編輯器中開啟它。
1. 視需要修改「類屬」和「後援」字型位置和名稱，並儲存檔案。

   FontManagerResources.properties檔案中的字型專案是相對於 *`[aem-forms root]`*/fonts目錄。 如果您指定的字型不是預設的AEM表單字型，則必須將這些字型安裝在此目錄結構內（在現有目錄內或新建立的目錄中）。

   >[!NOTE]
   >
   >如果指定的字型或預設字型未包含特定的Unicode字元，或者無法使用，則會根據下列優先順序從備援字型中取得該字元：

   * 地區設定的特定字型
   * ROOT字型（如果區域設定未設定）
   * 一般字型，依遞補表格中設定的順序搜尋

1. 重新封裝adobe-fontmanager.jar檔案。
1. 重新封裝adobe-livecycle-*`[appserver]`*.ear檔案，然後手動或執行Configuration Manager來重新部署。

>[!NOTE]
>
>請勿使用Configuration Manager重新封裝adobe-livecycle-`[appserver]`.ear檔案，因為它會以AEM表單預設值覆寫您的修改。
