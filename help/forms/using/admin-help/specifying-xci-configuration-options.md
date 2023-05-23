---
title: 指定XCI組態選項
seo-title: Specifying XCI configuration options
description: 瞭解如何指定XCI設定選項。
seo-description: Learn how to specify XCI configuration options.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 指定XCI組態選項 {#specifying-xci-configuration-options}

Forms可讓您指定自訂XCI檔案，以便用於呈現。 (請參閱 [設定Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) 依預設，Forms會覆寫XCI檔案中指定的某些選項，包括下列專案：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以選取取消上述選項覆寫的選項，在此情況下，Forms將使用自訂XCI檔案中指定的值。

1. 在Administration Console中，按一下「服務> Forms」。
1. 選取或取消選取「使用系統預設XCI選項」核取方塊。 選取此選項時，Forms會使用封包、建立者、製作者和compressObjectStream設定的預設值。 取消選取此選項時，Forms會使用自訂XCI檔案中指定的值。
1. 单击“保存”。
