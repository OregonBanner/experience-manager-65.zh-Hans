---
title: 設定LDAP繫結密碼
seo-title: Configure the LDAP bind password
description: 瞭解在將設定檔案匯入其他系統之前，如何設定繫結密碼欄位。
seo-description: Learn how to configure the bind password field before you import the configuration file into another system.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 設定LDAP繫結密碼{#configure-the-ldap-bind-password}

為避免安全風險，未設定匯出的設定檔案(config.xml)中的繫結密碼欄位。 將組態檔匯入其他系統之前，請確定您設定此密碼。 此密碼會覆寫儲存在資料庫中的現有密碼。 Null密碼不會覆寫現有的非Null密碼值。

1. 在管理控制檯中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」。
1. 若要將目前的組態設定匯出至檔案，請按一下「匯出」並將組態檔案儲存在其他位置。
1. 在檔案中，找到 `Domains` > *[您的網域名稱]* > `DirectoryConfigs` > `LDAPGroupConfig` 節點。 範例如下：

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   輸入值 `bindpassword` 並儲存您的變更。

1. 在檔案中，找到 `Domains` > *[您的網域名稱]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` 節點。 範例如下：

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   輸入值 `bindpassword` 並儲存您的變更。

1. 若要匯入更新的檔案，請在「使用者管理」中按一下「組態」>「匯入和匯出組態檔案」。
1. 按一下「瀏覽」尋找檔案，按一下「匯入」，然後按一下「確定」。
