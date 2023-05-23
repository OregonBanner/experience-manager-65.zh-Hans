---
title: Commerce多商店設定
description: 瞭解如何從Adobe Commerce將多個商店檢視對應至AEM。 如此一來，專案便可支援多租使用者和多語言使用案例。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---

# Commerce多商店設定 {#multi-store}

AEM CIF核心元件可用於多個AEM網站結構，且底層GraphQL使用者端實作可連線至不同的Adobe Commerce存放區/存放區檢視。 這可讓專案實作複雜的多存放區/多網站設定。

說明將多個Adobe Commerce商店檢視與Adobe Experience Manager Sites整合之選項的詳細影片逐步解說。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

即時副本和語言副本的AEM多網站管理功能可搭配Commerce Integration Framework使用，以全球管理跨區域和區域設定的網站。

建議的設定是使用AEM網站與Adobe Commerce商店檢視之間的1:1關係。

若要將AEM網站和AEM CIF核心元件也連線到專用的商店檢視，請遵循以下步驟：

## 配置 {#configuration}

1. 根據中所述的模式設定多個商店和商店檢視 [Adobe Commerce網站、商店和檢視](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. 請確定AEM與Adobe Commerce之間的連線正常運作。

3. 按照以下步驟建立CIFCloud Service設定的子設定：

   * 在AEM中前往「工具 — >一般 — >」 [設定瀏覽器](/help/sites-administering/configurations.md#using-configuration-browser)
   * 選取您建立的基本組態
   * 使用上述第2點所述的步驟建立新設定

   此新設定將建立為基本設定的子設定。 您現在可以前往「工具 — >一般 — >組態瀏覽器」並建立組態設定。

   >[!TIP]
   >
   >商業目錄可以使用ID或UID來處理。 Adobe Commerce 2.4.2引進了UID。只有在您的Commerce後端支援2.4.2版或更新版本的GraphQL結構描述時，才會啟用此功能。

4. 將子組態指派給AEM站台

   * 前往AEM Sites主控台
   * 導覽至您網站結構的區域或語言根目錄，例如/content/venia/us _或_ /content/venia/us/en代表Venia範例頁面
   * 選取頁面並開啟頁面屬性
   * 選取「進階」標籤
   * 在 `Configuration` 區段選取您在步驟中建立的組態

## 其他资源

* [Adobe Commerce網站、商店和檢視](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF核心元件 — 多商店/網站設定](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [使用多網站管理員](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重用内容：多站点管理器和 Live Copy](/help/sites-administering/msm.md)
