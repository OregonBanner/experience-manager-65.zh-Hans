---
title: 備份與還原服務APIQuick啟動
seo-title: Backup and Restore Service APIQuick Starts
description: 備份與還原服務APIQuick啟動
uuid: c3992be2-ceb4-480d-9c8f-71eb0ea66dde
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 813162be-dbf5-4dc1-80ff-e37dbc25ef60
role: Developer
exl-id: ae17fd3a-0ba4-4a00-907b-811e500b0e14
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 備份和還原服務API快速啟動 {#backup-and-restore-service-apiquick-starts}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

Java API快速入門(SOAP)適用於備份和還原服務API。

[快速入門：使用Java API(SOAP)進入備份模式](backup-restore-service-api-quick.md#quick-start-soap-mode-entering-backup-mode-using-the-java-api)

[快速入門：使用Java API(SOAP)離開備份模式](backup-restore-service-api-quick.md#quick-start-soap-mode-leaving-backup-mode-using-the-java-api)

AEM Forms作業可使用AEM Forms強型別API執行，且連線模式應設定為SOAP。

>[!NOTE]
>
>「使用AEM Forms進行程式設計」中的「快速入門」是以Forms作業系統為基礎。 不過，如果您使用其他作業系統（例如UNIX），請以適用的作業系統支援的路徑取代Windows特定路徑。 同樣地，如果您使用其他J2EE應用程式伺服器，請務必指定有效的連線屬性。 另請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## 快速入門（SOAP模式）：使用Java API進入備份模式 {#quick-start-soap-mode-entering-backup-mode-using-the-java-api}

以下Java程式碼範例會以唯一標籤進入備份模式兩小時。 在備份時間到期後或明確退出備份模式時，表單伺服器會返回從全域檔案儲存體清除檔案。 (請參閱 [在表單伺服器上進入備份模式](/help/forms/developing/preparing-aem-forms-backup.md#entering-backup-mode-on-the-forms-server).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-backup-restore-client-sdk.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.Properties;
 
 import com.adobe.idp.backup.dsc.client.BackupServiceClient;
 import com.adobe.idp.backup.dsc.service.BackupModeEntryResult;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class BackupRestoreEnter
 {
     public static void main(String[] args)
     {
         try
         {
             // Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a BackupService client object
             BackupServiceClient backup = new BackupServiceClient(myFactory);
 
             // Specify a generic label, 120 minutes to perform the backup,
             // and not to provide continous backup mode coverage (used for snapshot backups)
             String backUpLabel = new String("Snapshot2008July01");
             int minsInBackupMode = 120;
             boolean continousCoverage = false;
 
 
             // Enter backup mode on the forms server server
             BackupModeEntryResult backupResult = backup.enterBackupMode(backUpLabel,minsInBackupMode, continousCoverage);
 
             // Get information from entering backup mode ontheforms server server.
             if (backupResult != null)
             {
                 System.out.println("Start time is: " + backupResult.getStartTime());
                 System.out.println("Backup Current ID is: " + backupResult.getId());
                 System.out.println("Backup Previous ID is: " + backupResult.getPreviousReservationId());
                 System.out.println("Backup Label is: " + backupResult.getLabel());
                 System.out.println("Backup Time to complete is: " + backupResult.getReservationTimeout());
             }
             else
             {
                 System.out.println("Could not enter backup mode.");
             }
 
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
         return;
     }
 }
 
```

## 快速入門（SOAP模式）：使用Java API離開備份模式 {#quick-start-soap-mode-leaving-backup-mode-using-the-java-api}

以下Java程式碼範例明確導致Forms伺服器離開備份模式，並返回從全域檔案儲存體清除檔案。 (請參閱 [在表單伺服器上保留備份模式](/help/forms/developing/preparing-aem-forms-backup.md#leaving-backup-mode-on-the-forms-server).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-backup-restore-client-sdk.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.Properties;
 
 import com.adobe.idp.backup.dsc.client.BackupServiceClient;
 import com.adobe.idp.backup.dsc.service.BackupModeResult;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class BackupRestoreLeave
 {
 
     public static void main(String[] args)
     {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'server':`port`");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a BackupService object
             BackupServiceClient backup = new BackupServiceClient(myFactory);
 
             // Leave backup mode on the forms server
             BackupModeResult leaveBackupResult = backup.leaveBackupMode();
 
             //Get result information from leaving backup mode
             if (leaveBackupResult != null)
             {
                 System.out.println("Backup Mode ID is : " + leaveBackupResult.getId());
             }
             else
             {
                 System.out.println("Forms server is not in backup mode.");
             }
 
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
         return;
     }
 }
 
```
