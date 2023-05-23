---
title: OSGI組合
seo-title: OSGI Bundles
description: 管理OSGi套裝的秘訣
seo-description: Tips for managing your OSGi bundles
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# OSGI組合{#osgi-bundles}

## 使用語意版本設定 {#use-semantic-versioning}

語意版本編號的商定最佳實務可在 [https://semver.org/](https://semver.org/).

## 不要內嵌超過OSGi套件組合嚴格需要的類別和jar {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

通用程式庫應分解為個別的組合。 這可讓您在套件組合中重複使用它們。 包裝時 *JAR* 在OSGI套件組合中，請務必檢查線上來源，以檢視是否有人之前已執行此動作。 尋找現有套件組合包裝的常見位置包括：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse套件組合配方和SpringSource企業套件組合存放庫。

## 取決於所需的最低套件組合版本 {#depend-on-the-lowest-needed-bundle-versions}

針對POM檔案中的編譯時間相依性，一律取決於公開所需API的最低所需版本。 這樣可允許更高的回溯相容性，並使得對舊版進行反向移植修正更容易。

## 從OSGi套件組合匯出最小套件集 {#export-a-minimal-set-of-packages-from-osgi-bundles}

一旦匯出套件後，我們就會建立供其他人依賴的API。 請務必儘可能減少匯出次數，並確認要匯出的內容為API。 取得私密方法/類別並將其設為公用比取得先前匯出的內容並將其設為私密要容易得多。

實作應一律放在另一個檔案中 *實作* 封裝。 根據預設， *maven-bundle-plugin* 將會匯出專案中沒有 *實作* 在其名稱中。

## 一律明確定義每個匯出套件的語意版本 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

這可讓您API的消費者與您一同演化。 在這樣做時，請一律遵循語義版本設定最佳實務。 這可讓您API的消費者知道新版本中預期的變更型別。

## 在公開處包含中繼資料型別資訊 {#include-metatype-information-where-exposed}

藉由指定有意義的中繼型別資訊，讓您的服務和元件在Felix主控台中更容易理解。 SCR註釋和屬性清單可在以下網址找到： [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
