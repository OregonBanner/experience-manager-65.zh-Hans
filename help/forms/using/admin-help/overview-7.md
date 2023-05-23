---
title: 設定表單的基本知識
seo-title: Basics of configuring forms
description: 瞭解各種可幫助您建立互動式資料擷取應用程式的表單服務。
seo-description: Learn about the various forms services that help you create interactive data capture applications.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 設定表單的基本知識 {#basics-of-configuring-forms}

Forms服務可讓您建立互動式資料擷取使用者端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者會開發單一表單設計，Forms服務會以各種格式呈現：

* 作為Adobe Reader或瀏覽器中的PDF
* 在各種瀏覽器環境中（包括相容的XHTML 1.0轉譯）作為HTML
* 在支援AdobeFlash Player的各種瀏覽器環境中，以表單形式提供指南。

如需Forms服務的詳細資訊，請參閱 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

使用Administration Console中的Forms頁面，您可以設定Forms服務的行為。 這些設定會套用至服務的所有叫用。 透過AEM Forms SDK傳送的任何引數都會覆寫在管理主控台中設定的設定；但是，這些引數只會影響該特定叫用。

在管理主控台中變更Forms設定後，按一下「儲存」 。 您不需要重新啟動伺服器即可讓變更生效。 不過，在設定快取模式設定時，您可能需要停止並重新啟動Forms服務。 (請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
