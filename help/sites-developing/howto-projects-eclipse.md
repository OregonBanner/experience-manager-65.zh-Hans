---
title: 如何使用Eclipse開發AEM專案
seo-title: How to Develop AEM Projects Using Eclipse
description: 本指南說明如何使用Eclipse開發以AEM為基礎的專案
seo-description: This guide describes how to use Eclipse for developing AEM based projects
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 如何使用Eclipse開發AEM專案{#how-to-develop-aem-projects-using-eclipse}

本指南說明如何使用Eclipse開發以AEM為基礎的專案。

>[!NOTE]
>
>Adobe現在提供 [Eclipse適用的AEM開發工具](/help/sites-developing/aem-eclipse.md) 可協助您使用Eclipse開發AEM解決方案。

## 概述 {#overview}

若要開始使用Eclipse的AEM開發，需要下列步驟。

在本How-To的其餘部分中將更詳細地說明其中的每項。

* 安裝Eclipse 4.3 (Kepler)
* 根據Maven設定您的AEM專案
* 在Maven POM中為Eclipse準備JSP支援
* 將Maven專案匯入Eclipse

>[!NOTE]
>
>本指南以Eclipse 4.3 (Kepler)和AEM 5.6.1為基礎。

## 安裝Eclipse {#install-eclipse}

下載「適用於Java EE開發人員的Eclipse IDE」，網址為 [Eclipse下載頁面](https://www.eclipse.org/downloads/).

請依照以下說明安裝Eclipse [安裝指示](https://wiki.eclipse.org/Eclipse/Installation).

## 根據Maven設定您的AEM專案 {#set-up-your-aem-project-based-on-maven}

接下來，使用Maven設定您的專案，如所述 [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md).

## 為Eclipse準備JSP支援 {#prepare-jsp-support-for-eclipse}

Eclipse也可支援使用JSP，例如

* 自動完成標籤程式庫
* 定義的物件的Eclipse感知功能 &lt;cq:defineobjects /> 和 &lt;sling:defineobjects />

為了讓此功能發揮作用：

1. 請依照以下說明操作： [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) 在 [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md).
1. 將下列專案新增至 &lt;build /> 區段。

   Eclipse的Maven支援外掛程式m2e不提供對maven-jspc-plugin的支援，此設定會告知m2e忽略外掛程式和清除暫時編譯結果的相關任務。

   這不是問題：如中所述 [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)，此設定中的maven-jspc-plugin僅用於驗證JSP是否編譯為建置流程的一部分。 Eclipse已回報JSP中的任何問題，且不依賴此Maven外掛程式來回報。

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### 將Maven專案匯入Eclipse {#import-the-maven-project-into-eclipse}

1. 在Eclipse中，選擇「檔案>匯入……」
1. 在「匯入」對話方塊中，選擇「Maven」>「現有Maven專案」，然後按一下「下一步」。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 輸入專案最上層資料夾的路徑，然後按一下「全選」和「完成」。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 現在您已準備好使用Eclipse來開發您的AEM專案，包括JSP自動完成。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >若包含 `/libs/foundation/global.jsp` 或其他JSP `/libs`，您必須將其複製到專案，Eclipse才能解決包含問題。 同時，您需要確保它沒有被Maven捆綁到您的內容套件中。 中會說明如何達成此目的 [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md).
