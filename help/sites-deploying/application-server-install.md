---
title: 應用程式伺服器安裝
seo-title: Application Server Install
description: 瞭解如何使用應用程式伺服器安裝AEM。
seo-description: Learn how to install AEM with an application server.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# 應用程式伺服器安裝{#application-server-install}

>[!NOTE]
>
>`JAR` 和 `WAR` AEM發行所在的檔案型別。 這些格式正在進行品質保證，以符合Adobe所承諾的支援層級。

本節將說明如何使用應用程式伺服器安裝Adobe Experience Manager (AEM)。 請參閱 [支援的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 區段，以瞭解針對個別應用程式伺服器所提供的特定支援層級。

說明下列應用程式伺服器的安裝步驟：

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [oracleWebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

如需有關安裝Web應用程式、伺服器設定以及如何啟動和停止伺服器的詳細資訊，請參閱適當的應用程式伺服器檔案。

>[!NOTE]
>
>如果您在WAR部署中使用Dynamic Media，請參閱 [Dynamic Media檔案](/help/assets/config-dynamic.md#enabling-dynamic-media).

## 一般說明 {#general-description}

### 在應用程式伺服器中安裝AEM時的預設行為 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM會以單一war檔案的形式來部署。

如果部署，預設將會發生下列情況：

* 執行模式為 `author`
* 執行個體（存放庫、Felix OSGI環境、套件組合等） 安裝於 `${user.dir}/crx-quickstart`位置 `${user.dir}` 是當前工作目錄，此路徑會呼叫crx-quickstart `sling.home`

* 上下文根目錄是war檔案名稱，例如： `aem-6`

#### 配置 {#configuration}

您可以透過下列方式變更預設行為：

* 執行模式：設定 `sling.run.modes` 中的引數 `WEB-INF/web.xml` 部署前AEM war檔案的檔案

* sling.home：設定 `sling.home` 中的引數 `WEB-INF/web.xml`部署前AEM war檔案的檔案

* 內容根目錄：重新命名AEM war檔案

#### 發佈安裝 {#publish-installation}

若要部署發佈執行個體，您必須將執行模式設定為發佈：

* 從AEM war檔案中解壓縮WEB-INF/web.xml
* 將sling.run.modes引數變更為發佈
* 將web.xml檔案重新封裝成AEM war檔案
* 部署AEM war檔案

#### 安裝檢查 {#installation-check}

若要檢查是否已安裝all，您可以：

* 追蹤 `error.log`檔案來檢視是否已安裝所有內容
* 檢視 `/system/console` 已安裝所有組合

#### 同一應用程式伺服器上的兩個執行個體 {#two-instances-on-the-same-application-server}

為了示範，適合將製作和發佈執行個體安裝在一個應用程式伺服器上。 為此，請執行以下操作：

1. 變更發佈執行個體的sling.home變數和sling.run.modes變數。
1. 從AEM war檔案中解壓縮WEB-INF/web.xml檔案。
1. 將sling.home引數變更為不同的路徑（可以使用絕對和相對路徑）。
1. 將sling.run.modes變更為針對發佈執行個體發佈。
1. 重新封裝web.xml檔案。
1. 重新命名war檔案，使其擁有不同的名稱：例如，將其中一個重新命名為aemauthor.war，將另一個重新命名為aempublish.war。
1. 使用較高的記憶體設定，例如，預設AEM執行個體使用 — Xmx3072m
1. 部署兩個Web應用程式。
1. 部署後，請停止兩個Web應用程式。
1. 在author和publish執行個體中，都會確保在sling.properties檔案中，屬性felix.service.urlhandlers=false會設為false （預設值為設為true）。
1. 再次啟動兩個Web應用程式。

## 應用程式伺服器的安裝程式 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

在部署之前，請閱讀 [一般說明](#general-description) 以上。

**伺服器準備**

* 讓基本驗證標題通過：

   * 讓AEM驗證使用者身份的一種方法是停用WebSphere伺服器的全域管理安全性，方法是移至[安全性] -> [全域安全性]並取消勾選[啟用管理安全性]核取方塊，儲存並重新啟動伺服器。

* set `"JAVA_OPTS= -Xmx2048m"`
* 如果您想要使用內容根目錄= /安裝AEM，則必須先變更現有預設Web應用程式的內容根目錄

**部署AEM Web應用程式**

* 下載AEM war檔案
* 視需要在web.xml中建立設定（請參閱上方的「一般說明」）

   * 解壓縮WEB-INF/web.xml檔案
   * 將sling.run.modes引數變更為發佈
   * 取消註解sling.home初始引數並視需要設定此路徑
   * 重新封裝web.xml檔案

* 部署AEM war檔案

   * 選擇內容根目錄（如果要設定sling執行模式，則需要選取部署精靈的詳細步驟，然後在精靈的步驟6中指定它）

* 啟動AEM網頁應用程式

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

在部署之前，請閱讀 [一般說明](#general-description) 以上。

**準備JBoss伺服器**

在您的conf檔案中設定記憶體引數(例如 `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果您使用的部署掃描器來安裝AEM Web應用程式，則增加 `deployment-timeout,` 針對該集合 `deployment-timeout` 屬性（例如，Attribute） `configuration/standalone.xml)`：

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署AEM Web應用程式**

* 在您的JBoss管理主控台中上傳AEM Web應用程式。

* 啟用AEM Web應用程式。

#### oracleWebLogic 12.1.3/12.2 {#oracle-weblogic}

在部署之前，請閱讀 [一般說明](#general-description) 以上。

這會使用只有管理伺服器的簡單伺服器配置。

**WebLogic伺服器準備**

* 在 `${myDomain}/config/config.xml`新增至security-configuration區段：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 檢視於 [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) 正確位置（預設情況下，將其定位在截面的結尾是ok）

* 增加VM記憶體設定：

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp .sh)搜尋WLS_MEM_ARGS，設定，例如設定 `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新啟動WebLogic Server

* 建立於 `${myDomain}` 套件資料夾和cq資料夾內以及計畫資料夾內

**部署AEM Web應用程式**

* 下載AEM war檔案
* 將AEM war檔案放入${myDomain}/packages/cq資料夾
* 在中進行設定 `WEB-INF/web.xml` 如有需要（請參閱上述「一般說明」）

   * 解壓縮 `WEB-INF/web.xml`檔案
   * 將sling.run.modes引數變更為發佈
   * 取消註解sling.home初始引數並視需要設定此路徑（請參閱一般說明）
   * 重新封裝web.xml檔案

* 將AEM war檔案部署為應用程式（其他設定則使用預設設定）
* 安裝可能需要一些時間……
* 檢查安裝是否已如一般說明中所述完成（例如，追蹤error.log）
* 您可以在WebLogic的Web應用程式的「組態」標籤中變更前後關聯根目錄 `/console`

#### Tomcat 8/8.5 {#tomcat}

在部署之前，請閱讀 [一般說明](#general-description) 以上。

* **準備Tomcat伺服器**

   * 增加VM記憶體設定：

      * 在 `bin/catalina.bat` (resp `catalina.sh` 在unix上)新增下列設定：
      * `set "JAVA_OPTS= -Xmx2048m`
   * 在安裝時，Tomcat不會啟用管理員或管理員存取權。 因此，您必須手動編輯 `tomcat-users.xml` 若要允許這些帳戶的存取：

      * 編輯 `tomcat-users.xml` 以包含「管理員」和「管理員」的存取權。 設定看起來應該類似以下範例：

         ```xml
         <?xml version='1.0' encoding='utf-8'?>
         <tomcat-users>
         role rolename="manager"/>
         role rolename="tomcat"/>
         <role rolename="admin"/>
         <role rolename="role1"/>
         <role rolename="manager-gui"/>
         <user username="both" password="tomcat" roles="tomcat,role1"/>
         <user username="tomcat" password="tomcat" roles="tomcat"/>
         <user username="admin" password="admin" roles="admin,manager-gui"/>
         <user username="role1" password="tomcat" roles="role1"/>
         </tomcat-users>
         ```
   * 如果您想要使用內容根目錄「/」部署AEM，則必須變更現有ROOT Webapp的內容根目錄：

      * 停止和取消部署ROOT Web應用程式
      * 重新命名tomcat webapps資料夾中的ROOT.war資料夾
      * 再次啟動Web應用程式
   * 如果您使用manager-gui安裝AEM Web應用程式，則需要增加上傳檔案的最大尺寸，因為預設僅允許50MB上傳大小。 針對開啟管理程式Web應用程式的web.xml，

      `webapps/manager/WEB-INF/web.xml`

      並將max-file-size和max-request-size增加到至少500MB，請參閱以下內容 `multipart-config` 此類的範例 `web.xml` 檔案。

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **部署AEM Web應用程式**

   * 下載AEM war檔案
   * 視需要在web.xml中建立設定（請參閱上方的「一般說明」）

      * 解壓縮WEB-INF/web.xml檔案
      * 將sling.run.modes引數變更為發佈
      * 取消註解sling.home初始引數並視需要設定此路徑
      * 重新封裝web.xml檔案
   * 如果您想要將AEM war檔案部署為根webapp，請將其重新命名為ROOT.war；如果您想要將aemauthor重新命名為內容根，請將其重新命名為aemauthor.war
   * 將其複製到tomcat的webapps資料夾
   * 等到AEM安裝完成


## 疑难解答 {#troubleshooting}

如需有關處理安裝期間可能出現的問題之資訊，請參閱：

* [疑难解答](/help/sites-deploying/troubleshooting.md)
