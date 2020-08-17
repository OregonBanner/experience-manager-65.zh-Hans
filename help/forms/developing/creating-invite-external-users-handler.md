---
title: 创建邀请外部用户处理程序
description: 创建邀请外部用户处理程序
translation-type: tm+mt
source-git-commit: 92e5cc0b1934dad641357a22894e70a3660b774a
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# 创建邀请外部用户处理程序 {#create-invite-external-users-handler}

可以为Rights Management服务创建“邀请外部用户”处理程序。 邀请外部用户处理程序使Rights Management服务能够邀请外部用户成为Rights Management用户。 用户成为Rights Management用户后，用户可以执行任务，如打开受策略保护的PDF文档。 在将“邀请外部用户”处理程序部署到AEM Forms后，您可以使用管理控制台与其进行交互。

>[!NOTE]
>
>邀请外部用户处理程序是AEM Forms组件。 在创建“邀请外部用户”处理程序之前，建议您熟悉创建组件。

**步骤摘要**

要开发“邀请外部用户”处理程序，必须执行以下步骤：

1. 设置开发环境。
1. 定义“邀请外部用户”处理程序实现。
1. 定义组件XML文件。
1. 部署“邀请外部用户”处理程序。
1. 测试“邀请外部用户”处理程序。

## 设置开发环境 {#setting-up-development-environment}

要设置开发环境，必须创建新的Java项目，如Eclipse项目。 支持的Eclipse版本为或更高 `3.2.1` 版本。

Rights ManagementSPI要求 `edc-server-spi.jar` 在项目的类路径中设置文件。 如果不引用此JAR文件，则无法在Java项目中使用Rights ManagementSPI。 此JAR文件随文件夹中的AEM FormsSDK一 `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` 起安装。

除了将文件添 `edc-server-spi.jar` 加到项目的类路径之外，还必须添加使用Rights Management服务API所需的JAR文件。 需要这些文件才能在“邀请外部用户”处理程序中使用Rights Management服务API。

## 定义邀请外部用户处理程序实现 {#define-invite-external-users-handler}

要开发邀请外部用户处理程序，必须创建实现该接口的Java `com.adobe.edc.server.spi.ersp.InvitedUserProvider` 类。 此类包含一个名为的方 `invitedUser`法，当Rights Management服务使用可通过管理控制台访问的“添加受邀 **用户”页面提交电子邮件地址时，** 将调用该方法。

该方 `invitedUser` 法接受一 `java.util.List` 个实例，该实例包含从“添加被邀请的用户”页面提交的字符串类 **型电子邮件地址** 。 该方 `invitedUser` 法返回一组对 `InvitedUserProviderResult` 象，通常是电子邮件地址到用户对象的映射（不返回null）。

>[!NOTE]
>
>除了演示如何创建邀请外部用户处理程序外，本节还使用AEM FormsAPI。

邀请外部用户处理程序的实现包含一个名为的用户定义方法 `createLocalPrincipalAccount`。 此方法接受一个字符串值，该字符串值将电子邮件地址指定为参数值。 该 `createLocalPrincipalAccount` 方法假设存在名为的本地域 `EDC_EXTERNAL_REGISTERED`。 您可以将此域名配置为任何所需的域名；但是，对于生产应用程序，您可能希望与企业域集成。

该方 `createUsers` 法迭代每个电子邮件地址并创建相应的用户对象(域中的本 `EDC_EXTERNAL_REGISTERED` 地用户)。 最后，调用 `doEmails` 了该方法。 此方法有意保留为示例中的存根。 在生产实施中，它将包含应用程序逻辑，用于向新创建的用户发送邀请电子邮件。 它留在示例中，用于演示实际应用程序的应用程序逻辑流。

### 定义邀请外部用户处理程序实现 {#user-handler-implementation}

以下邀请外部用户处理程序实施接受从“添加已邀请的用户”页面提交的电子邮件地址，该页面可通过管理控制台访问。

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
>此Java类将保存为名为InviteExternalUsersSample.java的JAVA文件。

## 为授权处理程序定义组件XML文件 {#define-component-xml-authorization-handler}

