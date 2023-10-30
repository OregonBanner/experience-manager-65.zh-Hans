---
title: 指定要嵌入的字体
description: 了解如何指定要嵌入自适应表单中的字体。 您可以指定哪些字体嵌入或从未嵌入到Forms服务生成的表单。
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 指定要嵌入的字体{#specify-fonts-to-embed}

您可以指定哪些字体始终嵌入或从不嵌入到输出使用的表单中。 嵌入字体会增加表单的文件大小。 嵌入用户不太可能在其系统上拥有的异常字体，并且不嵌入他们即将安装的常用字体。

>[!NOTE]
>
>如果已为输出指定了自定义XCI文件，则XCI文件中的嵌入字体选项将覆盖这些设置。 (请参阅 [指定输出的文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. 在管理控制台中，单击“服务”>“输出”。
1. 在“字体嵌入设置”下的“始终嵌入字体”框中，键入要嵌入表单的字体名称，并用逗号分隔。 您指定的字体仅会嵌入到生成的表单中（如果它们在表单中使用）。 如果在传递到服务的XCI文件中启用了嵌入字体选项，则会忽略此设置。 在这种情况下，PDF中使用的所有字体始终会嵌入。
1. 在“从不嵌入字体”框中，键入不嵌入表单的字体的名称，名称之间用逗号分隔。 您指定的字体不会嵌入到PDF中，即使它们用在生成的PDF中也是如此。 如果在传递到服务的XCI文件中关闭了嵌入字体选项，则会忽略此设置。 在这种情况下，PDF中使用的字体都不会被嵌入。
1. 单击保存。
