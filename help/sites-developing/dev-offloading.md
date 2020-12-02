---
title: 为卸载创建和使用作业
seo-title: 为卸载创建和使用作业
description: Apache Sling Discovery功能提供一个Java API，使您能够创建JobManager作业和使用这些作业的JobConsumer服务
seo-description: Apache Sling Discovery功能提供一个Java API，使您能够创建JobManager作业和使用这些作业的JobConsumer服务
uuid: d6a5beb0-0618-4b61-9b52-570862eac920
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: e7b6b9ee-d807-4eb0-8e96-75ca1e66a4e4
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---


# 为卸载创建和使用作业{#creating-and-consuming-jobs-for-offloading}

Apache Sling Discovery功能提供一个Java API，使您能够创建使用JobManager作业和JobConsumer服务。

有关创建卸载拓扑和配置主题使用情况的信息，请参阅[卸载作业](/help/sites-deploying/offloading.md)。

## 处理作业有效负荷{#handling-job-payloads}

卸载框架定义了两个用于标识作业有效负荷的作业属性。 卸载的复制代理使用这些属性来标识要复制到拓扑中实例的资源：

* `offloading.job.input.payload`:内容路径的逗号分隔列表。内容将复制到执行作业的实例。
* `offloading.job.output.payload`:内容路径的逗号分隔列表。作业执行完成后，作业有效负荷将复制到创建该作业的实例上的这些路径。

使用`OffloadingJobProperties`枚举引用属性名称：

* `OffloadingJobProperties.INPUT_PAYLOAD.propertyName()`
* `OffloadingJobProperties.OUTPUT_PAYLOAD.propetyName()`

作业不需要有效负载。 但是，如果作业需要对资源进行操作并且作业被卸载到未创建作业的计算机，则有效负荷是必需的。

## 创建要卸载的作业{#creating-jobs-for-offloading}

创建调用JobManager.addJob方法的客户端，以创建由自动选择的JobConsumer执行的作业。 提供以下信息以创建作业：

* 主题：工作主题。
* 名称：（可选）
* 属性映射：`Map<String, Object>`对象，它包含任意数量的属性，如输入有效负荷路径和输出有效负荷路径。 此Map对象可用于执行作业的JobConsumer对象。

以下示例服务为给定主题和输入有效负荷路径创建作业。

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

当为`com/adobe/example/offloading`主题和`/content/geometrixx/de/services`负载调用JobGeneratorImpl.createJob时，日志中包含以下消息：

```shell
10.06.2013 15:43:33.868 *INFO* [JobHandler: /etc/workflow/instances/2013-06-10/model_1554418768647484:/content/geometrixx/en/company] com.adobe.example.offloading.JobGeneratorImpl Received request to make job for topic com/adobe/example/offloading and payload /content/geometrixx/de/services
```

## 开发工作用户{#developing-a-job-consumer}

要使用作业，请开发实现`org.apache.sling.event.jobs.consumer.JobConsumer`接口的OSGi服务。 使用`JobConsumer.PROPERTY_TOPICS`属性确定要消费的主题。

以下示例JobConsumer实现在`com/adobe/example/offloading`主题中注册。 使用者只需将有效负荷内容节点的“消耗”属性设置为true。

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

MyJobConsumer类为/content/geometrixx/de/services的输入有效负荷生成以下日志消息：

```shell
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Consuming job of topic: com/adobe/example/offloading
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job has Input Payload /content/geometrixx/de/services and Output Payload /content/geometrixx/de/services
10.06.2013 16:02:40.884 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job OK for payload /content/geometrixx/de/services
```

使用CRXDE Lite可以观察消耗的属性：

![chlimage_1-25](assets/chlimage_1-25a.png)

## Maven依赖项{#maven-dependencies}

向pom.xml文件添加以下依赖关系保护，以便Maven可以解析与卸载相关的类。

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

以前的示例还需要以下依赖关系定义：

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

