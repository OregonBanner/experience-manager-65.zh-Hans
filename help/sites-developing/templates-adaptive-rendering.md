---
title: 最適化範本演算
seo-title: Adaptive Template Rendering
description: 最適化範本演算
seo-description: null
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 最適化範本演算{#adaptive-template-rendering}

最適化範本演算提供管理變異頁面的方法。 此功能原本很適合用於為行動裝置提供各種HTML輸出（例如功能手機與智慧型手機），當體驗必須提供給需要不同標籤或HTML輸出的各種裝置時，此功能會很有用。

## 概述 {#overview}

範本通常建置在回應式格線上，根據這些範本建立的頁面會完全回應，並自動調整至使用者端裝置的檢視區。 作者可以使用頁面編輯器中的模擬器工具列，將版面鎖定在特定裝置。

也可以設定範本以支援最適化轉譯。 若裝置群組已正確設定，則在模擬器模式下選取裝置時，頁面將會以URL中的不同選取器呈現。 使用選取器，您可以透過URL直接呼叫特定頁面呈現。

設定裝置群組時請記住：

* 每個裝置至少必須位於一個裝置群組中。
* 一個裝置可以位於多個裝置群組中。
* 由於裝置可以位於多個裝置群組中，因此可組合選取器。
* 系統會自上而下評估選取器組合，因為會將其保留在存放庫中。

>[!NOTE]
>
>裝置群組 **回應式裝置** 永遠不會有選擇器，因為已辨識為支援回應式設計的裝置假設不需要最適化配置

## 配置 {#configuration}

最適化演算選擇器可針對現有裝置群組進行設定，或設定為 [您自己建立的群組。](/help/sites-developing/mobile.md#device-groups)

在此範例中，我們將設定現有的裝置群組 **智慧型手機** 將最適化轉譯選擇器作為 **體驗頁面** We.Retail中的範本。

1. 編輯中需要最適化選擇器的裝置群組 `http://localhost:4502/miscadmin#/etc/mobile/groups`

   設定選項 **停用模擬器** 並儲存。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 選擇器將適用於 **Blackberry** 和 **IPHONE 4** 已提供裝置群組 **智慧型手機** 會新增至下列步驟中的範本和頁面結構。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 使用CRX DE Lite，將裝置群組新增至多值字串屬性，以便用於您的範本 `cq:deviceGroups` 範本的結構。

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   例如，如果我們想要新增Smartphone裝置群組：

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. 使用CRX DE Lite，將裝置群組新增至多值字串屬性，讓該裝置群組可在您的網站上使用 `cq:deviceGroups` 您的網站結構。

   `/content/<your-site>/jcr:content`

   例如，如果我們想要允許 **智慧型手機** 裝置群組：

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

現在使用 [模擬器](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) (例如： [修改版面](/help/sites-authoring/responsive-layout.md))且選擇已設定裝置群組的裝置時，頁面會以URL中的選取器呈現。

在我們的範例中，根據以下範例編輯頁面時： **體驗頁面** 範本，並在模擬器中選擇iPhone 4，則會呈現包含選取器的頁面，如下所示 `arctic-surfing-in-lofoten.smart.html` 而非 `arctic-surfing-in-lofoten.html`

也可以使用此選取器直接呼叫頁面。

![chlimage_1-161](assets/chlimage_1-161.png)
