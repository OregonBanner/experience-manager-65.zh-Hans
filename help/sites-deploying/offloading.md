---
title: 正在解除安裝工作
seo-title: Offloading Jobs
description: 瞭解如何在拓撲中設定和使用AEM執行個體，以執行特定型別的處理。
seo-description: Learn how to configure and use AEM instances in a topology in order to perform specific types of processing.
uuid: e971d403-dfd2-471f-b23d-a67e35f1ed88
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 370151df-3b8e-41aa-b586-5c21ecb55ffe
feature: Configuring
exl-id: 429c96ff-4185-4215-97e8-9bd2c130a9b1
source-git-commit: 08a6777bf1ff3abf62f45fe1e164ef2027996848
workflow-type: tm+mt
source-wordcount: '2364'
ht-degree: 1%

---

# 正在解除安裝工作{#offloading-jobs}

## 简介 {#introduction}

解除安裝會將處理工作分散到拓撲中的Experience Manager執行個體之間。 透過解除安裝，您可以使用特定Experience Manager執行個體來執行特定型別的處理。 專業化的處理可讓您最大限度地使用可用的伺服器資源。

解除安裝是根據 [Apache Sling探索](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) 和Sling JobManager功能。 若要使用解除安裝，您可以將Experience Manager叢集新增至拓朴，並識別叢集處理的工作主題。 叢集是由一或多個Experience Manager執行處理所組成，因此單一執行處理可視為叢集。

