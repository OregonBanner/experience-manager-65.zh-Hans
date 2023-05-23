---
title: 變更驗證的評估順序
seo-title: Change the order of evaluation for authentication
description: 您可以變更AEM Forms評估多個驗證提供者的順序。
seo-description: You can change the order in which AEM forms evaluates multiple authentication providers.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 變更驗證的評估順序 {#change-the-order-of-evaluation-for-authentication}

如果您設定了多個驗證服務提供者，則可以變更AEM Forms評估其驗證順序。 config.xml檔案中列出的驗證提供者順序，決定了驗證的評估順序。

1. 在管理控制檯中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」。
1. 若要將目前的組態設定匯出至檔案，請按一下「匯出」並將組態檔案儲存在其他位置。
1. 在檔案中找到下列節點：

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   在 `<entry key="order" value="3" />`，編輯每個節點的值以設定驗證評估的順序。

1. 若要匯入更新的檔案，請在「使用者管理」中按一下「組態」>「匯入和匯出組態檔案」。
1. 按一下「瀏覽」尋找檔案，按一下「匯入」，然後按一下「確定」。
