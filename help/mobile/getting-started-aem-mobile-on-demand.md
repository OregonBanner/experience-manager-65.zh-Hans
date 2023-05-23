---
title: Adobe Experience Manager Mobile On-Demand
description: 開始新的AEM Mobile應用程式體驗時，必須先整合角色，才可編輯內容。 請依照本頁面的說明開始使用AEM Mobile On-Demand Services。
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>如果您沒有使用AEM作為內容管理來源，請參閱 [AEM Mobile On-demand Services說明](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM提供數種工具，可讓您將內容整合至行動應用程式。

下圖說明AEM Mobile和On-Demand Services的各種元件如何搭配使用，以將內容傳送至行動應用程式。

AEM Preflight應用程式可視為測試環境，可在發佈前預覽應用程式和內容；而AEM Mobile應用程式則是針對發佈而建立的最終應用程式。

>[!NOTE]
>
>若要深入瞭解預檢應用程式，請參閱 [使用AEM Preflight應用程式](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) (位於AEM Mobile On-demand Services說明)。

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>在上圖中，AEM發佈執行個體不需要AEM Mobile On-demand Services的典型部署案例。

## 啟動新的行動應用程式 {#starting-a-new-mobile-app}

AEM Mobile只是構成完整AEM平台的支柱之一。

開始新的AEM Mobile應用程式體驗時，必須先整合角色，才可編輯內容。 下列角色提供建立新AEM Mobile應用程式的起點：

* **管理员**
* **开发人员**
* **创作**

>[!NOTE]
>
>在使用AEM Mobile並按照本快速入門手冊中的步驟操作之前，使用者應該熟悉AEM。 瞭解AEM的基本概念 [此處](/help/sites-deploying/deploy.md).

### 瞭解AEM Mobile應用程式控制面板 {#understanding-the-aem-mobile-application-dashboard}

在瞭解角色和責任之前，使用者應該具備以下全面知識 **AEM Mobile控制中心** 或 **應用程式控制面板**. 按一下 [此處](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 以深入瞭解。

### AEM 管理员 {#aem-administrator}

一個 ***AEM管理員*** 負責透過使用建立精靈建立新應用程式，或匯入現有應用程式，將新應用程式新增至AEM Mobile目錄。 使用AEM Mobile建立新應用程式的AEM管理員 *建立精靈* 通常會從我們現成的參考範例或（大多數情況下）建立的自訂應用程式範本中，選取其中一個所需的應用程式範本 *AEM開發人員。*

使用AEM Mobile On-demand Services建立應用程式時，AEM管理員會負責下列工作：

* [設定AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [設定您的使用者和使用者群組](/help/mobile/aem-mobile-configure-users.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [管理內容服務](/help/mobile/developing-content-services.md)

若要開始使用管理員的角色和責任，請參閱 [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## AEM開發人員 {#aem-developer}

一個 **AEM開發人員** 延伸並建立自訂Web範本和元件，以讓*AEM Author *建立精美且吸引人的行動體驗。 這些範本和元件不僅已針對行動應用程式世界進行最佳化，而且可與裝置與全頻道服務端點的AEM伺服器（任何遠端伺服器）通訊。 AEM內建內容編輯器用於 *AEM作者* 在應用程式中建立豐富的相關體驗，包括與Adobe Marketing Cloud其他部分的整合。

使用AEM Mobile On-demand Services建立應用程式時，AEM開發人員會負責下列工作：

* [應用程式範本和元件](/help/mobile/app-templates-and-components1.md)
* [透過內容同步處理行動](/help/mobile/mobile-ondemand-contentsync.md)
* [內容屬性和匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [開發AEM Mobile內容服務](/help/mobile/developing-content-services.md)

若要開始使用開發人員的角色和責任，請參閱 [針對AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>一個 *AEM開發人員* 角色不會以範本和元件的開發開始和結束。 一個 *AEM開發人員* 可建立全新的應用程式，而不只是擴充現成的參考實作範例。

## AEM Author {#aem-author}

一個 ***AEM作者* (或 *行銷人員*)**使用自訂開發或現成可用的範本和元件來新增和編輯頁面、拖放元件，以及從DAM新增所有型別的媒體，包括影像、影片和文字片段（內容片段）。 AEM內建內容編輯器隨後由使用 *AEM作者* 在應用程式中建立豐富的相關體驗，包括與Adobe Marketing Cloud其他部分的整合。

使用AEM Mobile On-demand Services建立應用程式時，AEM作者必須瞭解下列主題：

* [AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [應用程式建立和設定動作](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [云配置](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [管理內容](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [內容服務概觀](/help/mobile/develop-content-as-a-service.md)

若要開始使用作者的角色和責任，請參閱 [為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>AEM作者也負責設定權益、建立卡片和版面配置，以及傳送推播通知。 此外，如需內容製作方法的詳細資訊；管理文章和集合；在AEM Mobile中建立橫幅、卡片和版面，請參閱 [AEM Mobile On-Demand入口網站](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
