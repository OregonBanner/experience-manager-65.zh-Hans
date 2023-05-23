---
title: 變更字元集
seo-title: Change the character set
description: 您可以指定用來編碼輸出資料流的字元集。 瞭解如何變更字元集。
seo-description: You can specify the character set used to encode the output stream. Learn how you can change the character set.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 變更字元集 {#change-the-character-set}

您可以指定用來編碼輸出資料流的字元集。

1. 在管理控制檯中，按一下 **[!UICONTROL 服務>輸出]**.
1. 在「國際化」下的「字元集」清單中，選取字元集。 此設定取決於 `TransformationFormat` 和 `PrintFormat` 透過API指定。 若要指定所列字元集以外的字元集，請選取「自訂」，然後在顯示的方塊中指定編碼值。

   若 `TransformationFormat` 是PDF和PDF/A或 `PrintFormat` 是PCL、PostScript、Zebra標籤、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，僅支援特定字元集。

   字元集必須是有效的正式名稱。 預設值為ISO-8859-1。

1. 单击“**[!UICONTROL 保存]**”。
