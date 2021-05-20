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
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 1%

---

# 指定XCI配置选项{#specify-xci-configuration-options}

输出允许您指定用于渲染的自定义XCI文件。 （请参阅[为输出指定文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。） 默认情况下，输出会覆盖XCI文件中指定的一些选项，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以为上面列出的选项选择取消覆盖的选项，在这种情况下，“输出”使用自定义XCI文件中指定的值。

1. 在管理控制台中，单击服务>输出。
1. 选中或取消选中使用系统默认XCI选项复选框。 如果选择此选项，“输出”将使用其数据包、创建者、制作者和compressObjectStream设置的默认值。 取消选择此选项后，“输出”将使用自定义XCI文件中指定的值。
1. 单击保存。
