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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 指定要嵌入的字体{#specify-fonts-to-embed}

您可以指定始终嵌入或从不嵌入由输出使用的表单的字体。 嵌入字体会增加表单的文件大小。 嵌入用户在系统上不太可能拥有的不寻常字体，并且不会嵌入他们将安装的常见字体。

>[!NOTE]
>
>如果已为“输出”指定自定义XCI文件，则XCI文件中的嵌入字体选项将覆盖这些设置。 (请参 [阅为输出指定文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。)

1. 在管理控制台中，单击“服务”>“输出”。
1. 在“字体嵌入设置”下的“始终嵌入字体”框中，键入要嵌入的字体名称，以逗号分隔。 您指定的字体仅嵌入在生成的表单中（如果在表单中使用）。 如果在传递给服务的XCI文件中打开了嵌入字体选项，则忽略此设置。 在这种情况下，PDF中使用的所有字体始终被嵌入。
1. 在“从不嵌入字体”框中，键入不要嵌入表单的字体名称，以逗号分隔。 您指定的字体不会嵌入到PDF中，即使在生成的PDF中使用也是如此。 如果传递给服务的XCI文件中的嵌入字体选项已关闭，则忽略此设置。 在这种情况下，PDF中使用的所有字体都不会嵌入。
1. 单击保存。

