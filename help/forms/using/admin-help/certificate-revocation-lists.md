---
title: 管理证书缩写列表
seo-title: 管理证书缩写列表
description: 了解如何管理证书吊销列表。
seo-description: 了解如何管理证书吊销列表。
uuid: d8c4b64c-a273-4f5d-8b71-f6ea455c0f0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9744cc2d-5e6b-4341-9270-43d479bdca04
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# 管理证书转座列表{#managing-certificate-revocationlists}

使用信任存储管理，您可以导入、编辑和删除证书吊销列表(CRL)。 支持Base64和DER编码的证书吊销列表。

## 导入CRL {#import-a-crl}

1. 在管理控制台中，单击设置>信任存储管理>证书吊销列表，然后单击导入。
1. 在别名框中，键入CRL的标识符。
1. 单击浏览以找到CRL，然后单击确定。

## 导出CRL {#export-a-crl}

1. 在管理控制台中，单击设置>信任存储管理>证书吊销列表。
1. 单击要导出的CRL的别名，然后单击“导出”。
1. 按照说明导出CRL。 CRL以Base64编码导出。
1. 单击确定。

## 删除CRL {#delete-a-crl}

1. 在管理控制台中，单击设置>信任存储管理>证书吊销列表。
1. 选中要删除的CRL的复选框，单击“删除”，然后单击“确定”。
