---
title: 設定資料擷取的Acrobat Reader DC擴充功能
seo-title: Configuring Acrobat Reader DC extensions for data capture
description: 瞭解如何設定Acrobat Reader DC擴充功能以進行資料擷取。
seo-description: Learn how to configure Acrobat Reader DC extensions for data capture.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 設定資料擷取的Acrobat Reader DC擴充功能 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

如果您安裝AEM Forms的使用者使用Content Services的資料擷取功能（已棄用），建議您為這些使用者建立具有唯讀存取權的角色。

***注意&#x200B;**：Adobe®LiveCycle® Content Services ES （已棄用）是隨LiveCycle安裝的內容管理系統。 它可讓使用者設計、管理、監控及最佳化以人為中心的流程。 內容服務（已棄用）支援將於2014年12月31日終止。 另請參閱 [Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).*

資料擷取需要您指派使用者角色來存取SampleReaderExtensionsCredential。 您可以指派標準的「信任管理員」角色，但認為此角色會賦予一般的非管理使用者強大的管理員許可權，可控制「PKI信任」設定並管理「PKI認證」，這可能會危及您在生產環境中安裝AEM表單的安全性。 建議AEM表單系統管理員建立僅授與信任存放區唯讀存取權的角色，並將此新角色指派給使用資料擷取的非管理員使用者。

## 為資料擷取使用者建立角色 {#create-a-role-for-data-capture-users}

1. 在管理控制檯中，按一下「設定>使用者管理>角色管理」，然後按一下「新增角色」。
1. 在適當的欄位中輸入角色名稱（例如「資料擷取使用者」）和說明，然後按一下「下一步」。
1. 在「角色許可權」畫面上，按一下「尋找許可權」，然後從可用許可權清單中選取「認證讀取」。
1. 按一下「確定」，然後按一下「完成」。

## 指派資料擷取角色 {#assign-the-data-capture-role}

1. 在管理控制檯中，按一下「設定>使用者管理>角色管理」，然後按一下「尋找」。
1. 按一下您建立的資料擷取使用者角色。
1. 在「角色使用者/群組」標籤上，按一下「尋找使用者/群組」。
1. 在「尋找使用者和群組」畫面上，按一下「尋找」，選取需要資料擷取使用者角色的使用者，然後按一下「確定」。
1. 在「編輯角色」畫面上，按一下「儲存」。
