---
title: 管理证书吊销列表
description: 了解如何管理证书吊销列表。 您可以使用信任存储区管理导入、编辑和删除证书吊销列表(CRL)。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# 管理证书吊销列表{#managing-certificate-revocationlists}

使用信任存储区管理，您可以导入、编辑和删除证书吊销列表(CRL)。 支持Base64和DER编码的证书吊销列表。

## 导入CRL {#import-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”，然后单击“导入”。
1. 在“别名”框中，键入CRL的标识符。
1. 单击“浏览”以找到CRL，然后单击“确定”。

## 导出CRL {#export-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”。
1. 单击CRL的别名以便导出，然后单击“导出”。
1. 按照说明导出CRL。 CRL以Base64编码导出。
1. 单击确定。

## 删除CRL {#delete-a-crl}

1. 在管理控制台中，单击“设置”>“信任存储区管理”>“证书吊销列表”。
1. 选中要删除的CRL的复选框，单击“删除”，然后单击“确定”。
