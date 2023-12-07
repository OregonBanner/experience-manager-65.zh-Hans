---
title: 指定要嵌入的字体
description: 了解如何指定要嵌入自适应表单中的字体。 您可以指定哪些字体嵌入或从未嵌入到Forms服务生成的表单。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 指定要嵌入的字体 {#specifying-fonts-to-embed}

您可以指定哪些字体始终嵌入或从未嵌入到Forms服务生成的表单中。 嵌入字体会增加表单的文件大小。 嵌入用户系统上很少使用的异常字体。 请勿嵌入通常已安装的常用字体。

>[!NOTE]
>
>如果您为Forms指定了自定义XCI文件，则XCI文件中的嵌入字体选项将覆盖这些设置。 (请参阅 [为Forms配置位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. 在管理控制台中，单击 **[!UICONTROL 服务> Forms]**.
1. 下 **[!UICONTROL 字体嵌入设置]**，在 **[!UICONTROL 始终嵌入字体]** 框中，键入要嵌入表单的字体的名称，名称之间用逗号分隔。 您指定的字体仅会嵌入到生成的表单中（如果它们在表单中使用）。 如果在传递到服务的XCI文件中启用了嵌入字体选项，则会忽略此设置，因为在这种情况下，PDF中使用的所有字体始终都会嵌入。
1. 在 **[!UICONTROL 从不嵌入字体]** 框中，键入不嵌入表单的字体的名称，名称之间用逗号分隔。 您指定的字体不会嵌入到PDF中，即使它们用在生成的PDF中也是如此。 如果在传递到服务的XCI文件中关闭了embed font选项，则会忽略此设置，因为在这种情况下，PDF中使用的字体都不会嵌入。
1. 单击&#x200B;**[!UICONTROL 保存]**。
