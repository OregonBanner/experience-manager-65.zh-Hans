---
title: 手動設定與Adobe Target的整合
seo-title: Manually Configuring the Integration with Adobe Target
description: 瞭解如何手動設定與Adobe Target的整合。
seo-description: Learn how to manually configure the integration with Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
source-git-commit: c96f83b84ed1473aee0ddcca08a0e585ec088aa1
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 30%

---

# 手動設定與Adobe Target的整合 {#manually-configuring-the-integration-with-adobe-target}

您可以修改使用精靈時所做的選擇加入精靈設定，也可以手動與Adobe Target整合，而不使用精靈。

## 修改選擇加入精靈設定 {#modifying-the-opt-in-wizard-configurations}

此 [選擇加入精靈](/help/sites-administering/opt-in.md) 該 [整合AEM與Adobe Target](/help/sites-administering/target.md) 自動建立名為布建的Target設定的Target雲端設定。 精靈也會為名為「布建的目標架構」的雲端設定建立Target架構。 您可以視需要修改雲端設定和框架的屬性。

您也可以透過設定A4T Analytics Cloud設定，將Adobe Target設定為目標定位內容時，使用Adobe Target作為報表來源。

若要找到雲端設定和架構，請導覽至 **Cloud Services** 透過 **工具** > **部署** > **雲端**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))在Adobe Target下方，按一下或點選 **顯示設定**.

### 布建的目標組態屬性 {#provisioned-target-configuration-properties}

以下屬性值用於選擇加入精靈建立的布建目標設定雲端設定中：

* **使用者端代碼：** 如選擇加入精靈中所輸入。
* **電子郵件：** 如選擇加入精靈中所輸入。
* **密碼：** 如選擇加入精靈中所輸入。
* **API型別：** REST
* **從Adobe Target同步區段：** 已選取。

* **使用者端資源庫：** mbox.js.
* **使用DTM來提供使用者端資源庫：** 未選取。 選取此選項，如果 [使用DTM](/help/sites-administering/dtm.md) 或其他標籤管理系統，以託管mbox.js或AT.js檔案。 Adobe建議您使用DTM來傳遞程式庫，而非AEM。

* **自訂mbox.js：** 未指定任何專案，因此會使用預設的mbox.js檔案。 視需要指定要使用的自訂mbox.js檔案。 僅在您已選取mbox.js時顯示。
* **自訂AT.js：** 未指定以便使用預設的AT.js檔案。 視需要指定要使用的自訂AT.js檔案。 僅當您已選取AT.js時顯示。

>[!NOTE]
>
>在AEM 6.3中，您可以選取Target程式庫檔案 [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/)，這是新的Adobe Target實作程式庫，專為典型Web實作和單頁應用程式而設計。
>
>AT.js 对 mbox.js 库进行了多项改进：
>
>* 缩短了 Web 实现的页面加载时间
>* 提高了安全性
>* 改善了针对单页应用程序的实施选项
>* AT.js包含target.js中所包含的元件，因此不再需要呼叫target。


<!-- OLD URL WHICH IS 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### 布建的目標架構屬性 {#provisioned-target-framework-properties}

選擇加入精靈建立的布建目標架構已設定為從設定檔資料存放區傳送內容資料。 依預設，會將存放區的年齡和性別資料專案傳送至Target。 您的解決方案可能需要傳送其他引數。

![chlimage_1-158](assets/chlimage_1-158.png)

