---
title: 選擇使用Adobe Analytics和Adobe Target
seo-title: Opting Into Adobe Analytics and Adobe Target
description: 瞭解如何選擇加入Adobe Analytics和Adobe Target。
seo-description: Learn how to opt into Adobe Analytics and Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
exl-id: 3603e929-2aa1-4c25-ad9a-b10ff52a59f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 10%

---

# 選擇使用Adobe Analytics和Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM有一個選擇加入程式，可協助您整合Adobe Analytics和Adobe Target。 這是現成可用的功能，可作為指派給管理員使用者群組的預先載入任務。

當您以管理員身分登入時，此工作(**設定分析和定位**)可從取得。 [收件匣](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). 它會根據您提供的認證，協助您設定和整合這些服務。

您有以下選項可設定整合：

* 透過任務設定整合。

   您可以立即執行或稍後執行，在執行某些動作之前，工作將保留在收件匣中。 無論哪種情況，設定都可直接在UI中完成，或使用預先定義的 `.properties` 檔案。

* 選擇退出整合。

   如果您偏好使用此選項 [手動設定整合](/help/sites-administering/marketing-cloud.md). 另請參閱 [使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* 使用指令碼來設定設定和布建。

## 設定整合 {#configuring-the-integration}

選擇加入與下列專案的整合：

* Analytics可讓您使用其頁面追蹤和分析功能。
* Target以啟用其個人化功能。

無論是哪一個選項，您都需要提供使用者帳戶資訊，並指定追蹤的頁面。

>[!NOTE]
>
>您可以選擇使用在伺服器啟動時讀取的屬性檔案來提供Analytics和Target帳戶資訊。 另請參閱 [使用屬性檔案提供帳戶資訊](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

當您選擇加入整合時，AEM會執行下列工作：

* 建立可連線至Analytics和Target的雲端設定。
* 建立可決定所追蹤資料的架構。
* 設定網頁以使用這些服務。

>[!NOTE]
>
>AT.js是預設的使用者端資料庫。 這是在「 」下設定的 [target cloud services設定](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration).
>
>Adobe建議您使用AT.js作為使用者端程式庫。

若要選擇加入預先載入的現成工作：

1. 從您的 [收件匣，選取和 **開啟** 設定分析和定位](/help/sites-authoring/inbox.md#taking-action-on-an-item) 任務。

   ![optin-01](assets/optin-01.png)

1. 若為Analytics：

   1. 輸入Analytics的使用者帳戶資訊，然後按一下對應的 **新增** 按鈕。
   1. 已驗證適當的認證。
   1. Analytics帳戶通過驗證後，請選取要使用的Analytics報表套裝。 AEM會擷取這些Analytics報表套裝。 狀態已更新至 **已新增**.

1. 針對Target：

   1. 輸入Target的使用者帳戶資訊，然後按一下對應的 **新增** 按鈕。
   1. 已驗證適當的認證。 狀態已更新至 **已新增**.

1. 选择&#x200B;**下一步**。
1. 選取應使用Analytics和/或Target的網站。

1. 選取 **完成** 完成。

   >[!CAUTION]
   >
   >選擇加入設定後，您需要發佈受影響的網站/頁面，將這些變更復寫至您的發佈執行個體。

## 選擇退出整合 {#opting-out-of-the-integration}

符合下列任一條件時，請退出與Analytics和Target的整合：

* 不想與這些產品整合。
* 偏好手動設定整合。

   如需手動設定整合的相關資訊，請參閱 [與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md) 和 [與Adobe Target整合](/help/sites-administering/target.md).

若要選擇退出，您必須完成預先載入的工作：

* 從您的 [收件匣，選取和 **完成** 設定分析和定位](/help/sites-authoring/inbox.md#taking-action-on-an-item) 任務。

## 使用屬性檔案提供帳戶資訊 {#providing-account-information-using-a-properties-file}

安裝AEM在伺服器啟動時讀取的屬性檔案，以設定帳戶屬性，與Analytics和Target整合。 當您使用屬性檔案時，選擇加入精靈會自動使用檔案中的屬性，並據此建立雲端設定。

屬性檔案是名為marketingcloud.properties的文字檔，您儲存在AEM處理序正在使用的工作目錄中（通常是與JAR檔案相同的目錄）。 檔案包含下列屬性：

* analytics.server：您使用的Analytics資料中心的URL。
* analytics.company：與您的Analytics使用者帳戶相關聯的公司。
* analytics.username：您的Analytics使用者名稱。
* analytics.secret：與您的Analytics使用者名稱相關聯的密碼。
* analytics.reportsuite：要使用的Analytics報表套裝名稱。
* target.clientcode：與您的Target帳戶相關聯的使用者端代碼。
* target.email：用於驗證Target帳戶的電子郵件地址。
* target.password：與您的電子郵件地址相關聯的密碼。

屬性和值以等號(=)分隔。 Analytics屬性會加上前置詞 `analytics`，且Target屬性會加上前置詞 `target`. 若要設定服務，請為該服務的所有屬性提供值。 如果您不想設定服務，則不要提供該服務的值。

以下範例 `.properties` 檔案包含用於建立Analytics雲端設定的屬性值：

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

以下程式說明如何使用屬性檔案選擇加入整合。

1. 建立 `marketingcloud.properties` 工作目錄中的AEM處理序所使用的檔案（製作例項）。

   >[!NOTE]
   >
   >工作目錄通常是儲存jar或 `license.properties` 檔案。
   >
   >不過，它也可以由系統屬性定義為絕對路徑：
   >
   >`mac.provisioning.file.container`

1. 根據您的Analytics和/或Target帳戶新增屬性值。
1. 啟動或重新啟動伺服器，然後使用系統管理員帳戶登入。
1. 開啟設定分析和鎖定目標工作，如所述 [設定整合](/help/sites-administering/opt-in.md#configuring-the-integration). 精靈不會要求您的帳戶資訊，而是會使用 `.properties` 檔案。

   選取 **新增** 取得適當的服務，然後繼續執行精靈。

   ![optin-02](assets/optin-02.png)

## 關於雲端設定 {#about-the-cloud-configurations}

當您設定與Analytics和Target的整合時，AEM會自動建立所需的雲端設定和架構。 例如，Analytics雲端設定稱為「已布建的Analytics帳戶」。

您不需要變更雲端設定。 不過，您可以視需要設定架構。 (請參閱 [將元件資料與Adobe Analytics屬性對應](/help/sites-administering/adobeanalytics-mapping.md) 和 [新增目標框架](/help/sites-administering/target.md).)

>[!NOTE]
>
>默认情况下，当您选择加入 Adobe Target 配置向导时，将启用“准确定位”。
>
>准确定位意味着，云服务配置将等到上下文加载完后，再加载内容。因此，就性能而言，准确定位可能会导致加载内容前有几毫秒的延迟。
>
>对于创作实例，“准确定位”始终处于启用状态。但在发布实例上，您可以通过清除云服务配置中“准确定位”旁边的复选标记来选择全局关闭准确定位 (**http://localhost:4502/etc/cloudservices.html**)。无论您在云服务配置中的设置如何，您都可以为各个组件打开和关闭“准确定位”。
>
>如果您&#x200B;***已经***&#x200B;创建目标组件并更改此设置，则您的更改不会影响这些组件。您必须直接对这些组件进行任何更改。

>[!CAUTION]
>
>當您選擇加入Analytics設定和特定的 `reportsuite` ，則架構會限製為發佈執行模式。 這表示追蹤僅適用於發佈執行個體。
>
>如果編寫執行個體上需要追蹤，則值應變更為 `all`.

## 透過Script設定設定和布建 {#configuring-the-setup-and-provisioning-via-script}

作為管理員，您可能想要使用指令碼觸發設定和布建，而不是手動逐步執行精靈。 您可以透過以下方式達成此目的：

* 傳送POST要求至 **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** ，並使用必要的引數。

您傳送哪些引數取決於下列專案：

* 如果您想使用 **marketingcloud.properties** 填入所有必要認證的檔案，然後您必須傳送下列引數：

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=要附加已建立雲端服務設定的AEM頁面路徑

   例如，同時建立Analytics和Target設定，並將它們附加至we.retail頁面的curl請求將是：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* 如果您不想使用 **marketingcloud.properties** 檔案之後，您必須傳送認證及引數；例如：

   * 自動布建= `true`
   * servicename= `analytics|target`
   * path=路徑至AEM頁面，以附加已建立的雲端服務設定；可以定義多個路徑
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

   在此情況下，同時建立Analytics和Target設定，並將它們附加至We-Retail頁面的curl要求將是：

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```
