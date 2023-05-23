---
title: 開發AEM商務
description: 瞭解如何使用AEM專案原型產生啟用AEM的商務專案。 瞭解如何建立專案並將其部署至本機開發環境。
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
source-git-commit: 78359fb8ecbcc0227ab5a3910175aed73d823902
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 8%

---

# 開發AEM商務 {#develop}

根據Commerce Integration Framework (CIF)為AEM開發AEM專案會遵循與其他AEM專案相同的規則和最佳實務。 請先檢閱下列內容：

- [AEM 6.5 Developing 用户指南](/help/sites-developing/home.md)
- [AEM核心概念](/help/sites-developing/the-basics.md)
- [AEM開發 — 指導方針與最佳作法](/help/sites-developing/dev-guidelines-bestpractices.md)
- [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md)

## AEM Commerce的本機開發 {#local}

建議使用本機開發環境搭配CIF專案使用。

>[!NOTE]
>
>下列指示可協助您使用CIF搭配AEM 6.5的焦點，為AEM Commerce設定本機AEM開發環境)。 如果您是使用AEMas a Cloud Service，請參閱 [AEM Commerceas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html) 說明檔案。

適用於AEM 6.5的AEM Commerce附加元件。 CIF附加元件也可用於本機開發，並以AEM套件的形式提供。 您可從以下網址下載： [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 作為Feature Pack。

### 必要軟體

下列專案應在本機安裝：

- 本機AEM 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7或更新版本
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) （3.3.9或更新版本）
- [節點LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 存取CIF附加元件

CIF附加元件可從以下網址下載： [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)，搜尋「AEM Commerce附加元件」。

>[!TIP]
>
>請務必使用最新的CIF附加元件版本。

### 本機設定

對於使用AEM和CIF附加元件的本機CIF專案開發，請執行以下步驟：

1. 取得AEM 6.5版本並安裝AEM 6.5 Service Pack。 AEM 6.5 Service Pack 7為必要版本，但建議您安裝最後一個可用的Service Pack。

1. 解壓縮AEM .jar以建立 `crx-quickstart` 資料夾，執行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立 `crx-quickstart/install` 資料夾

1. 將從軟體發佈入口網站下載的CIF附加元件所有套件複製到 `crx-quickstart/install` 資料夾。

>[!TIP]
>
>或者，您也可以透過Package Manager安裝CIF附加元件套件。

1. 啟動AEM快速入門

透過OSGI主控台驗證設定： `http://localhost:4502/system/console/osgi-installer`. 此清單應包括CIF附加元件相關的組合、內容套件和OSGI設定。 請確定所有套件組合都已啟動。

## 项目设置 {#project}

有兩種方法可使用CIF啟動AEM Commerce專案。

### 使用AEM專案原型

此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 是啟動預先設定的專案以開始使用CIF的主要工具。 產生的專案中可包含CIF核心元件和所有必要的設定，並提供一個額外的選項。

>[!TIP]
>
>使用 [AEM專案原型25或更新版本](https://github.com/adobe/aem-project-archetype/releases) 以產生專案。

請參閱AEM專案原型 [使用指示](https://github.com/adobe/aem-project-archetype#usage) 如何產生AEM專案。 若要將CIF納入專案，請使用 `includeCommerce` 選項。

例如：

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF核心元件可透過包含提供的 `all` 套件或個人使用CIF內容套件和相關OSGI套件組合。 若要手動將CIF核心元件新增至專案，請使用下列相依性：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### 使用AEM Venia參考存放區

啟動CIF專案的第二個選項是複製並使用 [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store是範例參考店面應用程式，可示範AEM的CIF核心元件的使用方式。 其目的是作為一組最佳實務範例，以及開發您自己的功能的潛在起點。

若要開始使用Venia Reference Store，只要複製 [Git存放庫](https://github.com/adobe/aem-cif-guides-venia) 並開始根據您的需求自訂專案。

>[!NOTE]
>
>Venia Reference Store專案包含AEMas a Cloud Service和AEM 6.5的兩個組建設定檔。檢查 [專案readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) 以瞭解其使用方式。 若為AEM 6.5，請使用 `classic` 設定檔。

### 將AEM連線至商務系統

若要將您的專案連線到商務系統，AEM必須設定為您的商務系統的GraphQL端點。

兩者，均為產生的專案 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 或 [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)，已包含 [預設設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) 必須調整的專案。

取代 `url` 在 `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` 與專案所使用的商務系統的GraphQL端點搭配使用。

AEM Commerce附加元件和CIF核心元件會透過AEM伺服器和直接透過瀏覽器，連線至商務GraphQL端點。 使用者端CIF核心元件和CIF附加撰寫工具預設會連線至 `/api/graphql`. 如有需要，可透過CIFCloud Service設定（請參閱下文）調整此設定。

CIF附加元件提供GraphQL Proxy servlet，位於 `/api/graphql`. 如果您不打算使用本機AEM Dispatcher，建議同時設定GraphQL Proxy servlet。

導覽至http://localhost:4502/system/console/configMgr ，並為建立OSGI設定 `Adobe CIF GraphQL Proxy Configuration` 服務。 使用與上述用於GraphQL使用者端相同的商務系統GraphQL端點。

## 其他资源

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
