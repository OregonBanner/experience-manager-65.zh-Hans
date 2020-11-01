---
title: Application Manager客户端JavaAPI快速开始(SOAP)
seo-title: Application Manager客户端JavaAPI快速开始(SOAP)
description: Application Manager客户端JavaAPI快速开始(SOAP)
uuid: 043f1c08-c7de-4e2d-88ca-b46428b1b551
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2ec2a75e-4191-4660-a6f2-26cc667720b3
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# Application Manager客户端JavaAPI快速开始(SOAP) {#application-manager-client-javaapi-quick-start-soap}

以下Java API快速开始(SOAP)可用于Application Manager客户端。

[快速开始（SOAP模式）:使用Java API创建应用程序版本](#quick-start-soap-mode-creating-application-version-using-the-java-api)

[快速开始（SOAP模式）:使用Java API导出应用程序](#quick-start-soap-mode-exporting-applications-using-the-java-api)

[快速开始（SOAP模式）:使用Java API导入应用程序](#quick-start-soap-mode-importing-applications-using-the-java-api)

[快速开始（SOAP模式）:使用Java API获取AEM Forms应用程序](application-manager-client-java-api.md#quick-start-soap-mode-getting-a-application-using-the-java-api)

[快速开始（SOAP模式）:使用Java API获取应用程序](application-manager-client-java-api.md#quick-start-soap-mode-getting-the-applications-using-the-java-api)

[快速开始（SOAP模式）:使用Java API获取应用程序状态](application-manager-client-java-api.md#quick-start-soap-mode-getting-status-of-applications-using-java-api)

[快速开始（SOAP模式）：使用Java API预览AEM Forms和更高版本的应用程序存档](application-manager-client-java-api.md#quick-start-soap-mode-previewing-the-livecycle-es2-and-later-application-archive-using-the-java-api)

[快速开始（SOAP模式）：使用Java API删除AEM Forms应用程序存档](application-manager-client-java-api.md#quick-start-soap-mode-deleting-the-application-archive-using-the-java-api)

AEM Forms操作可以使用AEM Forms强类型API执行，连接模式应设置为SOAP。

>[!NOTE]
>
>“使用AEM Forms进行编程”中的快速开始基于部署在JBoss和Windows操作系统上的Forms服务器。 但是，如果您使用的是其他操作系统，如Unix，则将特定于窗口的路径替换为适用操作系统支持的路径。 同样，如果您使用的是另一台J2EE应用程序服务器，请确保指定有效的连接属性。 请参 [阅设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

## 快速开始（SOAP模式）:使用Java API创建应用程序版本 {#quick-start-soap-mode-creating-application-version-using-the-java-api}

以下Java代码示例使用JAVA API创建应用程序。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 * 3. adobe-application-remote-client.jar
 * 4. adobe-repository-client.jar
 * 5. activation.jar (required for SOAP mode)
 * 6. axis.jar (required for SOAP mode)
 * 7. commons-codec-1.3.jar (required for SOAP mode)
 * 8. commons-collections-3.1.jar  (required for SOAP mode)
 * 9. commons-discovery.jar (required for SOAP mode)
 * 10. commons-logging.jar (required for SOAP mode)
 * 11. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 12. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 13. jaxrpc.jar (required for SOAP mode)
 * 14. log4j.jar (required for SOAP mode)
 * 15. mail.jar (required for SOAP mode)
 * 16. saaj.jar (required for SOAP mode)
 * 17. wsdl4j.jar (required for SOAP mode)
 * 18. xalan.jar (required for SOAP mode)
 * 19. xbean.jar (required for SOAP mode)
 * 20. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 *
 *
 */
package com.adobe.idp.dsc.applicationmanager;
import java.util.Properties;
import java.util.Random;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClient;
import com.adobe.repository.bindings.ResourceRepositoryDelegate;
import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
public class CreateApplicationVersion_SOAP {
    private static String applicationFolder = "Applications";
    private static String defaultAppVersion = "1.0";
    public static void main(String[] args) {
        // Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
        connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT",
                "https://'[server]:[port]'");
        connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL",
                ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty("DSC_SERVER_TYPE",
                ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
        connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
        connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
        // Create ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory
                .createInstance(connectionProps);
        // Create ApplicationManagerClient object
        ApplicationManagerClient appClient = new ApplicationManagerClient(
                myFactory);
        // Create ResourceRepositoryDelegate object
        ResourceRepositoryDelegate repositoryClient = new ResourceRepositoryClient(
                myFactory);
        final Random num = new Random();
        String appName = "App" + num.nextInt();
        String newAppName = null;
        try {
            // Create application with default application version
            newAppName = appClient.createApplication(appName);
            if (repositoryClient.resourceExists("/" + applicationFolder + "/"
                    + appName.toString() + "/" + defaultAppVersion)) {
                System.out.println("Application with name: " + appName + "/"
                        + defaultAppVersion + " is created succesfully!");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        try {
            // Create version of the new application
            appName = appClient.createApplicationVersion(newAppName,
                    defaultAppVersion, "2.0", "version increment");
            if (repositoryClient.resourceExists("/" + applicationFolder + "/"
                    + appName.toString() + "/" + "2.0")) {
                System.out.println("Application version 2.0 created : "
                        + appName + "/" + "2.0");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 快速开始（SOAP模式）:使用Java API导出应用程序 {#quick-start-soap-mode-exporting-applications-using-the-java-api}

以下Java代码示例使用JAVA API导出应用程序。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 * 3. adobe-application-remote-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 *
 *
 */
package com.adobe.idp.dsc.applicationmanager;
import java.io.File;
import java.io.FileInputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.Properties;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClient;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClientException;
public class ExportLCA_SOAP {
    public static void main(String[] args) {
        // Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
        connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT",
                "https://'[server]:[port]'");
        connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL",
                ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty("DSC_SERVER_TYPE",
                ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
        connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
        connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
        // Create ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory
                .createInstance(connectionProps);
        // Create ApplicationManagerClient object
        ApplicationManagerClient appClient = new ApplicationManagerClient(
                myFactory);
        Document doc = null;
        try {
            final FileInputStream fileApp = new FileInputStream(
                    "C:\\ImportSampleApp2.lca");
            doc = new Document(fileApp);
        } catch (Exception e) {
            e.printStackTrace();
        }
        String resourceID = null;
        try {
            // Import the application into the LC server
            resourceID = appClient.importApplication(doc);
            System.out.println("Import application with resource ID:"
                    + resourceID + " is completed successfully!");
        } catch (ApplicationManagerClientException e) {
            e.printStackTrace();
        }
        final String sampleAppName = "ExportSampleApp2";
        try {
            final List<String> eReqList = new ArrayList<String>();
            eReqList.add(resourceID);
            // Export the application imported above
            doc = appClient.export(eReqList, "lcaDescription");
            // Save into local LCA file
            final String archiveName = "C:/" + sampleAppName + "-" + "1.0"
                    + ".lca";
            final File fTemp = new File(archiveName);
            doc.copyToFile(fTemp);
            System.out.println("Export application completed with name: "
                    + archiveName);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 快速开始（SOAP模式）:使用Java API导入应用程序 {#quick-start-soap-mode-importing-applications-using-the-java-api}

以下Java代码示例使用JAVA API导入应用程序。

>[!NOTE]
>
>Java API importApplication()用较新的应用程序替换具有相同名称的现有应用程序。 要更新现有应用程序，请使用API importApplication()代替API updateApplication()。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 * 3. adobe-application-remote-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 *
 *
 */
package com.adobe.idp.dsc.applicationmanager;
import java.io.FileInputStream;
import java.util.Properties;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClient;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClientException;
public class ImportLCA_SOAP {
    public static void main(String[] args) {
        // Set connection properties required to invoke AEM FOrms
        Properties connectionProps = new Properties();
        connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT",
                "https://'[server]:[port]'");
        connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL",
                ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty("DSC_SERVER_TYPE",
                ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
        connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
        connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
        // Create ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory
                .createInstance(connectionProps);
        // Create ApplicationManagerClient object
        ApplicationManagerClient appClient = new ApplicationManagerClient(
                myFactory);
        Document doc = null;
        try {
            final FileInputStream fileApp = new FileInputStream(
                    "C:\\ImportSampleApp2.lca");
            doc = new Document(fileApp);
        } catch (Exception e) {
            e.printStackTrace();
        }
        try {
            // Import the application into the LC server
            final String resourceID = appClient.importApplication(doc);
            System.out.println("Import application with resource ID:"
                    + resourceID + " is completed successfully!");
        } catch (ApplicationManagerClientException e) {
            e.printStackTrace();
        }
    }
}
```

## 快速开始（SOAP模式）:使用Java API获取应用程序 {#quick-start-soap-mode-getting-a-application-using-the-java-api}

以下Java代码示例使用Java API获取应用程序。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 * 3. adobe-application-remote-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 *
 *
 */
package com.adobe.idp.dsc.applicationmanager;

import java.io.FileInputStream;
import java.util.Properties;

import com.adobe.idp.Document;
import com.adobe.idp.applicationmanager.application.Application;
import com.adobe.idp.applicationmanager.application.ApplicationId;
import com.adobe.idp.applicationmanager.application.impl.ApplicationIdImpl;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClient;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClientException;

public class GetApplication_SOAP {

    public static void main(String[] args) {
        //Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
        connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
        connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL", ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
        connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
        connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");

        //Create ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
        //Create ApplicationManagerClient object
        ApplicationManagerClient appClient = new ApplicationManagerClient(myFactory);

        Document doc = null;
        try {

            final FileInputStream fileApp = new FileInputStream("C:\\appraisal.lca");
            doc = new Document(fileApp);

        } catch (Exception e) {
            e.printStackTrace();
        }
        final String sampleAppName = "Samples - Performance Appraisal";
        try {

            //Import the application into the LC server
            final String resourceID = appClient.importApplication(doc);
            System.out.println("Import application with resource ID: " + resourceID + " is completed successfully!");
            //Deploy the application
            boolean result = appClient.deployApplication(sampleAppName);
            if (result) {
                System.out.println("Imported application is deployed.");
            }
        } catch (ApplicationManagerClientException e) {
            e.printStackTrace();
        }

        //Initialize the ApplicationId instance
        ApplicationId appId = new ApplicationIdImpl();
        appId.setApplicationName(sampleAppName);

        try {
                //Get the application by application id
                Application app = appClient.getApplication(appId);
                System.out.println("Get application with name: " + app.getApplicationId().getApplicationName());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 快速开始（SOAP模式）:使用Java API获取应用程序 {#quick-start-soap-mode-getting-the-applications-using-the-java-api}

以下Java代码示例使用Java API获取应用程序。

**注**:获取AEM Forms应用程序API, getApplications()只返回已部署的应用程序。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 * 3. adobe-application-remote-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 *
 *
 */

package com.adobe.idp.dsc.applicationmanager;

import java.io.FileInputStream;
import java.util.List;
import java.util.Properties;

import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClient;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClientException;

public class GetApplications_SOAP {

    public static void main(String[] args) {
        //Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
        connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
        connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL", ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
        connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
        connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");

        //Create ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
        //Create ApplicationManagerClient object
        ApplicationManagerClient appClient = new ApplicationManagerClient(myFactory);

        Document doc = null;
        try {

            final FileInputStream fileApp = new FileInputStream("C:\\appraisal.lca");
            doc = new Document(fileApp);

        } catch (Exception e) {
            e.printStackTrace();
        }

        try {

            //Import the application into the LC server
            final String resourceID = appClient.importApplication(doc);
            System.out.println("Import application with resource ID: " + resourceID + " is completed successfully!");

        } catch (ApplicationManagerClientException e) {
            e.printStackTrace();
        }

        try {
                //Get applications from LC server
                List appList = appClient.getApplications();
                System.out.println("Get applications from LC Server: " + appList.size());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 快速开始（SOAP模式）:使用Java API获取应用程序状态 {#quick-start-soap-mode-getting-status-of-applications-using-java-api}

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 * 3. adobe-application-remote-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 *
 *
 */
package com.adobe.idp.dsc.applicationmanager;

import java.io.FileInputStream;
import java.util.Properties;

import com.adobe.idp.Document;
import com.adobe.idp.applicationmanager.application.ApplicationId;
import com.adobe.idp.applicationmanager.application.ApplicationStatus;
import com.adobe.idp.applicationmanager.application.impl.ApplicationIdImpl;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClient;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClientException;

public class GetApplicationStatus_SOAP {

    public static void main(String[] args) {
        //Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
        connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
        connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL", ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
        connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
        connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");

        //Create ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
        //Create ApplicationManagerClient object
        ApplicationManagerClient appClient = new ApplicationManagerClient(myFactory);

        Document doc = null;
        try {

            final FileInputStream fileApp = new FileInputStream("C:\\appraisal.lca");
            doc = new Document(fileApp);

        } catch (Exception e) {
            e.printStackTrace();
        }
        final String sampleAppName = "Samples - Performance Appraisal";
        try {

            //Import the application into the LC server
            final String resourceID = appClient.importApplication(doc);
            System.out.println("Import application with resource ID: " + resourceID + " is completed successfully!");
            //Deploy the application
            boolean result = appClient.deployApplication(sampleAppName);
            if (result) {
                System.out.println("Imported application is deployed.");
            }
        } catch (ApplicationManagerClientException e) {
            e.printStackTrace();
        }

        //Initialize the ApplicationId instance
        ApplicationId appId = new ApplicationIdImpl();
        appId.setApplicationName(sampleAppName);

        try {
                //Get the application by application id
                ApplicationStatus status = appClient.getApplicationStatus(appId);
                System.out.println("Get application status with code: " + status.getStatusCode());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 快速开始（SOAP模式）：使用Java API预览LiveCycleES2和更高版本的应用程序存档 {#quick-start-soap-mode-previewing-the-livecycle-es2-and-later-application-archive-using-the-java-api}

以下Java代码示例用于使用Java API预览AEM Forms和更高版本的应用程序存档。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 * 3. adobe-application-remote-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 */
package com.adobe.idp.dsc.applicationmanager;
import java.io.FileInputStream;
import java.util.Properties;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClient;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClientException;
public class PreviewLCA_SOAP {
    public static void main(String[] args) {
        //Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
        connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
        connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL", ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
        connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
        connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
        //Create ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
        //Create ApplicationManagerClient object
        ApplicationManagerClient appClient = new ApplicationManagerClient(myFactory);

        Document doc = null;
        try {

            final FileInputStream fileApp = new FileInputStream("C:\\appraisal.lca");
            doc = new Document(fileApp);

        } catch (Exception e) {
            e.printStackTrace();
        }

        try {

            //Preview the LCA
            final Document newDoc = appClient.previewLCA(doc);

        } catch (ApplicationManagerClientException e) {
            e.printStackTrace();
        }
    }
}
```

## 快速开始（SOAP模式）：使用Java API删除应用程序存档 {#quick-start-soap-mode-deleting-the-application-archive-using-the-java-api}

以下Java代码示例用于删除应用程序归档文件。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 * 3. adobe-application-remote-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
 * 8. commons-discovery.jar (required for SOAP mode)
 * 9. commons-logging.jar (required for SOAP mode)
 * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
 * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
 * 12. jaxrpc.jar (required for SOAP mode)
 * 13. log4j.jar (required for SOAP mode)
 * 14. mail.jar (required for SOAP mode)
 * 15. saaj.jar (required for SOAP mode)
 * 16. wsdl4j.jar (required for SOAP mode)
 * 17. xalan.jar (required for SOAP mode)
 * 18. xbean.jar (required for SOAP mode)
 * 19. xercesImpl.jar (required for SOAP mode)
 *
 * These JAR files are located in the following path:
 * <install directory>/sdk/client-libs/common
 *
 *
 * SOAP required JAR files are located in the following path:
 * <install directory>/sdk/client-libs/thirdparty
 *
 *
 */
package com.adobe.idp.dsc.applicationmanager;

import java.io.FileInputStream;
import java.util.Properties;

import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClient;
import com.adobe.livecycle.applicationmanager.client.ApplicationManagerClientException;

public class DeleteApplication_SOAP {

    public static void main(String[] args) {
        //Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
        connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
        connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL", ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
        connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
        connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");

        //Create ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
        //Create ApplicationManagerClient object
        ApplicationManagerClient appClient = new ApplicationManagerClient(myFactory);

        Document doc = null;
        try {

            final FileInputStream fileApp = new FileInputStream("C:\\appraisal.lca");
            doc = new Document(fileApp);

        } catch (Exception e) {
            e.printStackTrace();
        }

        try {

            //Import the application into the LC server
            final String resourceID = appClient.importApplication(doc);
            System.out.println("Import application with resource ID: " + resourceID + " is completed successfully!");

        } catch (ApplicationManagerClientException e) {
            e.printStackTrace();
        }
        final String sampleAppName = "Samples - Performance Appraisal";
        try {
                //Delete the application imported above
                appClient.deleteApplication(sampleAppName, "1.0");
                System.out.println("Delete application completed with name: " + sampleAppName);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

