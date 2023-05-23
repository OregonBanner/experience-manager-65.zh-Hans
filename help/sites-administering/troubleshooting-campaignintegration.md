---
title: 疑難排解Adobe Campaign整合
seo-title: Troubleshooting your Adobe Campaign Integration
description: 瞭解如何疑難排解Adobe Campaign整合的問題。
seo-description: Learn how to troubleshoot issues with the Adobe Campaign Integration.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# 疑難排解Adobe Campaign整合{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>此頁面適用於Campaign Classic。

下列疑難排解提示可協助您解決在將AEM與Adobe Campaign整合時可能遇到的最常見問題：

## 一般疑難排解提示 {#general-troubleshooting-tips}

對於這兩種整合，您可以檢查是否已傳送HTTP呼叫(AEM > Adobe Campaign、Adobe Campaign > AEM)：

* 當整合失敗時，請確定這些呼叫到達另一端（以避免防火牆/SSL問題）。
* 針對AEM功能，您會看到已從AEM製作介面要求json呼叫；這些不應導致HTTP-500錯誤。 如果您看到HTTP-500錯誤，請檢查 `error.log` 以取得相關資訊。
* 提高AEM中促銷活動類別的偵錯層級也有助於疑難排解問題。

## 如果連線失敗 {#if-the-connection-fails}

檢查您是否已設定 **aemserver** 運運算元(在Adobe Campaign)。

## 如果影像未出現在Adobe Campaign主控台中 {#if-images-do-not-appear-in-the-adobe-campaign-console}

檢查HTML來源，並確認您可以從使用者端電腦開啟URL。 如果URL中包含localhost：4503，則變更Author執行個體上Day CQ Link Externalizer的設定，以指向可從Adobe Campaign主控台電腦存取的發佈執行個體。

另請參閱 [設定外部化程式。](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## 如果您無法從AEM連線到Adobe Campaign {#if-you-cannot-connect-from-aem-to-adobe-campaign}

在Adobe Campaign中尋找下列錯誤訊息：

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

若要修正此問題，請變更以下內容： **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**：

`<dataStore hosts="*" lang="en_GB">`

## 如果Adobe Campaign對話方塊中未顯示任何資料 {#if-no-data-displays-in-the-adobe-campaign-dialog}

在Adobe Campaign中，請確認連線埠號碼後面沒有尾隨斜線(/)。

![chlimage_1-149](assets/chlimage_1-149.png)

## 如果您收到有關您的setlocale的警告 {#if-you-get-a-warning-about-your-setlocale}

如果您正在啟動Apache HTTPD服務並看到錯誤 `"Warning: setlocale: LC_CTYPE cannot change locale"` 確定您已將 **en_CA.ISO-8859-15地區設定** 已安裝在您的系統上。

您可以使用檢查是否已安裝它 `local -a`. 如果尚未安裝，您可以修補 **/usr/local/neolane/nl6/env.sh** 指令碼並將地區設定變更為已安裝的地區設定。

## 如果您在編譯指令碼&#39;get_nms_amcGetSeedMetaData_jssp&#39;時發生錯誤 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

如果您在AEM記錄檔中看到下列錯誤訊息：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

使用下列因應措施：

1. 開啟檔案 **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. 修改方法「amcGetSeedMetaData」的第467行
1. 變更 `label : [inclView.@label](mailto:inclView.@label)` 至 `label : String([inclView.@label](mailto:inclView.@label))`

1. 保存.
1. 重新啟動伺服器。

## 如果Adobe Campaign在按一下「同步」按鈕時顯示錯誤 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

若按一下 **同步** Adobe Campaign Classic按鈕時，您會看到下列錯誤：

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

若要修正此問題，請確定外部帳戶中設定的AEM連線URL可以從電腦連線。

切換來源 **localhost** IP位址解決了這個問題。

## 如果您收到「無法剖析XTK日期+時間『未定義』錯誤」 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

按一下「同步」後，您會收到錯誤，指出頁面上出現指令碼：無法剖析XTK日期+時間「未定義」：不是有效的XTK值。

如果AEM執行個體上仍有過時的Adobe Campaign資訊，就會發生此情況。 移除並重新建置AEM上的所有促銷活動整合設定，即可解決此問題。 然後，建立新範本。

## 如果與SSL的連線在設定雲端服務時顯示錯誤 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

在AEM的error.log中，如果您看到以下內容：

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

請向Adobe Campaign支援團隊提出票證。

## 如果您在同步對話方塊中看到http而不是預期的https連結 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

透過下列設定：

* 使用https託管Adobe Campaign以與AEM作者通訊
* 反向Proxy終止SSL
* 內部部署AEM作者例項

嘗試同步Adobe Campaign傳送中的內容時，AEM會傳回電子報清單。 不過，清單中電子報的url是http位址。 選取清單中的專案之一時，會發生錯誤。

若要解決此問題：

* 需要將Dispatcher或反向Proxy設定為以標頭傳遞原始通訊協定。
* 此 *Apache Felix Http服務SSL篩選器* 在OSGi設定中([https://&lt;host>：&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr))需要設定為個別標題設定。 另請參閱 [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## 如果無法在頁面屬性中選取我建立的自訂範本 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

為Adobe Campaign建立郵件範本時，您必須包含屬性 **acMapping** 包含值 **mapRecipient** 在 **jcr：content** 範本的節點，否則您將無法在中選取Adobe Campaign範本 **頁面屬性** AEM （欄位已停用）。

## 如果您在記錄檔中收到錯誤「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

使用自訂範本時，您的記錄中會出現「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」錯誤。 在此情況下，請務必從安裝Featurepack 6576 [封裝共用](/help/sites-administering/package-manager.md#package-share). 如果將acMapping屬性設為recipient.firstName以外的值，則會在Adobe Campaign Manager端建立空白值。
