---
title: 以编程方式与工作流交互
seo-title: 以编程方式与工作流交互
description: 'null'
seo-description: 'null'
uuid: a0f19fc6-b9bd-4b98-9c0e-fbf4f7383026
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: cb621332-a149-4f8d-9425-fd815b033c38
translation-type: tm+mt
source-git-commit: 7d2ba937710e5931356512b812a8b8fbe3a52072

---


# 以编程方式与工作流交互{#interacting-with-workflows-programmatically}

自定义 [和扩展工作流时](/help/sites-developing/workflows-customizing-extending.md) ，您可以访问工作流对象：

* [使用Workflow Java API](#using-the-workflow-java-api)
* [在ECMA脚本中获取工作流对象](#obtaining-workflow-objects-in-ecma-scripts)
* [使用Workflow REST API](#using-the-workflow-rest-api)

## 使用Workflow Java API {#using-the-workflow-java-api}

工作流Java API由包和 [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) 多个子包组成。 API中最重要的成员是 `com.adobe.granite.workflow.WorkflowSession` 类。 该类 `WorkflowSession` 提供对设计时和运行时工作流对象的访问：

* 工作流模型
* 工作项
* 工作流实例
* 工作流程数据
* 收件箱项目

该类还提供了几种用于干预工作流生命周期的方法。

下表提供了与工作流进行有序交互时要使用的几个关键Java对象的参考文档的链接。 下面的示例演示如何获取和使用代码中的类对象。

| 功能 | 对象 |
|---|---|
| 访问工作流 | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| 执行和查询工作流实例 | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| 管理工作流模型 | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| 工作流中（或不是）节点的信息 | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## 在ECMA脚本中获取工作流对象 {#obtaining-workflow-objects-in-ecma-scripts}

如查找脚 [本中所述](/help/sites-developing/the-basics.md#locating-the-script),AEM（通过Apache Sling）提供了一个执行服务器端ECMA脚本的ECMA脚本引擎。 该 [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) 类作为变量可立即用于脚 `sling` 本。

该 `ScriptHelper` 类允许您访问最终 `SlingHttpServletRequest` 获得该对象的 `WorkflowSession` 对象；例如：

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## 使用Workflow REST API {#using-the-workflow-rest-api}

“工作流”控制台大量使用REST API;因此，本页介绍了工作流的REST API。

>[!NOTE]
>
>curl命令行工具使您能使用Workflow REST API访问工作流对象和管理实例生命周期。 本页中的示例演示了如何通过curl命令行工具使用REST API。

REST API支持以下操作：

* 启动或停止工作流服务
* 创建、更新或删除工作流模型
* [启动、暂停、继续或终止工作流实例](/help/sites-administering/workflows.md#workflow-status-and-actions)
* 完成或委派工作项目

>[!NOTE]
>
>通过使用Firebug（用于Web开发的Firefox扩展），可以在控制台操作时跟随HTTP通信。 例如，您可以检查发送到AEM服务器的参数和包含请求的 `POST` 值。

在此页中，假定AEM在端口的localhost上运 `4502` 行，并且安装上下文为“ `/`”（根）。 如果安装不是这样，则需要相应地调整HTTP请求所适用的URI。

请求支持的呈 `GET` 现是JSON呈现。 URL的扩 `GET` 展名应 `.json` 为，例如：

`http://localhost:4502/etc/workflow.json`

### 管理工作流实例 {#managing-workflow-instances}

以下HTTP请求方法适用于：

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>HTTP请求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出可用的工作流实例。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>创建新的工作流实例。 参数包括：<br /> - <code>model</code>:相应工作流模型的ID(URI)<br /> - <code>payloadType</code>:包含有效负荷的类型(例如， <code>JCR_PATH</code> 或URL)。<br /> 有效负荷作为参数发送 <code>payload</code>。 将 <code>201</code> (<code>CREATED</code>)响应与包含新工作流实例资源的URL的位置标题一起发送回。</p> </td>
  </tr>
 </tbody>
</table>

#### 按状态管理工作流实例 {#managing-a-workflow-instance-by-its-state}

以下HTTP请求方法适用于：

`http://localhost:4502/etc/workflow/instances.{state}`

| HTTP请求方法 | 操作 |
|---|---|
| `GET` | 列出可用的工作流实例及其状 `RUNNING`态( `SUSPENDED`、 `ABORTED` 或 `COMPLETED`) |

#### 按工作流实例的ID管理工作流实例 {#managing-a-workflow-instance-by-its-id}

以下HTTP请求方法适用于：

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>HTTP请求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>获取实例数据（定义和元数据），包括指向相应工作流模型的链接。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>更改实例的状态。 新状态将作为参数发 <code>state</code> 送，并且必须具有以下值之一： <code>RUNNING</code>、 <code>SUSPENDED</code>或 <code>ABORTED</code>。<br /> 如果新状态不可达（例如，当挂起终止的实例时），则 <code>409</code> (<code>CONFLICT</code>)响应将发送回客户端。</td>
  </tr>
 </tbody>
</table>

### 管理工作流模型 {#managing-workflow-models}

以下HTTP请求方法适用于：

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>HTTP请求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出可用的工作流模型。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>创建新工作流模型. 如果发送参 <code>title</code> 数，则会创建具有指定标题的新模型。 将JSON模型定义附加为参数 <code>model</code> 会根据提供的定义创建新的工作流模型。<br /> 回 <code>201</code> 应(<code>CREATED</code>)与包含新工作流模型资源的URL的位置标题一起发送。<br /> 当模型定义作为名为的文件参数附加时，也会发生同样的情况 <code>modelfile</code>。<br /> 在参数和参数的情 <code>model</code> 况下， <code>modelfile</code> 定义序列化格式时需要另 <code>type</code> 外一个名为的参数。 新的序列化格式可以使用OSGI API进行集成。 标准JSON序列化器随工作流引擎一起提供。 其类型为JSON。 有关格式的示例，请参见下文。</td>
  </tr>
 </tbody>
</table>

示例：在浏览器中，请求生 `http://localhost:4502/etc/workflow/models.json` 成与以下内容类似的json响应：

```
[
    {"uri":"/var/workflow/models/activationmodel"}
    ,{"uri":"/var/workflow/models/dam/adddamsize"}
    ,{"uri":"/var/workflow/models/cloudconfigs/dtm-reactor/library-download"}
    ,{"uri":"/var/workflow/models/ac-newsletter-workflow-simple"}
    ,{"uri":"/var/workflow/models/dam/dam-create-language-copy"}
    ,{"uri":"/var/workflow/models/dam/dam-create-and-translate-language-copy"}
    ,{"uri":"/var/workflow/models/dam-indesign-proxy"}
    ,{"uri":"/var/workflow/models/dam-xmp-writeback"}
    ,{"uri":"/var/workflow/models/dam-parse-word-documents"}
    ,{"uri":"/var/workflow/models/dam/process_subasset"}
    ,{"uri":"/var/workflow/models/dam/dam_set_last_modified"}
    ,{"uri":"/var/workflow/models/dam/dam-autotag-assets"}
    ,{"uri":"/var/workflow/models/dam/update_asset"}
    ,{"uri":"/var/workflow/models/dam/update_asset_offloading"}
    ,{"uri":"/var/workflow/models/dam/dam-update-language-copy"}
    ,{"uri":"/var/workflow/models/dam/update_from_lightbox"}
    ,{"uri":"/var/workflow/models/cloudservices/DTM_bundle_download"}
    ,{"uri":"/var/workflow/models/dam/dam_download_asset"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-encode-video"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-thumbnail-replacement"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail"}
    ,{"uri":"/var/workflow/models/newsletter_bounce_check"}
    ,{"uri":"/var/workflow/models/projects/photo_shoot_submission"}
    ,{"uri":"/var/workflow/models/projects/product_photo_shoot"}
    ,{"uri":"/var/workflow/models/projects/approval_workflow"}
    ,{"uri":"/var/workflow/models/prototype-01"}
    ,{"uri":"/var/workflow/models/publish_example"}
    ,{"uri":"/var/workflow/models/publish_to_campaign"}
    ,{"uri":"/var/workflow/models/screens/publish_to_author_bin"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_publish_to_youtube"}
    ,{"uri":"/var/workflow/models/projects/request_copy"}
    ,{"uri":"/var/workflow/models/projects/request_email"}
    ,{"uri":"/var/workflow/models/projects/request_landing_page"}
    ,{"uri":"/var/workflow/models/projects/request_launch"}
    ,{"uri":"/var/workflow/models/request_for_activation"}
    ,{"uri":"/var/workflow/models/request_for_deactivation"}
    ,{"uri":"/var/workflow/models/request_for_deletion"}
    ,{"uri":"/var/workflow/models/request_for_deletion_without_deactivation"}
    ,{"uri":"/var/workflow/models/request_to_complete_move_operation"}
    ,{"uri":"/var/workflow/models/reverse_replication"}
    ,{"uri":"/var/workflow/models/salesforce-com-export"}
    ,{"uri":"/var/workflow/models/scene7"}
    ,{"uri":"/var/workflow/models/scheduled_activation"}
    ,{"uri":"/var/workflow/models/scheduled_deactivation"}
    ,{"uri":"/var/workflow/models/screens/screens-update-asset"}
    ,{"uri":"/var/workflow/models/translation"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_remove_from_youtube"}
    ,{"uri":"/var/workflow/models/wcm-translation/create_language_copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/prepare_translation_project"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-i18n-dictionary"}
    ,{"uri":"/var/workflow/models/wcm-translation/sync_translation_job"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-language-copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/update_language_copy"}
]
```

#### 管理特定的工作流模型 {#managing-a-specific-workflow-model}

以下HTTP请求方法适用于：

`http://localhost:4502*{uri}*`

其中 `*{uri}*` 是存储库中模型节点的路径。

<table>
 <tbody>
  <tr>
   <td>HTTP请求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>获取模 <code>HEAD</code> 型的版本（定义和元数据）。</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>更新 <code>HEAD</code> 模型版本（创建新版本）。<br /> 必须将新版本的模型的完整模型定义添加为名为的参数 <code>model</code>。 此外， <code>type</code> 创建新模型时需要参数，并且需要具有该值 <code>JSON</code>。<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>与PUT相同的行为。 需要，因为AEM构件不支持操 <code>PUT</code> 作。</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>删除模型。 为了解决防火墙／代理问题， <code>POST</code> 包含具有值 <code>X-HTTP-Method-Override</code> 的头条目 <code>DELETE</code> 也将被接受为请 <code>DELETE</code> 求。</td>
  </tr>
 </tbody>
</table>

示例：在浏览器中，返回与 `http://localhost:4502/var/workflow/models/publish_example.json` 以下代 `json` 码类似的响应的请求：

```shell
{
  "id":"/var/workflow/models/publish_example",
  "title":"Publish Example",
  "version":"1.0",
  "description":"This example shows a simple review and publish process.",
  "metaData":
  {
    "multiResourceSupport":"true",
    "tags":"wcm,publish"
  },
  "nodes":
  [{
    "id":"node0",
    "type":"START",
    "title":"Start",
    "description":"The start node of the workflow.",
    "metaData":
    {
    }
  },
  {
    "id":"node1",
    "type":"PARTICIPANT",
    "title":"Validate Content",
    "description":"Validate the modified content.",
    "metaData":
    {
      "PARTICIPANT":"admin"
    }
  },
  {
    "id":"node2",
    "type":"PROCESS",
    "title":"Publish Content",
    "description":"Publish the modified content.",
    "metaData":
    {
      "PROCESS_AUTO_ADVANCE":"true",
      "PROCESS":"com.day.cq.wcm.workflow.process.ActivatePageProcess"
    }
  },
  {
    "id":"node3",
    "type":"END",
    "title":"End",
    "description":"The end node of the workflow.",
    "metaData":
    {
    }
  }],
  "transitions":
  [{
    "from":"node0",
    "to":"node1",
    "metaData":
    {
    }
  },
  {
    "from":"node1",
    "to":"node2",
    "metaData":
    {
    }
  },
  {
    "from":"node2",
    "to":"node3",
    "metaData":
    {
    }
  }
]}
```

#### 按版本管理工作流模型 {#managing-a-workflow-model-by-its-version}

以下HTTP请求方法适用于：

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| HTTP请求方法 | 操作 |
|---|---|
| `GET` | 获取给定版本中的模型数据（如果它存在）。 |

### 管理（用户）收件箱 {#managing-user-inboxes}

以下HTTP请求方法适用于：

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>HTTP请求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出用户收件箱中的工作项，HTTP身份验证标头会标识该用户。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>完成其URI作为参数发送的工作项，并将相应的工作流实例前进到下一个节点（由参数定义） <code>item</code><code>route</code><code>backroute</code> ，或者在后退一步时。<br /> 如果发送了 <code>delegatee</code> 参数，则由参数标识的工作项将委派 <code>item</code> 给指定的参加者。</td>
  </tr>
 </tbody>
</table>

#### 使用WorkItem ID管理（用户）收件箱 {#managing-a-user-inbox-by-the-workitem-id}

以下HTTP请求方法适用于：

`http://localhost:4502/bin/workflow/inbox/{id}`

| HTTP请求方法 | 操作 |
|---|---|
| `GET` | 获取由其ID标识的收件箱的数据(定 `WorkItem` 义和元数据)。 |

## 示例 {#examples}

### 如何获取所有正在运行的工作流及其ID的列表 {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

要获取所有正在运行的工作流的列表，请执行以下操作：

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### 如何获取所有正在运行的工作流及其ID的列表——使用curl的REST {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

使用curl的示例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

结 `uri` 果中显示的内容可以作为其他命令 `id` 的实例；例如：

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>此 `curl` 命令可用于替代任 [何工作流状态](/help/sites-administering/workflows.md#workflow-status-and-actions) 。 `RUNNING`

### 如何更改工作流标题 {#how-to-change-the-workflow-title}

要更改在工 **作流控制台的** “实例” **选项卡中显示的工作流标题**`POST` ，请发送一个命令：

* 到: `http://localhost:4502/etc/workflow/instances/{id}`

* 和以下参数：

   * `action`:其价值必须是： `UPDATE`
   * `workflowTitle`:工作流标题

#### 如何使用curl更改工作流标题- REST {#how-to-change-the-workflow-title-rest-using-curl}

使用curl的示例：

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### 如何列出所有工作流模型 {#how-to-list-all-workflow-models}

要获取所有可用工作流模型的列表，请执行以下操作：

`http://localhost:4502/etc/workflow/models.json`

#### 如何列出所有工作流模型——使用curl的REST {#how-to-list-all-workflow-models-rest-using-curl}

使用curl的示例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>另请参阅 [管理工作流模型](#managing-workflow-models)。

### 获取WorkflowSession对象 {#obtaining-a-workflowsession-object}

该 `com.adobe.granite.workflow.WorkflowSession` 类可从对象或对 `javax.jcr.Session` 象进行 `org.apache.sling.api.resource.ResourceResolver` 调整。

#### 获取WorkflowSession对象- Java {#obtaining-a-workflowsession-object-java}

在JSP脚本（或servlet类的Java代码）中，使用HTTP请求对象获取一个对象，该对象提供对 `SlingHttpServletRequest` 象的访问 `ResourceResolver` 权。 使对象 `ResourceResolver` 适应 `WorkflowSession`。

```java
<%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
    import="com.adobe.granite.workflow.WorkflowSession,
  org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
%>
```

#### 获取WorkflowSession对象- ECMA脚本 {#obtaining-a-workflowsession-object-ecma-script}

使用 `sling` 变量获取用 `SlingHttpServletRequest` 于获取对象的对 `ResourceResolver` 象。 使对象 `ResourceResolver` 适应该对 `WorkflowSession` 象。

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### 创建、读取或删除工作流模型 {#creating-reading-or-deleting-workflow-models}

以下示例显示如何访问工作流模型：

* Java和ECMA脚本的代码使用该方 `WorkflowSession.createNewModel` 法。
* curl命令使用其URL直接访问模型。

使用的示例：

1. 创建一个模型(使用ID `/var/workflow/models/mymodel/jcr:content/model`)。
1. 删除模型。

>[!NOTE]
>
>删除模型会将模 `deleted` 型的子节点的属 `metaData` 性设置为 `true`。
>
>删除不会删除模型节点。

创建新模型时：

* 工作流模型编辑器要求模型使用下面的特定节点结构 `/var/workflow/models`。 模型的父节点必须是具有以下 `cq:Page` 属性值 `jcr:content` 的节点的类型：

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`
   在创建模型时，必须首先创建此节 `cq:Page` 点并使用其节 `jcr:content` 点作为模型节点的父节点。

* 某些方 `id` 法需要识别模型的参数是存储库中模型节点的绝对路径：

   `/var/workflow/models/<*model_name>*/jcr:content/model`

   >[!NOTE]
   >
   >请参 [阅如何列出所有工作流模型](#how-to-list-all-workflow-models)。

#### 创建、读取或删除工作流模型- Java {#creating-reading-or-deleting-workflow-models-java}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" import="com.adobe.granite.workflow.WorkflowSession,
                 com.adobe.granite.workflow.model.WorkflowModel,
             org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
/* Create the parent page */
String modelRepo = new String("/var/workflow/models");
String modelTemplate = new String ("/libs/cq/workflow/templates/model");
String modelName = new String("mymodel");
Page modelParent = pageManager.create(modelRepo, modelName, modelTemplate, "My workflow model");

/* create the model */
String modelId = new String(modelParent.getPath()+"/jcr:content/model")
WorkflowModel model = wfSession.createNewModel("Made using Java",modelId);

/* delete the model */
wfSession.deleteModel(modelId);
%>
```

#### 创建、读取或删除工作流模型- ECMA脚本 {#creating-reading-or-deleting-workflow-models-ecma-script}

```
var resolver = sling.getRequest().getResource().getResourceResolver();
var wfSession = resolver.adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
var pageManager = resolver.adaptTo(Packages.com.day.cq.wcm.api.PageManager);

//create the parent page node
var workflowPage = pageManager.create("/var/workflow/models", "mymodel", "/libs/cq/workflow/templates/model", "Created via ECMA Script");
var modelId = workflowPage.getPath()+ "/jcr:content/model";
//create the model
var model = wfSession.createNewModel("My Model", modelId);
//delete the model
var model = wfSession.deleteModel(modelId);
```

#### 删除工作流模型——使用curl进行REST {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>由于需要详细程度，curl不被认为可用于创建和／或阅读模型。

### 检查工作流状态时过滤掉系统工作流 {#filtering-out-system-workflows-when-checking-workflow-status}

您可以使用 [WorkflowStatus API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) 来检索有关节点的工作流状态的信息。

各种方法都有以下参数：

`excludeSystemWorkflows`

此参数可设置为指 `true` 示应从相关结果中排除系统工作流。

您可 [以更新OSGi配置](/help/sites-deploying/configuring-osgi.md) Adobe Granite Workflow PayloadMapCache **，该配置指定要视**`Models` 为系统工作流的工作流。 默认（运行时）工作流模型包括：

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### 超时后自动前进参加者步骤 {#auto-advance-participant-step-after-a-timeout}

如果您需要自动前进在预 **定义时间内** 尚未完成的“参加者”步骤，您可以：

1. 实现OSGI事件监听器以监听任务创建和修改。
1. 指定超时（截止日期），然后创建一个计划的sling作业以在该时间触发。
1. 编写一个作业处理函数，该处理函数在超时过期时通知并触发该作业。

   如果任务尚未完成，此处理函数将对任务执行所需的操作

>[!NOTE]
>
>必须明确界定要采取的行动才能采用这种方法。

### 与工作流实例交互 {#interacting-with-workflow-instances}

下面提供了如何与工作流实例进行交互（程序化）的基本示例。

#### 与工作流实例交互- Java {#interacting-with-workflow-instances-java}

```java
// starting a workflow
WorkflowModel model = wfSession.getModel(workflowId);
WorkflowData wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
Workflow[] workflows workflows = wfSession.getAllWorkflows();
Workflow workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 与工作流实例交互- ECMA脚本 {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows(“RUNNING“);
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 与工作流实例交互——使用curl的REST {#interacting-with-workflow-instances-rest-using-curl}

* **启动工作流**

   ```shell
   # starting a workflow
   curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
   
   # for example:
   curl -u admin:admin -d "model=/var/workflow/models/request_for_activation/jcr:content/model&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
   ```

* **列出实例**

   ```shell
   # listing the instances
   curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
   ```

   这将列出所有实例；例如：

   ```shell
   [
       {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
       ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
   ]
   ```

   >[!NOTE]
   >
   >有关 [列出具有特定状态的实例的ID](#how-to-get-a-list-of-all-running-workflows-with-their-ids) ，请参阅如何获取所有正在运行的工作流的列表。

* **暂停工作流**

   ```shell
   # suspending a workflow
   curl -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **恢复工作流**

   ```shell
   # resuming a workflow
   curl -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **终止工作流实例**

   ```shell
   # terminating a workflow
   curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

### 与工作项交互 {#interacting-with-work-items}

下面提供了如何与工作项交互（按程序）的基本示例。

#### 与工作项交互- Java {#interacting-with-work-items-java}

```java
// querying work items
WorkItem[] workItems = wfSession.getActiveWorkItems();
WorkItem workItem = wfSession.getWorkItem(id);

// getting routes
List<Route> routes = wfSession.getRoutes(workItem);

// delegating
Iterator<Participant> delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### 与工作项交互- ECMA脚本 {#interacting-with-work-items-ecma-script}

```
// querying work items
var workItems = wfSession.getActiveWorkItems();
var workItem = wfSession.getWorkItem(id);

// getting routes
var routes = wfSession.getRoutes(workItem);

// delegating
var delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### 与工作项交互——使用curl的REST {#interacting-with-work-items-rest-using-curl}

* **从收件箱中列出工作项**

   ```shell
   # listing the work items
   curl -u admin:admin http://localhost:4502/bin/workflow/inbox
   ```

   系统将列出收件箱中当前工作项目的详细信息；例如：

   ```shell
   [{
       "uri_xss": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
       "uri": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
       "currentAssignee_xss": "workflow-administrators",
       "currentAssignee": "workflow-administrators",
       "startTime": 1519656289274,
       "payloadType_xss": "JCR_PATH",
       "payloadType": "JCR_PATH",
       "payload_xss": "/content/we-retail/es/es",
       "payload": "/content/we-retail/es/es",
       "comment_xss": "Process resource is null",
       "comment": "Process resource is null",
       "type_xss": "WorkItem",
       "type": "WorkItem"
     },{
       "uri_xss": "configuration/configure_analyticstargeting",
       "uri": "configuration/configure_analyticstargeting",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/securitychecklist",
       "uri": "configuration/securitychecklist",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/enable_collectionofanonymoususagedata",
       "uri": "configuration/enable_collectionofanonymoususagedata",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/configuressl",
       "uri": "configuration/configuressl",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     }
   ```

* **委派工作项**

   ```xml
   # delegating
   curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
   ```

   >[!NOTE]
   >
   >对于 `delegatee` 工作流步骤，必须是有效的选项。

* **完成或将工作项推向下一步**

   ```xml
   # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
   http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
   
   # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
   curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
   ```

### 侦听工作流事件 {#listening-for-workflow-events}

使用OSGi事件框架侦听类定义的 [ 事 `com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html) 件。 此类还提供了几种用于获取有关事件主题的信息的有用方法。 例如，该方 `getWorkItem` 法返回 `WorkItem` 事件中涉及的工作项的对象。

以下示例代码定义一个服务，该服务监听工作流事件并根据事件类型执行任务。

```java
package com.adobe.example.workflow.listeners;

import org.apache.sling.event.jobs.JobProcessor;
import org.apache.sling.event.jobs.JobUtil;

import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import com.adobe.granite.workflow.event.WorkflowEvent;
import com.adobe.granite.workflow.exec.WorkItem;

/**
 * The <code>WorkflowEventCatcher</code> class listens to workflow events.
 */
@Component(metatype=false, immediate=true)
@Service(value=org.osgi.service.event.EventHandler.class)
public class WorkflowEventCatcher implements EventHandler, JobProcessor {

 @Property(value=com.adobe.granite.workflow.event.WorkflowEvent.EVENT_TOPIC)
 static final String EVENT_TOPICS = "event.topics";

 private static final Logger logger = LoggerFactory.getLogger(WorkflowEventCatcher.class);

 public void handleEvent(Event event) {
  JobUtil.processJob(event, this);
 }

 public boolean process(Event event) {
  logger.info("Received event of topic: " + event.getTopic());
  String topic = event.getTopic();

  try {
   if (topic.equals(WorkflowEvent.EVENT_TOPIC)) {
    WorkflowEvent wfevent = (WorkflowEvent)event;
    String eventType = wfevent.getEventType();
    String instanceId = wfevent.getWorkflowInstanceId();

    if (instanceId != null) {
     //workflow instance events
     if (eventType.equals(WorkflowEvent.WORKFLOW_STARTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_RESUMED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_SUSPENDED_EVENT)) {
      // your code comes here...
     } else if (
       eventType.equals(WorkflowEvent.WORKFLOW_ABORTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_COMPLETED_EVENT)) {
      // your code comes here...
     }
     // workflow node event
     if (eventType.equals(WorkflowEvent.NODE_TRANSITION_EVENT)) {
      WorkItem currentItem = (WorkItem) event.getProperty(WorkflowEvent.WORK_ITEM);
      // your code comes here...
     }
    }
   }
  } catch(Exception e){
   logger.debug(e.getMessage());
   e.printStackTrace();
  }
  return true;
 }
}
```

