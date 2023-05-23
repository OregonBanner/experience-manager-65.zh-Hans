---
title: AEM Content and Commerce入門
description: 瞭解如何部署AEM內容與商務專案。
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 5%

---

# AEM Content and Commerce入門 {#start}

若要開始使用AEM Content and Commerce，您必須安裝適用於AEM 6.5的AEM Content and Commerce附加元件。

## 最低軟體需求

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 需要7或更新版本。

## 入门培训 {#onboarding}

AEM Content and Commerce入門有兩個步驟：

1. 安裝適用於AEM 6.5的AEM Content and Commerce附加元件

2. 將AEM與您的商務解決方案連線

### 安裝適用於AEM 6.5的AEM Content and Commerce附加元件 {#install-add-on}

從下載並安裝適用於AEM 6.5的AEM Commerce附加元件 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 入口網站。

啟動並安裝必要的AEM 6.5 Service Pack。 建議您安裝最後一個可用的Service Pack。

>[!NOTE]
>
>CSE將針對AEM Managed Service客戶完成這項工作。

### 將AEM連線至您的Commerce系統 {#connect}

AEM可連線至任何具有AEM的可存取GraphQL端點的商務系統。 這些端點通常是公開可用的，或者可以根據個別專案設定透過私人VPN或本機連線來連線。

可選擇是否提供驗證標頭，以使用需要驗證的其他CIF功能。

產生的專案 [AEM專案原型](https://github.com/adobe/aem-project-archetype)，以及 [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia) 此專案已包含在 [預設設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) 必須調整。

取代 `url` 在 `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` 商務系統的GraphQL端點。 此設定可以透過OSGI主控台完成，或透過專案部署OSGI設定來完成。 使用不同的AEM執行模式支援中繼和生產系統的不同設定。

AEM Content and Commerce附加元件和CIF核心元件同時使用AEM伺服器端和使用者端連線。 使用者端CIF核心元件和CIF附加撰寫工具預設會連線至 `/api/graphql`. 如有需要，可透過CIFCloud Service設定調整此設定（請參閱下文）。

CIF附加元件提供GraphQL Proxy servlet，位於 `/api/graphql` 可選擇用於 [本機開發](develop.md). 對於生產部署，強烈建議透過AEM Dispatcher或其他網路層（例如CDN）設定商務GraphQL端點的反向Proxy。

## 設定存放區和目錄 {#catalog}

附加元件和 [CIF Core Components](https://github.com/adobe/aem-core-cif-components) 可用於連線至不同商業商店（或商店檢視等）的多個AEM網站結構。 根據預設，CIF附加元件會以預設設定部署，並連線至Adobe Commerce的預設存放區和目錄。

您可以按照以下步驟，透過CIFCloud Service設定來針對專案調整此設定：

1. 在AEM中前往「工具 — >Cloud Services-> CIF設定」

2. 選取您要變更的商務設定

3. 透過動作列開啟設定屬性

![CIFCloud Services設定](/help/commerce/cif/assets/cif-cloud-service-config.png)

可設定下列屬性：

- GraphQL使用者端 — 選取已設定的GraphQL使用者端以進行商務後端通訊。 這通常應該保持在預設值。
- 存放區檢視 — 存放區檢視識別碼。 如果為空，則使用預設存放區檢視。
- GraphQL Proxy路徑 — AEM中的GraphQL Proxy用來將請求代理至商務後端GraphQL端點的URL路徑。

   >[!NOTE]
   >
   >在大多數設定中，預設值 `/api/graphql` 不可變更。 只有不使用所提供的GraphQL Proxy的進階設定才應變更此設定。

- 啟用目錄UID支援 — 在商務後端GraphQL呼叫中啟用UID而非ID支援。

   >[!NOTE]
   >
   >Adobe Commerce 2.4.2匯入UID支援。只有在您的Commerce後端支援2.4.2版或更新版本的GraphQL結構描述時，才會啟用此功能。

- 目錄根類別識別碼 — 商店目錄根的識別碼（UID或ID）

   >[!CAUTION]
   >
   >從CIF Core Components 2.0.0版開始，支援 `id` 已移除並取代為 `uid`. 如果您的專案使用CIF核心元件2.0.0版，您必須啟用目錄UID支援，並使用有效的類別UID作為「目錄根類別識別碼」。

以上所示的設定僅供參考。 專案應提供自己的設定。

如需使用多個AEM網站結構與不同商業目錄結合的更複雜設定，請參閱 [Commerce多商店設定](configuring/multi-store-setup.md) 教學課程。

## 其他资源 {#additional-resources}

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce多商店設定](configuring/multi-store-setup.md)
