---
title: 输出服务概述
seo-title: 输出服务概述
description: 通过“输出”，您可以将XML表单数据与在Designer中创建的表单设计合并，以创建各种格式的文档输出流。
seo-description: 通过“输出”，您可以将XML表单数据与在Designer中创建的表单设计合并，以创建各种格式的文档输出流。
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 输出服务概述 {#overview-of-output-service}

通过“输出”，您可以将XML表单数据与在Designer中创建的表单设计合并，以创建各种格式的文档输出流。 输出流可被发送到网络打印机、本地打印机或磁盘文件

您可以使用管理控制台中的“输出”页面来管理“输出”服务。 运行时，当未通过AEM forms API指定对等设置时，将使用您配置的设置。 通过AEM Forms SDK完成的配置将覆盖使用管理控制台配置的设置。

有关输出服务的其他信息，请参阅服 [务参考](https://www.adobe.com/go/learn_aemforms_services_61)。

在管理控制台的“输出”页面上，您可以执行多项任务：

* 为国际化指定字符集。 (请参 [阅更改字符集](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)。)
* 为URL、URI、XCI和文件位置指定绝对路径和相对路径。 (请参 [阅为输出指定文件位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。)
* 配置缓存大小和策略。 (请参 [阅指定缓存模式](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) 和配 [置缓存设置](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)。)
* 使字体在应用程序服务器上可用。 (请参阅 [使字体可用](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)。)
* 指定要嵌入的字体。 (请参 [阅指定要嵌入的字体](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)。)
* 指定XCI配置选项。 (请参 [阅指定XCI配置选项](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)。)
* 指定安全设置。 (请参阅 [指定安全设置](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)。)

更改设置后，单击“保存”以将其应用于“输出”。 您无需重新启动服务器，更改即可生效，但配置缓存设置时可能需要重新启动输出服务。
