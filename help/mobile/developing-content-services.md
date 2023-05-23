---
title: Content Services
seo-title: Content Services
description: Content Services
seo-description: null
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# Content Services{#content-services}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Content Services功能僅供預覽之用。
>
>此版本可能會隨著6.3 GA Service Pack 1的發行而有所變更。

AEM Mobile Content Services是輕量級的功能，可請求由AEM管理的內容。 這可讓所有應用程式開發人員以高效能的方式擷取內容，而不需要深入瞭解AEM內容存放庫(JCR)和網頁架構(Sling)。 這可讓請求的應用程式與內容存放庫分離。

Content Services引進了數種新的AEM建構，可讓開發人員存取AEM管理的內容，而不需要瞭解該內容的存放庫結構。

這些建構對於在AEM管理的內容和使用內容的行動應用程式之間提供抽象層，以保持靈活性並啟用未來擴充是必要的。 這可讓AEM Content Services在原生應用程式的內容需求和AEM內容存放庫之間充當抽象層。

Content Services可將內容以資產、封裝HTML(HTML/CSS/JS)或頻道獨立內容的形式傳送。

>[!CAUTION]
>
>**前提条件:**
>
>開始使用內容服務之前，請務必啟用「內容服務」標幟。 若要啟用在您的應用程式中建立和管理模型，您必須在設定瀏覽器中啟用資料模型。
>
>另請參閱 **[管理內容服務](/help/mobile/developing-content-services.md)** 和 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。

![chlimage_1-143](assets/chlimage_1-143.png)

設定Content Services標幟並在Configuration Browser中啟用資料模型後，請參閱下列資源以開始使用AEM Mobile Content Services，熟悉AEM Mobile Content Services概念，例如模型管理、實體管理，然後為Content Services傳送內容/轉譯。

* 存放庫中的模型
* 呈現和傳遞
