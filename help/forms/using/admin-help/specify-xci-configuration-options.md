---
title: 指定XCI設定選項
seo-title: Specify XCI configuration options
description: 瞭解如何指定XCI設定選項。
seo-description: Learn how to specify XCI configuration options.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 1%

---

# 指定XCI設定選項 {#specify-xci-configuration-options}

輸出可讓您指定用於呈現的自訂XCI檔案。 (請參閱 [指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).) 依預設，「輸出」會覆寫XCI檔案中指定的某些選項，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以選取取消上述選項覆寫的選項，在這種情況下「輸出」會使用自訂XCI檔案中指定的值。

1. 在Administration Console中，按一下「服務>輸出」。
1. 選取或取消選取「使用系統預設XCI選項」核取方塊。 選取此選項時，Output會使用封包、建立者、製作者和compressObjectStream設定的預設值。 取消選取此選項時，輸出會使用自訂XCI檔案中指定的值。
1. 单击“保存”。
