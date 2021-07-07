---
title: '[!DNL Assets] 代理开发'
description: 代理是 [!DNL Experience Manager] instance that uses proxy workers to process jobs. Learn how to configure an [!DNL Experience Manager] 代理、支持的操作、代理组件，以及如何开发自定义代理工作程序。
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: b3acfdba41e1bd94c65bb7a87f63b9c326a80dd2
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---

# [!DNL Assets] 代理开发 {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] 使用代理来分发某些任务的处理。

代理是一个特定的（有时是独立的）Experience Manager实例，它使用代理工作程序作为负责处理工作和创建结果的处理器。 代理工作程序可用于各种任务。 对于[!DNL Assets]代理，可使用此代理加载资产以在Assets中进行渲染。 例如， [IDS代理工作程序](indesign.md)使用[!DNL Adobe InDesign]服务器处理要在资产中使用的文件。

当代理是单独的[!DNL Experience Manager]实例时，这有助于减少[!DNL Experience Manager]创作实例的负载。 默认情况下，[!DNL Assets]在同一JVM（通过代理外部化）中执行资产处理任务，以减少[!DNL Experience Manager]创作实例的负载。

## 代理（HTTP访问） {#proxy-http-access}

将HTTP Servlet配置为在以下位置接受处理作业时，可通过HTTP Servlet使用代理：`/libs/dam/cloud/proxy`。 此Servlet通过已发布的参数创建Sling作业。 然后，该任务将添加到代理作业队列并连接到相应的代理工作程序。

### 支持的操作 {#supported-operations}

* `job`

   **要求**:参数必 `jobevent` 须设置为序列化值映射。它用于为作业处理器创建`Event`。

   **结果**:添加新作业。如果成功，则返回唯一的作业ID。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **要求**:必须 `jobid` 设置参数。

   **结果**:返回作业处理器创建的结果节点的JSON表示形式。

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **要求**:必须设置参数jobid。

   **结果**:返回与给定作业关联的资源。

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **要求**:必须设置参数jobid。

   **结果**:如果找到，则删除作业。

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### 代理工作程序 {#proxy-worker}

代理工作程序是负责处理作业并创建结果的处理器。 工作程序驻留在代理实例上，必须实施[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html)才能被识别为代理工作程序。

>[!NOTE]
>
>该工作程序必须实施[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html)才能被识别为代理工作程序。

### 客户端API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 可作为OSGi服务使用，该服务提供了创建作业、删除作业以及从这些作业中获取结果的方法。此服务的默认实现(`JobServiceImpl`)使用HTTP客户端与远程代理Servlet通信。

以下是API使用示例：

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### Cloud Service配置 {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

代理和代理工作程序配置均可通过云服务配置来使用，这些配置可从[!DNL Assets] **工具**&#x200B;控制台或`/etc/cloudservices/proxy`下访问。 对于特定于工作程序的配置详细信息（例如，`/etc/cloudservices/proxy/workername`），每个代理工作程序应在`/etc/cloudservices/proxy`下添加一个节点。

>[!NOTE]
>
>有关更多信息，请参阅[InDesign Server代理工作器配置](indesign.md#configuring-the-proxy-worker-for-indesign-server)和[Cloud Services配置](../sites-developing/extending-cloud-config.md)。

以下是API使用示例：

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### 开发自定义代理工作程序 {#developing-a-customized-proxy-worker}

[IDS代理工作程序](indesign.md)是[!DNL Assets]代理工作程序的示例，该代理工作程序已提供现成的，用于外包InDesign资产的处理。

您还可以开发并配置自己的[!DNL Assets]代理工作程序，以创建一个专门的工作程序来调度和外包您的[!DNL Assets]处理任务。

要设置您自己的自定义代理工作程序，您需要：

* 设置和实施（使用Sling事件）：

   * 自定义作业主题
   * 自定义作业事件处理程序

* 然后，使用JobService API执行以下操作：

   * 将您的自定义作业派送给代理
   * 管理您的工作

* 如果要使用工作流中的代理，则必须使用WorkflowExternalProcess API和JobService API实施自定义外部步骤。

下图和步骤详细说明了如何继续：

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>在以下步骤中，InDesign等效项作为参考示例。

1. 使用了[Sling作业](https://sling.apache.org/site/eventing-and-jobs.html)，因此您需要为用例定义作业主题。

   例如，有关IDS代理工作程序的信息，请参阅`IDSJob.IDS_EXTENDSCRIPT_JOB` 。

1. 外部步骤用于触发事件，然后等到该事件完成；这是通过轮询id来完成的。 您必须自行开发步骤来实施新功能。

   实施`WorkflowExternalProcess`，然后使用JobService API和作业主题准备作业事件并将其调度到JobService（OSGi服务）。

   例如，请参阅`INDDMediaExtractProcess`.java以获取IDS代理工作程序。

1. 为主题实施作业处理程序。 此处理程序需要进行开发，以便执行您的特定操作并被视为工作程序实施。

   例如，有关IDS代理工作程序的信息，请参阅`IDSJobProcessor.java` 。

1. 在dam-commons中使用`ProxyUtil.java`。 这允许您使用dam代理向员工调度作业。

>[!NOTE]
>
>[!DNL Assets]代理框架不提供现成的池机制。
>
>[!DNL InDesign]集成允许访问[!DNL InDesign]服务器(IDSPool)的池。 此池特定于[!DNL InDesign]集成，而不是[!DNL Assets]代理框架的一部分。

>[!NOTE]
>
>结果同步：
>
>如果n个实例使用相同的代理，则处理结果将与代理一起保留。 客户端(Experience Manager作者)的作业是使用在创建作业时给客户端的相同唯一作业ID来请求结果。 代理只需完成作业并准备好请求结果即可。
