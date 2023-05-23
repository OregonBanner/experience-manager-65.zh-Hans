---
title: 編輯和轉換現有網域
seo-title: Editing and converting existing domains
description: 瞭解如何從「網域管理」頁面變更現有網域的設定。 將現有企業網域轉換為混合網域，反之亦然。
seo-description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or vice versa.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# 編輯和轉換現有網域{#editing-and-converting-existing-domains}

您可以從「網域管理」頁面變更現有網域的設定。 您也可以將現有的企業網域轉換為混合網域。

## 編輯現有網域 {#edit-an-existing-domain}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下要編輯的網域名稱。
1. 若要變更網域名稱，請變更「名稱」方塊中的文字。
1. 若要變更企業或混合式網域的驗證資訊，請按一下頁面底部適當的驗證名稱。 在「編輯驗證」頁面上，視需要變更設定。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 若要變更企業網域的目錄資訊，請按一下頁面底部的適當目錄名稱。 在「編輯目錄」頁面上，視需要變更設定。 (請參閱 [新增目錄或自訂SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. 完成變更後，按一下「確定」。

## 將企業網域轉換為混合網域 {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下要轉換的企業網域名稱。
1. 按一下「轉換為混合網域」。
1. 檢閱顯示的關於使用者和群組資料以及使用者驗證的資訊，然後按一下「確定」。
1. 編輯混合網域的設定，然後按一下「確定」。

>[!NOTE]
>
>如果您要轉換的企業網域不包含目錄設定，則會遺失任何LDAP驗證設定。

## 將混合網域轉換為企業網域 {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下要轉換的混合網域名稱。
1. 按一下「轉換為企業網域」。
1. 檢閱顯示的關於使用者和群組資料以及使用者驗證的資訊，然後按一下「確定」。
1. 按一下「新增目錄」並設定所需的目錄資訊。 (請參閱 [新增目錄或自訂SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
