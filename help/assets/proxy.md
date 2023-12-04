---
title: '"[!DNL Assets] 代理开发”'
description: 代理是 [!DNL Experience Manager] 使用代理工作程序处理作业的实例。 了解如何配置 [!DNL Experience Manager] 代理、支持的操作、代理组件以及如何开发自定义代理工作程序。
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# [!DNL Assets] 代理开发 {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] 使用代理为特定任务分发处理。

代理是一种特定的（有时是单独的）Experience Manager实例，它使用代理工作程序作为负责处理作业和创建结果的处理器。 代理工作程序可用于多种任务。 如果有 [!DNL Assets] 代理这可用于加载资源以在Assets中呈现。 例如， [IDS代理工作进程](indesign.md) 使用 [!DNL Adobe InDesign] 用于处理资源中使用的文件的服务器。

当代理是单独的 [!DNL Experience Manager] 实例这有助于减轻 [!DNL Experience Manager] 创作实例。 默认情况下， [!DNL Assets] 在同一JVM中执行资源处理任务（通过代理外部化）以减少 [!DNL Experience Manager] 创作实例。

## 代理（HTTP访问） {#proxy-http-access}

当代理配置为接受以下位置的处理作业时，可通过HTTP Servlet使用该代理： `/libs/dam/cloud/proxy`. 此servlet根据发布的参数创建sling作业。 然后将其添加到代理作业队列，并连接到相应的代理工作进程。

### 支持的操作 {#supported-operations}

* `job`

  **要求**：参数 `jobevent` 必须设置为序列化值映射。 用于创建 `Event` 用于作业处理器。

  **结果**：添加新作业。 如果成功，则会返回唯一的作业ID。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

  **要求**：参数 `jobid` 必须设置。

  **结果**：返回由作业处理器创建的结果节点的JSON表示形式。

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

  **要求**：必须设置参数jobid。

  **结果**：返回与给定作业关联的资源。

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

  **要求**：必须设置参数jobid。

  **结果**：删除找到的作业。

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### 代理工作进程 {#proxy-worker}

代理工作程序是负责处理作业和创建结果的处理器。 工作进程驻留在代理实例上，并且必须实施 [sling作业处理器](https://sling.apache.org/site/eventing-and-jobs.html) 将被识别为代理工作程序。

>[!NOTE]
>
>工作人员必须实施 [sling作业处理器](https://sling.apache.org/site/eventing-and-jobs.html) 将被识别为代理工作程序。

### 客户端API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 作为OSGi服务提供，该服务提供创建作业、删除作业以及从这些作业获取结果的方法。 此服务的默认实施(`JobServiceImpl`)使用HTTP客户端与远程代理servlet进行通信。

以下是API用法的示例：

```java
@Reference
 JobService proxyJobService;

 // to create a job
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

代理和代理工作程序配置均可通过云服务配置获取，可从访问 [!DNL Assets] **工具** 控制台或下 `/etc/cloudservices/proxy`. 每个代理工作进程应在 `/etc/cloudservices/proxy` 用于工作进程特定的配置详细信息(例如， `/etc/cloudservices/proxy/workername`)。

>[!NOTE]
>
>请参阅 [InDesign Server代理工作进程配置](indesign.md#configuring-the-proxy-worker-for-indesign-server) 和 [Cloud Service配置](../sites-developing/extending-cloud-config.md) 以了解更多信息。

以下是API用法的示例：

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

### 开发自定义的代理工作程序 {#developing-a-customized-proxy-worker}

此 [IDS代理工作进程](indesign.md) 是 [!DNL Assets] 现成可用的代理工作程序，用于外包InDesign资源的处理。

您还可以开发和配置自己的 [!DNL Assets] 代理员工，创建一名专门的员工来派遣并外包 [!DNL Assets] 正在处理任务。

设置您自己的自定义代理工作程序需要您：

* 设置和实施（使用Sling事件）：

   * 自定义作业主题
   * 自定义作业事件处理程序

* 然后，使用JobService API执行以下操作：

   * 将自定义作业分派给代理
   * 管理您的作业

* 如果要使用工作流中的代理，则必须使用WorkflowExternalProcess API和JobService API实施自定义外部步骤。

以下图表和步骤详细介绍了操作步骤：

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>在以下步骤中，InDesign等效项作为参考示例表示。

1. A [Sling作业](https://sling.apache.org/site/eventing-and-jobs.html) 使用，因此您需要为用例定义作业主题。

   例如，请参阅 `IDSJob.IDS_EXTENDSCRIPT_JOB` 用于IDS代理工作进程。

1. 外部步骤用于触发事件，然后等待该操作完成；这是通过对id进行轮询来完成的。 自行开发实施新功能的步骤。

   实施 `WorkflowExternalProcess`，然后使用JobService API和作业主题准备作业事件并将其调度到JobService（一种OSGi服务）。

   例如，请参阅 `INDDMediaExtractProcess`.java用于IDS代理工作进程。

1. 为主题实施作业处理程序。 此处理程序需要进行开发，以便执行特定操作并被视为工作人员实施。

   例如，请参阅 `IDSJobProcessor.java` 用于IDS代理工作进程。

1. 利用 `ProxyUtil.java` 在dam-commons中。 这允许您使用dam代理将作业分派给工作人员。

>[!NOTE]
>
>什么是 [!DNL Assets] 代理框架不提供现成的池机制。
>
>此 [!DNL InDesign] 集成允许访问池 [!DNL InDesign] 服务器(IDSPool)。 此池特定于 [!DNL InDesign] 集成，而不是的一部分 [!DNL Assets] 代理框架。

>[!NOTE]
>
>结果同步：
>
>如果n个实例使用相同的代理，则处理结果将保留在代理中。 客户端(Experience Manager作者)的作业将使用在创建作业时提供给客户端的相同唯一作业ID来请求结果。 代理只需完成作业并将结果保留为可请求的结果即可。
