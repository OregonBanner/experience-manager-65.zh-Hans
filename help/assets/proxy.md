---
title: 资产代理开发
description: 代理是使用代理Worker处理作业的AEM实例。 了解如何配置AEM代理、支持的操作、代理组件，以及如何开发自定义代理Worker。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# 资产代理开发 {#assets-proxy-development}

Adobe Experience Manager(AEM)资产使用代理分发特定任务的处理。

代理是特定（有时也是单独的）AEM实例，它使用代理Worker作为负责处理作业和创建结果的处理器。 代理工作器可用于各种任务。 对于AEM资产代理，此代理可用于加载资产以在AEM资产中呈现。 例如， [](indesign.md) IDS代理worker使用InDesign Server处理文件以在AEM资产中使用。

当代理是单独的AEM实例时，这有助于减少AEM创作实例的负载。 默认情况下，AEM资产会在同一JVM（通过代理外部化）中执行资产处理任务，以减少AEM创作实例的负载。

## 代理（HTTP访问） {#proxy-http-access}

将代理配置为在以下位置接受处理作业时，可通过HTTP Servlet使用代理： `/libs/dam/cloud/proxy`. 此Servlet根据已发布的参数创建sling作业。 然后，此操作会添加到代理作业队列，并连接到相应的代理工作器。

### 支持的操作 {#supported-operations}

* `job`

   **要求**:必须将 `jobevent` 参数设置为序列化值映射。 这用于为作业处理 `Event` 器创建一个。

   **结果**:添加新作业。 如果成功，则返回唯一的作业ID。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **要求**:必须 `jobid` 设置参数。

   **结果**:返回由作业处理者创建的结果节点的JSON表示形式。

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

### Proxy Worker {#proxy-worker}

代理Worker是负责处理作业和创建结果的处理器。 Worker驻留在代理实例上，必须实现 [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) ，才能被识别为代理Worker。

>[!NOTE]
>
>该工作者必须实 [施sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) ，才能被识别为代理工作者。

### 客户端API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 可作为OSGi服务使用，该服务提供创建作业、删除作业以及从这些作业获取结果的方法。 此服务(`JobServiceImpl`)的默认实现使用HTTP客户端与远程代理servlet通信。

以下是API使用的示例：

```xml
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

### 云服务配置 {#cloud-service-configurations}

>[!NOTE]
>
>有关代理API的参考文档，请访问 [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html)。

代理和代理Worker配置都可通过云服务配置获得，并可从AEM Assets **Tools控制台或下方访问**`/etc/cloudservices/proxy`。 每个代理Worker应在下面添加一个节点， `/etc/cloudservices/proxy` 以了解Worker特定的配置详细信息(例如 `/etc/cloudservices/proxy/workername`)。

>[!NOTE]
>
>有关 [详细信息，请参阅Indesign Server Proxy Worker配置](indesign.md#configuring-the-proxy-worker-for-indesign-server)[和云服务配置](../sites-developing/extending-cloud-config.md) 。

以下是API使用的示例：

```xml
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### 开发自定义代理Worker {#developing-a-customized-proxy-worker}

IDS代 [](indesign.md) 理工作者是AEM Assets代理工作者的一个示例，该代理工作者已开箱即用地提供用于外包Indesign资产的处理。

您还可以开发和配置自己的AEM Assets代理工作人员，以创建专门的工作人员来调度和外包AEM Assets处理任务。

设置您自己的自定义代理Worker需要您：

* 设置和实施（使用Sling事件）:

   * 自定义作业主题
   * 自定义作业事件处理程序

* 然后，使用JobService API可以：

   * 将自定义作业调度到代理
   * 管理您的工作

* 如果要从工作流中使用代理，则必须使用WorkflowExternalProcess API和JobService API实现自定义外部步骤。

下图和步骤详细说明了如何继续：

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>在以下步骤中，Indesign等效项指示为参考示例。

1. 使 [用Sling作业](https://sling.apache.org/site/eventing-and-jobs.html) ，因此您需要为用例定义作业主题。

   例如，请参阅 `IDSJob.IDS_EXTENDSCRIPT_JOB` IDS代理worker。

1. 外部步骤用于触发事件，然后等待完成；这是通过轮询id来完成的。 您必须自行制定实施新功能的步骤。

   实施 `WorkflowExternalProcess`，然后使用JobService API和您的作业主题准备作业事件并将其调度到JobService（OSGi服务）。

   例如，请参阅 `INDDMediaExtractProcess`IDS代理worker的。java。

1. 为您的主题实施作业处理程序。 此处理函数需要开发，以便执行您的特定操作，并被视为worker实现。

   例如，请参阅 `IDSJobProcessor.java` IDS代理worker。

1. 在公 `ProxyUtil.java` 地中利用。 这允许您使用dam代理向工人分派作业。

>[!NOTE]
>
>AEM资产代理框架不提供现成的池机制。
>
>InDesign集成允许访问InDesign服务器池(IDSPool)。 此池特定于Indesign集成，而不是AEM Assets代理框架的一部分。

>[!NOTE]
>
>结果同步：
>
>如果n个实例使用相同的代理，则处理结果将与代理保持同步。 客户端（AEM作者）的作业使用与创建作业时向客户端提供的唯一作业ID请求结果。 代理只需完成作业，并将结果保持为可请求状态。
