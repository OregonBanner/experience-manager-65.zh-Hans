---
title: 將Adobe Sign與AEM Forms整合
seo-title: Integrate Adobe Sign with AEM Forms
description: 瞭解如何設定適用於AEM Forms的Adobe Sign
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 25%

---

# 整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 啟用最適化表單的電子簽章工作流程。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在一般情況下 [!DNL Adobe Sign] 在最適化表單情境下，使用者填寫最適化表單以 **申請服務**. 例如，信用卡申请表和公民权益表。在用户填写、签署和提交申请表后，该表将发送给服务提供商以执行后续操作。服务提供商将审核申请，并使用 [!DNL Adobe Sign] 将申请标记为已批准。若要啟用類似的電子簽章工作流程，您可以整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms].

使用 [!DNL Adobe Sign] 使用AEM [!DNL Forms]，設定 [!DNL Adobe Sign] 在AEM雲端服務中：

## 前提条件 {#prerequisites}

您需要下列專案才能整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms]：

* 作用中 [Adobe Sign開發人員帳戶。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 一個 [SSL已啟用](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 伺服器。
* [Adobe Sign API 应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API 应用程序的凭据（客户端 ID 和客户端密码）。
* 重新設定時，移除現有的 [!DNL Adobe Sign] 來自作者和發佈執行個體的設定。
* 针对创作实例和发布实例，使用[相同的加密密钥](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 設定 [!DNL Adobe Sign] 使用AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

已具備下列先決條件後，請執行以下步驟來設定 [!DNL Adobe Sign] 使用AEM [!DNL Forms] 在作者執行個體上：

1. 在AEM上 [!DNL Forms] 作者執行個體，導覽至 **工具** ![槌子](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**.
1. 於 **[!UICONTROL 設定瀏覽器]** 頁面，點選 **[!UICONTROL 建立]**.
   * 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定 **[!UICONTROL 標題]** 針對設定，啟用 **[!UICONTROL 雲端設定]**，然後點選 **[!UICONTROL 建立]**. 它會建立雲端服務的設定容器。
1. 導覽至 **工具** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** 並選取您在上一步中建立的設定容器。

   >[!NOTE]
   >
   >您可以執行步驟1至4來建立新的設定容器並建立 [!DNL Adobe Sign] 容器中的設定或使用現有的 `global` 資料夾位於 **工具** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 如果您在新設定容器中建立設定，請務必在 **[!UICONTROL 設定容器]** 欄位建立最適化表單時。

   >[!NOTE]
   確定雲端服務設定頁面的URL開頭為 **HTTPS**. 如果沒有， [啟用SSL](/help/sites-administering/ssl-by-default.md) 適用於AEM [!DNL Forms] 伺服器。

1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] AEM中的設定 [!DNL Forms].
1. 在 **[!UICONTROL 一般]** 的標籤 **[!UICONTROL 建立Adobe Sign設定]** 頁面，指定 **[!UICONTROL 名稱]** 設定並點選 **[!UICONTROL 下一個]**. 您可以選擇指定標題並瀏覽以選取設定的縮圖。

1. 将当前浏览器窗口中的 URL 复制到记事本。需要設定 [!DNL Adobe Sign] 使用AEM的應用程式[!DNL Forms].

1. 在 **[!UICONTROL 設定]** 標籤， **[!UICONTROL OAuth URL]** 欄位包含預設URL。 URL 的格式为：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 指默认数据库分片。您可以修改数据库分片的值。确保 [!DNL  Adobe Sign] 云配置指向[正确分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   如果为 Adobe Experience Manager 功能或组件创建另一个 [!DNL Adobe Sign] 配置，请确保所有 [!DNL Adobe Sign] 云配置指向同一分片。

   >[!NOTE]
   保留 **建立Adobe Sign設定** 頁面開啟。 不要關閉它。 您可以擷取 **使用者端ID** 和 **使用者端密碼** 設定的OAuth設定後 [!DNL Adobe Sign] 應用程式，如未來步驟所述。


1. 配置 [!DNL Adobe Sign] 应用程序的 OAuth 设置：

   1. 開啟瀏覽器視窗並登入 [!DNL Adobe Sign] 開發人員帳戶。
   1. 選取為AEM設定的應用程式 [!DNL Forms]，然後點選 **[!UICONTROL 設定應用程式的OAuth]**.
   1. 複製 **[!UICONTROL 使用者端ID]** 和 **[!UICONTROL 使用者端密碼]** 記事本。
   1. 在 **[!UICONTROL 重新導向URL]** 方塊中，新增在上一步中複製的HTTPS URL。
   1. 啟用下列OAuth設定 [!DNL Adobe Sign] 應用程式並按一下 **[!UICONTROL 儲存]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   有关为 [!DNL Adobe Sign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)开发人员文档。

   ![OAuth 配置](assets/oauthconfig_new.png)

1. 返回 **[!UICONTROL 建立Adobe Sign設定]** 頁面。 在 **[!UICONTROL 設定]** 標籤， **[!UICONTROL OAuth URL]** 欄位提及預設URL。 URL 的格式为：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 指默认数据库分片。

   您可以修改数据库分片的值。重新啟動伺服器，以便能夠使用資料庫分片的新值。

   >[!NOTE]
   確保您的作者和發佈執行個體設定指向相同分片。 如果您為組織建立多個Adobe Sign設定，請確定所有設定都使用相同分片。

1. 返回 **[!UICONTROL 建立Adobe Sign設定]** 頁面。 在 **[!UICONTROL 設定]** 索引標籤中，指定 **使用者端ID** （也稱為應用程式ID）和 **使用者端密碼**. 使用 [Adobe Sign應用程式的使用者端ID和使用者端密碼](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 已為AEM Forms建立。

1. 選取 **[!UICONTROL 也啟用附件的Adobe Sign]** 用於將附加到最適化表單的檔案附加至對應 [!DNL Adobe Sign] 檔案已傳送供簽署。

1. 點選 **[!UICONTROL 連線至Adobe Sign]**. 在系统提示输入凭据时，提供在创建 [!DNL Adobe Sign] 应用程序时所用帐户的用户名和密码。

1. 點選 **[!UICONTROL 建立]** 建立 [!DNL Adobe Sign] 設定。

1. 開啟AEM Web Console。 URL是 `https://'[server]:[port]'/system/console/configMgr`
1. 開啟 **[!UICONTROL Forms通用設定服務].**
1. 在 **[!UICONTROL 允許]** 欄位， **選取** 所有使用者 — 所有使用者（匿名或登入）都可以預覽附件、驗證和簽署表單，以及按一下 **[!UICONTROL 儲存].** 作者執行個體已設定為使用 [!DNL Adobe Sign].
1. 發佈設定。
1. 使用 [復寫](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=zh-Hans) 以在對應的發佈執行個體上建立相同的設定。

現在， [!DNL Adobe Sign] 與AEM整合 [!DNL Forms] 並準備用於調適型表單。 至 [在最適化表單中使用Adobe Sign服務](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，請在最適化表單屬性中指定上述建立的設定容器。



## 設定 [!DNL Adobe Sign] 同步簽名狀態的排程器 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

一個 [!DNL Adobe Sign] 啟用的最適化表單只會在所有簽署者完成簽署程式後提交。 根據預設， [!DNL Adobe Sign] 排程器服務已排程為每24小時檢查（輪詢）簽署者回應。 您可以为您的环境更改此默认间隔。執行以下步驟來變更預設間隔：

1. 登入AEM [!DNL Forms] 含管理員憑證的伺服器，並導覽至 **工具** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.

   您也可以在瀏覽器視窗中開啟下列URL：
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到並開啟 **[!UICONTROL Adobe Sign設定服務]** 選項。 指定 [cron運算式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 在 **[!UICONTROL 狀態更新排程器運算式]** 欄位並按一下 **[!UICONTROL 儲存]**. 例如，若要在每日午夜12點執行設定服務，請指定 `0 0 0 1/1 * ? *` 在 **[!UICONTROL 狀態更新排程器運算式]** 欄位。

同步狀態的預設間隔 [!DNL Adobe Sign] 現已變更。

## 相关文章 {#related-articles}

* [在最適化表單中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [將Adobe Sign與AEM Forms搭配使用（影片）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
