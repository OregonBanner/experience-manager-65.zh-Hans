---
title: 推送通知
description: 請依照本頁面的說明操作，瞭解如何在Adobe Experience Manager Mobile應用程式中使用推播通知。
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '3293'
ht-degree: 1%

---

# 推送通知{#push-notifications}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

能夠透過重要通知立即提醒您的AEM Mobile應用程式使用者，對行動應用程式及其行銷活動的價值至關重要。 我們在此處說明允許應用程式接收推播通知所需執行的步驟，以及如何設定推播並從AEM Mobile傳送推播至安裝在電話上的應用程式。 此外，本節將說明如何設定 [深層連結](#deeplinking) 功能加入推播通知。

>[!NOTE]
>
>*推播通知並不保證一定會傳送；它們更像是公告。 盡最大努力確保每個人都能收到這些訊息，但並非保證傳送機制。 此外，傳送推播的時間也可能從不到一秒到最多半小時不等。*

搭配AEM使用推播通知需要幾項不同的技術。 首先，推播通知服務提供者必須用來管理通知和裝置(AEM尚未執行此操作)。 使用AEM可立即使用兩個提供者進行設定： [Amazon Simple Notification Service](https://aws.amazon.com/sns/) （或SNS），以及 [Pushwoosh](https://www.pushwoosh.com/). 其次，特定行動作業系統的推送技術必須通過適當的服務 — 適用於iOS裝置的Apple推送通知服務（或APNS），以及適用於Android裝置的Google雲端通訊（或GCM）。 雖然AEM不會直接與這些平台特定服務通訊，但AEM必須隨附通知來提供某些相關設定資訊，這些服務才能執行推送。

安裝及設定後（如下所述），其運作方式如下：

1. 推播通知會在AEM中建立，並傳送給服務提供者(Amazon SNS或Pushwoosh)。
1. 服務提供者會收到該資訊，然後傳送給核心提供者（APNS或GCM）。
1. 核心提供者會將通知推播至已註冊該推播的所有裝置。 對於每個裝置，它會使用行動資料網路或WiFi，以裝置上目前可用的任何專案為準。
1. 如果為其註冊的應用程式未執行，則通知會顯示在裝置上。 使用者點選通知將會啟動應用程式，並在應用程式中顯示通知。 如果應用程式已在執行中，則只會顯示應用程式內通知。

此版本的AEM支援iOS和Android行動裝置。

## 概述與程式 {#overview-and-procedure}

若要在AEM Mobile應用程式中使用推播通知，您必須採取下列高階步驟。

通常，Experience Manager開發人員會執行以下操作：

1. 註冊Apple和Google訊息服務
1. 註冊並設定推送訊息服務
1. 新增推送支援至應用程式
1. 準備電話以進行測試

當Experience Manager管理員執行下列操作時：

1. 在AEM應用程式上設定推播
1. 建置和部署應用程式
1. 傳送推播通知
1. 設定深層連結 *（選擇性）*

### 步驟1：註冊Apple和Google訊息服務 {#step-register-with-apple-and-google-messaging-services}

#### 使用Apple推播通知服務(APNS) {#using-the-apple-push-notification-service-apns}

前往Apple頁面 [此處](https://developer.apple.com/documentation/usernotifications#//apple_ref/doc/uid/TP40008194-CH8-SW1) 熟悉Apple推播通知服務。

若要使用APN，您需要 **憑證** 檔案（.cer檔案），推播 **私密金鑰** （a .p12檔案）和 **私密金鑰密碼** 來自Apple。 操作說明，請參閱 [此處](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/).

#### 使用Google雲端通訊(GCM)服務 {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google正在以名為Firebase Cloud Messaging (FCM)的類似服務取代GCM。 如需FCM的詳細資訊，請按一下 [此處](https://developers.google.com/cloud-messaging/faq).

前往Google頁面 [此處](https://developer.android.com/google/gcm/index.html) 熟悉Android適用的Google Cloud Messaging。

您需要依照步驟操作 [此處](https://developer.android.com/google/gcm/gs.html) 至 **建立Google API專案**， **啟用GCM服務**、和 **取得API金鑰**. 您將需要 **API金鑰** 傳送推播通知至Android裝置。 此外，請記錄您的 **專案編號**，有時也稱為 **GCM寄件者ID**.

下列步驟顯示建立GCM API金鑰的不同方法：

1. 登入google並前往 [Google的開發人員頁面](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. 從清單中選擇您的應用程式（或建立新應用程式）。
1. 在「Android套件名稱」下方輸入您的應用程式ID，即 `com.adobe.cq.mobile.weretail.outdoorsapp`. （如果這樣還是不行，請用「test.test」再試一次。）
1. 按一下 **繼續選擇及設定服務**
1. 選取「雲端通訊」，然後按一下 **啟用Google雲端通訊**.
1. 隨後將顯示新的伺服器API金鑰和（新的或現有的）寄件者ID。

>[!NOTE]
>
>記錄伺服器API金鑰。 此值是在您的推送提供者的網站上輸入。

### 步驟2：註冊並設定推送訊息服務 {#step-register-and-configure-a-push-messaging-service}

AEM已設定為使用下列三種服務之一來推送通知：

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

*AMAZON SNS* 和 *Pushwoosh* 設定可讓您從AEM畫面內傳送推播。

*Adobe行動服務* 設定可讓您使用Adobe Analytics帳戶從Adobe Mobile Services中設定及傳送推播通知（但應用程式必須透過此設定集建置，才能啟用AMS推播通知）。

#### 使用Amazon SNS傳訊服務 {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*如需Amazon SNS的相關資訊，以及建立新AWS帳戶的連結，請參閱 [此處](https://aws.amazon.com/sns/). 您可以取得一年的免費帳戶。*

如果您不想使用Amazon SNS，可以跳過這些步驟。

請依照下列步驟設定推播通知的Amazon SNS：

1. **註冊Amazon SNS**

   1. 記錄您的帳戶ID。 格式應為12位數，且不含空格或破折號，即「123456789012」。
   1. 確定您位於「美國東部」或「歐盟」地區，因為後續步驟（建立身分識別集區）需要這些步驟之一。
   1. 註冊之後，登入管理主控台並選取 [SNS](https://console.aws.amazon.com/sns/) （推播通知服務）。 如果出現，請按一下「開始使用」。

1. **建立存取金鑰和ID**

   1. 按一下畫面右上方的登入名稱，然後從功能表選擇[安全性認證]。
   1. 按一下「存取金鑰」，然後在下列空白處按一下 **建立新的存取金鑰**.
   1. 按一下 **顯示存取金鑰**，並複製及儲存顯示的存取金鑰ID和秘密存取金鑰。 如果您選擇下載金鑰的選項，則會得到包含這些相同值的csv檔案。
   1. 您可以在此頁面管理其他安全性相關憑證，以及某些其他憑證。

   >[!NOTE]
   >
   >存取金鑰可用於多個應用程式。

   對於使用「AWS沙箱」帳戶的組織，步驟非常類似，並概述如下：

   1. 按一下畫面右上方的登入名稱，然後從功能表選擇[我的安全性認證]。
   1. 按一下動作左側清單中的「使用者」 ，然後選擇您的使用者名稱。
   1. 按一下「安全性證明資料」標籤。
   1. 從這裡，您可以看到您的金鑰並建立新金鑰。 儲存金鑰以供日後使用。


1. **建立主題**

   1. 按一下 **建立主題** 並選擇主題名稱。 記錄所有欄位，例如「主題ARN」、「主題擁有者」、「區域」、「顯示名稱」。
   1. 按一下 **其他主題動作** > **編輯主題原則**. 下 **允許這些使用者訂閱此主題**，選取 **每個人。**
   1. 按一下 **更新原則**.

   >[!NOTE]
   >
   >您可以為不同的情境建立多個主題，例如開發、測試、示範等。 其餘的SNS設定可以維持不變。 使用不同主題建置應用程式；傳送至該主題的推播通知只會由該主題建置的應用程式接收。

1. **建立平台應用程式**

   1. 按一下應用程式，然後按一下建立平台應用程式。 選擇名稱並選取平台(APNS適用於iOS，GCM適用於Android)。 視平台而定，需要填寫其他欄位：

      1. 對於APNS，必須輸入P12檔案、密碼、憑證和私密金鑰。 這些應該已在步驟中取得 *使用Apple推播通知服務(APNS)* 以上。
      1. 對於GCM，必須輸入API金鑰。 這應該已在步驟中取得 *使用Google雲端通訊(GCM)服務* 以上。
   1. 針對您將支援的每個平台重複上述步驟一次。 若要同時推送至iOS和Android，您必須建立兩個平台應用程式。


1. **建立識別集區**

   1. 使用 [Cognito](https://console.aws.amazon.com/cognito) 建立身分識別集區，以儲存未驗證使用者的基本資料。 請注意，Amazon Cognito目前僅支援「美國東部」和「歐盟」地區。
   1. 為其命名，並勾選「啟用對未驗證身分的存取」方塊。
   1. 在下一頁(&quot;*您的Cognito身分識別需要存取您的資源*&quot;)按一下「允許」。
   1. 在頁面的右上角，按一下連結»*編輯身分識別集區*. 此時會顯示身分識別集區ID。 儲存此文字以供稍後使用。
   1. 在同一頁面上，選擇「Unauthenticated role」旁的下拉式清單，並確定其角色為Cognito_&lt;pool name=&quot;&quot;>已選取UnauthRole。 儲存您的變更。

1. **配置访问权限**

   1. 登入 [Identity and Access Management](https://console.aws.amazon.com/iam/home) (IAM)
   1. 選取角色
   1. 按一下在上一步建立的角色，稱為Cognito_&lt;youridentitypoolname>Unauth_Role。 記錄顯示的「角色ARN」。
   1. 開啟「內嵌原則」（如果尚未開啟）。 您應該會看到名稱為oneClick_Cognito_的原則&lt;youridentitypoolname>Unauth_Role_1234567890123。
   1. 按一下「編輯原則」。 將原則檔案的內容替換為此JSON片段：

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> 「版本」：「2012-10-17」，</p> <p> "语句": [</p> <p> {</p> <p> "操作": [</p> <p> "mobileanalytics：PutEvents"，</p> <p> "cognito-sync：*"，</p> <p> "SNS：CreatePlatformEndpoint"，</p> <p> "SNS：Subscribe"</p> <p> ],</p> <p> "Effect"： "Allow"，</p> <p> "资源": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. 按一下 **套用原則**


#### 使用Pushwoosh訊息服務 {#using-the-pushwoosh-messaging-service}

如果您不想要使用Pushwoosh，可以略過此步驟。

若要使用Pushwoosh：

1. **註冊Pushwoosh**

   1. 前往pushwoosh.com並建立新帳戶。

1. **建立API存取權杖**

   1. 在Pushwoosh網站上，前往API存取功能表專案來產生API存取權杖。 您必須安全地記錄此內容。

1. **创建新应用程序**

   1. 如需Android支援，您需要提供GCM API金鑰。
   1. 設定應用程式時，請選擇Cordova做為架構。
   1. 如需iOS支援，您需要提供憑證檔案(.cer)、推送憑證(.p12)和私密金鑰密碼；這些應該已從Apple的APNS網站取得。 對於「框架」，請選擇「Cordova」。
   1. Pushwoosh會為該應用程式產生應用程式ID，格式為「XXXXX-XXXXX」，其中每個X都是十六進位值（0到F）。

>[!NOTE]
>
>*如果在AEM中使用相同的應用程式ID （及其他相關值： API存取權杖和GCM ID）設定第二個應用程式，任何透過AEM上的第二個應用程式傳送的推播通知都會傳送到具有該應用程式ID的任何其他應用程式。*

### 步驟3：將推送支援新增至應用程式 {#step-add-push-support-to-the-app}

#### 新增ContentSync設定 {#add-contentsync-configuration}

建立兩個名為notificationsConfig的內容節點（一個在app-config中，一個在app-config-dev中）：

* /content/`<your app>`/shell/jcr：content/pge-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr：content/pge-app/app-config/notificationsConfig

使用這些屬性（.content.xml檔案） ：
&lt;jcr:root xmlns:jcr=&quot; &lt;span id=&quot; translate=&quot;no&quot; />https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; xmlns：nt=&quot; [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; jcr：primaryType=&quot;nt：unstructured&quot; excludeProperties=&quot;[appAPIAccessToken]&quot; path=&quot;。./../../..&quot;
[targetRootDirectory=&quot;www&quot; type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>內容同步處理常式會尋找這些節點，如果它們不存在，則不會寫出pge-notifications-config.json檔案。

#### 新增使用者端資料庫 {#add-client-libraries}

您必須依照下列步驟，將推播通知使用者端程式庫新增至應用程式：

CRXDE Lite：

1. 導覽至 */etc/designs/phonegap/&lt;app name=&quot;&quot;>/clientlibsall。*
1. 在屬性窗格中的內嵌區段上按兩下。
1. 在出現的對話方塊中，按一下+按鈕以新增使用者端程式庫。
1. 在新文字欄位中新增&quot;cq.mobile.push&quot;，然後按一下「確定」。
1. 再新增一個名為cq.mobile.push.amazon的專案，然後按一下「確定」。
1. 保存更改。

>[!NOTE]
>
>如果出於應用程式上空間考量而移除或未使用推播通知，並為了避免主控台錯誤訊息，請從您的應用程式中移除這些clientlibs。

### 步驟4：準備電話以進行測試 {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*對於推播通知，您需要在實際裝置上進行測試，因為模擬器無法接收推播通知。*

#### iOS {#ios}

若使用iOS，您需要使用Mac作業系統電腦，並且加入 [iOS開發人員計畫](https://developer.apple.com/programs/ios/). 有些公司擁有公司授權，所有開發人員皆可取得。

使用XCode 8.1時，您必須先前往專案中的「功能」標籤，然後將「推送通知」切換為「開啟」，才能使用「推送通知」。

#### Android {#android}

若要使用CLI在Android手機上安裝應用程式(請參閱下文： **步驟6 — 建置和部署應用程式**)，您必須先將手機置於「開發人員模式」。 另請參閱 [啟用裝置上開發人員選項](https://developer.android.com/tools/device.html#developer-device-options) 以取得執行此動作的詳細資訊。

### 步驟5：在AEM應用程式上設定推播 {#step-configure-push-on-aem-apps}

在建置和部署到您設定的行動裝置之前，您必須為您決定使用的訊息服務設定通知設定。

1. 為推播通知建立適當的授權群組。
1. 以適當使用者身分登入AEM，然後按一下「應用程式」標籤。
1. 按一下應用程式。
1. 找到「管理Cloud Services」圖磚，然後按一下鉛筆圖磚，即可修改您的雲端設定。
1. 選取Amazon SNS Connection、Pushwoosh Connection或Adobe Mobile Services作為通知設定。
1. 輸入提供者屬性，然後按一下送出以儲存它們，然後按一下完成。 除了在AMS的情況下，目前階段不會從遠端驗證這些事件。
1. 您現在應該會看到您剛才在「管理Cloud Services」表徵圖上輸入的設定。

### 步驟6：建置和部署應用程式 {#step-build-and-deploy-the-app}

**注意：** 另請參閱我們的指示 [此處](/help/mobile/building-app-mobile-phonegap.md) 建立PhoneGap應用程式的相關資訊。

有兩種方法可使用PhoneGap建置和部署您的應用程式。

**注意：** 對於推播通知測試，模擬器是不夠的，因為推播通知在推播提供者(Apple或Google)和裝置之間使用不同的通訊協定。 目前的Mac/PC硬體和模擬器不支援此功能。

1. *PhoneGap Build* 是PhoneGap提供的服務，可在伺服器上為您建立應用程式，並允許您直接下載至裝置。 請參閱 [PhoneGap Build檔案](https://build.phonegap.com/) 以瞭解如何設定和使用PhoneGap Build。

1. *PhoneGap命令列介面* (CLI)可讓您在命令列上使用一組豐富的PhoneGap命令，以建置、偵錯和部署您的應用程式。 請參閱 [PhoneGap開發人員檔案](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) 瞭解如何設定和使用PhoneGap CLI。

### 步驟7：傳送推播通知 {#step-send-a-push-notification}

若要建立新通知並傳送，請依照下列步驟進行。

1. 建立新通知

   * 在AEM Mobile應用程式的儀表板中，找出「推播通知」表徵圖。
   * 在右上方的功能表中，選擇「建立」。 請注意，在首次設定雲端設定之前，此按鈕不可用。
   * 在「建立通知精靈」中輸入標題和訊息，然後按一下「建立」按鈕。 您的通知現在已準備好立即或稍後傳送。 可以編輯它，並且可以變更和儲存訊息和/或標題。

1. 傳送通知

   * 在應用程式控制面板中，找出「推播通知」表徵圖。
   * 選取通知，或按一下右下方的詳細資訊按鈕(...)，顯示通知清單。 此清單也會指出通知是否已準備好傳送、已傳送，或傳送期間是否發生錯誤。
   * 勾選一個通知的核取方塊（僅限），然後按一下清單上方的「傳送通知」按鈕。 您有機會在出現的對話方塊上「取消」或「傳送」通知。

1. 處理結果

   * 如果推播通知服務(Amazon SNS或Pushwoosh)收到傳送要求，確認其有效，然後成功傳送給原生提供者（APNS和GCM），傳送對話方塊會關閉，但不顯示任何訊息。 在通知清單中，該通知的狀態將列為「已傳送」。
   * 如果推送傳送失敗，對話方塊會顯示訊息指出問題。 在通知清單中，該通知的狀態將列為「錯誤」，但如果問題已解決，則可再次傳送通知。 發生錯誤時，伺服器錯誤記錄中應會顯示其他錯誤資訊。
   * 請注意，iOS和Android推播通知之間在平台上有一些差異。 其中包括：

      * 使用CLI建置應用程式後，應用程式就會在Android上部署後啟動。 在iOS上，您必須手動啟動。 由於推播註冊步驟會在啟動時進行，Android應用程式會立即收到推播通知（因為它會啟動並註冊），而iOS應用程式不會收到通知。
      * 在Android上，「確定」按鈕文字全部為大寫字母（以及在應用程式內通知中新增的任何其他按鈕中也一樣），但在iOS中則否。

對於AMS推播通知，必須撰寫通知並從AMS伺服器傳送。 AMS提供的推播通知功能比AEM通知隨AWS和Pushwoosh提供的功能更多。

>[!NOTE]
>
>*推播通知並不保證一定會傳送；它們更像是公告。 盡最大努力確保每個人都能聽到，但他們不是保證的傳送機制。 此外，傳送推播的時間也可能從不到一秒到最多半小時不等。*

### 使用推播通知設定深層連結 {#configuring-deep-linking-with-push-notifications}

什麼是深層連結？ 在推播通知的情境下，這是一種允許應用程式開啟或導向（如果開啟）至應用程式內指定位置的方法。

如何運作？ 推播通知的作者可選擇新增按鈕標籤（即「顯示給我！」） 並透過視覺路徑瀏覽器，選擇要在通知中連結的頁面。 傳送後，推播會正常發生，除了應用程式內訊息中，「確定」按鈕會被「關閉」按鈕取代，而新按鈕會指定（「顯示我！」） 也會出現。 按一下新按鈕，應用程式就會移至應用程式內的指定頁面。 按一下「關閉」只會關閉訊息。

如果應用程式未開啟，則陰影會正常顯示。 對陰影中的通知採取行動將開啟應用程式，然後根據推播通知中的設定向使用者顯示深層連結按鈕。

建立通知、新增按鈕文字，以及選擇性深層連結的連結路徑：

>[!CAUTION]
>
>.若要存取控制面板中的「推播通知」表徵圖，請遵循下列步驟。

1. 按一下右上角的編輯 **管理Cloud Services** 圖磚。

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. 選取 **Pushwoosh連線**. 单击&#x200B;**下一步**。

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. 輸入屬性的詳細資訊，然後按一下 **提交**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   一旦您提交設定， **推播通知** 圖磚會顯示在控制面板中。

   ![chlimage_1-111](assets/chlimage_1-111.png)

### 创建通知向导 {#create-notification-wizard}

一旦 **推播通知** 圖磚會顯示在您的儀表板中，使用建立通知精靈來新增內容：

1. 按一下右上角的新增符號 **推播通知** 圖磚以開啟 **建立通知精靈**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. 按一下連結路徑中的瀏覽圖示，使用者就會看到應用程式的內容結構。

   選取路徑後，按一下核取圖示。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >連結按鈕文字限製為20個字元。
   >
   >如果一般使用者沒有最新版本的應用程式，而且連結的路徑不可用，則確認深層連結的動作會將使用者引導至應用程式的首頁面。

1. 輸入 **文字詳細資料** 在 **建立通知精靈** 並按一下 **建立**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   按一下您從「 」建立的推播通知，以開啟詳細資料 **推播通知** 圖磚。

   您可以編輯屬性、傳送通知或刪除通知。

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**附加信息**:
>
>6.4版之後將不再支援Pushwoosh和Amazon SNS，並會以套件共用的附加元件形式提供。

### 后续步骤 {#the-next-steps}

瞭解應用程式的推播通知詳細資料後，請參閱 [AEM Mobile內容個人化](/help/mobile/phonegap-aem-mobile-content-personalization.md).
