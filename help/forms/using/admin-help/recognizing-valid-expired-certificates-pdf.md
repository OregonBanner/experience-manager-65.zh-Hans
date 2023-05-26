---
title: 识别PDF文档中的有效证书和过期证书
seo-title: Recognizing valid and expired certificates in PDF documents
description: 了解如何识别PDF文档中的有效证书和过期证书。
seo-description: Learn how to recognize valid and expired certificates in PDF documents.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 识别PDF文档中的有效证书和过期证书 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

在Adobe Reader中打开具有由PDF扩展应用的使用权限的Reader文档时，将显示一个状态栏，其中描述在PDF文档中启用的特定使用权限。

当指定PDF文档使用权限的数字证书过期并在Adobe Reader中打开PDF文档时，会出现一个对话框，提示用户该PDF文档具有使用权限，但这些权限被禁用。 尽管该消息表明PDF文档已被更改或篡改，但情况不一定如此。 当证书过期或修改文档时，Adobe Reader会显示此消息。 在Adobe Reader 7.0.x或更高版本中，您无法确定当前问题是哪种情况。

关闭对话框后，Adobe Reader会打开PDF文档。 使用Acrobat Reader DC扩展应用的使用权限将无法按预期使用。 如果PDF文档是交互式表单，则表单字段将被锁定，用户无法更改表单数据。
