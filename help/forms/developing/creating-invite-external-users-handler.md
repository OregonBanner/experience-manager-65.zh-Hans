---
title: 建立邀請外部使用者處理常式
description: 建立邀請外部使用者處理常式
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---

# 建立邀請外部使用者處理常式 {#create-invite-external-users-handler}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

您可以為Rights Management服務建立邀請外部使用者處理常式。 邀請外部使用者處理常式可讓Rights Management服務邀請外部使用者成為Rights Management使用者。 當使用者成為Rights Management使用者後，該使用者便能執行工作，例如開啟受原則保護的PDF檔案。 將邀請外部使用者處理常式部署到AEM Forms後，您可以使用管理主控台與其互動。

>[!NOTE]
>
>邀請外部使用者處理常式是AEM Forms元件。 建立「邀請外部使用者」處理常式之前，建議您先熟悉如何建立元件。

**步驟摘要**

若要開發「邀請外部使用者」處理常式，您必須執行下列步驟：

1. 設定您的開發環境。
1. 定義Invite External Users處理常式實施。
1. 定義元件XML檔案。
1. 部署邀請外部使用者處理常式。
1. 測試「邀請外部使用者」處理常式。

## 設定您的開發環境 {#setting-up-development-environment}

若要設定開發環境，您必須建立新的Java專案，例如Eclipse專案。 支援的Eclipse版本為 `3.2.1` 或更新版本。

Rights ManagementSPI需要 `edc-server-spi.jar` 檔案中設定的類別路徑。 如果您未參照此JAR檔案，則無法在Java專案中使用Rights ManagementSPI。 此JAR檔案會與AEM Forms SDK安裝在中 `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` 資料夾。

除了新增 `edc-server-spi.jar` 檔案至專案的類別路徑，您也必須新增使用Rights Management服務API所需的JAR檔案。 若要在邀請外部使用者處理常式中使用Rights Management服務API，則需要這些檔案。

## 定義邀請外部使用者處理常式實作 {#define-invite-external-users-handler}

若要開發邀請外部使用者處理常式，您必須建立實作的Java類別 `com.adobe.edc.server.spi.ersp.InvitedUserProvider` 介面。 此類別包含方法，名為 `invitedUser`，當使用提交電子郵件地址時，Rights Management服務會叫用它 **新增受邀使用者** 可透過管理控制檯存取的頁面。

此 `invitedUser` 方法接受 `java.util.List` 執行個體，其中包含從提交的字串型別電子郵件地址 **新增受邀使用者** 頁面。 此 `invitedUser` 方法傳回陣列 `InvitedUserProviderResult` 物件，通常是電子郵件地址到使用者物件的對應（不傳回null）。

>[!NOTE]
>
>除了示範如何建立邀請外部使用者處理常式外，本節也使用AEM Forms API。

Invite外部使用者處理常式的實作包含使用者定義的方法，名為 `createLocalPrincipalAccount`. 此方法接受將電子郵件地址指定為引數值的字串值。 此 `createLocalPrincipalAccount` 方法假設名為的本機網域已存在 `EDC_EXTERNAL_REGISTERED`. 您可以將此網域名稱設定為您想要的任何名稱；但是，對於生產應用程式，您可能想要與企業網域整合。

此 `createUsers` 方法會遍歷每個電子郵件地址，並建立對應的使用者物件（位於中的本機使用者）。 `EDC_EXTERNAL_REGISTERED` 網域)。 最後， `doEmails` 方法已呼叫。 此方法有意地留作範例中的虛設常式。 在生產環境實作中，它會包含應用程式邏輯，以將邀請電子郵件訊息傳送給新建立的使用者。 範例中會保留此功能，以示範實際應用程式的應用程式邏輯流程。

### 定義邀請外部使用者處理常式實作 {#user-handler-implementation}

下列邀請外部使用者處理常式實作接受從「新增受邀使用者」頁面提交的電子郵件地址，可透過管理控制檯進行存取。

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>此Java類別會儲存為名為InviteExternalUsersSample.java的JAVA檔案。

## 定義授權處理常式的元件XML檔案 {#define-component-xml-authorization-handler}

