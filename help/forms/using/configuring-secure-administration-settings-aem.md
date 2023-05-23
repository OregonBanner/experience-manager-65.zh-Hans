---
title: 為JEE上的AEM Forms進行安全管理設定
seo-title: Configuring Secure Administration Settings for AEM Forms on JEE
description: 瞭解如何管理私密開發環境中雖然需要，但在JEE上的AEM Forms生產環境中不需要的使用者帳戶和服務。
seo-description: Learn how to administer user accounts and services that, although required in a private development environment, are not required in a production environment of AEM Forms on JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
role: Admin
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# 為JEE上的AEM Forms進行安全管理設定 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

瞭解如何管理私密開發環境中雖然需要，但在JEE上的AEM Forms生產環境中不需要的使用者帳戶和服務。

一般而言，開發人員不會使用生產環境來建置和測試他們的應用程式。 因此，您必須管理使用者帳戶和服務，雖然這些帳戶和服務在私人開發環境中是必要的，但在生產環境中卻不是必要的。

本文介紹透過AEM Forms on JEE提供的管理選項來減少整體攻擊面的方法。

## 停用對服務的非必要遠端存取 {#disabling-non-essential-remote-access-to-services}

安裝及設定JEE上的AEM Forms後，許多服務都可透過SOAP和Enterprise JavaBeans™ (EJB)進行遠端叫用。在此案例中，遠端一詞是指任何可存取應用程式伺服器SOAP、EJB或Action Message Format (AMF)連線埠的網路呼叫者。

雖然JEE服務上的AEM Forms需要向授權來電者傳遞有效的認證，但您應僅允許從遠端存取您需要存取的服務。 若要達到有限的協助功能，您應該儘可能減少遠端可存取的服務組合，讓系統正常運作，然後啟用遠端呼叫其他您需要的服務。

JEE服務上的AEM Forms一律需要至少SOAP存取權。 這些服務通常是Workbench使用的必要服務，但也包括Workspace Web應用程式呼叫的服務。

使用Administration Console中的「應用程式和服務」網頁完成此程式：

1. 在網頁瀏覽器中輸入下列URL登入Administration Console：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **服務>應用程式和服務>偏好設定**.
1. 設定「偏好設定」可檢視相同頁面上最多200個服務和端點。
1. 按一下 **服務** > **應用程式和服務** > **端點管理**.
1. 選取 **EJB** 從 **提供者** 清單，然後按一下 **篩選**.
1. 若要停用所有EJB端點，請選取清單中每個端點旁的核取方塊，然後按一下 **停用**.
1. 按一下 **下一個** 並對所有EJB端點重複上述步驟。 在停用端點之前，請確定EJB列在「提供者」資料欄中。
1. 選取 **SOAP** 從 **提供者** 清單，然後按一下 **篩選**.
1. 若要移除SOAP端點，請選取清單中每個端點旁的核取方塊，然後按一下 **移除**. 請勿移除下列端點：

   * AuthenticationManagerService
   * 目錄管理員服務
   * 工作管理員
   * event_management_service
   * event_configuration_service
   * Processmanager
   * 範本管理員
   * 存放庫服務
   * 任務管理員服務
   * TaskQueueManager
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * 應用程式管理員

1. 按一下 **下一個** 並對不在上述清單中的SOAP端點重複上述步驟。 在移除端點之前，請確定SOAP列在「提供者」欄中。

## 停用對服務的非必要匿名存取 {#disabling-non-essential-anonymous-access-to-services}

某些表單伺服器服務允許對某些作業進行未經驗證的（匿名）引發。 這表示服務公開的一或多個作業可能會以任何已驗證使用者或完全沒有驗證使用者的身分叫用。

1. 在網頁瀏覽器中輸入下列URL來登入管理主控台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **服務>應用程式和服務>服務管理**.
1. 按一下要停用的服務名稱（例如AuthenticationManagerService）。
1. 按一下 **安全性索引標籤**，取消選取 **允許匿名存取**，然後按一下 **儲存**.
1. 完成下列服務的步驟3和4：

   * AuthenticationManagerService
   * EJB
   * 电子邮件
   * 工作管理員
   * 觀察資料夾
   * UsermanagerUtilservice
   * 遠端
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * 任務管理員服務
   * TaskmanagerConnector
   * TaskManagerQueryService
   * TaskQueueManager
   * 任務端點管理員
   * 使用者服務
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * 輸出服務
   * FormsService

   如果您要公開這些服務的任何一項以進行遠端引發，您也應考慮停用這些服務的匿名存取。 否則，任何具有此服務網路存取權的呼叫者都可以在不傳遞有效認證的情況下叫用服務。

   任何不需要的服務都應該停用匿名存取。 許多內部服務都要求啟用匿名驗證，因為它們可能需要由系統中的任何使用者叫用，而不需要預先授權。

## 變更預設全域逾時 {#changing-the-default-global-time-out}

一般使用者可透過Workbench、AEM Forms Web應用程式或叫用AEM Forms伺服器服務的自訂應用程式，驗證AEM Forms。 一個全域逾時設定用於指定這類使用者在被迫重新驗證之前，可以與AEM Forms互動多久的時間（使用以SAML為基礎的判斷提示）。 預設設定是兩個小時。 在生產環境中，時間量需要減少至可接受的最小分鐘數。

### 將重新驗證時間限制最小化 {#minimize-reauthentication-time-limit}

1. 在網頁瀏覽器中輸入下列URL來登入管理主控台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 按一下 **「設定」 > 「使用者管理」 > 「組態」 > 「匯入和匯出組態檔」**.
1. 按一下 **匯出** 以使用現有的AEM Forms設定產生config.xml檔案。
1. 在編輯器中開啟XML檔案，並找出下列專案：

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. 將值變更為大於5 （以分鐘為單位）的任何數字，並儲存檔案。
1. 在Administration Console中，瀏覽至Import And Export Configuration Files頁面。
1. 輸入修改過的config.xml檔案的路徑，或按一下「瀏覽」瀏覽至該檔案。
1. 按一下 **匯入** 上傳修改過的config.xml檔案，然後按一下 **確定**.
