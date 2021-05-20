---
title: 指定XCI配置选项
seo-title: 指定XCI配置选项
description: 了解如何指定XCI配置选项。
seo-description: 了解如何指定XCI配置选项。
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---

# 指定XCI配置选项{#specifying-xci-configuration-options}

Forms允许您指定用于渲染的自定义XCI文件。 (请参阅[配置Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。) 默认情况下，Forms会覆盖XCI文件中指定的一些选项，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以为上面列出的选项选择取消覆盖的选项，在这种情况下，Forms将使用自定义XCI文件中指定的值。

1. 在管理控制台中，单击服务> Forms。
1. 选中或取消选中使用系统默认XCI选项复选框。 如果选择此选项，Forms会对数据包、创建者、制作者和compressObjectStream设置使用其默认值。 取消选择此选项后，Forms会使用自定义XCI文件中指定的值。
1. 单击保存。
