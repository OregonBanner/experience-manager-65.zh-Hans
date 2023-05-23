---
title: 建立與使用解除安裝工單
seo-title: Creating and Consuming Jobs for Offloading
description: Apache Sling Discovery功能提供Java API，可讓您建立JobManager作業和使用這些作業的JobConsumer服務
seo-description: The Apache Sling Discovery feature provides a Java API that enables you to create JobManager jobs and JobConsumer services that consume them
uuid: d6a5beb0-0618-4b61-9b52-570862eac920
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: e7b6b9ee-d807-4eb0-8e96-75ca1e66a4e4
exl-id: 4e6f452d-0251-46f3-ba29-1bd85cda73a6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 建立與使用解除安裝工單{#creating-and-consuming-jobs-for-offloading}

Apache Sling Discovery功能提供Java API，可讓您建立JobManager作業和使用這些作業的JobConsumer服務。

如需建立解除安裝拓撲和設定主題使用量的相關資訊，請參閱 [正在解除安裝工作](/help/sites-deploying/offloading.md).

## 處理工作裝載 {#handling-job-payloads}

解除安裝架構會定義兩個用於識別工作裝載的工作屬性。 解除安裝復寫代理程式會使用這些屬性來識別要復寫到拓撲中執行個體的資源：

* `offloading.job.input.payload`：以逗號分隔的內容路徑清單。 內容會復寫到執行工作的執行處理。
* `offloading.job.output.payload`：以逗號分隔的內容路徑清單。 當工作執行完成時，會將工作裝載復寫到建立工作的執行個體上的這些路徑。

使用 `OffloadingJobProperties` 列舉以參照屬性名稱：

* `OffloadingJobProperties.INPUT_PAYLOAD.propertyName()`
* `OffloadingJobProperties.OUTPUT_PAYLOAD.propetyName()`

工作不需要裝載。 不過，如果工作需要操作資源，且工作解除安裝至未建立工作的電腦，則裝載是必要的。

## 建立解除安裝工作 {#creating-jobs-for-offloading}

建立呼叫JobManager.addJob方法的使用者端，以建立由自動選取的JobConsumer執行的工作。 提供下列資訊以建立工作：

* 主題：工作主題。
* 名稱： （選擇性）
* 屬性對應： A `Map<String, Object>` 包含任何數量屬性的物件，例如輸入裝載路徑和輸出裝載路徑。 執行工作的JobConsumer物件可使用此Map物件。

以下範例服務會為指定主題和輸入裝載路徑建立作業。

```java
package com.adobe.example.offloading;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;

import java.util.HashMap;

import org.apache.sling.event.jobs.Job;
import org.apache.sling.event.jobs.JobManager;

import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.ResourceResolver;

import com.adobe.granite.offloading.api.OffloadingJobProperties;

@Component
@Service
public class JobGeneratorImpl implements JobGenerator  {

 @Reference
 private JobManager jobManager;
 @Reference ResourceResolverFactory resolverFactory;

 public String createJob(String topic, String payload) throws Exception {
  Job offloadingJob;

  ResourceResolver resolver = resolverFactory.getResourceResolver(null);
  if(resolver.getResource(payload)!=null){

   HashMap<String, Object> jobprops = new HashMap<String, Object>();
   jobprops.put(OffloadingJobProperties.INPUT_PAYLOAD.propertyName(), payload);

   offloadingJob = jobManager.addJob(topic, null, jobprops);
  } else {
   throw new Exception("Payload for job cannot be found");
  }
  if (offloadingJob == null){
   throw new Exception ("Offloading job could not be created");
  }
  return offloadingJob.getId();
 }
}
```

為呼叫JobGeneratorImpl.createJob時，記錄會包含下列訊息 `com/adobe/example/offloading` 主題與 `/content/geometrixx/de/services` 裝載：

```shell
10.06.2013 15:43:33.868 *INFO* [JobHandler: /etc/workflow/instances/2013-06-10/model_1554418768647484:/content/geometrixx/en/company] com.adobe.example.offloading.JobGeneratorImpl Received request to make job for topic com/adobe/example/offloading and payload /content/geometrixx/de/services
```

## 開發工作消費者 {#developing-a-job-consumer}

若要使用工作，請開發實作的OSGi服務 `org.apache.sling.event.jobs.consumer.JobConsumer` 介面。 使用要使用的主題來識別 `JobConsumer.PROPERTY_TOPICS` 屬性。

以下範例JobConsumer實作會註冊 `com/adobe/example/offloading` 主題。 取用者只需將裝載內容節點的Consumed屬性設定為true即可。

```java
package com.adobe.example.offloading;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.event.jobs.Job;
import org.apache.sling.event.jobs.JobManager;
import org.apache.sling.event.jobs.consumer.JobConsumer;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Session;
import javax.jcr.Node;

import com.adobe.granite.offloading.api.OffloadingJobProperties;

@Component
@Service
public class MyJobConsumer implements JobConsumer {

 public static final String TOPIC = "com/adobe/example/offloading";

 @Property(value = TOPIC)
 static final String myTopic = JobConsumer.PROPERTY_TOPICS;

 @Reference
 private ResourceResolverFactory resolverFactory;

 @Reference
 private JobManager jobManager;

 private final Logger log = LoggerFactory.getLogger(getClass());

 public JobResult process(Job job) {
  JobResult result = JobResult.FAILED;
  String topic = job.getTopic();
  log.info("Consuming job of topic: {}", topic);
  String payloadIn =  (String) job.getProperty(OffloadingJobProperties.INPUT_PAYLOAD.propertyName());
  String payloadOut =  (String) job.getProperty(OffloadingJobProperties.OUTPUT_PAYLOAD.propertyName());

  log.info("Job has Input Payload {} and Output Payload {}",payloadIn, payloadOut);

  ResourceResolver resolver = null;
  try {
   resolver = resolverFactory.getAdministrativeResourceResolver(null);
   Session session = resolver.adaptTo(Session.class);
   Node inNode = session.getNode(payloadIn);
   inNode.getNode(Node.JCR_CONTENT).setProperty("consumed",true);
   result = JobResult.OK;
  }catch (Exception e){
   log.info("ERROR -- JOB RESULT IS FAILURE " + e.getMessage());
   result = JobResult.FAILED;
  }
  log.info("Job OK for payload {}",payloadIn);
  return result;
 }
}
```

MyJobConsumer類別會為/content/geometrixx/de/services的輸入裝載產生下列記錄訊息：

```shell
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Consuming job of topic: com/adobe/example/offloading
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job has Input Payload /content/geometrixx/de/services and Output Payload /content/geometrixx/de/services
10.06.2013 16:02:40.884 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job OK for payload /content/geometrixx/de/services
```

可以使用CRXDE Lite來觀察Consumed屬性：

![chlimage_1-25](assets/chlimage_1-25a.png)

## Maven相依性 {#maven-dependencies}

將下列相依性定義新增至您的pom.xml檔案，以便Maven能夠解析解除安裝相關類別。

```xml
<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.event</artifactId>
   <version>3.1.5-R1485539</version>
   <scope>provided</scope>
</dependency>
<dependency>
   <groupId>com.adobe.granite</groupId>
   <artifactId>com.adobe.granite.offloading.core</artifactId>
   <version>1.0.4</version>
   <scope>provided</scope>
</dependency>
```

前面的範例還需要下列相依性定義：

```xml
<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.api</artifactId>
   <version>2.4.3-R1488084</version>
   <scope>provided</scope>
</dependency>

<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
   <version>2.0.0</version>
   <scope>provided</scope>
</dependency>
```