必须定义组件XML文件，才能部署邀请外部用户处理程序组件。 每个组件都存在一个组件XML文件，它提供有关该组件的元数据。

以下文 `component.xml` 件用于邀请外部用户处理程序。 请注意，服务名称 `InviteExternalUsersSample` 为，此服务公开的操作为名称 `invitedUser`。 输入参数是 `java.util.List` 一个实例，输出值是实例的 `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` 数组。

### 为邀请外部用户处理程序定义组件XML文件 {#component-xml-invite-external-users-handler}

```as3
<component xmlns="http://adobe.com/idp/dsc/component/document"> 
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

## 打包邀请外部用户处理程序 {#packaging-invite-external-users-handler}

要将邀请外部用户处理程序部署到AEM Forms，必须将Java项目打包到JAR文件中。 必须确保邀请外部用户处理程序的业务逻辑所依赖的外部JAR文件(如 `edc-server-spi.jar` 和 `adobe-rightsmanagement-client.jar` 文件)也包含在JAR文件中。 此外，组件XML文件必须存在。 文 `component.xml` 件和外部JAR文件必须位于JAR文件的根目录下。

>[!NOTE]
>
>在下图中，显示 `BootstrapImpl` 了一个类。 本节不讨论如何创建 `BootstrapImpl` 类。

下图显示了打包到邀请外部用户处理程序的JAR文件中的Java项目内容。

![邀请用户](assets/ci_ci_InviteUsers.png)

A.组件需要的外部JAR文件B. JAVA文件

必须将邀请外部用户处理程序打包到JAR文件中。 在上一图中，请注意列出了。JAVA文件。 打包到JAR文件后，还必须指定相应的。CLASS文件。 如果没有。CLASS文件，授权处理程序将不工作。

>[!NOTE]
>
>将外部授权处理程序打包到JAR文件后，可以将组件部署到AEM Forms。 在给定时间只能部署一个邀请外部用户处理程序。

>[!NOTE]
>
>您还可以通过编程方式部署组件。

## 测试邀请外部用户处理程序 {#testing-invite-external-users-handler}

要测试邀请外部用户处理程序，您可以使用管理控制台添加要邀请的外部用户。

要使用管理控制台添加要邀请的外部用户，请执行以下操作：

1. 使用Workbench部署邀请外部用户处理程序的JAR文件。
1. 重新启动应用程序服务器。
1. 登录到管理控制台。
1. 单击 **[!UICONTROL 服务]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 配置]** >受邀用 **[!UICONTROL 户注]**&#x200B;册。
1. 选中“启用已邀请的用户注册”框， **[!UICONTROL 启用已邀请的用户]** 注册。 在“ **[!UICONTROL 使用内置注册系统]**”下， **[!UICONTROL 单击“否]**”。 保存设置。
1. 在管理控制台主页中，单 **[!UICONTROL 击“设置]** ” **[!UICONTROL >“用户管理]** ” **[!UICONTROL >“]**&#x200B;域管理”。
1. 单击 **[!UICONTROL “新建本地域]**”。 在下一页中，创建名称和标识符值为的域 `EDC_EXTERNAL_REGISTERED`。 保存更改。
1. 在管理控制台主页中，单 **[!UICONTROL 击“服务]** ”> **[!UICONTROL “Rights Management]** ” **[!UICONTROL >“已]**&#x200B;邀请和本地用户”。 此时将 **[!UICONTROL 显示“添加受邀用户]** ”页面。
1. 输入电子邮件地址（因为当前邀请外部用户处理程序实际上并不发送电子邮件，所以该电子邮件地址不一定有效）。 单击&#x200B;**[!UICONTROL 确定]**。用户被邀请到系统。
1. 在管理控制台主页中，单 **[!UICONTROL 击“设置]** ”>“ **[!UICONTROL 用户管理]** ” **[!UICONTROL >“用]**&#x200B;户和用户组”。
1. 在“查 **[!UICONTROL 找]** ”字段中，输入您指定的电子邮件地址。 单击“ **[!UICONTROL 查找]**”。 您邀请的用户在本地域中显示为 `EDC_EXTERNAL_REGISTERED` 用户。

>[!NOTE]
>
>如果停止或卸载组件，邀请外部用户处理程序将失败。
