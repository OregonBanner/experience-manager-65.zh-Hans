---
title: 设置超时值以用于Acrobat Reader DC扩展
seo-title: Setting timeout values for use with Acrobat Reader DC extensions
description: 了解如何设置超时值以用于Acrobat Reader DC扩展。
seo-description: Learn how to set timeout values for use with Acrobat Reader DC extensions.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 设置超时值以用于Acrobat Reader DC扩展  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

处理Acrobat Reader DC扩展中的许多PDF文件时，请确保正确设置了以下超时值，以防止作业超时和失败：

**文档处理超时**

可以在管理控制台中设置此值。 单击设置>核心系统设置>配置，并指定默认文档处理超时值。

**用户管理器AEM表单超时：** 可以通过编辑config.xml文件来设置此值。 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件，然后单击导出。 打开导出的config.xml文件并编辑以下行：

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

保存config.xml文件，然后将其导入管理控制台。

**应用程序服务器会话超时：** 可以在应用程序服务器上设置此值。 有关详细信息，请参阅随应用程序服务器提供的文档。
