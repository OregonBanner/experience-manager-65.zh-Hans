---
title: 透過Dynamic Media Classic使內容傳遞網路快取失效
description: 使CDN （內容傳遞網路）快取內容失效可讓您快速更新Dynamic Media Classic傳送的資產，而不是等待快取過期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
source-git-commit: b61157b0e9afa49ef72150ae0c1703a959d154be
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 13%

---

# 透過Dynamic Media Classic使內容傳遞網路快取失效 {#invalidating-your-cdn-cached-content}

CDN （內容傳遞網路）會快取Dynamic Media資產，以快速遞送。 不過，當您更新資產時，希望這些變更立即生效。 使CDN快取內容失效可讓您快速更新Dynamic Media傳送的資產，而不是等待快取過期。

>[!NOTE]
>
>此功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。

>[!IMPORTANT]
>
>下列步驟僅適用於Adobe Experience Manager 6.5 Service Pack 5 (Experience Manager6.5.5)或更舊版本中的Dynamic Media。<br>如果您在Experience Manager6.5、Service Pack 6 (Experience Manager 6.5.6)或更新版本中使用Dynamic Media，請依照下列步驟操作： [透過Dynamic Media使CDN快取失效](/help/assets/invalidate-cdn-cache-dynamic-media.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**透過Dynamic Media Classic使CDN快取失效：**

1. 開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)，然後登入您的帳戶。

   您的認證和登入是由Adobe在布建時提供的。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在頁面的右上角附近，瀏覽至 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**.
1. 在「應用程式一般設定」頁面的「伺服器」群組標題下方，找到 **[!UICONTROL CDN失效範本]** 文字方塊。

1. 指定用來讓CDN （內容傳遞網路）快取失效的範本。

   例如，假設您輸入參照的影像URL （包括影像預設集或修飾元） `<ID>`，而非如下列範例所示的特定影像ID：

   `https://server.com/is/image/Company/<ID>?$product$`

   如果範本僅包含 `<ID>`，然後Dynamic Media填入 `https://<server>/is/image` 位置 `<server>` 是在「一般設定」中定義的發佈伺服器名稱，並且 &lt;id> 是選取要失效的資產。

1. 在頁面的右下角，選取 **[!UICONTROL 關閉]**.
1. 在Dynamic Media Classic使用者介面中，選取一或多個資產，然後前往 **[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**. 您會看到從您建立的範本和您選取的資產產生的一個或多個URL清單。 它會使用「應用程式一般設定」下「已發佈的伺服器名稱」下列出的伺服器URL。

   例如，在上一步中設定CDN失效範本，假設您選取了名為的單一影像資產影像 `Backpack_B`. 當您前往 **[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**，則會在CDN失效使用者介面中產生下列URL：

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. 在URL清單方塊中，選取 **[!UICONTROL 繼續]** 以清除每個特定URL的快取。 您可以編輯URL，也可以透過輸入或貼到URL清單方塊中來新增URL；您不需要事先設定CDN失效範本。

   在您選取之後 **[!UICONTROL 繼續]**，會顯示一個指標，為您提供清除快取所需的預估時間。

   如果您選取多個資產，則前往 **[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**，每個資產都會在儲存的檔案中參照 **[!UICONTROL 範本URL]**. 因此，您可以定義 **[!UICONTROL CDN失效範本]** 參考網站上參考的每個URL影像預設集（例如產品詳細資料和搜尋結果）。 然后，当您从缓存中选择一个或多个要失效的图像时，URL 会自动填充该界面。

   >[!NOTE]
   >
   >當您選取資產，然後前往 **[!UICONTROL 檔案]** > **[!UICONTROL 使CDN失效]**，Dynamic Media會使用失效CDN範本，自動建立要使內容傳遞網路(CDN)失效的URL。 如果 **[!UICONTROL CDN 无效模板]**&#x200B;文本框中没有任何内容，则会显示空白 URL 列表。CDN 上的缓存不是基于资产，而是基于 URL。因此，必须了解您网站上的完整 URL。确定这些 URL 后，可以将其添加到步骤前面的&#x200B;**[!UICONTROL 无效 CDN 模板]**。然后，您可以选择这些资产，并在一个步骤中使 URL 失效。
   >
   >另一個選項是將完整URL新增至 **[!UICONTROL 使CDN失效]** 清單。 如果您依照此方法，就不需要先在Dynamic Media Classic中選取資產，然後再前往 **[!UICONTROL 檔案>使CDN失效]** 選項。
