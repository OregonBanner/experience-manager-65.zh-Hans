---
title: 管理证书转换列表
seo-title: 管理证书转换列表
description: 了解如何管理证书吊销列表。
seo-description: 了解如何管理证书吊销列表。
uuid: d8c4b64c-a273-4f5d-8b71-f6ea455c0f0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9744cc2d-5e6b-4341-9270-43d479bdca04
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---


# 管理证书转换列表{#managing-certificate-revocationlists}

使用信任存储管理，您可以导入、编辑和删除证书吊销列表(CRL)。 支持Base64和DER编码的证书撤销列表。

## 导入CRL {#import-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“证书吊销列表”，然后单击“导入”。
1. 在“别名”框中，键入CRL的标识符。
1. 单击“浏览”查找CRL，然后单击“确定”。

## 导出CRL {#export-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“证书吊销列表”。
1. 单击要导出的CRL别名，然后单击“Export（导出）”。
1. 请按照指示导出CRL。 CRL以Base64编码导出。
1. 单击确定。

## 删除CRL {#delete-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储管理”>“证书吊销列表”。
1. 选中要删除的CRL的复选框，单击“删除”，然后单击“确定”。

