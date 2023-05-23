---
title: 管理憑證撤銷清單
seo-title: Managing certificate revocationlists
description: 瞭解如何管理憑證撤銷清單。
seo-description: Learn how to manage certificate revocation lists.
uuid: d8c4b64c-a273-4f5d-8b71-f6ea455c0f0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9744cc2d-5e6b-4341-9270-43d479bdca04
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# 管理憑證撤銷清單{#managing-certificate-revocationlists}

使用「信任存放區管理」，您可以匯入、編輯和刪除憑證撤銷清單(CRL)。 支援Base64和DER編碼的憑證撤銷清單。

## 匯入CRL {#import-a-crl}

1. 在Administration Console中，按一下[Settings] > [Trust Store Management] > [Certificate Revocation Lists]，然後按一下[Import]。
1. 在「別名」方塊中，輸入CRL的識別碼。
1. 按一下「瀏覽」來尋找CRL，然後按一下「確定」。

## 匯出CRL {#export-a-crl}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「憑證撤銷清單」。
1. 按一下要匯出的CRL別名，然後按一下「匯出」。
1. 依照指示匯出CRL。 CRL會以Base64編碼匯出。
1. 单击确定。

## 刪除CRL {#delete-a-crl}

1. 在管理控制檯中，按一下「設定」>「信任存放區管理」>「憑證撤銷清單」。
1. 選取要刪除的CRL核取方塊，按一下「刪除」，然後按一下「確定」。
