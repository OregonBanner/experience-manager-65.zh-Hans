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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 更改字符集 {#change-the-character-set}

您可以指定用于对输出流进行编码的字符集。

1. 在管理控制台中，单击“ **[!UICONTROL 服务”>“输出]**”。
1. 在“国际化”下的“字符集”列表中，选择一个字符集。 此设置取决于通过API `TransformationFormat` 指 `PrintFormat` 定的和。 要指定列出的字符集以外的字符集，请选择“自定义”，然后在显示的框中指定编码值。

   如果 `TransformationFormat``PrintFormat` 是PDF和PDF/A或是PCL、PostScript、Zebra标签、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，则仅支持特定字符集。

   字符集必须是有效的规范名称。 默认值为ISO-8859-1。

1. 单击&#x200B;**[!UICONTROL 保存]**。

