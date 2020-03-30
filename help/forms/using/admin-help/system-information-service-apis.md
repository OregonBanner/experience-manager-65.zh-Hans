---
title: 系统信息服务API
seo-title: 系统信息服务API
description: 本文档提供有关系统信息服务提供的API的详细信息。
seo-description: 本文档提供有关系统信息服务提供的API的详细信息。
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 系统信息服务API {#system-information-service-apis}

系统信息服务提供一组REST API来检索信息。 下表提供了有关API的详细信息：

<table>
 <thead>
  <tr>
   <th><p>名称</p></th>
   <th><p>URL</p></th>
   <th><p>说明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.properties`</p></td>
   <td><p>此API是system.getProperties <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()"></a> Java API的包装器。 它检索当前工作环境的配置。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.envVar</p></td>
   <td><p>检索主机操作系统的所有环境变量。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.logs</p></td>
   <td><p>下载包含应用程序服务器日志的zip文件。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.config</p></td>
   <td><p>检索config.xml文件的所有内容。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.services</p></td>
   <td><p>检索AEM表单服务的状态和配置参数。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.vitalDetails</p></td>
   <td><p>检索服务器正常运行时间、JVM参数、系统内存、堆大小、操作系统名称、活动线程数和线程数。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.coreSettings</p></td>
   <td><p>检索以下属性的值：</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposationTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>启用FIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.database</p></td>
   <td><p>检索有关数据库的详细信息。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.licenseInfo</p></td>
   <td><p>检索已安装AEM表单组件的版本和许可证信息。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.serverConfig</p></td>
   <td><p>下载主机应用程序服务器的配置文件。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>检索活动线程的计数和堆栈跟踪。 它接受以下参数：</p>
    <ul>
     <li><p>iterations= [n]:指定迭代计数。 用数字替换n。 </p></li>
     <li><p>延迟= [n]:指定在开始下一次迭代之前要等待的毫秒数。 </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.info</p></td>
   <td><p>此API是所有系统信息服务API的包装器。 在内部，它运行所有系统信息API并下载zip格式的信息。 </p><p><i><strong>注意</strong>:SystemInfo.info不提供活动线程的计数和堆栈跟踪。 </i></p></td>
  </tr>
 </tbody>
</table>

