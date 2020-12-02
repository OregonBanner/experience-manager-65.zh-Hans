---
title: 识别PDF文档中的有效和过期证书
seo-title: 识别PDF文档中的有效和过期证书
description: 了解如何识别PDF文档中的有效和过期证书。
seo-description: 了解如何识别PDF文档中的有效和过期证书。
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 识别PDF文档{#recognizing-valid-and-expired-certificates-in-pdf-documents}中的有效和过期的证书

当在Adobe Reader打开具有由Reader扩展应用的使用权限的PDF文档时，将显示一个状态栏，其中描述在PDF文档中启用的特定使用权限。

当指定PDF文档的使用权限的数字证书过期且在Adobe Reader打开PDF文档时，将显示一个对话框，告知用户PDF文档具有使用权限，但这些权限被禁用。 尽管消息指示PDF文档被更改或篡改，但情况不一定如此。 Adobe Reader在证书过期或文档被修改时显示此消息。 在Adobe Reader7.0.x或更高版本中，您无法确定当前问题出在哪种情况。

关闭对话框后，Adobe Reader将打开PDF文档。 使用Acrobat Reader DC扩展应用的使用权限未按预期可用。 如果PDF文档是交互式表单，则表单字段将被锁定，用户无法更改表单数据。
