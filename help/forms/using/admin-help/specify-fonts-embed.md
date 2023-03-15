---
title: 指定要嵌入的字体
seo-title: Specify fonts to embed
description: 了解如何指定要嵌入的字体。
seo-description: Learn how to specify fonts to embed.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 指定要嵌入的字体{#specify-fonts-to-embed}

您可以指定哪些字体始终嵌入或从不嵌入到输出使用的表单中。 嵌入字体会增加表单的文件大小。 嵌入用户在其系统上不太可能拥有的异常字体，并且不要嵌入他们将安装的常见字体。

>[!NOTE]
>
>如果已为输出指定了自定义XCI文件，则XCI文件中的嵌入字体选项将覆盖这些设置。 (请参阅 [指定输出的文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. 在管理控制台中，单击服务>输出。
1. 在“字体嵌入设置”下的“始终嵌入字体”框中，键入要嵌入表单的字体名称，并用逗号分隔。 您指定的字体只有在生成表单中使用时才会嵌入到生成表单中。 如果在传递到服务的XCI文件中启用了嵌入字体选项，则会忽略此设置。 在这种情况下，PDF中使用的所有字体始终都会嵌入。
1. 在“从不嵌入字体”框中，键入不嵌入表单的字体名称，并用逗号分隔。 您指定的字体不会嵌入到PDF中，即使它们在生成的PDF中使用也是如此。 如果在传递到服务的XCI文件中关闭了嵌入字体选项，则会忽略此设置。 在这种情况下，不会嵌入PDF中使用的任何字体。
1. 单击“保存”。
