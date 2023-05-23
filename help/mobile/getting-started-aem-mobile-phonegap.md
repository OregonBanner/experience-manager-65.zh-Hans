---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM與PhoneGap整合，因此您可以使用AEM頁面輕鬆建立應用程式。 請依照本頁面的說明開始使用Adobe PhoneGap Enterprise。
seo-description: AEM integrates with PhoneGap so that you can easily create apps using AEM pages. Follow this page to get started with Adobe PhoneGap Enterprise.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

AEM與PhoneGap整合，因此您可以使用AEM頁面輕鬆建立應用程式。 PhoneGap可讓使用者建立公用程式應用程式，讓使用者使用內容。 內容同步可讓您建立頁面的版本化封存，以便與應用程式整合。

通常， ***AEM管理員*** 負責透過使用建立精靈建立新應用程式，或匯入現有應用程式，將新應用程式新增至AEM Mobile目錄。

從這裡開始 ***AEM作者*** (或 *行銷人員*)現在可以使用現成的範本和元件來新增和編輯頁面、拖放元件，以及從DAM新增所有型別的媒體，包括影像、影片和文字片段（內容片段）。

AEM Mobile的真正優勢在於 *精明* ***AEM開發人員*** 可擴充及建立自訂Web範本和元件，以啟用 *AEM作者* 打造美觀且引人入勝的行動體驗。 這些範本和元件不僅已針對行動應用程式世界進行最佳化，而且可與裝置與全頻道服務端點的AEM伺服器（任何遠端伺服器）通訊。

>[!NOTE]
>
>當 *AEM作者* 相信應用程式已就緒，他們可以先讓利害關係人下載應用程式，並搭配 **[Adobe驗證](/help/mobile/phonegap-mobile-quickstart.md)** （可在AppStore和PlayStore中使用）以供檢閱和核准。 收到綠燈後，他們就能透過AEM Mobile ContentSync內容發行管理控制面板，直接發行這項新內容或更新內容給使用者。 一個人可以擔任任意數量的角色，具體取決於您和您的治理政策。

## 前提条件 {#prerequisites}

AEM Mobile只是構成完整AEM平台的支柱之一。

在使用AEM Mobile並按照本快速入門手冊中的步驟操作之前，使用者應該熟悉AEM和AEM Mobile控制中心。 请参阅：

[AEM 快速入门](/help/sites-deploying/deploy.md)

[AEM Mobile控制中心逐步解說](/help/mobile/phonegap-authoring-apps.md)

## 作者的快速連結 {#quicklinks-for-authors}

另請參閱 [在AEM中為Adobe PhoneGap Enterprise製作](/help/mobile/phonegap.md) 以瞭解作者的角色和責任。

## 適用於開發人員的快速連結 {#quicklinks-for-developers}

有些範例應用程式會與AEM Mobile整合，並可由開發人員自訂。 按一下 [使用AEM開發Adobe PhoneGap Enterprise](/help/mobile/developing-in-phonegap.md).

在接下來的章節中，您將瞭解如白色標籤應用程式、本地化、國際化、ContentSync、目標定位、分析等進階概念。

## 適用於管理員的快速連結 {#quicklinks-for-administrators}

另請參閱 [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md) 以設定及管理您的行動應用程式。

>[!NOTE]
>
>使用混合行動技術，您可以建立豐富的行動應用程式， *離線和線上執行* 事實上，透過AEM Mobile，許多客戶會選擇建立應用程式，以便檢查他們何時線上上或離線，並據此採取相應的行動。
