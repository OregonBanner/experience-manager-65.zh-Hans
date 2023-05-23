---
title: 設定遠端端點
seo-title: Configuring Remoting endpoints
description: 瞭解如何設定遠端端點。
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 設定遠端端點 {#configuring-remoting-endpoints}

遠端端點可讓以Flex建置的應用程式使用(已針對AEM表單棄用) AEM Forms Remoting來叫用服務。 系統會自動為每個啟用的服務建立遠端端點。 會建立與端點同名的Flex目的地，而Flex使用者端可建立指向此目的地的遠端物件，以叫用相關服務的作業。

## 遠端端點設定 {#remoting-endpoint-settings}

**Flex使用者端驗證方法：** 決定當叫用的服務已啟用安全性、叫用的操作不支援匿名叫用，而且使用者端傳入沒有或無效的認證時，伺服器傳回給使用者端的回應型別。
