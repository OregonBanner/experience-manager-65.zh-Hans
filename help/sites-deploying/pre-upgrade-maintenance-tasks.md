---
title: 升級前維護任務
seo-title: Pre-Upgrade Maintenance Tasks
description: 瞭解AEM中的升級前工作。
seo-description: Learn about the pre-upgrade tasks in AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 1%

---

# 升級前維護任務{#pre-upgrade-maintenance-tasks}

在開始升級之前，請務必遵循這些維護任務，以確保系統準備就緒，並可在發生問題時回覆：

* [確保有足夠的磁碟空間](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完全備份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [將變更備份至/etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [產生quickstart.properties檔案](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [設定工作流程和稽核記錄清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安裝、設定及執行升級前工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [停用自訂登入模組](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [從/install目錄移除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷待命執行個體](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [停用自訂排程工作](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [執行離線修訂清理](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [執行資料存放區垃圾收集](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [視需要升級資料庫結構描述](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [刪除可能阻礙升級的使用者](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [輪換記錄檔](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 確保有足夠的磁碟空間 {#ensure-sufficient-disk-space}

執行升級時，除了內容和程式碼升級活動之外，還必須執行存放庫移轉。 移轉會以新的Segment Tar格式建立存放庫的復本。 因此，您需要足夠的磁碟空間，以保留儲存庫的第二個（可能更大）版本。

## 完全備份AEM {#fully-back-up-aem}

在開始升級之前，應該先完整備份AEM。 請務必備份存放庫、應用程式安裝、資料存放區和Mongo執行個體（如適用）。 如需有關備份和還原AEM執行個體的詳細資訊，請參閱 [備份與還原](/help/sites-administering/backup-and-restore.md).

## 將變更備份至/etc {#backup-changes-etc}

升級程式能很好地維護和合併下的現有內容和設定。 `/apps` 和 `/libs` 存放庫中的路徑。 若對下列專案進行變更： `/etc` 路徑（包括Context Hub設定）通常需要在升級後重新套用這些變更。 升級時會對任何無法合併的變更建立備份復本 `/var`，Adobe建議您在開始升級前手動備份這些變更。

## 產生quickstart.properties檔案 {#generate-quickstart-properties}

從jar檔案啟動AEM時， `quickstart.properties` 檔案產生於 `crx-quickstart/conf`. 如果AEM過去僅以啟動指令碼啟動，則此檔案不存在，且升級失敗。 請確定檢查此檔案是否存在，如果不存在，請從jar檔案重新啟動AEM。

## 設定工作流程和稽核記錄清除 {#configure-wf-audit-purging}

此 `WorkflowPurgeTask` 和 `com.day.cq.audit.impl.AuditLogMaintenanceTask` 任務需要單獨的OSGi設定，沒有它們就無法運作。 如果它們在升級前任務執行期間失敗，遺失設定是最可能的原因。 因此，請務必為這些任務新增OSGi設定，或如果您不想執行，請從升級前最佳化任務清單中將其完全移除。 有關設定工作流程清除任務的檔案，請參閱 [管理工作流程例項](/help/sites-administering/workflows-administering.md) 和稽核記錄維護任務設定可在下列網址找到： [AEM 6中的稽核記錄維護](/help/sites-administering/operations-audit-log.md).

如需在CQ 5.6上清除工作流程和稽核記錄，以及在AEM 6.0上清除稽核記錄，請參閱 [清除工作流程與稽核節點](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## 安裝、設定及執行升級前工作 {#install-configure-run-pre-upgrade-tasks}

由於AEM允許的自訂等級，環境通常不遵循統一的執行升級方式。 因此，建立標準化的升級程式會相當困難。

在舊版中，已停止或無法安全恢復的AEM升級也很困難。 此問題會導致需要重新啟動完整升級程式，或執行有缺陷的升級而未觸發任何警告的情況。

為了解決這些問題，Adobe在升級程式中新增了數項增強功能，使其更具彈性且更方便使用。 之前必須手動執行的升級前維護任務正在最佳化並自動化。 此外，也新增了升級後報告，以便可以完全審查該過程，希望更容易發現任何問題。

升級前維護任務目前分散在手動執行部分或全部的各種介面中。 AEM 6.3中引入的升級前維護最佳化可讓您以統一方式觸發這些任務，並可依需求檢查其結果。

升級前最佳化步驟中包含的所有工作與AEM 6.0以後的所有版本相容。

### 如何設定 {#how-to-set-it-up}

在AEM 6.3和更新版本中，快速入門jar中包含升級前維護最佳化任務。

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### 使用方式 {#how-to-use-it}

此 `PreUpgradeTasksMBean` OSGI元件預先設定了可一次執行所有升級前維護工作的清單。 您可以依照下列程式來設定這些工作：

1. 瀏覽至Web主控台 *https://serveraddress:serverport/system/console/configMgr*

1. 搜尋&quot;**preupgradetasks**「」，然後按一下第一個相符的元件。 元件的完整名稱是 `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改必須執行的維護工作清單，如下所示：

   ![1487758925984](assets/1487758925984.png)

工作清單會依用來啟動執行個體的執行模式而有所不同。 以下說明每個維護任務所針對的執行模式。

<table>
 <tbody>
  <tr>
   <td><strong>任务</strong></td>
   <td><strong>运行模式</strong></td>
   <td><strong>注释</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>執行標籤和掃描。 針對共用資料存放區，請移除此步驟並執行<br /> 在執行之前手動或正確準備執行個體。</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>在執行之前，必須設定AdobeGranite工作流程清除設定OSGi。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>若為AEM 6.0至6.2上的TarMK執行個體，請改為手動執行離線修訂清除。</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>必須先設定[稽核記錄清除排程器]OSGi設定，才能執行。</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>此 `DataStoreGarbageCollectionTask` 使用標籤和掃描階段時，會呼叫資料存放區垃圾收集作業（如已使用）。 對於使用共用資料存放區的部署，請務必正確重新設定或準備執行個體，以避免刪除其他執行個體參考的專案。 此程式可能需要在觸發此升級前工作之前，在所有執行個體上手動執行標籤階段。

### 升級前健康狀態檢查的預設設定 {#default-configuration-of-the-pre-upgrade-health-checks}

此 `PreUpgradeTasksMBeanImpl` OSGI元件預先設定了升級前健康情況檢查標籤的清單，以便 `runAllPreUpgradeHealthChecks` 方法稱為：

* **系統** - granite維護狀況檢查所使用的標籤

* **升級前**  — 可新增至所有健康情況檢查的自訂標籤，這些檢查可設定為在升級前執行

清單可編輯。 您可以使用加號 **(+)** 和減號 **(-)** 標籤以外的按鈕，以新增更多自訂標籤或移除預設標籤。

**MBean方法**

Managed Bean功能可使用以下專案來存取： [JMX主控台](/help/sites-administering/jmx-console.md).

存取MBean的方法有：

1. 前往位於的JMX主控台 *https://serveraddress:serverport/system/console/jmx*
1. 搜尋 **PreUpgradeTasks** 並按一下結果

1. 從中選擇任何方法 **作業** 區段並選取 **叫用** 於下列視窗中。

以下列出了 `PreUpgradeTasksMBeanImpl` 公開：

<table>
 <tbody>
  <tr>
   <td><strong>方法名稱</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>信息</td>
   <td>顯示可用的升級前維護工作名稱清單。</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>信息</td>
   <td>顯示升級前健康情況檢查標籤名稱的清單。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>动作</td>
   <td>執行清單中的所有升級前維護任務。</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>執行升級前維護任務，並將名稱指定為引數。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>檢查 <code>runAllPreUpgradeTasksmaintenance</code> 工作正在執行。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>檢查是否有任何升級前維護任務在執行中，以及<br /> 傳回包含目前執行中工作名稱的陣列。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>顯示升級前維護工作的確切執行時間，並將名稱指定為引數。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>顯示升級前維護任務的最後一次執行狀態，其名稱會指定為引數。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>动作</td>
   <td><p>執行所有升級前的健康情況檢查，並將其狀態儲存在名為的檔案中 <code>preUpgradeHCStatus.properties</code> 在sling首頁路徑中。 如果 <code>shutDownOnSuccess</code> 引數已設為 <code>true</code>，會關閉AEM執行個體，但前提是所有升級前健康情況檢查的狀態均為「正常」。</p> <p>屬性檔案會作為任何未來升級的先決條件<br /> 而且升級前健康情況檢查會停止升級程式<br /> 執行失敗。 如果您要忽略升級前的結果<br /> 健康情況檢查並啟動升級，您可以刪除檔案。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>动作</td>
   <td>列出所有匯入的套件，這些套件在<br /> 升級至指定的AEM版本。 目標AEM版本必須是<br /> 以引數形式提供。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可以透過以下方式叫用MBean方法：
>
>* JMX主控台
>* 連線到JMX的任何外部應用程式
>* cURL
>


## 停用自訂登入模組 {#disable-custom-login-modules}

>[!NOTE]
>
>唯有當您從AEM 5版本升級時，才需要執行此步驟。 從舊版AEM 6升級時，可完全略過該步驟。

自訂方式 `LoginModules` 針對存放庫層級的驗證而設定的Apache Oak已發生根本性變更。

在使用CRX2設定的AEM版本中，將放在 `repository.xml` 從AEM 6開始，檔案會透過Web主控台在Apache Felix JAAS Configuration Factory服務中完成。

因此，在升級後，必須停用任何現有的設定，並重新建立Apache Oak。

若要停用的JAAS設定中定義的自訂模組 `repository.xml`，您必須編輯設定才能使用預設值 `LoginModule`，如下列範例所示：

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>如需詳細資訊，請參閱 [使用外部登入模組進行驗證](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>例如 `LoginModule` 在AEM 6中的設定，請參閱 [使用AEM 6設定LDAP](/help/sites-administering/ldap-config.md).

## 從/install目錄移除更新 {#remove-updates-install-directory}

>[!NOTE]
>
>在關閉AEM執行個體之後，僅從crx-quickstart/install目錄移除套件。 此步驟是開始就地升級程式之前的最後一個步驟。

移除透過部署的任何Service Pack、Feature Pack或Hotfix。 `crx-quickstart/install` 目錄。 這麼做可防止在更新完成後，在新AEM版本之上意外安裝舊版Hotfix和Service Pack。

## 停止任何冷待命執行個體 {#stop-tarmk-coldstandby-instance}

如果使用TarMK冷待命，請停止任何冷待命執行個體。 這麼做可保證在升級過程中發生問題時能以有效率的方式重新上線。 成功完成升級後，必須從升級的主要執行個體重建冷待命執行個體。

## 停用自訂排程工作 {#disable-custom-scheduled-jobs}

停用應用程式程式碼中包含的任何OSGi排程工作。

## 執行離線修訂清理 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>只有TarMK安裝才需要此步驟

如果使用TarMK，您應該在升級前執行離線修訂清理。 如此一來，存放庫移轉步驟和後續升級任務的執行速度就會大幅加快，有助於確保線上修訂清除在升級完成後能夠成功執行。 如需有關執行離線修訂清除的資訊，請參閱 [正在執行離線修訂清理](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## 執行資料存放區垃圾收集 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>只有執行crx3的執行個體才需要此步驟

在CRX3執行個體上執行修訂清除後，您應該執行資料存放區垃圾收藏集，以移除資料存放區中任何未參考的blob。 如需指示，請參閱以下說明檔案： [資料存放區垃圾收集](/help/sites-administering/data-store-garbage-collection.md).

## 視需要升級資料庫結構描述 {#upgrade-the-database-schema-if-needed}

通常，AEM用於持續性的基礎Apache Oak棧疊會視需要負責升級資料庫架構。

但是，當結構描述無法自動升級時可能會發生這種情況。 這類情況大多是安全性高的環境，資料庫是在許可權有限的使用者下執行。 如果發生這種情況，AEM會繼續使用舊的結構描述。

若要避免發生這類情況，請執行以下動作來升級結構：

1. 關閉必須升級的AEM執行個體。
1. 升級資料庫結構。 請參閱資料庫型別的檔案，瞭解需要什麼工具才能取得結果。

   如需Oak如何處理架構升級的詳細資訊，請參閱 [Apache網站上的此頁面](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. 繼續升級AEM。

## 刪除可能阻礙升級的使用者 {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>只有在下列情況下，才需要此升級前維護任務：
>
>* 您正從AEM 6.3之前的AEM版本升級
>* 在升級期間，您會遇到下列任何錯誤。
>


在例外情況下，服務使用者在舊版AEM中可能會錯誤地標籤為一般使用者。

如果發生這種情況，升級會失敗，並出現以下訊息：

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

若要解決此問題，請務必執行下列動作：

1. 從生產流量分離執行個體
1. 建立一個或多個造成問題的使用者的備份。 您可以透過「封裝管理員」來執行此工作。 如需詳細資訊，請參閱 [如何使用套件。](/help/sites-administering/package-manager.md)
1. 刪除一或多個造成問題的使用者。 以下是可能屬於此類別的使用者清單：

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## 輪換記錄檔 {#rotate-log-files}

Adobe建議您在開始升級之前，先封存目前的記錄檔。 如此一來，升級期間和升級後，您就可以更輕鬆地監視和掃描記錄檔，以識別並解決可能發生的任何問題。
