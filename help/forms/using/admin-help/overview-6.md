---
title: 設定SSL的概觀
seo-title: Overview of configuring SSL
description: 瞭解如何透過設定SSL來增強通訊的安全性。
seo-description: Learn about how to enhance security of communication by configuring SSL.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 設定SSL的概觀 {#overview-of-configuring-ssl}

您可以建立安全通訊端層(SSL)認證，並在應用程式伺服器上設定SSL，以加強與應用程式伺服器通訊的安全性。

作為安全性產品，Rights Management需要設定SSL。 設定SSL憑證時，請確定您僅使用RSA金鑰。 不支援具有DSA金鑰的SSL憑證。

提供的資訊適用於交鑰匙安裝、自動安裝和手動安裝。 它提供設定SSL方法的範例。 您也可以使用其他更適合您的網路或組織的方法。

>[!NOTE]
>
>建議您先完成AEM表單模組的安裝、設定和部署，並在應用程式伺服器上設定SSL之前，確保產品可正確執行。

>[!NOTE]
>
>建立SSL安全性憑證和認證時，請使用您用來執行應用程式伺服器的相同使用者帳戶許可權。 如果使用其他使用者許可權執行應用程式伺服器，則當ContentRootURI指向https時，表單可能無法正確轉譯為PDFForm轉譯。

如果您有啟用SSL的LDAP伺服器，請設定「使用者管理」以搭配使用。 (請參閱 [為啟用SSL的LDAP伺服器設定使用者管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
