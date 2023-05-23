---
title: 在安裝時設定管理員密碼
seo-title: Configure the Admin Password on Installation
description: 瞭解如何在AEM安裝時變更管理員密碼。
seo-description: Learn how to change the Admin Password on AEM Installation.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 在安裝時設定管理員密碼{#configure-the-admin-password-on-installation}

## 概述 {#overview}

自6.3版開始，AEM可在安裝新執行個體時，使用命令列設定管理員密碼。

使用舊版AEM時，在安裝後必須變更管理員帳戶的密碼以及各種其他主控台的密碼。

此功能新增在安裝AEM執行個體期間為存放庫和Servlet引擎設定新管理員密碼的功能，因此不需要在之後手動進行。

>[!CAUTION]
>
>請注意，功能未涵蓋Felix主控台，需要手動變更密碼。 如需詳細資訊，請參閱相關 [安全性檢查清單區段](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## 如何使用它？ {#how-do-i-use-it}

如果您選擇透過命令列安裝AEM，而不是從檔案系統總管連按兩下JAR，則會自動觸發此功能。

從命令列執行AEM執行個體的一般語法為：

```shell
java -jar aem6.3.jar
```

從命令列執行執行個體時，您將會看到在安裝過程中變更管理員密碼的選項：

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>只有在安裝新的AEM執行個體時，才會出現變更管理員密碼的提示。

## 使用 — nointeractive旗標 {#using-the-nointeractive-flag}

您也可以選擇從屬性檔案指定密碼。 這是透過使用 `-nointeractive` 與組合的標幟`-Dadmin.password.file` 系統屬性。

範例如下：

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

內的密碼 `passwordfile.properties` 檔案的格式必須如下：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>如果您只使用 `-nointeractive` 引數不含 `-Dadmin.password.file` 系統屬性時，AEM會使用預設的管理密碼，而不會要求您進行變更，基本上會複製舊版的行為。 此非互動模式可用於在安裝指令碼中使用命令列的自動安裝。
