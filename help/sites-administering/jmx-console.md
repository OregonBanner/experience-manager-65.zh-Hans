---
title: 使用JMX主控台監控伺服器資源
seo-title: Monitoring Server Resources Using the JMX Console
description: 瞭解如何使用JMX主控台監控伺服器資源。
seo-description: Learn how to monitor server resources using the JMX console.
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
exl-id: eabd8335-6140-4c15-8cff-21608719aa5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4957'
ht-degree: 1%

---

# 使用JMX主控台監控伺服器資源{#monitoring-server-resources-using-the-jmx-console}

JMX主控台可讓您監視和管理CRX伺服器上的服務。 以下各節會概述透過JMX架構公開的屬性和操作。

如需有關如何使用主控台控制項的資訊，請參閱 [使用JMX控制檯](#using-the-jmx-console). 如需JMX的背景資訊，請參閱 [Java管理擴充功能(JMX)技術](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) oracle網站頁面。

如需有關建立MBean以使用JMX主控台管理服務的資訊，請參閱 [將服務與JMX主控台整合](/help/sites-developing/jmx-integration.md).

## 工作流程維護 {#workflow-maintenance}

管理執行中、已完成、過時和失敗的工作流程例項的作業。

* 網域： com.adobe.granite.workflow
* 型別：維護

>[!NOTE]
>
>請參閱 [工作流程主控台](/help/sites-administering/workflows-administering.md) 以取得其他工作流程管理工具及可能的工作流程執行個體狀態說明。

### 运营 {#operations}

**listRunningWorkflowsPerModel** 列出針對每個工作流程模型執行的工作流程例項數目。

* 引數：無
* 傳回值：包含Count和ModelId欄的表格資料。

**listCompletedWorkflowsPerModel** 列出每個工作流程模型的已完成工作流程例項數目。

* 引數：無
* 傳回值：包含Count和ModelId欄的表格資料。

**returnWorkflowQueueInfo** 列出已處理和已排入處理佇列之工作流程專案的相關資訊。

* 引數：無
* 傳回的值：包含下列資料行的表格資料：

   * Jobs
   * 佇列名稱
   * 活动作业
   * 平均處理時間
   * 平均等待時間
   * 取消的作业
   * 失败的作业
   * 已完成的工作
   * 已處理工作
   * 已排入佇列的工作

**returnWorkflowJobTopicInfo** 列出工作流程工作的處理資訊，依主題組織。

* 引數：無
* 傳回值：包含下列資料行的表格資料：

   * 主題名稱
   * 平均處理時間
   * 平均等待時間
   * 取消的作业
   * 失败的作业
   * 已完成的工作
   * 已處理工作

**returnFailedWorkflowCount** 顯示失敗的工作流程執行個體數目。 您可以指定工作流程模型，以查詢或擷取所有工作流程模型的資訊。

* 参数:

   * model：要查詢的模型ID。 若要檢視所有工作流程模型的失敗工作流程例項計數，請不要指定任何值。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回的值：失敗的工作流程例項數目。

**returnFailedWorkflowCountPerModel** 顯示每個工作流程模型失敗的工作流程例項數目。

* 引數：無。
* 傳回值：包含「計數」和「模型ID」欄的表格資料。

**terminateFailedInstances** 終止失敗的工作流程執行個體。 您可以終止所有失敗的執行個體，或僅終止特定模型的失敗執行個體。 您可以選擇在執行個體終止後重新啟動執行個體。 您也可以測試作業以檢視結果，而無需實際執行作業。

* 参数:

   * 重新啟動執行個體： （選擇性）指定值 `true` 要在執行個體終止後重新啟動執行個體。 預設值 `false` 不會重新啟動已終止的工作流程執行個體。
   * 試執行： （選擇性）指定值 `true` 以檢視作業結果，而不實際執行作業。 預設值 `false` 導致執行作業。
   * 模型： （選用）要套用作業的模型識別碼。 指定沒有模型可將操作套用至所有工作流程模型的失敗執行個體。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回的值：關於已終止之執行處理的表格資料，包含下列資料行：

   * 发起者
   * InstanceId
   * ModelId
   * 有效负荷
   * StartComment
   * 工作流程標題

**retryFailedWorkItems** 嘗試執行失敗的工作專案步驟。 您可以針對特定工作流程模型，重試所有失敗的工作專案或僅重試失敗的工作專案。 您可以選擇性地測試作業以檢視結果，而不實際執行作業。

* 参数:

   * 試執行： （選擇性）指定值 `true` 以檢視作業結果，而不實際執行作業。 預設值 `false` 導致執行作業。
   * 模型： （選用）要套用作業的模型識別碼。 指定沒有模型可將操作套用至所有工作流程模型的失敗工作專案。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回值：關於重試的失敗工作專案的表格資料，包括下列欄：

   * 发起者
   * InstanceId
   * ModelId
   * 有效负荷
   * StartComment
   * 工作流程標題

**清除活動** 移除特定頁面的作用中工作流程例項。 您可以清除所有模型的作用中例證，或僅清除特定模型的例證。 您可以選擇性地測試作業以檢視結果，而無需實際執行作業。

* 参数:

   * 模型： （選用）要套用作業的模型識別碼。 指定沒有模型可將操作套用至所有工作流程模型的工作流程例項。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 自工作流程開始以來的天數：要清除的工作流程例項存留期（以天為單位）。
   * 試執行： （選擇性）指定值 `true` 以檢視作業結果，而不實際執行作業。 預設值 `false` 導致執行作業。

* 傳回的值：有關已清除之作用中工作流程執行處理的表格資料，包括下列欄：

   * 发起者
   * InstanceId
   * ModelId
   * 有效负荷
   * StartComment
   * 工作流程標題

**countStaleWorkflows** 傳回過時的工作流程例項數目。 您可以擷取所有工作流程模型或特定模型的過時例項數。

* 参数:

   * 模型： （選用）要套用作業的模型識別碼。 指定沒有模型可將操作套用至所有工作流程模型的工作流程例項。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回的值：過時的工作流程例項數目。

**restartStaleWorkflows** 重新啟動過時的工作流程例項。 您可以重新啟動所有過時的例項，或僅重新啟動特定模型的過時的例項。 您也可以測試作業以檢視結果，而無需實際執行作業。

* 参数:

   * 模型： （選用）要套用作業的模型識別碼。 指定沒有模型可將操作套用至所有工作流程模型的過時執行個體。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 試執行： （選擇性）指定值 `true` 以檢視作業結果，而不實際執行作業。 預設值 `false` 導致執行作業。

* 傳回的值：重新啟動的工作流程執行個體清單。

**fetchModelList** 列出所有工作流程模型。

* 引數：無
* 傳回值：可識別工作流程模型（包括ModelId和ModelName欄）的表格式資料。

**countRunningWorkflows** 傳回正在執行的工作流程例項數目。 您可以擷取所有工作流程模型或特定模型的執行中例證數目。

* 参数:

   * 模型： （選用）傳回執行中例項數目的模型ID。 指定無模型可傳回所有工作流程模型的執行中例項數。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回的值：執行中的工作流程例項數目。

**countCompletedWorkflows** 傳回已完成的工作流程例項數目。 您可以擷取所有工作流程模型或特定模型的已完成例項數。

* 参数:

   * 模型： （選用）傳回已完成例項數目的模型ID。 指定無模型可傳回所有工作流程模型的已完成例項數。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 傳回的值：已完成的工作流程例項數目。

**purgeCompleted** 從存放庫移除特定年齡的已完成工作流程記錄。 當您大量使用工作流程時，請定期使用此作業，以將存放庫的大小最小化。 您可以清除所有模型的已完成例證，或僅清除特定模型的例證。 您可以選擇性地測試作業以檢視結果，而無需實際執行作業。

* 参数:

   * 模型： （選用）要套用作業的模型識別碼。 指定沒有模型可將操作套用至所有工作流程模型的工作流程例項。 ID是模型節點的路徑，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 自工作流程完成以來的天數：工作流程例項處於完成狀態的天數。
   * 試執行： （選擇性）指定值 `true` 以檢視作業結果，而不實際執行作業。 預設值 `false` 導致執行作業。

* 傳回值：已清除之已完成工作流程執行處理的表格資料，包括下列各欄：

   * 发起者
   * InstanceId
   * ModelId
   * 有效负荷
   * StartComment
   * 工作流程標題

## 存储库 {#repository}

CRX存放庫的相關資訊

* 網域： com.adobe.granite
* 型別：存放庫

### 属性 {#attributes}

**名稱** JCR存放庫實作的名稱。 只读.

**版本** 存放庫實作版本。 只读.

**HomeDir** 存放庫所在的目錄。 預設位置為 &lt;quickstart_jar_location>/crx-quickstart/repository。 只读.

**客戶名稱** 軟體授權所核發之客戶的名稱。 只读.

**授權金鑰** 此存放庫安裝的唯一授權金鑰。 只读.

**AvailablediskSpace** 存放庫執行個體可用的磁碟空間（以MB為單位）。 只读.

**MaximumNumberOfOpenFiles** 可一次開啟的檔案數。 只读.

**SessionTracker** crx.debug.sessions系統變數的值。 true表示偵錯工作階段。 false表示正常工作階段。 讀取/寫入。

**描述項** 代表存放庫屬性的索引鍵值配對集。 所有屬性均為唯讀。

<table>
 <tbody>
  <tr>
   <th>键</th>
   <th>价值</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>指示節點和節點的屬性是否可以擁有相同的名稱。 true表示支援相同名稱，false表示不支援。 </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>指示不可參照節點識別碼的穩定性。 可能的值如下：
    <ul>
     <li>identifier.stability.indefinition.duration：識別碼不會變更。</li>
     <li>identifier.stability.method.duration：識別碼可以在方法呼叫之間變更。</li>
     <li>identifier.stability.save.duration：識別碼不會在儲存/重新整理週期內變更。</li>
     <li>identifier.stability.session.duration：識別碼在工作階段期間不會變更。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>指出是否支援JCR 1.0 XPath查詢語言。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>在system.id檔案中找到的系統識別碼。</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>指出是否支援JCR 1.0 XPath查詢語言。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>存放庫實作的版本。</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>指示節點的主要節點型別是否可以變更。 true表示您可以變更主要節點型別，false表示不支援此變更。</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>指出是否支援節點型別管理。 true表示支援，false表示不支援。</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>指示您是否可以覆寫節點型別的繼承屬性或子節點定義。 true表示支援覆寫，false表示無覆寫。</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true表示支援非同步觀察存放庫變更。 支援非同步觀察可讓應用程式在每次變更發生時接收和回應有關變更的通知。</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true表示jcr：score虛擬屬性可在XPath和SQL查詢中使用，該查詢包含jcrfn：contains （在XPath中）或CONTAINS （在SQL中）函式以執行全文檢索搜尋。</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true表示存放庫支援簡單的版本設定。 透過簡單的版本設定，存放庫可維護節點的連續一系列版本。</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true表示存放庫支援使用API建立和刪除工作區。</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true表示存放庫支援新增和移除現有節點的mixin節點型別。</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true表示儲存庫可讓節點定義包含作為子項的主要專案。 在不知道專案名稱的情況下，可使用API存取主要專案。</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true表示LEVEL_1_SUPPORTED和OPTION_XML_IMPORT_SUPPORTED皆為true。</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true表示存放庫會使用API提供寫入許可權。 false表示唯讀存取。</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true表示您可以變更現有節點正在使用的節點定義。</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>存放庫實施的JCR規格版本。</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true表示應用程式可對存放庫執行日誌觀察。 透過日誌觀察，可取得特定期間的一組變更通知。 </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>存放庫支援的查詢語言。 無值表示不支援查詢。</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true表示存放庫支援將節點匯出為XML程式碼。</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true表示存放庫支援註冊具有多個二進位屬性的節點型別。 false表示節點型別支援單一二進位屬性。</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true表示存放庫支援存取控制，用於設定和決定節點存取的使用者許可權。</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true表示存放庫同時支援設定和基準線。</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true表示存放庫支援建立可共用的節點。</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>存放庫叢集的識別碼。</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true表示存放庫支援儲存的查詢。</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true表示存放庫支援全文檢索。</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>表示節點型別繼承的存放庫支援層級。 可能的值如下：</p> <p>node.type.management.inheritance.minimal：主要節點型別的註冊僅限於只有nt：base作為超型別的型別。 mixin節點型別的註冊僅限於沒有超級型別的節點。</p> <p>node.type.management.inheritance.single：主要節點型別的註冊僅限於具有一個超級型別的節點。 mixin節點型別的註冊僅限於最多有一個超級型別的節點。</p> <p><br /> node.type.management.inheritance.multiple：主要節點型別可使用一或多個超級型別登入。 Mixin節點型別可使用零個或多個超型別登入。</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true表示此叢集節點是叢集的偏好主節點。</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true表示存放庫支援交易。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>存放庫廠商的URL。</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true表示存放庫支援節點屬性的值限制。</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>javax.jcr.PropertyType常數陣列，代表註冊節點型別可指定的屬性型別。 零長度陣列表示註冊的節點型別無法指定屬性定義。 屬性型別包括STRING、URI、BOOLEAN、LONG、DOUBLE、DECIMAL、BINARY、DATE、NAME、PATH、WEAKREFERENCE、REFERENCE和UNDEFINED （如果支援）</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true表示存放庫支援保留子節點的順序。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>存放庫廠商的名稱。</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>查詢中聯結的支援等級。 可能的值如下：</p>
    <ul>
     <li>query.joins.none：不支援聯結。 查詢可以使用一個選擇器。</li>
     <li>query.joins.inner：支援內部聯結。</li>
     <li>query.joins.inner.outer：支援內部和外部聯結。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true表示存放庫支援XPath 1.0查詢語言。</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true表示存放庫支援將XML程式碼匯入為內容。</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true表示存放庫支援同名的同層級節點（具有相同父系的節點）。</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true表示存放庫支援具有剩餘定義的名稱屬性。 若有支援，專案定義的名稱屬性可以是星號(「*」)。</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true表示在建立節點時，存放庫支援自動建立節點的子專案（節點或屬性）。</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true表示此存放庫節點是叢集的主節點。</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true表示option.xml.export.support為true，而query.languages的長度不為零。</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true表示存放庫支援未歸檔的內容。 未歸檔的節點不是存放庫階層的一部分。</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>存放庫實作的JCR規格名稱。</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true表示存放庫支援完整版本設定。</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>存放庫的名稱。</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true表示存放庫支援節點鎖定。 鎖定可讓使用者暫時防止其他使用者進行變更。</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true表示存放庫支援活動。 活動是在工作區中執行的一組變更，這些變更會合併到另一個工作區中。</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true表示存放庫支援零或更多值的節點屬性。</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true表示存放庫支援使用外部保留管理應用程式來套用保留原則至內容，並支援保留和釋放。</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true表示存放庫支援生命週期管理。</td>
  </tr>
 </tbody>
</table>

**工作區名稱** 存放庫中的工作區名稱。 只读.

**DataStoreGarbageCollectionDelay** 掃描每10個節點後垃圾收集休眠的時間長度（以毫秒為單位）。 讀取/寫入。

**BackupDelay** 備份程式在備份的每個步驟之間休眠的時間（以毫秒為單位）。 讀取/寫入。

**BackupInProgress** 值為true表示備份程式正在執行。 只读.

**BackupProgress** 對於目前的備份，所有已備份檔案的百分比。 只读.

**目前備份目標** 對於目前的備份，為儲存備份檔案的ZIP檔案。 備份未進行時，不會顯示任何值。 只读.

**BackupWasSuccessful** 值為true表示目前備份期間沒有發生錯誤，或沒有進行中的備份。 false表示目前備份期間發生錯誤。 只读.

**BackupResult** 目前備份的狀態。 可能的值如下：

* 備份進行中：備份目前正在執行中。
* 已取消備份：已取消備份。
* 備份完成，但發生錯誤：備份期間發生錯誤。 錯誤訊息會提供有關原因的資訊。
* 備份完成：備份成功。
* 目前尚未執行任何備份：沒有進行中的備份。

只读.

**TarOptimizationRunningSince** 目前TAR檔案最佳化程式開始的時間。 只读.

**TarOptimizationDelay** TAR最佳化程式在程式每個步驟之間休眠的時間量（毫秒）。 讀取/寫入。

**叢集屬性** 代表叢集屬性和值的一組機碼值組。 表格中的每一列代表叢集屬性。 只读.

**叢集節點** 存放庫叢集的成員。

**ClusterId** 此存放庫叢集的識別碼。 只读.

**ClusterMasterId** 此存放庫叢集之主要節點的識別碼。 只读.

**ClusterNodeId** 存放庫叢集的這個節點的識別碼。 只读.

### 运营 {#operations-1}

**createWorkspace** 在此存放庫中建立工作區。

* 参数:

   * name：代表新工作區名稱的字串值。

* 傳回值：無

**runDataStoreGarbageCollection** 在存放庫節點上執行垃圾收集。

* 参数:

   * delete：指示是否刪除未使用的存放庫專案的布林值。 值為true會刪除未使用的節點和屬性。 若值為false，則會掃描所有節點，但不會刪除任何節點。

* 傳回值：無

**stopDataStoreGarbageCollection** 停止執行中的資料存放區垃圾收集。

* 引數：無
* 傳回值：目前狀態的字串表示

**startBackup** 以ZIP檔案備份存放庫資料。

* 参数:

   * `target`：（選用） A `String` 值，代表要封存存放庫資料的ZIP檔案或目錄的名稱。 若要使用ZIP檔案，請包含ZIP副檔名。 若要使用目錄，請勿包含副檔名。

      若要執行增量備份，請指定先前用於備份的目錄。

      您可以指定絕對或相對路徑。 相對路徑是相對於crx-quickstart目錄的父路徑。

      若您未指定任何值，預設值為 `backup-currentdate.zip` 使用，其中 `currentdate` 為格式 `yyyyMMdd-HHmm`.

* 傳回值：無

**cancelerbackup** 停止目前的備份程式，並刪除程式為封存資料所建立的暫時封存。

* 引數：無
* 傳回值：無

**Blockrepositorwrites** 封鎖對存放庫資料的變更。 所有存放庫備份接聽程式都會收到區塊的通知。

* 引數：無
* 傳回值：無

**unblockRepositoryWrite** 從存放庫移除區塊。 所有存放庫備份接聽程式都會收到區塊移除的通知。

* 引數：無
* 傳回值：無

**startTarOptimization** 使用tarOptimizationDelay的預設值啟動TAR檔案最佳化程式。

* 引數：無
* 傳回值：無

**stopTarOptimization** 停止TAR檔案最佳化。

* 引數：無
* 傳回值：無

**tarIndexMerge** 合併所有TAR集的頂層索引檔案。 排名在前的索引檔案是主要版本不同的檔案。 例如，下列檔案會合併至index_3_1.tar檔案： index_1_1.tar、index_2_0.tar、index_3_0.tar。 已合併的檔案會被刪除（在前一個範例中，會刪除index_1_1.tar、index_2_0.tar和index_3_0.tar）。

* 参数:

   * `background`：布林值，指出是否要在背景執行操作，以便在執行期間可以使用Web主控台。 值為true會在背景中執行操作。

* 傳回值：無

**Beendeclustmaster** 將此存放庫節點設定為叢集的主節點。 如果不是master，這個命令會停止目前主要執行處理的監聽器，並在目前節點上啟動主要監聽器。 然後，此節點會設定為主節點並重新啟動，導致叢集中的所有其他節點（即由主節點控制的節點）連線至此執行個體。

* 引數：無
* 傳回值：無

**joinCluster** 將此存放庫新增至叢集，作為由叢集主節點控制的節點。 您必須提供使用者名稱和密碼以進行驗證。 連線使用基本驗證。 安全性認證在傳送至伺服器之前會進行base-64編碼。

* 参数:

   * `master`：字串值，代表執行主要存放庫節點之電腦的IP位址或電腦名稱。
   * `username`：用於向叢集驗證的名稱。
   * `password`：用於驗證的密碼。

* 傳回值：無

**traversalCheck** 從特定節點開始遍歷並選擇性修正子樹狀結構中的不一致。 有關持續性管理員的檔案將對此進行完整詳細說明。

**consistencyCheck** 檢查並選擇性修正資料存放區中的一致性。 Datastore的檔案將對此進行完整詳細說明。

## 存放庫統計資料（時間序列） {#repository-statistics-timeseries}

每個統計資料型別的「時間序列」欄位值，該統計資料型別會 `org.apache.jackrabbit.api.stats.RepositoryStatistics` 定義。

* 域: `com.adobe.granite`
* 类型: `TimeSeries`
* 名稱：下列其中一個值，來自 `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` 列舉類別：

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * QUERY_COUNT
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### 属性 {#attributes-1}

系統會針對每個報表的統計資料型別，提供下列屬性：

* ValuePerSecond：最後一分鐘每秒的測量值。 只读.
* ValuePerMinute：過去一小時內每分鐘測量到的值。 只读.
* ValuePerHour：上週每小時的測量值。 只读.
* ValuePerWeek：過去三年每週的測量值。 只读.

## 存放庫查詢統計資料 {#repository-query-stats}

關於存放庫查詢的統計資訊。

* 網域： com.adobe.granite
* 型別： QueryStat

### 属性 {#attributes-2}

**緩慢查詢** 完成時間最長的存放庫查詢相關資訊。 只读.

**SlowQueriesQueueSize** 要包含在SlowQueries清單中的查詢數量上限。 讀寫。

**PopularQueries** 發生次數最多的存放庫查詢相關資訊。 只读.

**PopularQueriesQueueSize** PopularQueries清單中的查詢數上限。 讀寫。

### 运营 {#operations-2}

**clearSlowQueriesQueue** 從SlowQueries清單移除所有查詢。

* 引數：無
* 傳回值：無

**clearPopularQueriesQueue** 從PopularQueries清單移除所有查詢。

* 引數：無
* 傳回值：無

## 复制代理 {#replication-agents}

監視每個復寫代理程式的服務。 當您建立復寫代理程式時，服務會自動出現在JMX主控台中。

* **網域：** com.adobe.granite.replication
* **型別：** 代理程式
* **名稱：** 無值
* **屬性：** {id=&quot;*名稱*「}，其中 *名稱* 是代理程式名稱屬性的值。

### 属性 {#attributes-3}

**Id** 代表復寫代理程式組態識別碼的字串值。 多個代理程式可使用相同的設定。 只读.

**有效** 表示代理程式是否正確設定的布林值：

* `true`：有效的設定。
* `false` ：設定包含錯誤。

只读.

**已啟用** 表示代理程式是否已啟用的布林值：

* `true`: 启用.
* `false`: 已禁用.

**佇列已封鎖** 表示佇列是否存在且已封鎖的布林值：

* `true`: 已阻止. 正在等候自動重試。
* `false`：未封鎖或不存在。

只读.

**QueuePaused** 指示工作佇列是否暫停的布林值：

* `true`：已暫停（已暫停）
* `false`：未暫停或不存在。

讀寫。

**QueueNumEntries** int值，代表代理程式佇列中的工作數目。 只读.

**QueueStatusTime** 日期值，指出取得顯示的狀態值時伺服器上的時間。 該值對應至頁面載入的時間。 只读.

**QueueNextRetryTime** 對於已封鎖的佇列，指出下次自動重試發生的日期值。 若未顯示時間，則不會封鎖佇列。 只读.

**QueueProcessingSince** 指出目前工作開始處理的日期值。 若沒有出現時間，佇列會遭到封鎖或閒置。 只读.

**QueueLastProcessTime** 指出前一個作業完成時間的日期值。 只读.

### 运营 {#operations-3}

**queueForceRetry** 針對封鎖的佇列，向佇列發出重試命令。

* 引數：無
* 傳回值：無

**queueClear** 從佇列中移除所有工作。

* 引數：無
* 傳回值：無

## Sling Engine {#sling-engine}

提供有關HTTP要求的統計資料，以便您可以監視SlingRequestProcessor服務的效能。

* 網域： org.apache.sling
* 型別：引擎
* 屬性：{service=RequestProcessor}

### 属性 {#attributes-4}

**請求計數** 自上次重設統計資料後發生的要求數目。

**MinRequestDurationMsec** 自上次重設統計資料以來，處理要求所需的最短時間（以毫秒為單位）。

**MaxRequestDurationMsec** 自上次重設統計資料以來，處理要求所需的最長時間（以毫秒為單位）。

**StandardDeviationDurationMsec** 處理請求所需時間的標準差。 會使用自上次重設統計資料以來的所有請求來計算標準差。

**MeanRequestDurationMsec** 處理請求所需的平均時間。 平均數使用自上次重設統計資料以來的所有要求來計算

### 运营 {#operations-4}

**resetStatistics** 將所有統計值設為零。 當您需要分析特定時間範圍內的請求處理效能時，請重設統計資料。

* 引數：無
* 傳回值：無

**id** 套件ID的字串表示法。

**已安裝** 表示是否已安裝套件的布林值：

* `true`: 已安装.
* `false`: 未安装.

**installedBy** 上次安裝套件之使用者的ID。

**installedDate** 上次安裝套件的日期。

**大小** 儲存封裝大小（位元組）的長數值。


## 快速入門啟動器 {#quickstart-launcher}

有關啟動程式和Quickstart啟動器的資訊。

* 網域： com.adobe.granite.quickstart
* 型別：啟動器

### 运营 {#operations-5}

**記錄**

在QuickStart視窗中顯示訊息。

参数:

* p1：A `String` 代表要顯示之訊息的值。
* 傳回值：無

**startupFinished**

呼叫伺服器啟動器的startupFinished方法。 方法會嘗試在網頁瀏覽器中開啟歡迎頁面。

* 引數：無
* 傳回值：無

**startupProgress**

設定伺服器啟動程式的完成值。 QuickStart視窗上的進度列代表完成值。

* 参数:
   * p1：浮點值，以小數表示，代表啟動程式完成的程度。 該值應介於0和1之間。 例如，0.3表示30%完成。
* 傳回值：無。

## 協力廠商服務 {#third-party-services}

數個協力廠商伺服器資源會安裝MBean，將屬性和作業公開給JMX主控台。 下表列出協力廠商資源，並提供更多資訊的連結。

<table>
 <tbody>
  <tr>
   <th>域</th>
   <th>类型</th>
   <th>MBean類別</th>
  </tr>
  <tr>
   <td>JMI實作</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotSpotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>類別載入</li>
     <li>編譯</li>
     <li>垃圾收集器</li>
     <li>内存</li>
     <li>記憶體管理員</li>
     <li>MemoryPool</li>
     <li>作業系統</li>
     <li>執行階段</li>
     <li>執行緒</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a> 封裝</td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>框架</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> 封裝</td>
  </tr>
 </tbody>
</table>

## 使用JMX控制檯 {#using-the-jmx-console}

JMX主控台會顯示伺服器上執行之數個服務的相關資訊：

* 屬性：服務屬性，例如設定或執行階段資料。 屬性可以是唯讀或讀寫。
* 作業：您可以在服務上叫用的命令。

與OSGi服務一起部署的MBean會將服務屬性和操作公開給主控台。 MBean會決定公開的屬性和作業，以及屬性是唯讀還是讀寫。

JMX主控台的首頁包含服務表格。 表格中的每一列代表由MBean公開的服務。

1. 開啟Web主控台，然後按一下JMX標籤。 ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. 按一下服務的儲存格值，即可檢視服務的屬性和作業。
3. 若要變更屬性值，請按一下該值，在出現的對話方塊中指定值，然後按一下「儲存」。
4. 若要叫用服務作業，請按一下作業名稱，在出現的對話方塊中指定引數值，然後按一下叫用。

## 使用外部JMX應用程式進行監視 {#using-external-jmx-applications-for-monitoring}

CRX可讓外部應用程式透過以下方式與受管理的Bean (MBean)互動： [Java管理擴充功能(JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). 使用一般主控台，例如 [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) 或網域特定的監控應用程式，可取得和設定CRX設定和屬性，以及監控效能和資源使用情況。

### 使用JConsole連線至CRX {#using-jconsole-to-connect-to-crx}

若要使用JConsole連線至CRX，請遵循下列步驟：

1. 開啟終端機視窗。
1. 輸入下列命令：

   `jconsole`

JConsole將會啟動，JConsole視窗將會出現。

### 連線到本機CRX程式 {#connecting-to-a-local-crx-process}

JConsole將顯示本機Java虛擬機器器處理程式的清單。 清單將包含兩個快速入門流程。 從本機處理序清單中選取快速入門「CHILD」處理序（通常是PID較高的處理序）。

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### 連線到遠端CRX程式 {#connecting-to-a-remote-crx-process}

若要連線到遠端CRX處理序，裝載遠端CRX處理序的JVM必須啟用才能接受遠端JMX連線。

若要啟用遠端JMX連線，啟動JVM時必須設定下列系統屬性：

`com.sun.management.jmxremote.port=portNum`

在上述屬性中， `portNum` 是要啟用JMX RMI連線的連線埠號碼。 請務必指定未使用的連線埠號碼。 除了發佈RMI聯結器以供本機存取外，設定此屬性也會使用已知名稱「jmxrmi」在指定連線埠的私人唯讀登入中發佈其他RMI聯結器。

依預設，當您啟用JMX代理程式進行遠端監視時，它會根據密碼檔案使用密碼驗證，而啟動Java VM時需要使用以下系統屬性來指定密碼檔案：

`com.sun.management.jmxremote.password.file=pwFilePath`

請參閱 [相關JMX檔案](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) 以取得設定密碼檔的詳細指示。

示例:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### 使用CRX提供的MBean {#using-the-mbeans-provided-by-crx}

連線至快速入門程式後，JConsole會針對CRX執行所在的JVM提供一系列一般監控工具。

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

若要存取CRX的內部監視和設定選項，請移至MBeans標籤，然後從左側的階層式內容樹狀結構選取您感興趣的「屬性」或「作業」區段。 例如com.adobe.granite/Repository/Operations區段。

在該區段中，在左窗格中選取所需的屬性或作業。

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
