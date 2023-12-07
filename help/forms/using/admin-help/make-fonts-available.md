---
title: 使字体可用
description: 确保表单中使用的字体可用于托管AEM表单的J2EE应用程序服务器。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 使字体可用 {#make-fonts-available}

确保表单中使用的字体可用于托管AEM表单的J2EE应用程序服务器。 例如，请考虑以下方案。 窗体设计器将字体添加到Designer使用的字体目录中，并创建在单独的计算机上使用该字体的窗体。 要使Output服务使用该字体，请将其放置在Customer fonts目录中。 如果Customer fonts目录不存在，请在托管AEM表单的J2EE应用程序服务器上创建一个目录。

有关其他字体设置的信息，请参阅 [配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**指定客户字体目录的位置**

1. 在管理控制台中，单击设置>核心系统设置>配置。
1. 在“System Fonts目录的位置”框中，键入Customer Fonts目录的路径。 可以添加多个目录，以分号分隔 **；**
1. 单击“确定”。
1. 重新启动安装了AEM表单的系统。

>[!NOTE]
>
>字体是从Windows系统字体缓存中挑选的，需要重新启动系统才能更新缓存。 指定Customer font目录后，请确保重新启动安装了AEM表单的系统。
