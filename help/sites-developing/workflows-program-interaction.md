---
title: 以程式設計方式與工作流程互動
seo-title: Interacting with Workflows Programmatically
description: 以程式設計方式與工作流程互動
seo-description: null
uuid: a0f19fc6-b9bd-4b98-9c0e-fbf4f7383026
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: cb621332-a149-4f8d-9425-fd815b033c38
exl-id: 2b396850-e9fb-46d9-9daa-ebd410a9e1a5
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# 以程式設計方式與工作流程互動{#interacting-with-workflows-programmatically}

時間 [自訂和擴充您的工作流程](/help/sites-developing/workflows-customizing-extending.md) 您可以存取工作流程物件：

* [使用工作流程Java API](#using-the-workflow-java-api)
* [在ECMA指令碼中取得工作流程物件](#obtaining-workflow-objects-in-ecma-scripts)
* [使用工作流程REST API](#using-the-workflow-rest-api)

## 使用工作流程Java API {#using-the-workflow-java-api}

工作流程Java API包含 [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) 套件和多個子套件。 API最重要的成員為 `com.adobe.granite.workflow.WorkflowSession` 類別。 此 `WorkflowSession` 類別可讓您存取設計階段和執行階段工作流程物件：

* 工作流程模型
* 工作專案
* 工作流程例項
* 工作流程資料
* 收件匣專案

此類別也提供幾種干預工作流程生命週期的方法。

下表提供以程式設計方式與工作流程互動時，要使用的幾個關鍵Java物件的參考檔案連結。 下列範例示範如何取得和使用程式碼中的類別物件。

| 功能 | 对象 |
|---|---|
| 存取工作流程 | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| 執行和查詢工作流程執行個體 | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| 管理工作流程模型 | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| 工作流程中（或不在）的節點資訊 | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## 在ECMA指令碼中取得工作流程物件 {#obtaining-workflow-objects-in-ecma-scripts}

如所述 [找到指令碼](/help/sites-developing/the-basics.md#locating-the-script)，AEM （透過Apache Sling）提供可執行伺服器端ECMA指令碼的ECMA指令碼引擎。 此 [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) 類別可立即供您的指令碼使用，作為 `sling` 變數。

此 `ScriptHelper` 類別可讓您存取 `SlingHttpServletRequest` 您可使用來最終取得 `WorkflowSession` 物件；例如：

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## 使用工作流程REST API {#using-the-workflow-rest-api}

「工作流程」主控台大量使用REST API，因此本頁會說明工作流程的REST API。

>[!NOTE]
>
>curl命令列工具可讓您使用Workflow REST API來存取工作流程物件及管理執行個體生命週期。 本頁面的範例示範如何透過curl命令列工具使用REST API。

REST API支援下列動作：

* 啟動或停止工作流程服務
* 建立、更新或刪除工作流程模型
* [啟動、暫停、繼續或終止工作流程例項](/help/sites-administering/workflows.md#workflow-status-and-actions)
* 完成或委派工作專案

>[!NOTE]
>
>藉由使用適用於Web開發的Firefox擴充功能Firebug，您可以在操作主控台時追蹤HTTP流量。 例如，您可以使用檢查引數和傳送至AEM伺服器的值 `POST` 要求。

在此頁面中，假設AEM會在連線埠的localhost上執行 `4502` 而且安裝內容是&quot; `/`「 」（根）。 如果不是安裝，則需要相應地調整HTTP請求適用的URI。

支援的轉譯 `GET` requests是JSON轉譯。 的URL `GET` 應該具有 `.json` 延伸模組，例如：

`http://localhost:4502/etc/workflow.json`

### 管理工作流程例項 {#managing-workflow-instances}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出可用的工作流程例項。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>建立新的工作流程例項。 引數包括：<br /> - <code>model</code>：個別工作流程模型的ID (URI)<br /> - <code>payloadType</code>：包含裝載的型別(例如 <code>JCR_PATH</code> 或URL)。<br /> 裝載會以引數形式傳送 <code>payload</code>. A <code>201</code> (<code>CREATED</code>)回應會以包含新工作流程執行個體資源URL的位置標頭傳回。</p> </td>
  </tr>
 </tbody>
</table>

#### 依狀態管理工作流程執行個體 {#managing-a-workflow-instance-by-its-state}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/instances.{state}`

| HTTP要求方法 | 操作 |
|---|---|
| `GET` | 列出可用的工作流程例項及其狀態( `RUNNING`， `SUSPENDED`， `ABORTED` 或 `COMPLETED`) |

#### 依其ID管理工作流程例項 {#managing-a-workflow-instance-by-its-id}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>取得包含個別工作流程模型連結的執行個體資料（定義和中繼資料）。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>變更執行個體的狀態。 新狀態會以引數的形式傳送 <code>state</code> 和必須具有下列其中一個值： <code>RUNNING</code>， <code>SUSPENDED</code>，或 <code>ABORTED</code>.<br /> 如果無法連線到新狀態（例如暫停終止的執行個體時） a <code>409</code> (<code>CONFLICT</code>)回應會傳回給使用者端。</td>
  </tr>
 </tbody>
</table>

### 管理工作流程模型 {#managing-workflow-models}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出可用的工作流程模型。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>创建新工作流模型. 如果引數 <code>title</code> ，則會以指定的標題建立新模型。 附加JSON模型定義作為引數 <code>model</code> 根據提供的定義建立新的工作流程模型。<br /> A <code>201</code> 回應(<code>CREATED</code>)會以包含新工作流程模型資源的URL的位置標頭傳回。<br /> 當模型定義附加為名為的檔案引數時，也會發生相同情況 <code>modelfile</code>.<br /> 在這兩種情況下 <code>model</code> 和 <code>modelfile</code> 引數，另一個引數稱為 <code>type</code> 定義序列化格式時需要。 可使用OSGI API整合新的序列化格式。 標準JSON序列化程式會與工作流程引擎一併傳送。 其型別為JSON。 如需格式的範例，請參閱下文。</td>
  </tr>
 </tbody>
</table>

範例：在瀏覽器中，請求 `http://localhost:4502/etc/workflow/models.json` 會產生類似於以下內容的json回應：

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

#### 管理特定工作流程模型 {#managing-a-specific-workflow-model}

下列HTTP要求方法適用於：

`http://localhost:4502*{uri}*`

位置 `*{uri}*` 是存放庫中模型節點的路徑。

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>取得 <code>HEAD</code> 模型的版本（定義和中繼資料）。</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>更新 <code>HEAD</code> 模型的版本（建立新版本）。<br /> 新版本模型的完整模型定義必須新增為引數，稱為 <code>model</code>. 此外， <code>type</code> 建立新模型時需要引數，並且需要值 <code>JSON</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>與PUT的行為相同。 需要，因為AEM Widget不支援 <code>PUT</code> 作業。</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>刪除模型。 為了解決防火牆/Proxy問題， <code>POST</code> 包含 <code>X-HTTP-Method-Override</code> 具有值的標頭專案 <code>DELETE</code> 也會被接受為 <code>DELETE</code> 要求。</td>
  </tr>
 </tbody>
</table>

範例：在瀏覽器中，請求 `http://localhost:4502/var/workflow/models/publish_example.json` 傳回 `json` 與下列程式碼類似的回應：

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

#### 依版本管理工作流程模型 {#managing-a-workflow-model-by-its-version}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| HTTP要求方法 | 操作 |
|---|---|
| `GET` | 取得指定版本中的模型資料（如果存在）。 |

### 管理（使用者）收件匣 {#managing-user-inboxes}

下列HTTP要求方法適用於：

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>操作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出使用者收件匣中的工作專案，使用者由HTTP驗證標頭識別。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>完成URI作為引數傳送的工作專案 <code>item</code> 和會根據工作流程例項前進到下一個節點（由引數定義） <code>route</code> 或 <code>backroute</code> 如果後退一步。<br /> 如果引數 <code>delegatee</code> 「 」已傳送，工作專案由引數識別 <code>item</code> 已委派給指定的參與者。</td>
  </tr>
 </tbody>
</table>

#### 依工作專案ID管理（使用者）收件匣 {#managing-a-user-inbox-by-the-workitem-id}

下列HTTP要求方法適用於：

`http://localhost:4502/bin/workflow/inbox/{id}`

| HTTP要求方法 | 操作 |
|---|---|
| `GET` | 取得收件匣的資料（定義和中繼資料） `WorkItem` 由其ID識別。 |

## 示例 {#examples}

### 如何取得所有執行中的工作流程清單及其ID {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

若要取得所有執行中工作流程的清單，請執行GET：

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### 如何使用ID取得所有執行中工作流程的清單 — 使用CURL重設 {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

使用curl的範例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

此 `uri` 顯示在結果中可作為例項使用 `id` 在其他命令中；例如：

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>此 `curl` 命令可與任何 [工作流程狀態](/help/sites-administering/workflows.md#workflow-status-and-actions) 取代 `RUNNING`.

### 如何變更工作流程標題 {#how-to-change-the-workflow-title}

若要變更 **工作流程標題** 顯示在 **執行個體** 索引標籤中，傳送 `POST` 命令：

* 到: `http://localhost:4502/etc/workflow/instances/{id}`

* ，並使用下列引數：

   * `action`：其值必須是： `UPDATE`
   * `workflowTitle`：工作流程標題

#### 如何使用curl變更工作流程標題 — REST {#how-to-change-the-workflow-title-rest-using-curl}

使用curl的範例：

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### 如何列出所有工作流程模型 {#how-to-list-all-workflow-models}

若要取得所有可用工作流程模型的清單，請執行GET：

`http://localhost:4502/etc/workflow/models.json`

#### 如何列出所有工作流程模型 — REST使用curl {#how-to-list-all-workflow-models-rest-using-curl}

使用curl的範例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>另請參閱 [管理工作流程模型](#managing-workflow-models).

### 取得WorkflowSession物件 {#obtaining-a-workflowsession-object}

此 `com.adobe.granite.workflow.WorkflowSession` 類別可從 `javax.jcr.Session` 物件或 `org.apache.sling.api.resource.ResourceResolver` 物件。

#### 取得WorkflowSession物件 — Java {#obtaining-a-workflowsession-object-java}

在JSP指令碼（或servlet類別的Java程式碼）中，使用HTTP請求物件來取得 `SlingHttpServletRequest` 物件，可讓您存取 `ResourceResolver` 物件。 調整 `ResourceResolver` 物件至 `WorkflowSession`.

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

#### 取得WorkflowSession物件 — ECMA指令碼 {#obtaining-a-workflowsession-object-ecma-script}

使用 `sling` 變數來取得 `SlingHttpServletRequest` 用來取得 `ResourceResolver` 物件。 調整 `ResourceResolver` 物件至 `WorkflowSession` 物件。

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### 建立、讀取或刪除工作流程模型 {#creating-reading-or-deleting-workflow-models}

下列範例說明如何存取工作流程模型：

* Java和ECMA指令碼的程式碼會使用 `WorkflowSession.createNewModel` 方法。
* curl指令直接使用模型的URL來存取模型。

使用的範例：

1. 建立模型（使用ID） `/var/workflow/models/mymodel/jcr:content/model`)。
1. 刪除模型。

>[!NOTE]
>
>刪除模型會設定 `deleted` 模型的屬性 `metaData` 子節點至 `true`.
>
>刪除不會移除模型節點。

建立新模型時：

* 工作流程模型編輯器要求模型使用下面的特定節點結構 `/var/workflow/models`. 模型的父節點必須是型別 `cq:Page` 具有 `jcr:content` 具有下列屬性值的節點：

   * `sling:resourceType`： `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`

   當您建立模型時，您必須先建立這個 `cq:Page` 節點並使用其 `jcr:content` 節點作為模型節點的父節點。

* 此 `id` 某些用來識別模型的方法所需的引數是存放庫中模型節點的絕對路徑：

   `/var/workflow/models/<*model_name>*/jcr:content/model`

   >[!NOTE]
   >
   >另請參閱 [如何列出所有工作流程模型](#how-to-list-all-workflow-models).

#### 建立、讀取或刪除工作流程模型 — Java {#creating-reading-or-deleting-workflow-models-java}

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

#### 建立、讀取或刪除工作流程模型 — ECMA指令碼 {#creating-reading-or-deleting-workflow-models-ecma-script}

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

#### 刪除工作流程模型 — REST使用curl {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>由於所需的詳細程度，Curl對於建立和/或讀取模型並不實際。

### 檢查工作流程狀態時篩選出系統工作流程 {#filtering-out-system-workflows-when-checking-workflow-status}

您可以使用 [WorkflowStatus API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) 以擷取有關節點的工作流程狀態的資訊。

各種方法都有引數：

`excludeSystemWorkflows`

此引數可設為 `true` 以指出系統工作流程應從相關結果中排除。

您 [可以更新OSGi設定](/help/sites-deploying/configuring-osgi.md) **AdobeGranite工作流程PayloadMapCache** 指定工作流程 `Models` 視為系統工作流程。 預設（執行階段）工作流程模型為：

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### 逾時後自動前進參與者步驟 {#auto-advance-participant-step-after-a-timeout}

如果您需要自動前進 **參與者** 在預先定義的時間內尚未完成的步驟，您可以：

1. 實作OSGI事件接聽程式，以接聽建立與修改工作的作業。
1. 指定逾時（期限），然後建立排程的Sling作業，以在該時間引發。
1. 撰寫作業處理常式，在逾時過期並觸發作業時通知此處理常式。

   如果工作尚未完成，此處理常式會對工作採取必要的動作

>[!NOTE]
>
>必須清楚定義要採取的動作，才能使用此方法。

### 與工作流程例項互動 {#interacting-with-workflow-instances}

以下提供如何與工作流程例項互動（程式化）的基本範例。

#### 與工作流程例項互動 — Java {#interacting-with-workflow-instances-java}

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

#### 與工作流程執行個體互動 — ECMA指令碼 {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows("RUNNING");
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 與工作流程例項互動 — 使用CURL重設 {#interacting-with-workflow-instances-rest-using-curl}

* **啟動工作流程**

   ```shell
   # starting a workflow
   curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
   
   # for example:
   curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
   ```

* **列出執行個體**

   ```shell
   # listing the instances
   curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
   ```

   這會列出所有例項，例如：

   ```shell
   [
       {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
       ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
   ]
   ```

   >[!NOTE]
   >
   >另請參閱 [如何取得所有執行中工作流程的清單](#how-to-get-a-list-of-all-running-workflows-with-their-ids) 具有用於列出具有特定狀態之執行個體的ID。

* **暫停工作流程**

   ```shell
   # suspending a workflow
   curl -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **繼續工作流程**

   ```shell
   # resuming a workflow
   curl -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **終止工作流程例項**

   ```shell
   # terminating a workflow
   curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

### 與工作專案互動 {#interacting-with-work-items}

以下提供如何與工作專案互動（程式化）的基本範例。

#### 與工作專案互動 — Java {#interacting-with-work-items-java}

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

#### 與工作專案互動 — ECMA指令碼 {#interacting-with-work-items-ecma-script}

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

#### 與工作專案互動 — 使用CURL重設 {#interacting-with-work-items-rest-using-curl}

* **從收件匣列出工作專案**

   ```shell
   # listing the work items
   curl -u admin:admin http://localhost:4502/bin/workflow/inbox
   ```

   將會列出目前在「收件匣」中的工作專案詳細資訊；例如：

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

* **委派工作專案**

   ```xml
   # delegating
   curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
   ```

   >[!NOTE]
   >
   >此 `delegatee` 必須為工作流程步驟的有效選項。

* **完成或推進工作專案至下一個步驟**

   ```xml
   # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
   http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
   
   # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
   curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
   ```

### 接聽工作流程事件 {#listening-for-workflow-events}

使用OSGi事件架構接聽 [ `com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html) 類別定義。 此類別也提供幾個實用方法，用於取得事件主旨的相關資訊。 例如， `getWorkItem` 方法會傳回 `WorkItem` 事件所涉及之工作專案的物件。

以下範常式式碼會定義一個服務，用於監聽工作流程事件並根據事件型別執行任務。

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
