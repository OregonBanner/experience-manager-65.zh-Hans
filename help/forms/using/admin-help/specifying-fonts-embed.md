---
title: 指定要嵌入的字体
seo-title: 指定要嵌入的字体
description: 了解如何指定要嵌入的字体。
seo-description: 了解如何指定要嵌入的字体。
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 指定要嵌入的字体 {#specifying-fonts-to-embed}

您可以指定始终嵌入或从不嵌入Forms服务生成的表单的字体。 嵌入字体会增加表单的文件大小。 嵌入用户在其系统上很少使用的不寻常字体。 请勿嵌入他们通常安装的常用字体。

>[!NOTE]
>
>如果您为Forms指定了自定义XCI文件，则XCI文件中的嵌入字体选项将覆盖这些设置。 (请参阅 [配置表单的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。)

1. 在管理控制台中，单击“ **[!UICONTROL 服务”>“表单]**”。
1. 在“ **[!UICONTROL 字体嵌入设置]**”下，在“始终嵌 **** 入字体”框中，键入要嵌入的字体名称，以逗号分隔。 您指定的字体仅嵌入在生成的表单中（如果在表单中使用）。 如果在传递给服务的XCI文件中打开了嵌入字体选项，则忽略此设置，因为在这种情况下，PDF中使用的所有字体始终嵌入。
1. 在“从 **[!UICONTROL 不嵌入字体]** ”框中，键入不要嵌入表单的字体名称，以逗号分隔。 您指定的字体不会嵌入到PDF中，即使在生成的PDF中使用也是如此。 如果传递给服务的XCI文件中的嵌入字体选项已关闭，则忽略此设置，因为在这种情况下，PDF中使用的字体均未嵌入。
1. 单击&#x200B;**[!UICONTROL 保存]**。

