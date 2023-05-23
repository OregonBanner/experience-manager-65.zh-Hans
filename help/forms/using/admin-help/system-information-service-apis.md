---
title: 系統資訊服務API
seo-title: System information Service APIs
description: 本檔案提供System Information Service所提供API的詳細資訊。
seo-description: This document provides detailed information about the APIs provided bythesystem information service.
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 系統資訊服務API {#system-information-service-apis}

系統資訊服務提供一組REST API來擷取資訊。 下表提供有關API的詳細資訊：

<table>
 <thead>
  <tr>
   <th><p>名称</p></th>
   <th><p>URL</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]：[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>此API是以下專案的包裝函式： <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> Java API。 它會擷取目前工作環境的設定。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>擷取主機作業系統的所有環境變數。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>下載包含應用程式伺服器記錄檔的zip檔案。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>擷取config.xml檔案的所有內容。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>擷取AEM表單服務的狀態和設定引數。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>擷取伺服器運作時間、JVM引數、系統記憶體、棧積大小、作業系統名稱、作用中執行緒數目和執行緒計數。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>擷取下列屬性的值：</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposalTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>擷取有關資料庫的詳細資訊。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>擷取已安裝的AEM表單元件的版本和授權資訊。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>下載主機應用程式伺服器的組態檔。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads？delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.threads？delay=[n]&amp;iterations=[n]</p></td>
   <td><p>擷取作用中執行緒的計數和棧疊追蹤。 它接受下列引數：</p>
    <ul>
     <li><p>反複專案= [n]：指定反複專案的計數。 以數字取代n。 </p></li>
     <li><p>Delay= [n]：指定在開始下一個反複專案之前等待的毫秒數。 </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]：[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>此API是所有系統資訊服務API的包裝函式。 在內部，它會執行所有系統資訊API，並以zip格式下載資訊。 </p><p><i><strong>注意</strong>： SystemInfo.info不提供作用中執行緒的計數和棧疊追蹤。 </i></p></td>
  </tr>
 </tbody>
</table>
