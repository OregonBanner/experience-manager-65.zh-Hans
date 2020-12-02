---
title: 设置用于Acrobat Reader DC扩展的超时值
seo-title: 设置用于Acrobat Reader DC扩展的超时值
description: 了解如何设置超时值以用于Acrobat Reader DC扩展。
seo-description: 了解如何设置超时值以用于Acrobat Reader DC扩展。
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 设置用于Acrobat Reader DC扩展{#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}的超时值

在Acrobat Reader DC扩展中处理许多PDF文件时，请确保正确设置以下超时值以防止作业超时和失败：

**文档处理超时**

此值可在管理控制台中设置。 单击“设置”>“核心系统设置”>“配置”，然后为“默认文档处理超时”指定一个值。

**用户管理器AEM表单超** 时：可通过编辑config.xml文件设置此值。在管理控制台中，单击“设置”>“用户管理”>“配置”>“导入和导出配置文件”，然后单击“导出”。 打开导出的config.xml文件并编辑以下行：

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot; />

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot; />

保存，然后将config.xml文件导入管理控制台。

**应用程序服务器会话超** 时：可以在应用程序服务器上设置此值。有关详细信息，请参阅随应用程序服务器提供的文档。
