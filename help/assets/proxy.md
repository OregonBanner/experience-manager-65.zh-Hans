---
title: '[!DNL Assets] 代理开发'
description: 代理是 [!DNL Experience Manager] instance that uses proxy workers to process jobs. Learn how to configure an [!DNL Experience Manager] 代理，支持的操作、代理组件，以及如何开发自定义代理工作器。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# [!DNL Assets] 代理开发  {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] 使用代理分发某些任务的处理。

代理是一个特定（有时也是单独的）Experience Manager实例，它使用代理工作器作为处理器，负责处理作业并创建结果。 代理工作器可用于各种任务。 对于[!DNL Assets]代理，此代理可用于加载资产以在资产中呈现。 例如，[IDS代理工作者](indesign.md)使用[!DNL Adobe InDesign]服务器处理要在资产中使用的文件。

当代理是单独的[!DNL Experience Manager]实例时，这有助于减少Experience Manager创作实例的负载。 默认情况下，[!DNL Assets]在同一JVM（通过代理外部化）中执行资产处理任务，以减少Experience Manager创作实例的负载。

## 代理（HTTP访问）{#proxy-http-access}

当代理配置为在以下位置接受处理作业时，可通过HTTP Servlet使用：`/libs/dam/cloud/proxy`。 此servlet根据已发布的参数创建sling作业。 然后，此操作会添加到代理作业队列并连接到相应的代理工作器。

### 支持的操作{#supported-operations}

* `job`

   **要求**:该参 `jobevent` 数必须设置为序列化值映射。它用于为作业处理器创建`Event`。

   **结果**:添加新作业。如果成功，则返回唯一作业ID。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **要求**:必须 `jobid` 设置参数。

   **结果**:返回作业处理者创建的结果节点的JSON表示形式。

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

### 代理工作器{#proxy-worker}

代理工作者是负责处理作业和创建结果的处理器。 Worker驻留在代理实例上，必须实现[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html)才能被识别为代理Worker。

>[!NOTE]
>
>该工作人员必须实施[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html)才能被识别为代理工作人员。

### 客户端API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 可用作OSGi服务，它提供创建作业、删除作业和从这些作业获取结果的方法。此服务的默认实现(`JobServiceImpl`)使用HTTP客户端与远程代理servlet通信。

以下是API使用的示例：

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

### 云服务配置 {#cloud-service-configurations}

>[!NOTE]
>
>[`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html)下提供代理API的参考文档。

代理和代理工作器配置均可通过云服务配置使用，这些配置可从[!DNL Assets] **工具**&#x200B;控制台或`/etc/cloudservices/proxy`下访问。 每个代理工作器应在`/etc/cloudservices/proxy`下添加一个节点，以了解工作器特定的配置详细信息（例如`/etc/cloudservices/proxy/workername`）。

>[!NOTE]
>
>有关详细信息，请参阅[InDesign Server代理工作器配置](indesign.md#configuring-the-proxy-worker-for-indesign-server)和[Cloud Services配置](../sites-developing/extending-cloud-config.md)。

以下是API使用的示例：

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

### 开发自定义代理工作器{#developing-a-customized-proxy-worker}

[IDS代理工作者](indesign.md)是[!DNL Assets]代理工作者的示例，该代理工作者已经提供现成的，用于外包InDesign资产的处理。

您还可以开发和配置自己的[!DNL Assets]代理工作者，以创建专门的工作者来调度和外包您的[!DNL Assets]处理任务。

设置您自己的自定义代理工作者需要您：

* 设置和实施（使用Sling事件）:

   * 自定义作业主题
   * 自定义作业事件处理程序

* 然后，使用JobService API可以：

   * 向代理派送自定义作业
   * 管理您的作业

* 如果要从工作流中使用代理，则必须使用WorkflowExternalProcess API和JobService API实现自定义外部步骤。

以下示意图和步骤详细说明了如何继续：

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>在以下步骤中，InDesign等效项作为参考示例。

1. 使用[Sling作业](https://sling.apache.org/site/eventing-and-jobs.html)，因此您需要为您的用例定义作业主题。

   例如，请参见`IDSJob.IDS_EXTENDSCRIPT_JOB`了解IDS代理工作器。

1. 外部步骤用于触发事件，然后等待完成；这是通过轮询id来完成的。 您必须自行制定实施新功能的步骤。

   实施`WorkflowExternalProcess`，然后使用JobService API和您的作业主题准备作业事件并将其调度到JobService（一种OSGi服务）。

   例如，请参阅IDS代理工作器的`INDDMediaExtractProcess`.java。

1. 为您的主题实施作业处理程序。 此处理程序需要进行开发，以便执行您的特定操作并被视为工作者实现。

   例如，请参见`IDSJobProcessor.java`了解IDS代理工作器。

1. 在dam-commons中利用`ProxyUtil.java`。 这允许您使用dam代理向员工分派任务。

>[!NOTE]
>
>[!DNL Assets]代理框架不提供现成的池机制。
>
>[!DNL InDesign]集成允许访问[!DNL InDesign]服务器(IDSPool)的池。 此池特定于[!DNL InDesign]集成，而不是[!DNL Assets]代理框架的一部分。

>[!NOTE]
>
>结果同步：
>
>如果n个实例使用同一代理，则处理结果与代理保持一致。 客户端(Experience Manager作者)的作业使用与创建作业时给客户端的相同唯一作业ID请求结果。 代理只需完成作业，并将结果保持为可请求。
