---
title: 将AEM Forms与AdobeLiveCycle连接
description: Adobe Experience Manager (AEM)LiveCycle连接器允许您从AEM应用程序和工作流LiveCycleES4 Acrobat服务。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
role: Admin
exl-id: 562f8a22-cbab-4915-bc0d-da9bea7d18fa
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# 将AEM Forms与AdobeLiveCycle连接 {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager (AEM)LiveCycle连接器允许从AEM Web应用程序和工作流中无缝调用AdobeLiveCycleES4 Acrobat服务。 LiveCycle提供了一个富客户端SDK，允许客户端应用程序使用Java™ API启动LiveCycle服务。 AEMLiveCycle连接器简化了OSGi环境中使用这些API的过程。

## 正在将AEM服务器连接到AdobeLiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEMLiveCycle连接器属于 [AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md). 安装AEM Forms附加组件包后，请执行以下步骤，以便可以将LiveCycle服务器的详细信息添加到AEM Web控制台。

1. 在AEM Web控制台配置管理器中，找到AdobeLiveCycle客户端SDK配置组件。
1. 单击该组件，以便编辑配置服务器的URL、用户名和密码。
1. 查看设置并单击 **保存**.

虽然其性质不言自明，但重要之处如下：

* **服务器URL**  — 指定LiveCycle服务器的URL。 如果希望LiveCycle和AEM通过https进行通信，请使用以下JVM启动AEM

  ```java
  argument
   -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
  ```

  选项。

* **用户名** — 指定用于在AEM和LiveCycle之间建立通信的帐户的用户名。 帐户是具有启动Acrobat服务的权限的LiveCycle用户帐户。
* **密码** — 指定密码。
* **服务名称**  — 指定使用用户名和密码字段中提供的用户凭据启动的服务。 默认情况下，启动LiveCycle服务时不会传递任何凭据。

## 启动文档服务 {#starting-document-services}

客户端应用程序可以使用Java™ API、Web服务、远程处理和REST以编程方式启动LiveCycle服务。 对于Java™客户端，应用程序可以使用LiveCycleSDK。 LiveCycleSDK提供了一个用于远程启动这些服务的Java™ API。 例如，要将Microsoft® Word Document转换为PDF，客户端将启动GeneratePDFervice。 调用流包含以下步骤：

1. 创建ServiceClientFactory实例。
1. 每个服务都提供一个客户端类。 要启动服务，请创建服务的客户端实例。
1. 启动服务并处理结果。

AEMLiveCycle连接器通过将这些客户端实例公开为OSGi服务（可使用标准OSGi方式访问）简化了流程。 LiveCycle连接器提供以下功能：

* OSGi服务形式的客户端实例：中列出了打包为OSGI捆绑包的客户端 [Acrobat Services列表](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) 部分。 每个客户端jar都在OSGi服务注册表中将客户端实例注册为OSGi服务。
* 用户凭据传播：在中心位置管理连接到LiveCycle服务器所需的连接详细信息。
* ServiceClientFactory服务：要启动进程，客户端应用程序可以访问ServiceClientFactory实例。

### 从OSGi服务注册表中通过服务引用启动 {#starting-via-service-references-from-osgi-service-registry}

要从AEM中启动公开的服务，请执行以下步骤：

1. 确定maven依赖项。 将依赖项添加到maven pom.xml文件中所需的客户端jar。 至少应向adobe-livecycle-client和adobe-usermanager-client jar添加依赖项。

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   要启动服务，请为该服务添加相应的Maven依赖项。 有关依赖关系列表，请参见 [Acrobat服务列表](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). 例如，对于生成PDF服务，添加以下依赖关系：

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. 获取服务引用。 获取服务实例的句柄。 如果要编写Java™类，可以使用Declarative Services注释。

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   上述代码片段启动GeneratePdfServiceClient的createPDF API以将文档转换为PDF。 在JSP中，可以使用以下代码执行类似的调用。 主要区别在于以下代码使用Sling ScriptHelper访问GeneratePdfServiceClient。

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### 通过ServiceClientFactory启动 {#starting-via-serviceclientfactory}

有时需要ServiceClientFactory类。 例如，需要ServiceClientFactory调用进程。

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## 运行方式支持 {#runas-support}

几乎所有LiveCycle中的Acrobat服务都需要身份验证。 您可以使用以下任意选项启动这些服务，而无需在代码中提供显式凭据：

### 允许列表配置 {#allowlist-configuration}

LiveCycle客户端SDK配置包含有关服务名的设置。 此配置是调用逻辑开箱即用管理员凭据的服务列表。 例如，如果将DirectoryManager服务（用户管理API的一部分）添加到此列表，则任何客户端代码都可以直接使用该服务。 此外，调用层会在发送给LiveCycle服务器的请求过程中自动传递配置的凭据。

### RunAsManager {#runasmanager}

作为集成的一部分，提供了新的服务RunAsManager。 它可让您以编程方式控制调用LiveCycle服务器时要使用的凭据。

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

如果要传递其他凭据，可以使用采用PasswordCredential实例的重载方法。

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest属性 {#invocationrequest-property}

如果调用进程或直接使用ServiceClientFactory类并创建InvocationRequest，则可以指定一个属性来指示调用层应使用配置的凭据。

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Acrobat Services列表 {#document-services-list}

### AdobeLiveCycle客户端SDK API包 {#adobe-livecycle-client-sdk-api-bundle}

可以使用以下服务：

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Maven依赖项 {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle客户端SDK包 {#adobe-livecycle-client-sdk-bundle}

可以使用以下服务：

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Maven依赖项 {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### AdobeLiveCycleTaskManager客户端包 {#adobe-livecycle-taskmanager-client-bundle}

可以使用以下服务：

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Maven依赖项 {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle Workflow客户端捆绑包 {#adobe-livecycle-workflow-client-bundle}

以下服务可用：

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Maven依赖项 {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle PDF Generator客户端捆绑包 {#adobe-livecycle-pdf-generator-client-bundle}

以下服务可用：

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Maven依赖项 {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle应用程序管理器客户端包 {#adobe-livecycle-application-manager-client-bundle}

可以使用以下服务：

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Maven依赖项 {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle汇编程序客户端包 {#adobe-livecycle-assembler-client-bundle}

以下服务可用：

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Maven依赖项 {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle表单数据集成客户端捆绑包 {#adobe-livecycle-form-data-integration-client-bundle}

以下服务可用：

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Maven依赖项 {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms客户端捆绑包 {#adobe-livecycle-forms-client-bundle}

以下服务可用：

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Maven依赖项 {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output客户端捆绑包 {#adobe-livecycle-output-client-bundle}

以下服务可用：

* com.adobe.livecycle.output.client.OutputClient

#### Maven依赖项 {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions客户端捆绑包 {#adobe-livecycle-reader-extensions-client-bundle}

以下服务可用：

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Maven依赖项 {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle权限管理器客户端包 {#adobe-livecycle-rights-manager-client-bundle}

可以使用以下服务：

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Maven依赖项 {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle签名客户端包 {#adobe-livecycle-signatures-client-bundle}

以下服务可用：

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Maven依赖项 {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycleTruststore客户端捆绑包 {#adobe-livecycle-truststore-client-bundle}

可以使用以下服务：

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Maven依赖项 {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### AdobeLiveCycle存储库客户端包 {#adobe-livecycle-repository-client-bundle}

可以使用以下服务：

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Maven依赖项 {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
