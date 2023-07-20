---
title: 指定XCI配置
description: 了解如何指定XCI配置选项
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# 指定XCI配置 {#specify-xci-configuration-options}

输出允许您指定用于渲染的自定义XCI文件。 参见 [指定输出的文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

默认情况下，“输出”会覆盖XCI文件中指定的某些选项，其中包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以选择取消上述选项覆盖的选项，在这种情况下，输出将使用自定义XCI文件中指定的值。

1. 在管理控制台中，单击 **服务** >输出。
1. 选中或取消选中“使用系统默认XCI选项”复选框。 选中此选项后， Output将对数据包、 creator 、 producer和compressObjectStream设置使用其默认值。 取消选中此选项时，输出使用自定义XCI文件中指定的值。
1. 单击“**保存**”。