如需將執行處理新增至拓朴的詳細資訊，請參閱 [管理拓撲](/help/sites-deploying/offloading.md#administering-topologies).

### 工作分佈 {#job-distribution}

Sling JobManager和JobConsumer可讓您建立拓撲中處理的工作：

* 工作管理員：為特定主題建立工作的服務。
* JobConsumer：執行一或多個主題工作的服務。 可以針對相同主題註冊多個JobConsumer服務。

當JobManager建立工作時，解除安裝架構會在拓撲中選取Experience Manager叢集以執行工作：

* 叢集必須包含一或多個執行處理，這些執行處理正在執行為工作主題註冊的JobConsumer。
* 叢集中至少必須啟用一個執行處理的主題。

另請參閱 [設定主題使用量](/help/sites-deploying/offloading.md#configuring-topic-consumption) 以取得精簡工作分配的資訊。

![chlimage_1-109](assets/chlimage_1-109.png)

當「解除安裝」架構選取叢集來執行工作，且叢集由多個執行個體組成時，Sling Distribution會判斷叢集中的哪個執行個體執行工作。

### 工作裝載 {#job-payloads}

「解除安裝」架構支援將工作與儲存庫中的資源相關聯的工作裝載。 建立處理資源的工作時，工作裝載很有用，而且工作已解除安裝到另一部電腦。

建立工作後，保證只會將裝載放在建立工作的執行個體上。 解除安裝工作時，復寫代理程式會確保在最終佔用工作的執行個體上建立裝載。 工作執行完成後，反向復寫會將裝載複製回建立工作的執行個體。

## 管理拓撲 {#administering-topologies}

拓撲是參與解除安裝的鬆散耦合Experience Manager叢集。 叢集由一或多個Experience Manager伺服器執行處理（單一執行處理視為叢集）組成。

每個Experience Manager執行個體都會執行下列解除安裝相關服務：

* 探索服務：傳送要求給拓撲聯結器以加入拓撲。
* 拓撲聯結器：接收加入要求，並接受或拒絕每個要求。

拓撲的所有成員的「探索服務」指向其中一個成員上的「拓撲聯結器」。 在接下來的章節中，此成員稱為根成員。

![chlimage_1-110](assets/chlimage_1-110.png)

拓撲中的每個叢集都包含被識別為導引的執行個體。 叢集導線代表叢集的其他成員與拓撲互動。 當導引線離開叢集時，會自動為叢集選擇新的導引線。

### 檢視拓撲 {#viewing-the-topology}

使用「拓朴瀏覽器」來探索Experience Manager執行個體所參與的拓朴的狀態。 「拓朴瀏覽器」會顯示拓朴的叢集和執行處理。

對於每個叢集，您會看到一個叢整合員清單，指出每個成員加入叢集的順序，以及哪個成員是領導者。 「目前」屬性指出您目前所管理的執行處理。

對於叢集中的每個執行處理，您可以看到幾個拓撲相關屬性：

* 執行個體工作消費者的允許主題清單。
* 用來連線拓朴的開放端點。
* 為其註冊執行個體以進行解除安裝的工作主題。
* 執行處理所處理的工作主題。

1. 使用Touch UI，按一下「工具」標籤。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. 在「Granite作業」區域中，按一下「解除安裝瀏覽器」。
1. 在導覽面板中，按一下「拓朴瀏覽器」。

   參與拓朴的叢集隨即顯示。

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. 按一下叢集可檢視叢集中的執行處理清單，以及其ID、目前狀態和Leader狀態。
1. 按一下執行個體ID可檢視更多詳細屬性。

您也可以使用Web主控台來檢視拓撲資訊。 主控台提供拓朴叢集的進一步資訊：

* 哪個執行個體是本機執行個體。
* 此執行個體用來連線至拓撲（傳出）的Topology Connector服務，以及連線至此執行個體（傳入）的服務。
* 變更拓撲和執行個體屬性的歷史記錄。

請使用下列程式來開啟「Web主控台」的「拓朴管理」頁面：

1. 在瀏覽器中開啟Web主控台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下「主要」>「拓朴管理」。

   ![chlimage_1-112](assets/chlimage_1-112.png)

### 設定拓朴成員資格 {#configuring-topology-membership}

Apache Sling Resource-Based Discovery Service會在每個執行個體上執行，以控制Experience Manager執行個體與拓撲互動的方式。

探索服務會定期傳送POST要求（心率）給拓朴聯結器服務，以建立和維護與拓朴的連線。 Topology Connector服務會維護允許加入拓撲的IP位址或主機名稱允許清單：

* 若要將執行個體聯結至拓撲，請指定根成員的Topology Connector服務的URL。
* 若要啟用執行個體以加入拓撲，請將執行個體新增至根成員的Topology Connector服務的允許清單。

使用Web主控台或sling：OsgiConfig節點來設定org.apache.sling.discovery.impt.Config服務的下列屬性：

<table>
 <tbody>
  <tr>
   <th>属性名称</th>
   <th>OSGi名稱</th>
   <th>描述</th>
   <th>默认值</th>
  </tr>
  <tr>
   <td>心率逾時（秒）</td>
   <td>heartbeattimeout</td>
   <td>在目標執行個體被視為不可用之前，等待心率回應的時間量（以秒為單位）。 </td>
   <td>20</td>
  </tr>
  <tr>
   <td>心率間隔（秒）</td>
   <td>心率間隔</td>
   <td>心率之間的時間長度（以秒為單位）。</td>
   <td>15</td>
  </tr>
  <tr>
   <td>最小事件延遲（秒）</td>
   <td>minEventDelay</td>
   <td><p>當拓撲發生變更時，延遲狀態從TOPOLOGY_CHANGING變更到TOPOLOGY_CHANGED的時間量。 當狀態為TOPOLOGY_CHANGING時發生的每次變更都會增加延遲的時間。</p> <p>此延遲可防止接聽程式被事件淹沒。 </p> <p>若要使用無延遲，請指定0或負數。</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>拓撲聯結器URL</td>
   <td>topologyConnectorUrl</td>
   <td>用於傳送心率訊息的Topology Connector服務的URL。</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>拓朴聯結器允許清單</td>
   <td>topologyConnectorWhitelist</td>
   <td>本機Topology Connector服務允許在拓撲中的IP位址或主機名稱清單。 </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>存放庫描述項名稱</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;无值&gt;</td>
  </tr>
 </tbody>
</table>

使用下列程式將CQ執行處理連線到拓撲的根成員。 此程式會將執行個體指向根拓撲成員的拓撲聯結器URL。 對拓撲的所有成員執行此程式。

1. 在瀏覽器中開啟Web主控台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下「主要」>「拓朴管理」。
1. 按一下設定探索服務。
1. 將專案新增至Topology Connector URLs屬性，並指定根拓撲成員Topology Connector服務的URL。 URL的格式為https://rootservername:4502/libs/sling/topology/connector。

對拓朴的根成員執行下列程式。 程式會將其他拓朴成員的名稱新增至其[探索服務]允許清單。

1. 在瀏覽器中開啟Web主控台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 按一下「主要」>「拓朴管理」。
1. 按一下設定探索服務。
1. 對於拓撲的每個成員，將專案新增至拓撲聯結器允許清單屬性，並指定拓撲成員的主機名稱或IP位址。

## 設定主題使用量 {#configuring-topic-consumption}

使用解除安裝瀏覽器來設定拓撲中Experience Manager執行個體的主題使用量。 您可以為每個執行個體指定其使用的主題。 例如，若要設定拓朴，讓只有一個執行處理使用特定型別的主題，請停用除一個執行處理之外的所有執行處理上的主題。

工作會分散在使用循環配置邏輯啟用相關主題的執行個體之間。

1. 使用Touch UI，按一下「工具」標籤。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. 在「Granite作業」區域中，按一下「解除安裝瀏覽器」。
1. 在導覽面板中，按一下「解除安裝瀏覽器」。

   將會顯示解除安裝主題和可使用主題的伺服器執行個體。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 若要停用某個執行處理的主題使用，請在主題名稱下方按一下執行處理旁的「停用」。
1. 若要設定執行處理的所有主題使用量，請按一下任何主題下方的執行處理識別碼。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 按一下主題旁的下列按鈕之一，設定執行處理的使用行為，然後按一下儲存：

   * 已啟用：此執行個體會使用此主題的工作。
   * 停用：此執行個體不會使用這個主題的工作。
   * 獨佔：此執行個體只會使用這個主題的工作。

   **注意：** 當您選取主題的「獨佔」時，其他所有主題都會自動設定為「停用」。

### 已安裝的工作消費者 {#installed-job-consumers}

Experience Manager中安裝了數個JobConsumer實作。 註冊這些JobConsumers的主題會顯示在「解除安裝瀏覽器」中。 出現的其他主題是自訂JobConsumers已註冊的主題。 下表說明預設的JobConsumers。

| 工作主題 | 服务 PID | 描述 |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | 隨Apache Sling安裝。 為了回溯相容性，處理OSGi事件管理員產生的工作。 |
| com/day/cq/replication/job/&amp;ast； | com.day.cq.replication.impl.AgentManagerImpl | 復製作業裝載的復寫代理程式。 |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### 停用和啟用執行處理的主題 {#disabling-and-enabling-topics-for-an-instance}

Apache Sling作業消費者管理員服務提供主題允許清單和封鎖清單屬性。 設定這些屬性以啟用或停用處理Experience Manager執行個體上的特定主題。

**注意：** 如果執行個體屬於拓撲，您也可以在拓撲中的任何電腦上使用解除安裝瀏覽器來啟用或停用主題。

建立已啟用主題清單的邏輯會先允許允許清單中的所有主題，然後移除封鎖清單上的主題。 預設會啟用所有主題(允許清單值為 `*`)且沒有停用的主題（封鎖清單沒有值）。

使用Web主控台或 `sling:OsgiConfig` 節點，以設定下列屬性。 對象 `sling:OsgiConfig` 節點，工作消費者管理員服務的PID為org.apache.sling.event.impl.jobs.JobConsumerManager。

| Web主控台中的屬性名稱 | OSGi ID | 描述 |
|---|---|---|
| 主題允許清單 | job.consumermanager.whitelist | 本機JobManager服務處理的主題清單。 預設值&amp;ast；會使所有主題都傳送至已註冊的TopicConsumer服務。 |
| 主題區塊清單 | job.consumermanager.blacklist | 本機JobManager服務不處理的主題清單。 |

## 建立解除安裝復寫代理 {#creating-replication-agents-for-offloading}

解除安裝架構會使用復寫，在作者和工作者之間傳輸資源。 當執行個體加入拓撲時，解除安裝架構會自動建立復寫代理。 代理程式是以預設值建立的。 您必須手動變更代理程式用於驗證的密碼。

>[!CAUTION]
>
>自動產生的復寫代理的已知問題需要您手動建立新的復寫代理。

建立可在執行個體之間傳輸工作裝載以進行解除安裝的復寫代理。 下圖顯示從作者解除安裝至背景工作執行個體所需的代理程式。 作者的Sling ID為1，而背景工作執行個體的Sling ID為2：

![chlimage_1-115](assets/chlimage_1-115.png)

此設定需要下列三個代理程式：

1. 製作執行個體上複製到工作者執行個體的傳出代理程式。
1. 作者執行個體上從背景工作執行個體上的寄件匣提取的反向代理程式。
1. 背景工作執行個體上的寄件匣代理程式。

此復寫配置類似於製作和發佈執行個體之間使用的復寫配置。 然而，對於解除安裝情況，所有相關的執行個體都是編寫執行個體。

>[!NOTE]
>
>解除安裝架構會使用拓撲來取得解除安裝執行個體的IP位址。 然後，架構會根據這些IP位址自動建立復寫代理。 如果解除安裝執行個體的IP位址稍後變更，則在執行個體重新啟動後，變更會自動傳播到拓撲上。 不過，解除安裝架構不會自動更新復寫代理程式以反映新的IP位址。 為避免這種情況，請為拓撲中的所有執行個體使用固定IP位址。

### 命名要解除安裝的復寫代理 {#naming-the-replication-agents-for-offloading}

使用特定格式進行 ***名稱*** 復寫代理的屬性，讓解除安裝架構自動針對特定背景工作執行個體使用正確的代理。

**為編寫執行個體上的傳出代理程式命名：**

`offloading_<slingid>`，其中 `<slingid>` 是工作者執行個體的Sling ID。

示例: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**在製作執行個體上命名反向代理程式：**

`offloading_reverse_<slingid>`，其中 `<slingid>` 是工作者執行個體的Sling ID。

示例: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**為背景工作執行個體上的寄件匣命名：**

`offloading_outbox`

### 建立連出代理程式 {#creating-the-outgoing-agent}

1. 建立 **復寫代理** 作者。 (請參閱 [復寫代理程式檔案](/help/sites-deploying/replication.md))。 指定任何 **標題**. 此 **名稱** 必須符合命名慣例。
1. 使用下列屬性建立代理程式：

   | 属性 | 价值 |
   |---|---|
   | 設定>序列化型別 | 默认 |
   | 傳輸>傳輸URI | https://*`<ip of target instance>`*：*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 傳輸>傳輸使用者 | 目標執行個體上的復寫使用者 |
   | 傳輸>傳輸密碼 | 目標執行個體上的復寫使用者密碼 |
   | 延伸> HTTP方法 | POST |
   | 觸發器>忽略預設值 | True |

### 建立反向代理程式 {#creating-the-reverse-agent}

1. 建立 **反向復寫代理** 作者。 (請參閱 [復寫代理程式檔案](/help/sites-deploying/replication.md).) 指定任何 **標題**. 此 **名稱** 必須符合命名慣例。
1. 使用下列屬性建立代理程式：

   | 属性 | 价值 |
   |---|---|
   | 設定>序列化型別 | 默认 |
   | 傳輸>傳輸URI | https://*`<ip of target instance>`*：*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 傳輸>傳輸使用者 | 目標執行個體上的復寫使用者 |
   | 傳輸>傳輸密碼 | 目標執行個體上的復寫使用者密碼 |
   | 延伸> HTTP方法 | GET |

### 建立寄件匣代理程式 {#creating-the-outbox-agent}

1. 建立 **復寫代理** 在背景工作執行個體上。 (請參閱 [復寫代理程式檔案](/help/sites-deploying/replication.md).) 指定任何 **標題**. 此 **名稱** 必須是 `offloading_outbox`.
1. 使用下列屬性建立代理程式。

   | 属性 | 价值 |
   |---|---|
   | 設定>序列化型別 | 默认 |
   | 傳輸>傳輸URI | repo://var/replication/outbox |
   | 觸發器>忽略預設值 | True |

### 尋找Sling ID {#finding-the-sling-id}

使用下列任一種方法取得Experience Manager例項的Sling ID：

* 開啟Web主控台，並在Sling設定中找到Sling ID屬性的值([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings))。 如果執行個體尚未成為拓撲的一部分，則此方法很有用。
* 如果執行個體已經是拓撲的一部分，請使用「拓撲」瀏覽器。

<!--
## Offloading the Processing of DAM Assets {#offloading-the-processing-of-dam-assets}

Configure the instances of a topology so that specific instances perform the background processing of assets that are added or updated in DAM.

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>No workflow should be transient when used with workflow offloading. For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

The following procedure assumes the following characteristics for the offloading topology:

* One or more Experience Manager instance are authoring instances that users interact with for adding or updating DAM assets.
* Users to do not directly interact with one or more Experience Manager instances that process the DAM assets. These instances are dedicated to the background processing of DAM assets.

1. On each Experience Manager instance, configure the Discovery Service so that it points to the root Topography Connector. (See [Configuring Topology Membership](#title4).)
1. Configure the root Topography Connector so that the connecting instances are on the allow list.
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

    1. Open the Workflow console.
    1. Click the Launcher tab.
    1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
    1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.
-->

## 深入阅读 {#further-reading}

除了此頁面上顯示的詳細資訊外，您也可以閱讀下列內容：

* 如需使用Java API建立工作與工作消費者的相關資訊，請參閱 [建立與使用解除安裝工單](/help/sites-developing/dev-offloading.md).
