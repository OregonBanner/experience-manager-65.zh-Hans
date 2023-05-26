---
title: 创建“邀请外部用户”处理程序
description: 创建“邀请外部用户”处理程序
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---

# 创建“邀请外部用户”处理程序 {#create-invite-external-users-handler}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

您可以为Rights Management服务创建邀请外部用户处理程序。 通过“邀请外部用户”处理程序，Rights Management服务可邀请外部用户成为Rights Management用户。 当用户成为Rights Management用户后，用户能够执行任务，例如打开受策略保护的PDF文档。 将邀请外部用户处理程序部署到AEM Forms后，您可以使用管理控制台与其交互。

>[!NOTE]
>
>邀请外部用户处理程序是一个AEM Forms组件。 在创建邀请外部用户处理程序之前，建议您熟悉如何创建组件。

**步骤摘要**

要开发邀请外部用户处理程序，必须执行以下步骤：

1. 设置开发环境。
1. 定义“邀请外部用户”处理程序实施。
1. 定义组件XML文件。
1. 部署邀请外部用户处理程序。
1. 测试Invite External Users处理程序。

## 设置开发环境 {#setting-up-development-environment}

要设置开发环境，您必须创建一个新的Java项目，例如Eclipse项目。 支持的Eclipse版本是 `3.2.1` 或更高版本。

Rights ManagementSPI需要 `edc-server-spi.jar` 文件在项目的类路径中设置。 如果不引用此JAR文件，则无法在Java项目中使用Rights ManagementSPI。 此JAR文件随AEM Forms SDK一起安装在中 `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` 文件夹。

除了添加 `edc-server-spi.jar` 文件到项目的类路径，还必须添加使用Rights Management服务API所需的JAR文件。 在邀请外部Rights Management处理程序中使用用户服务API时需要这些文件。

## 定义邀请外部用户处理程序实施 {#define-invite-external-users-handler}

要开发邀请外部用户处理程序，您必须创建一个实现 `com.adobe.edc.server.spi.ersp.InvitedUserProvider` 界面。 此类包含一个名为的方法 `invitedUser`，在使用提交电子邮件地址时，Rights Management服务会调用该参数 **添加受邀用户** 通过Administration Console访问的页面。

此 `invitedUser` 方法接受 `java.util.List` 实例，其中包含从提交的字符串类型电子邮件地址 **添加受邀用户** 页面。 此 `invitedUser` 方法返回数组 `InvitedUserProviderResult` 对象，通常是电子邮件地址到用户对象的映射（不返回null）。

>[!NOTE]
>
>除了演示如何创建“邀请外部用户”处理程序外，本节还使用AEM Forms API。

Invite外部用户处理程序的实现包含一个用户定义的方法，名为 `createLocalPrincipalAccount`. 此方法接受将电子邮件地址指定为参数值的字符串值。 此 `createLocalPrincipalAccount` 方法假定预先存在一个名为的本地域 `EDC_EXTERNAL_REGISTERED`. 您可以将此域名配置为所需的任何名称；但是，对于生产应用程序，您可能希望与企业域集成。

此 `createUsers` 方法遍历每个电子邮件地址，并创建相应的用户对象（中的本地用户）。 `EDC_EXTERNAL_REGISTERED` 域)。 最后， `doEmails` 方法名为。 此方法刻意保留为示例中的存根。 在生产实施中，它将包含应用程序逻辑，用于向新创建的用户发送邀请电子邮件。 在示例中还留有它来演示实际应用程序的应用程序逻辑流程。

### 定义邀请外部用户处理程序实施 {#user-handler-implementation}

以下邀请外部用户处理程序实施接受从“添加受邀用户”页面提交的电子邮件地址，可通过管理控制台访问该页面。

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
>此Java类保存为名为InviteExternalUsersSample.java的JAVA文件。

## 为授权处理程序定义组件XML文件 {#define-component-xml-authorization-handler}

