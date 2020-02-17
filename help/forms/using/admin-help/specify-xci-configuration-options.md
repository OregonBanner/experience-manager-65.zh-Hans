---
title: 指定XCI配置选项
seo-title: 指定XCI配置选项
description: 了解如何指定XCI配置选项。
seo-description: 了解如何指定XCI配置选项。
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 指定XCI配置选项 {#specify-xci-configuration-options}

输出允许您指定用于渲染的自定义XCI文件。 (请参 [阅为输出指定文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。)默认情况下，“输出”将覆盖XCI文件中指定的一些选项，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以选择取消上述选项覆盖的选项，在这种情况下，“输出”将使用自定义XCI文件中指定的值。

1. 在管理控制台中，单击“服务”>“输出”。
1. 选中或取消选中“使用系统默认XCI选项”复选框。 选择此选项后，“输出”将使用其默认值设置包、创建者、producer和compressObjectStream。 取消选择此选项后，“输出”将使用自定义XCI文件中指定的值。
1. 单击保存。

