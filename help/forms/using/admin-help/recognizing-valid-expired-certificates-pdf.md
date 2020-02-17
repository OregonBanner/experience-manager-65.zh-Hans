---
title: 识别PDF文档中的有效和过期的证书
seo-title: 识别PDF文档中的有效和过期的证书
description: 了解如何识别PDF文档中的有效和过期的证书。
seo-description: 了解如何识别PDF文档中的有效和过期的证书。
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 识别PDF文档中的有效和过期的证书 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

在Adobe Reader中打开具有Reader扩展应用的使用权限的PDF文档时，将显示一个状态栏，其中描述了在PDF文档中启用的特定使用权限。

当指定PDF文档使用权限的数字证书过期，并在Adobe reader中打开PDF文档时，将显示一个对话框，告知用户PDF文档具有使用权限，但这些权限被禁用。 尽管消息指示PDF文档已被更改或篡改，但这不一定是事实。 当证书过期或文档被修改时，Adobe Reader会显示此消息。 在Adobe Reader 7.0.x或更高版本中，您无法确定当前问题出在哪种情况下。

关闭对话框后，Adobe Reader将打开PDF文档。 使用Acrobat Reader DC扩展应用的使用权限不可用，如预期。 如果PDF文档是交互式表单，则表单字段被锁定，用户无法更改表单数据。
