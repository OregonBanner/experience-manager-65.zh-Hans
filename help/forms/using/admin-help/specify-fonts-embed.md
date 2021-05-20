---
title: 指定要嵌入的字体
seo-title: 指定要嵌入的字体
description: 了解如何指定要嵌入的字体。
seo-description: 了解如何指定要嵌入的字体。
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# 指定要嵌入的字体{#specify-fonts-to-embed}

您可以指定始终嵌入或从不嵌入由输出使用的表单的字体。 嵌入字体会增加表单的文件大小。 嵌入了用户在其系统上不太可能具有的异常字体，并且不会嵌入他们将安装的常用字体。

>[!NOTE]
>
>如果为“输出”指定了自定义XCI文件，则XCI文件中的嵌入字体选项将覆盖这些设置。 （请参阅[为输出指定文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。）

1. 在管理控制台中，单击服务>输出。
1. 在“字体嵌入设置”下的“始终嵌入字体”框中，键入要与表单嵌入的字体名称，并用逗号分隔。 仅当在表单中使用您指定的字体时，这些字体才会嵌入生成的表单中。 如果在传递到服务的XCI文件中打开了嵌入字体选项，则忽略此设置。 在这种情况下，PDF中使用的所有字体都始终被嵌入。
1. 在“从不嵌入字体”框中，键入不要与表单嵌入的字体的名称，并使用逗号分隔。 您指定的字体不会嵌入到PDF中，即使这些字体在生成的PDF中使用也是如此。 如果在传递到服务的XCI文件中关闭了嵌入字体选项，则会忽略此设置。 在这种情况下，PDF中使用的字体均未嵌入。
1. 单击保存。
