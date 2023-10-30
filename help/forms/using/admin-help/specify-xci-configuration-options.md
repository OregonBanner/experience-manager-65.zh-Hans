---
title: 指定XCI配置选项
description: 了解如何指定XCI配置选项 您可以为自适应表单指定自定义XCI文件值，以便在表单渲染时使用该值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# 指定XCI配置选项 {#specify-xci-configuration-options}

输出允许您指定用于呈现的自定义XCI文件。 请参阅 [指定输出的文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

默认情况下，“输出”会覆盖XCI文件中指定的某些选项，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以选择取消上面所列选项覆盖的选项，在这种情况下，输出使用自定义XCI文件中指定的值。

1. 在管理控制台中，单击 **服务** >输出。
1. 选中或取消选中使用系统默认XCI选项复选框。 如果选择该选项， Output将对数据包、创建者、生成者和compressObjectStream设置使用其默认值。 取消选择此选项时，输出使用自定义XCI文件中指定的值。
1. 单击&#x200B;**保存**。
