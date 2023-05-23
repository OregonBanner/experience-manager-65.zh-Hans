---
title: 將登入頁面與Adobe Analytics整合
seo-title: Integrating Landing Pages with Adobe Analytics
description: 瞭解如何將登入頁面與Adobe Analytics整合。
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 將登入頁面與Adobe Analytics整合{#integrating-landing-pages-with-adobe-analytics}

AEM已將登入頁面解決方案與 [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) 使用下列號召性用語(CTA)元件：

1. 點進元件
1. 圖形連結元件

這些元件會公開某些可透過Adobe Analytics變數（流量、轉換變數）和成功事件對應的屬性，以將資訊傳送至Adobe Analytics。

## 前提条件 {#prerequisites}

Adobe建議您透過 [現有AEM-Adobe Analytics整合](/help/sites-administering/adobeanalytics.md) 以瞭解此整合的運作方式。

## 可用於對應的元件 {#components-available-for-mapping}

在AEM中， **行動號召** 元件 —  **點進連結** 和 **GraphicalLink**  — 顯示在sidekick中，可對映至Adobe Analytics變數。

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### 將登入頁面元件對應至Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

若要將登入頁面元件對應至Adobe Analytics：

1. 建立Adobe Analytics設定和建立新框架後，請從下拉式選單中選取適當的報表套裝。 這會擷取Adobe Analytics變數，並在內容尋找器中顯示它們。
1. 視情況將Call to Action (CTA)元件從Sidekick拖放至頁面中間的對應區域。

<table>
 <tbody>
  <tr>
   <td><strong>元件名稱</strong></td>
   <td><strong>屬性已公開</strong></td>
   <td><strong>屬性的含義</strong></td>
  </tr>
  <tr>
   <td><strong>cta點進連結</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>連結上的標籤或連結的文字 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>按一下連結時所前往的目的地 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>點選事件 </td>
  </tr>
  <tr>
   <td><strong>CTA圖形連結</strong></td>
   <td><i>eventdata.clickgroughImageLabel</i> <br /> </td>
   <td>CTA影像的標題 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>按一下包含連結的影像時所拍攝的目的地</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickgroughImageAsset</i> <br /> </td>
   <td>存放庫中影像資產的路徑 </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickgroughImageClick</i> <br /> </td>
   <td>點選事件</td>
  </tr>
 </tbody>
</table>

1. 從內容尋找器將這些公開的屬性與任何Adobe Analytics變數對應。 架構現已準備就緒，可供使用。
1. 您現在可以建立新登陸頁面，或使用現有CTA元件開啟現有登陸頁面，然後按一下 **Cloud Services** 定位於 **頁面屬性** 從sidekick (在觸控最佳化UI中，選取 **開啟屬性** 並按一下 **Cloud Services**)並設定框架以搭配登陸頁面使用。 從下拉式清單中選取架構。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 使用登入頁面設定框架後，您現在可以使用儀表化的元件，對CTA的任何點按都會記錄在Adobe Analytics中。
