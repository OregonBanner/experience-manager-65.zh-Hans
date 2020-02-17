---
title: 使字体可用
seo-title: 使字体可用
description: 确保表单中使用的字体可用于承载AEM表单的J2EE应用程序服务器。
seo-description: 确保表单中使用的字体可用于承载AEM表单的J2EE应用程序服务器。
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使字体可用 {#make-fonts-available}

确保表单中使用的字体可用于承载AEM表单的J2EE应用程序服务器。 例如，请考虑以下情况。 表单设计人员将一种字体添加到设计人员使用的字体目录中，并在另一台计算机上创建一个使用该字体的表单。 为了使输出服务使用字体，请将其放在Customer字体目录中。 如果客户字体目录不存在，请在承载AEM表单的J2EE应用程序服务器上创建一个目录。

有关其他字体设置的信息，请参阅配 [置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。

**指定客户字体目录的位置**

1. 在管理控制台中，单击设置>核心系统设置>配置。
1. 在“系统字体目录的位置”框中，键入客户字体目录的路径。 可以添加多个目录，以分号分隔 **;**
1. 单击“确定”。
1. 重新启动安装了AEM表单的系统。

>[!NOTE]
>
>从Windows系统字体缓存中选取字体，并需要重新启动系统才能更新缓存。 指定客户字体目录后，请确保重新启动安装了AEM表单的系统。