您可以設定架構以傳送其他內容資訊至Target，如所述 [新增目標框架](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### 設定A4T Analytics Cloud設定 {#configuring-a-t-analytics-cloud-configuration}

您可以設定Adobe Target，以便在鎖定目標內容時使用Adobe Analytics作為報表來源。

>[!NOTE]
>
>使用者認證驗證（舊版）無法搭配A4T使用（適用於Target和Analytics）。 因此，客戶應使用IMS驗證，而不是使用者認證驗證。

若要這麼做，您必須指定要將您的Adobe Target雲端設定與以下專案連結的A4T雲端設定：

1. 導覽至 **Cloud Services** 透過 **AEM標誌** > **工具** > **部署** > **Cloud Services**.
1. 在 **Adobe Target** 部分中，单击&#x200B;**立即配置**。
1. 重新連線至您的Adobe Target設定。
1. 在 **A4T Analytics Cloud設定** 下拉式功能表，選取架構。

   >[!NOTE]
   >
   >只有啟用A4T的Analytics設定才可使用。
   >
   >使用AEM設定A4T時，您可能會看到遺漏專案的「組態」參考。 若要選取分析框架，請執行下列動作：
   >
   >1. 導覽至 **工具** > **一般** > **CRXDE Lite**.
   1. 導覽至 [A4T分析設定對話方塊](#a4t-analytics-config-dialog) （請參閱下文）
   1. 設定屬性 **disable** 至 **false**.
   1. 點選或按一下 **全部儲存**.


#### A4T分析設定對話方塊 {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

单击&#x200B;**确定**。使用Adobe Target鎖定目標內容時，您可以 [選取您的報表來源](/help/sites-authoring/content-targeting-touch.md).

## 手動與Adobe Target整合 {#manually-integrating-with-adobe-target}

手動與Adobe Target整合，而不使用選擇加入精靈。

>[!NOTE]
Target 库文件 [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/) 是 Adobe Target 的新实施库，专为典型的 Web 实施和单页应用程序而设计。Adobe 建议您使用 AT.js 而不是 mbox.js 作为客户端库。
AT.js 对 mbox.js 库进行了多项改进：
* 缩短了 Web 实现的页面加载时间
* 提高了安全性
* 改善了针对单页应用程序的实施选项
* AT.js 包含 target.js 具有的组件，因此不再调用 target.js
>
您可以在&#x200B;**客户端库**&#x200B;下拉菜单中选择 AT.js 或 mbox.js。

<!-- OLD URL from above was 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### 创建 Target 云配置 {#creating-a-target-cloud-configuration}

要启用 AEM 以便与 Adobe Target 交互，请创建 Target 云配置。要创建配置，您需要提供 Adobe Target 客户端代码和用户凭据。

您只需创建一次 Target 云配置，因为您可以将该配置与多个 AEM 活动关联。如果您有多个 Adobe Target 客户端代码，请为每个客户端代码创建一个配置。

您可以配置云配置以从 Adobe Target 同步片段。如果您啟用同步，儲存雲端設定時，會在背景從Target匯入區段。

使用以下过程可在 AEM 中创建 Target 云配置：

1. 導覽至 **Cloud Services** 透過 **AEM標誌** > **工具** > **Cloud Services** > **舊版Cloud Services**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   此 **Cloud Services** 概觀頁面隨即開啟。

1. 在 **Adobe Target** 部分中，单击&#x200B;**立即配置**。
1. 在&#x200B;**创建配置**&#x200B;对话框中：

   1. 为配置提供&#x200B;**标题**。
   1. 选择 **Adobe Target 配置**&#x200B;模板。
   1. 单击&#x200B;**创建**。

   此时将打开编辑对话框。

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   使用AEM設定A4T時，您可能會看到遺漏專案的「組態」參考。 若要選取分析框架，請執行下列動作：
   1. 導覽至 **工具** > **一般** > **CRXDE Lite**.
   1. 導覽至 **/libs/cq/analytics/components/testandtargetpage/dialog/items/tables/items/tab1_general/items/a4tAnalyticsConfig**
   1. 設定屬性 **disable** 至 **false**.
   1. 點選或按一下 **全部儲存**.


1. 在對話方塊中，提供這些屬性的值。

   * **客户端代码**：Target 帐户的客户端代码
   * **電子郵件**：Target帳戶電子郵件。
   * **密碼**：Target帳戶密碼。
   * **API型別**：REST或XML
   * **A4T Analytics Cloud設定**：選取用於Target活動目標和量度的Analytics Cloud設定。 如果您在鎖定目標內容時使用Adobe Analytics作為報表來源，則需要此設定。 如果您沒有看到雲端設定，請參閱中的注意事項 [設定A4T Analytics Cloud設定](#configuring-a-t-analytics-cloud-configuration).

   * **使用准确定位：**&#x200B;默认情况下，此复选框处于选中状态。如果選取，雲端服務設定會等待內容載入後再載入內容。 请参阅以下注释。
   * **從Adobe Target同步區段：** 選取此選項，您就可以下載Target中定義的區段，以便在AEM中使用它們。 當「API型別」屬性為REST時，選取此選項，因為不支援內嵌區段，且您必須使用Target中的區段。 (「區段」的AEM辭彙等同於目標「對象」。)
   * **使用者端資源庫：** 選取您想要使用mbox.js或AT.js使用者端資料庫。
   * **使用DTM來提供使用者端資源庫**  — 選取此選項可使用DTM或其他標籤管理系統中的AT.js或mbox.js。 設定 [DTM整合](/help/sites-administering/dtm.md) 以使用此選項。 Adobe建議您使用DTM來傳遞程式庫，而非AEM。
   * **自訂mbox.js**：如果您已核取DTM方塊或使用預設的mbox.js，請留空。 或者，您也可以上傳自訂mbox.js。 僅在您已選取mbox.js時顯示。
   * **自訂AT.js**：如果您已核取DTM方塊或使用預設的AT.js，請留空。 或者，您也可以上傳自訂AT.js。 僅當您已選取AT.js時顯示。

   >[!NOTE]
   默认情况下，当您选择加入 Adobe Target 配置向导时，将启用“准确定位”。
   准确定位意味着，云服务配置将等到上下文加载完后，再加载内容。因此，就性能而言，准确定位可能会导致加载内容前有几毫秒的延迟。
   对于创作实例，“准确定位”始终处于启用状态。但在发布实例上，您可以通过清除云服务配置中“准确定位”旁边的复选标记来选择全局关闭准确定位 (**http://localhost:4502/etc/cloudservices.html**)。无论您在云服务配置中的设置如何，您都可以为各个组件打开和关闭“准确定位”。
   如果您&#x200B;***已经***&#x200B;创建目标组件并更改此设置，则您的更改不会影响这些组件。直接變更這些元件。

1. 单击&#x200B;**连接到 Target** 可初始化与 Target 的连接。如果连接成功，则将显示消息&#x200B;**连接成功**。单击消息上的&#x200B;**确定**，然后单击对话框上的&#x200B;**确定**。

   如果无法连接到 Target，请参阅[疑难解答](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems)部分。

### 添加 Target 框架 {#adding-a-target-framework}

配置 Target 云配置后，可以添加 Target 框架。此架構會識別從可用傳送至Adobe Target的預設引數 [使用者端內容](/help/sites-administering/client-context.md) 或 [ContextHub](/help/sites-developing/ch-configuring.md) 元件。 Target 使用参数来确定适用于当前上下文的分段。

您可以为单个 Target 配置创建多个框架。您必須針對網站的不同區段傳送一組不同的引數至Target時，多個架構會很有用。 為您傳送的每組引數建立架構。 将网站的每个部分与适当的框架关联。一個網頁一次只能使用一個架構。

1. 在Target設定頁面上，按一下 **+** （加號）。
1. 在“创建框架”对话框中，指定&#x200B;**标题**，选择 **Adobe Target 框架**，然后单击&#x200B;**创建**。

   ![chlimage_1-161](assets/chlimage_1-161.png)

   这将打开框架页面。Sidekick提供的元件代表來自 [使用者端內容](/help/sites-administering/client-context.md) 或 [ContextHub](/help/sites-developing/ch-configuring.md) 您可以對應哪些物件。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 将表示要用于映射的数据的客户端上下文组件拖动到放置目标。或者，将 **ContextHub 存储**&#x200B;组件拖动到框架。

   >[!NOTE]
   映射时，参数通过简单字符串传递给 mbox。无法从 ContextHub 映射数组。

   例如，若要使用 **設定檔資料** 關於控制您的Target促銷活動的網站訪客，請拖曳 **設定檔資料** 元件至頁面。 可用于映射到 Target 参数的配置文件数据变量随即显示。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 通过选中相应列中的&#x200B;**共享**&#x200B;复选框，选择要对 Adobe Target 系统可见的变量。

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   同步参数是唯一方式 – 从 AEM 到 Adobe Target。

此时将创建您的框架。要将框架复制到发布实例，请使用 sidekick 中的&#x200B;**激活框架**&#x200B;选项。

### 將活動與Target雲端設定建立關聯  {#associating-activities-with-the-target-cloud-configuration}

建立您的關聯 [AEM活動](/help/sites-authoring/activitylib.md) 雲端設定，以便映象中的活動 [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
可用的活动类型由以下因素决定：
* 如果 **xt_only** 在AEM端使用的Adobe Target租使用者(clientcode)上啟用選項以連線至Adobe Target，然後您可以建立 **僅限** AEM中的XT活動。
* 如果 **xt_only** 選項為 **not** 已在Adobe Target租使用者(clientcode)上啟用，然後您可以建立 **兩者** AEM中的XT和A/B活動
>
**其他附註：** **xt_only** 選項是套用至特定Target租使用者(clientcode)的設定，且只能在Adobe Target中直接修改。 您无法在 AEM 中启用或禁用此选项。

### 將Target架構與您的網站建立關聯 {#associating-the-target-framework-with-your-site}

在AEM中建立Target架構後，請建立網頁與架構的關聯。 頁面上的目標元件會將框架定義的資料傳送至Adobe Target進行追蹤。 (請參閱 [內容目標定位](/help/sites-authoring/content-targeting-touch.md).)

將頁面與框架建立關聯時，子頁面會繼承關聯。

1. 在 **網站** 主控台，導覽至您要設定的網站。
1. 使用 [快速動作](/help/sites-authoring/basic-handling.md#quick-actions) 或 [選擇模式](/help/sites-authoring/basic-handling.md)，選取 **檢視屬性。**
1. 选择&#x200B;**云服务**&#x200B;选项卡。
1. 点按/单击&#x200B;**编辑**。
1. 點選/按一下 **新增設定** 在 **Cloud Service設定** 並選取 **Adobe Target**.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 選取您想要在其下的架構 **設定參考**.

   >[!NOTE]
   請務必選取 **框架** 不是您建立的Target雲端設定，而是在其中建立雲端設定。

1. 點選/按一下 **完成**.
1. 啟動網站的根頁面，以便將其復寫至發佈伺服器。 (請參閱 [如何發佈頁面](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   如果您附加至頁面的框架尚未啟動，則會開啟精靈，供您一併發佈。

## 疑難排解Target連線問題 {#troubleshooting-target-connection-problems}

若要疑難排解連線至Target時發生的問題，您可以執行下列工作：

* 請確定您提供的使用者認證正確無誤。
* 請確定AEM執行個體可以連線至Target伺服器。 例如，請確定防火牆規則並未封鎖輸出AEM連線，或是AEM已設定為使用必要的代理程式。
* 在AEM錯誤記錄檔中尋找有用的訊息。 error.log檔案位於 **crx-quickstart/logs** 安裝AEM的目錄。
* 在Adobe Target中編輯活動時，URL會指向localhost。 將AEM Externalizer設定為正確的URL，以解決此問題。