必须定义一个组件XML文件，才能部署邀请外部用户处理程序组件。 每个组件都存在一个组件XML文件，该文件提供了有关该组件的元数据。

以下各项 `component.xml` 文件用于invite外部用户处理程序。 请注意，服务名称为 `InviteExternalUsersSample` 并且此服务公开的操作名为 `invitedUser`. 输入参数为 `java.util.List` 实例且输出值是 `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` 实例。

### 为邀请外部用户处理程序定义组件XML文件 {#component-xml-invite-external-users-handler}

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

## 正在打包Invite外部用户处理程序 {#packaging-invite-external-users-handler}

要将邀请外部用户处理程序部署到AEM Forms，必须将Java项目打包到JAR文件中。 必须确保邀请外部用户处理程序的业务逻辑所依赖的外部JAR文件，例如 `edc-server-spi.jar` 和 `adobe-rightsmanagement-client.jar` 文件也包含在JAR文件中。 此外，组件XML文件必须存在。 此 `component.xml` 文件和外部JAR文件必须位于JAR文件的根目录下。

>[!NOTE]
>
>在下图中， `BootstrapImpl` 显示类。 本节不讨论如何创建 `BootstrapImpl` 类。

下图显示了打包到邀请外部用户处理程序的JAR文件中的Java项目内容。

![邀请用户](assets/ci_ci_InviteUsers.png)

A.组件所需的外部JAR文件B. JAVA文件

必须将邀请外部用户处理程序打包到JAR文件中。 在上图中，请注意列出了.JAVA文件。 打包到JAR文件后，还必须指定相应的.CLASS文件。 如果没有.CLASS文件，授权处理程序将无法工作。

>[!NOTE]
>
>将外部授权处理程序打包到JAR文件后，可以将组件部署到AEM Forms。 在给定时间只能部署一个邀请外部用户处理程序。

>[!NOTE]
>
>您还可以以编程方式部署组件。

## 测试邀请外部用户处理程序 {#testing-invite-external-users-handler}

要测试邀请外部用户处理程序，可以使用管理控制台添加要邀请的外部用户。

要使用管理控制台添加要邀请的外部用户，请执行以下操作：

1. 使用Workbench部署邀请外部用户处理程序的JAR文件。
1. 重新启动应用程序服务器。
1. 登录到管理控制台。
1. 单击 **[!UICONTROL 服务]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 配置]** >已邀请 **[!UICONTROL 用户注册]**.
1. 通过选中 **[!UICONTROL 启用受邀用户注册]** 盒子。 下 **[!UICONTROL 使用内置注册系统]**，单击 **[!UICONTROL 否]**. 保存您的设置。
1. 在管理控制台主页中，单击 **[!UICONTROL 设置]** > **[!UICONTROL User Management]** > **[!UICONTROL 域管理]**.
1. 单击 **[!UICONTROL 新建本地域]**. 在以下页面中，创建一个名称和标识符值为的域 `EDC_EXTERNAL_REGISTERED`. 保存更改。
1. 在管理控制台主页中，单击 **[!UICONTROL 服务]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 受邀用户和本地用户]**. 此 **[!UICONTROL 添加受邀用户]** 页面。
1. 输入电子邮件地址（由于当前的邀请外部用户处理程序实际上并不发送电子邮件，因此电子邮件地址不一定有效）。 单击&#x200B;**[!UICONTROL 确定]**。用户受邀加入系统。
1. 在管理控制台主页中，单击 **[!UICONTROL 设置]** > **[!UICONTROL User Management]** > **[!UICONTROL 用户和组]**.
1. 在 **[!UICONTROL 查找]** 字段中，输入您指定的电子邮件地址。 单击 **[!UICONTROL 查找]**. 您邀请的用户将作为用户显示在本地 `EDC_EXTERNAL_REGISTERED` 域。

>[!NOTE]
>
>如果停止或卸载该组件，则邀请外部用户处理程序将失败。
