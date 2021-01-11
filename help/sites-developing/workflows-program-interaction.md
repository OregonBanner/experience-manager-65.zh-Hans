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
source-git-commit: edf7ef93372e44cb71d8eac8712db53f4e45b6cf
workflow-type: tm+mt
source-wordcount: '2006'
ht-degree: 0%

---


# 以编程方式与工作流交互{#interacting-with-workflows-programmatically}

在[自定义和扩展工作流](/help/sites-developing/workflows-customizing-extending.md)时，您可以访问工作流对象：

* [使用Workflow Java API](#using-the-workflow-java-api)
* [在ECMA脚本中获取工作流对象](#obtaining-workflow-objects-in-ecma-scripts)
* [使用Workflow REST API](#using-the-workflow-rest-api)

## 使用Workflow Java API {#using-the-workflow-java-api}

工作流Java API由[`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html)包和多个子包组成。 API中最重要的成员是`com.adobe.granite.workflow.WorkflowSession`类。 `WorkflowSession`类提供对设计时和运行时工作流对象的访问：

* 工作流模型
* 工作项
* 工作流实例
* 工作流数据
* 收件箱项目

该类还提供了几种用于干预工作流生命周期的方法。

下表提供了与工作流进行有序交互时要使用的几个关键Java对象的参考文档的链接。 下面的示例演示如何获取和使用代码中的类对象。

| 功能 | 对象 |
|---|---|
| 访问工作流 | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| 执行和查询工作流实例 | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| 管理工作流模型 | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| 工作流中（或不是）节点的信息 | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## 在ECMA脚本{#obtaining-workflow-objects-in-ecma-scripts}中获取工作流对象

如[查找脚本](/help/sites-developing/the-basics.md#locating-the-script)中所述，AEM（通过Apache Sling）提供了执行服务器端ECMA脚本的ECMA脚本引擎。 [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html)类作为`sling`变量可立即用于脚本。

`ScriptHelper`类提供对`SlingHttpServletRequest`的访问，您可以使用它最终获取`WorkflowSession`对象；例如：

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## 使用Workflow REST API {#using-the-workflow-rest-api}

“工作流”控制台大量使用REST API;因此，本页介绍了工作流的REST API。

>[!NOTE]
>
>curl命令行工具允许您使用Workflow REST API访问工作流对象和管理实例生命周期。 本页中的示例演示了如何通过curl命令行工具使用REST API。

REST API支持以下操作：

* 开始或停止工作流服务
* 创建、更新或删除工作流模型
* [开始、暂停、恢复或终止工作流实例](/help/sites-administering/workflows.md#workflow-status-and-actions)
* 完成或委派工作项

>[!NOTE]
>
>通过使用Firebug（用于Web开发的Firefox扩展），可以在控制台操作时跟踪HTTP流量。 例如，您可以检查发送到AEM服务器的参数和值（请求`POST`）。

在此页中，假定AEM在本地主机上的端口`4502`运行，并且安装上下文为“ `/`”(root)。 如果安装时不适用，则需要相应地调整HTTP请求所适用的URI。

`GET`请求支持的渲染是JSON渲染。 `GET`的URL应具有`.json`扩展名，例如：

`http://localhost:4502/etc/workflow.json`

### 管理工作流实例{#managing-workflow-instances}

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
   <td>列表可用的工作流实例。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>创建新的工作流实例。 参数为：<br /> - <code>model</code>:相应工作流模型<br />的ID(URI)- <code>payloadType</code>:包含有效负荷的类型（例如<code>JCR_PATH</code>或URL）。<br /> 有效负荷作为参数发送 <code>payload</code>。将回发<code>201</code>(<code>CREATED</code>)响应，其中包含新工作流实例资源的URL的位置标头。</p> </td>
  </tr>
 </tbody>
</table>

#### 按状态{#managing-a-workflow-instance-by-its-state}管理工作流实例

以下HTTP请求方法适用于：

`http://localhost:4502/etc/workflow/instances.{state}`

| HTTP请求方法 | 操作 |
|---|---|
| `GET` | 列表可用工作流实例及其状态（`RUNNING`、`SUSPENDED`、`ABORTED`或`COMPLETED`） |

#### 按ID {#managing-a-workflow-instance-by-its-id}管理工作流实例

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
   <td>更改实例的状态。 新状态将作为参数<code>state</code>发送，且必须具有以下值之一：<code>RUNNING</code>、<code>SUSPENDED</code>或<code>ABORTED</code>。<br /> 如果新状态不可访问（例如，当挂起终止的实例时）, <code>409</code> 则(<code>CONFLICT</code>)响应将发回到客户端。</td>
  </tr>
 </tbody>
</table>

### 管理工作流模型{#managing-workflow-models}

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
   <td>列表可用的工作流模型。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>创建新工作流模型. 如果发送参数<code>title</code>，则使用指定的标题创建新模型。 将JSON模型定义作为参数<code>model</code>附加后，将根据提供的定义创建新的工作流模型。<br /> 回 <code>201</code> 应(<code>CREATED</code>)会与包含新工作流模型资源的URL的位置标题一起发送。<br /> 当模型定义作为名为的文件参数附加时，也会发生同样的情况 <code>modelfile</code>。<br /> 在参数和参数的情 <code>model</code> 况 <code>modelfile</code> 下，定义序列化格 <code>type</code> 式时都需要另外一个名为的参数。新的序列化格式可以使用OSGI API进行集成。 标准JSON序列化器随工作流引擎一起提供。 其类型为JSON。 有关格式的示例，请参见下文。</td>
  </tr>
 </tbody>
</table>

示例：在浏览器中，对`http://localhost:4502/etc/workflow/models.json`的请求将生成与以下内容类似的json响应：

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

#### 管理特定工作流模型{#managing-a-specific-workflow-model}

以下HTTP请求方法适用于：

`http://localhost:4502*{uri}*`

其中`*{uri}*`是存储库中模型节点的路径。

<table>
 <tbody>
  <tr>
   <td>HTTP请求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>获取模型的<code>HEAD</code>版本（定义和元数据）。</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>更新<code>HEAD</code>版本的模型（创建新版本）。<br /> 必须将新版本的模型的完整模型定义添加为名为的参数 <code>model</code>。此外，创建新模型时需要<code>type</code>参数，并且需要具有值<code>JSON</code>。<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>行为与PUT相同。 需要，因为AEM构件不支持<code>PUT</code>操作。</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>删除模型。 为了解决防火墙／代理问题，<code>POST</code>中包含值<code>DELETE</code>的<code>X-HTTP-Method-Override</code>头条目的&lt;a0/&gt;也将作为<code>DELETE</code>请求接受。</td>
  </tr>
 </tbody>
</table>

示例：在浏览器中，对`http://localhost:4502/var/workflow/models/publish_example.json`的请求返回与以下代码类似的`json`响应：

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

#### 按{#managing-a-workflow-model-by-its-version}版本管理工作流模型

以下HTTP请求方法适用于：

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| HTTP请求方法 | 操作 |
|---|---|
| `GET` | 获取给定版本中的模型数据（如果存在）。 |

### 管理（用户）收件箱{#managing-user-inboxes}

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
   <td>列表用户收件箱中的工作项，HTTP身份验证头会识别该用户。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>完成其URI作为参数<code>item</code>发送的工作项，并将根据工作流实例前进到下一个节点，该节点由参数<code>route</code>或<code>backroute</code>定义，以便返回。<br /> 如果发送参 <code>delegatee</code> 数，则由参数标识的工作项将 <code>item</code> 委派给指定的参加者。</td>
  </tr>
 </tbody>
</table>

#### 使用WorkItem ID {#managing-a-user-inbox-by-the-workitem-id}管理（用户）收件箱

以下HTTP请求方法适用于：

`http://localhost:4502/bin/workflow/inbox/{id}`

| HTTP请求方法 | 操作 |
|---|---|
| `GET` | 获取由收件箱ID标识的收件箱`WorkItem`的数据（定义和元数据）。 |

## 示例 {#examples}

### 如何获取所有正在运行的工作流的列表，其ID {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

要获取所有正在运行的工作流的列表，请执行GET以：

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### 如何获取所有正在运行的工作流的列表及其ID —— 使用curl {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}的REST

使用curl的示例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

结果中显示的`uri`可以作为其他命令中的实例`id`;例如：

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>此`curl`命令可以与任何[工作流状态](/help/sites-administering/workflows.md#workflow-status-and-actions)一起使用，而不是`RUNNING`。

### 如何更改工作流标题{#how-to-change-the-workflow-title}

要更改在工作流控制台的&#x200B;**实例**&#x200B;选项卡中显示的&#x200B;**工作流标题**，请发送`POST`命令：

* 到: `http://localhost:4502/etc/workflow/instances/{id}`

* 使用以下参数：

   * `action`:其价值必须是：  `UPDATE`
   * `workflowTitle`:工作流标题

#### 如何使用curl {#how-to-change-the-workflow-title-rest-using-curl}更改工作流标题- REST

使用curl的示例：

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### 如何列表所有工作流模型{#how-to-list-all-workflow-models}

要获取所有可用工作流模型的列表，请执行GET以：

`http://localhost:4502/etc/workflow/models.json`

#### 如何列表所有工作流模型——使用curl {#how-to-list-all-workflow-models-rest-using-curl}的REST

使用curl的示例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>另请参阅[管理工作流模型](#managing-workflow-models)。

### 获取WorkflowSession对象{#obtaining-a-workflowsession-object}

`com.adobe.granite.workflow.WorkflowSession`类可从`javax.jcr.Session`对象或`org.apache.sling.api.resource.ResourceResolver`对象进行调整。

#### 获取WorkflowSession对象- Java {#obtaining-a-workflowsession-object-java}

在JSP脚本（或Servlet类的Java代码）中，使用HTTP请求对象获取`SlingHttpServletRequest`对象，该对象提供对`ResourceResolver`对象的访问。 将`ResourceResolver`对象调整为`WorkflowSession`。

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

#### 获取WorkflowSession对象- ECMA脚本{#obtaining-a-workflowsession-object-ecma-script}

使用`sling`变量获取用于获取`ResourceResolver`对象的`SlingHttpServletRequest`对象。 将`ResourceResolver`对象调整为`WorkflowSession`对象。

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### 创建、读取或删除工作流模型{#creating-reading-or-deleting-workflow-models}

以下示例显示如何访问工作流模型：

* Java和ECMA脚本的代码使用`WorkflowSession.createNewModel`方法。
* curl命令直接使用其URL访问模型。

使用的示例：

1. 创建模型（ID为`/var/workflow/models/mymodel/jcr:content/model`）。
1. 删除模型。

>[!NOTE]
>
>删除模型会将模型的`metaData`子节点的`deleted`属性设置为`true`。
>
>删除不会删除模型节点。

创建新模型时：

* 工作流模型编辑器要求模型使用`/var/workflow/models`下的特定节点结构。 模型的父节点必须为具有以下属性值的`jcr:content`节点的类型`cq:Page`:

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`:  `/libs/cq/workflow/templates/model`

   创建模型时，必须先创建此`cq:Page`节点，并使用其`jcr:content`节点作为模型节点的父节点。

* 某些方法识别模型所需的`id`参数是存储库中模型节点的绝对路径：

   `/var/workflow/models/<*model_name>*/jcr:content/model`

   >[!NOTE]
   >
   >请参阅[如何列表所有工作流模型](#how-to-list-all-workflow-models)。

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

#### 创建、读取或删除工作流模型- ECMA脚本{#creating-reading-or-deleting-workflow-models-ecma-script}

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

#### 删除工作流模型——使用curl {#deleting-a-workflow-model-rest-using-curl}进行REST

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>由于所需的详细程度，在创建和／或读取模型时，curl不被认为是实用的。

### 检查工作流状态{#filtering-out-system-workflows-when-checking-workflow-status}时过滤掉系统工作流

您可以使用[WorkflowStatus API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html)检索有关节点工作流状态的信息。

各种方法都具有参数：

`excludeSystemWorkflows`

此参数可设置为`true`以指示应从相关结果中排除系统工作流。

您[可以更新OSGi配置](/help/sites-deploying/configuring-osgi.md) **AdobeGranite工作流PayloadMapCache**，该配置指定要视为系统工作流的工作流`Models`。 默认（运行时）工作流模型为：

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### 超时{#auto-advance-participant-step-after-a-timeout}后的自动前进参与者步骤

如果您需要自动前进在预定义时间内尚未完成的&#x200B;**参与者**&#x200B;步骤，您可以：

1. 实现OSGI事件监听器以监听任务创建和修改。
1. 指定超时（截止日期），然后创建计划的sling作业以在该时间触发。
1. 编写一个作业处理程序，该处理程序在超时过期时通知并触发作业。

   如果任务尚未完成，此处理程序将对任务执行所需的操作

>[!NOTE]
>
>必须明确界定要采取的行动才能采用这种方法。

### 与工作流实例{#interacting-with-workflow-instances}交互

下面提供了如何与工作流实例进行交互(progamaly)的基本示例。

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

#### 与工作流实例交互- ECMA脚本{#interacting-with-workflow-instances-ecma-script}

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

#### 与工作流实例交互——使用curl {#interacting-with-workflow-instances-rest-using-curl}的REST

* **启动工作流**

   ```shell
   # starting a workflow
   curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
   
   # for example:
   curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
   ```

* **列出实例**

   ```shell
   # listing the instances
   curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
   ```

   这将列表所有情况；例如：

   ```shell
   [
       {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
       ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
   ]
   ```

   >[!NOTE]
   >
   >请参阅[如何获取所有正在运行的列表](#how-to-get-a-list-of-all-running-workflows-with-their-ids)及其ID，以列出具有特定状态的实例。

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

### 与工作项{#interacting-with-work-items}交互

下面提供了如何与工作项进行交互（按程序）的基本示例。

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

#### 与工作项交互- ECMA脚本{#interacting-with-work-items-ecma-script}

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

#### 与工作项交互——使用curl {#interacting-with-work-items-rest-using-curl}的REST

* **从收件箱中列出工作项**

   ```shell
   # listing the work items
   curl -u admin:admin http://localhost:4502/bin/workflow/inbox
   ```

   将列出收件箱中当前工作项的详细信息；例如：

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
   >`delegatee`必须是工作流步骤的有效选项。

* **完成或将工作项推向下一步**

   ```xml
   # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
   http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
   
   # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
   curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
   ```

### 侦听工作流事件{#listening-for-workflow-events}

使用OSGi事件框架监听[ `com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html)类定义的事件。 此类还提供几种有用的方法，用于获取有关事件主题的信息。 例如，`getWorkItem`方法返回与事件相关的工作项的`WorkItem`对象。

以下示例代码定义一个服务，它监听工作流事件并根据事件类型执行任务。

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

