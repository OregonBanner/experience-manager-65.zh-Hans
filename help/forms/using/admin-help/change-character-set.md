---
title: 更改字符集
seo-title: 更改字符集
description: 您可以指定用于对输出流进行编码的字符集。 了解如何更改字符集。
seo-description: 您可以指定用于对输出流进行编码的字符集。 了解如何更改字符集。
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# 更改字符集{#change-the-character-set}

您可以指定用于对输出流进行编码的字符集。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务>输出]**。
1. 在“国际化”下的“字符集”列表中，选择一个字符集。 此设置取决于通过API指定的`TransformationFormat`和`PrintFormat`。 要指定所列字符集以外的字符集，请选择“自定义”，然后在显示的框中指定编码值。

   如果`TransformationFormat`是PDF，而PDF/A或`PrintFormat`是PCL、PostScript、Zebra标签、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，则仅支持特定字符集。

   字符集必须是有效的规范名称。 默认值为ISO-8859-1。

1. 单击&#x200B;**[!UICONTROL 保存]**。