您必須定義元件XML檔案，才能部署Invite外部使用者處理常式元件。 每個元件都有一個元件XML檔案，並提供有關元件的中繼資料。

下列專案 `component.xml` 檔案用於invite external users處理常式。 請注意，服務名稱為 `InviteExternalUsersSample` 此服務公開的操作已命名 `invitedUser`. 輸入引數是 `java.util.List` 執行個體，而輸出值是以下陣列 `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` 執行個體。

### 定義邀請外部使用者處理常式的元件XML檔案 {#component-xml-invite-external-users-handler}

```as3
<component xmlns="https://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## 正在封裝邀請外部使用者處理常式 {#packaging-invite-external-users-handler}

若要將邀請外部使用者處理常式部署到AEM Forms，您必須將您的Java專案封裝到JAR檔案中。 您必須確保邀請外部使用者處理常式商業邏輯所依賴的外部JAR檔案，例如 `edc-server-spi.jar` 和 `adobe-rightsmanagement-client.jar` 檔案也包含在JAR檔案中。 此外，元件XML檔案必須存在。 此 `component.xml` 檔案和外部JAR檔案必須位於JAR檔案的根目錄下。

>[!NOTE]
>
>在下圖中， `BootstrapImpl` 類別會顯示出來。 本節不討論如何建立 `BootstrapImpl` 類別。

下圖顯示封裝至邀請外部使用者處理常式的JAR檔案中的Java專案內容。

![邀請使用者](assets/ci_ci_InviteUsers.png)

A.元件所需的外部JAR檔案B. JAVA檔案

您必須將邀請外部使用者處理常式封裝到JAR檔案中。 在上圖中，請注意已列出.JAVA檔案。 封裝成JAR檔案後，也必須指定對應的.CLASS檔案。 如果沒有.CLASS檔案，授權處理常式將無法運作。

>[!NOTE]
>
>將外部授權處理常式封裝成JAR檔案後，您可以將元件部署到AEM Forms。 一次只能部署一個邀請外部使用者處理常式。

>[!NOTE]
>
>您也可以以程式設計方式部署元件。

## 測試邀請外部使用者處理常式 {#testing-invite-external-users-handler}

若要測試邀請外部使用者處理常式，您可以使用管理主控台新增要邀請的外部使用者。

若要使用管理主控台新增要邀請的外部使用者：

1. 使用Workbench部署邀請外部使用者處理常式的JAR檔案。
1. 重新啟動應用程式伺服器。
1. 登入管理主控台。
1. 按一下 **[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 設定]** >已邀請 **[!UICONTROL 使用者註冊]**.
1. 啟用受邀使用者註冊，方法是檢查 **[!UICONTROL 啟用受邀使用者註冊]** 方塊。 下 **[!UICONTROL 使用內建註冊系統]**，按一下 **[!UICONTROL 否]**. 儲存您的設定。
1. 在管理控制檯首頁上，按一下 **[!UICONTROL 設定]** > **[!UICONTROL User Management]** > **[!UICONTROL 網域管理]**.
1. 按一下 **[!UICONTROL 新增本機網域]**. 在下列頁面中，使用名稱和識別碼值建立網域 `EDC_EXTERNAL_REGISTERED`. 儲存您的變更。
1. 在管理控制檯首頁上，按一下 **[!UICONTROL 服務]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 受邀和本機使用者]**. 此 **[!UICONTROL 新增受邀使用者]** 頁面便會顯示。
1. 輸入電子郵件地址（由於目前的邀請外部使用者處理常式實際上並不會傳送電子郵件訊息，因此電子郵件地址不一定有效）。 单击&#x200B;**[!UICONTROL 确定]**。使用者受邀加入系統。
1. 在管理控制檯首頁上，按一下 **[!UICONTROL 設定]** > **[!UICONTROL User Management]** > **[!UICONTROL 使用者和群組]**.
1. 在 **[!UICONTROL 尋找]** 欄位，輸入您指定的電子郵件地址。 按一下 **[!UICONTROL 尋找]**. 您邀請的使用者在本機中顯示為使用者 `EDC_EXTERNAL_REGISTERED` 網域。

>[!NOTE]
>
>如果停止或解除安裝元件，邀請外部使用者處理常式會失敗。
