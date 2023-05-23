---
title: 配置 Live Copy 同步
seo-title: Configuring Live Copy Synchronization
description: 瞭解如何設定即時副本同步。
seo-description: Learn about configuring Live Copy Synchronization.
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
feature: Multi Site Manager
exl-id: ac24b8b4-b3ed-47fa-9a73-03f0c9e68ac8
source-git-commit: 96aa75dec7433aa3961944fa57a80c4719316ba5
workflow-type: tm+mt
source-wordcount: '2696'
ht-degree: 25%

---

# 配置 Live Copy 同步{#configuring-live-copy-synchronization}

執行下列工作，控制即時副本與其來源內容同步化的方式與時間。

* 決定現有轉出設定是否符合您的需求，或您是否需要建立一個或多個轉出設定。
* 指定用於即時副本的轉出設定。

## 已安裝及自訂轉出設定 {#installed-and-custom-rollout-configurations}

本節提供有關已安裝轉出設定及其使用的同步化動作，以及如何視需要建立自訂設定的資訊。

>[!CAUTION]
>
>更新或變更立即可用（已安裝）轉出設定為 **not** 建議使用。 如果需要自定义实时操作，则应将其添加到自定义转出配置中。

### 轉出觸發器 {#rollout-triggers}

每個轉出設定都會使用轉出觸發器，導致轉出發生。 轉出設定可以使用下列其中一個觸發程式：

* **轉出時**：此 **轉出** 命令用於blue print頁面，或 **同步** 命令用於「即時副本」頁面。

* **修改**：修改源页面。

* **激活**：激活源页面。

* **停用**：停用源页面。

>[!NOTE]
>
>使用修改触发器可能会影响性能。请参阅 [MSM 最佳实践](/help/sites-administering/msm-best-practices.md#onmodify)以了解更多信息。

### 已安裝的轉出設定 {#installed-rollout-configurations}

下表列出與AEM一起安裝的轉出設定。 该表包含每个转出配置的触发器和同步操作。如果安裝的轉出設定動作不符合您的需求，您可以 [建立新的轉出設定](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>名称</th>
   <th>描述</th>
   <th>触发器</th>
   <th>同步化動作<br /> <br /> 另請參閱 <a href="#installed-synchronization-actions">已安裝的同步化動作</a></th>
  </tr>
  <tr>
   <td>标准转出配置</td>
   <td>标准转出配置，允许在触发转出时启动转出流程，并执行以下操作：创建、更新、删除内容和对子节点进行排序。</td>
   <td>转出</td>
   <td>contentupdate<br /> contentcopy<br /> contentDelete<br /> referencesupdate<br /> 產品更新<br /> orderchildren</td>
  </tr>
  <tr>
   <td>在 Blueprint 激活时激活</td>
   <td>發佈來源時發佈即時副本。</td>
   <td>激活</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>在 Blueprint 停用时停用</td>
   <td>停用來源時停用即時副本。</td>
   <td>停用</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>修改时推送</td>
   <td><p>修改來源時將內容推送至即時副本。</p> <p>謹慎使用此轉出設定，因為它使用「修改」觸發器。</p> </td>
   <td>修改</td>
   <td>contentupdate<br /> contentcopy<br /> contentDelete<br /> referencesupdate<br /> orderchildren<br /> </td>
  </tr>
  <tr>
   <td>修改时推送（简略）</td>
   <td><p>修改Blueprint頁面時將內容推送至即時副本，而不更新引用（例如淺層副本）。</p> <p>謹慎使用此轉出設定，因為它使用「修改」觸發器。</p> </td>
   <td>修改</td>
   <td>contentupdate<br /> contentcopy<br /> contentDelete<br /> orderchildren</td>
  </tr>
  <tr>
   <td>提升发布内容</td>
   <td>用于提升发布页面的标准转出配置。</td>
   <td>转出</td>
   <td>contentupdate<br /> contentcopy<br /> contentDelete<br /> referencesupdate<br /> orderchildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>目錄頁面內容轉出設定</td>
   <td>从目录 Blueprint 中应用页面模板。</td>
   <td>转出</td>
   <td>contentupdate<br /> contentcopy<br /> contentDelete<br /> referencesupdate<br /> productCreateUpdate<br /> orderchildren</td>
  </tr>
  <tr>
   <td>目录页面更新转出配置</td>
   <td>從目錄Blueprint套用目標屬性。 必須在目錄頁面內容轉出設定之後執行。</td>
   <td>转出</td>
   <td>catalogRolloutHooks</td>
  </tr>
  <tr>
   <td>DPS 发布转出配置</td>
   <td>DPS發佈轉出設定，允許在初始轉出排除FolioProducer繫結屬性時，在轉出觸發器中開始轉出程式</td>
   <td>转出</td>
   <td>contentupdate<br /> contentcopy<br /> contentDelete<br /> referencesupdate<br /> orderchildren<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>舊版(5.6.0)目錄轉出設定</td>
   <td>已弃用。请使用 Catalog Generator 代替 MSM 进行目录转出。</td>
   <td>转出</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### 已安裝的同步化動作 {#installed-synchronization-actions}

下表列出與AEM一起安裝的同步化動作。 如果安裝的動作不符合您的需求，您可以 [建立新的同步化動作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).

<table>
 <tbody>
  <tr>
   <th>動作名稱</th>
   <th>描述</th>
   <th>属性<br /> </th>
  </tr>
  <tr>
   <td>contentcopy</td>
   <td>當即時副本上不存在來源的節點時，會將節點複製到即時副本。 <a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM內容複製動作服務</a> 以指定要排除的節點型別、段落專案和頁面屬性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>刪除不在來源上的即時副本節點。 <a href="#excluding-properties-and-node-types-from-synchronization">配置 CQ MSM 内容删除操作服务</a>，以指定要排除的节点类型、段落项和页面属性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentupdate</td>
   <td>使用來源的變更來更新即時副本內容。 <a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM內容更新動作服務</a> 以指定要排除的節點型別、段落專案和頁面屬性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>編輯即時副本的屬性。 editMap屬性決定要編輯哪些屬性及其值。 editMap屬性的值必須使用下列格式：</p> <p><code>[property_name_1]#[current_value]#</code>[new_value]，<br /> <code>[property_name_2]#[current_value]#</code>[new_value]，<br /> ... ，<br /> <code>[property_name_n]#[current_value]#</code>[new_value]</p> <p>此 <code>current_value</code> 和 <code>new_value</code> 專案是規則運算式。 <br /> </p> <p>例如，請考慮editMap的下列值：</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage，<br /> cq：template#/contentpage#/mobilecontentpage</p> <p>此值會編輯即時副本節點的屬性，如下所示：</p>
    <ul>
     <li>此 <code>sling:resourceType</code> 屬性已設定為 <code>contentpage</code> 或 <code>homepage</code> 設為 <code>mobilecontentpage.</code></li>
     <li>此 <code>cq:template</code> 屬性已設定為 <code>contentpage</code> 設為 <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap： （字串）識別屬性、目前值和新值。 如需詳細資訊，請參閱說明。<br /> </p> </td>
  </tr>
  <tr>
   <td>notify</td>
   <td>傳送已轉出頁面的頁面事件。 要接收通知，首先需要订阅转出事件。</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderchildren</td>
   <td>在即時副本上，它會根據Blueprint上的順序來排序子項（節點）<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesupdate</td>
   <td><p>在即時副本上，此同步動作會更新參照，例如連結。<br /> 它會搜尋即時副本頁面中指向Blueprint內資源的路徑。 找到後，它會更新路徑以指向即時副本內的相關資源（而不是Blueprint）。 具有 Blueprint 外部目标的引用不会发生更改。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">配置 CQ MSM 引用更新操作服务</a>，以指定要排除的节点类型、段落项和页面属性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>建立即時副本的版本。</p> <p>此操作必须是转出配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>啟動即時副本。</p> <p>此操作必须是转出配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>停用即時副本。</p> <p>此操作必须是转出配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><p>啟動目標屬性定義的工作流程（僅適用於頁面），並將即時副本視為裝載。</p> <p>目标路径是模型节点的路径。</p> </td>
   <td>target： （字串）工作流程模型的路徑。<br /> </td>
  </tr>
  <tr>
   <td>強制</td>
   <td><p>將即時副本頁面上若干ACL的許可權，設為特定使用者群組的唯讀。 已設定下列ACL：</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>仅对页面使用此操作。</p> </td>
   <td>target： （字串）您為其設定許可權的群組識別碼。 <br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>將即時副本頁面上若干ACL的許可權，設為特定使用者群組的唯讀。 已設定下列ACL：</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>仅对页面使用此操作。</p> </td>
   <td>target： （字串）您為其設定許可權的群組識別碼。 </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>針對特定使用者群組，將即時副本頁面上ActionSet.ACTION_NAME_REMOVE ACL的許可權設為唯讀。 仅对页面使用此操作。</td>
   <td>target： （字串）您為其設定許可權的群組識別碼。 </td>
  </tr>
  <tr>
   <td>VersionCopyaction</td>
   <td>如果Blueprint/來源頁面已發佈至少一次，會使用發佈的版本建立即時副本頁面。 注意：此動作僅適用於根據已發佈的來源頁面建立即時副本頁面，不適用於更新現有的即時副本頁面。 </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>頁面在Blueprint中移動時會套用PageMoveAction 。</p> <p>動作會將（相關的） LiveCopy頁面從移動前的位置複製到移動後的位置，而不是移動頁面。</p> <p>PageMoveAction不會變更位於移動前位置的LiveCopy頁面。 因此，對於連續RolloutConfigurations，它具有不含Blueprint的LiveRelationship狀態。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">配置 CQ MSM 页面移动操作服务</a>，以指定要排除的节点类型、段落项和页面属性。 </p> <p>此操作必须是转出配置中包含的唯一同步操作。</p> </td>
   <td><p>prop_referenceUpdate： （布林值）設為true可更新參照。 預設值為true。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>建立或更新目錄中的產品資源。 此動作旨在用於下列其中一種情況：
    <ul>
     <li>產生或轉出目錄（或目錄區段）</li>
     <li>使用者恢復產品元件的同步繼承。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>表示啟動項建立的內容存在即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRolloutHooks</td>
   <td>執行目錄產生特定的轉出掛接。 呼叫CatalogGenerator的executePageRolloutHooks和executeProductRolloutHooks方法。<br /> 請參閱AEM Javadocs中的com.adobe.cq.commerce.pim.api.CatalogGenerator 。</td>
   <td> </td>
  </tr>
  <tr>
   <td>產品更新</td>
   <td>更新產品目錄即時副本中的產品頁面</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 建立轉出設定 {#creating-a-rollout-configuration}

您可以 [建立轉出設定](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) 當安裝的轉出設定不符合您的應用程式需求時：

* [建立轉出設定](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
* [將同步化動作新增至轉出設定](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

然後，當您在Blueprint或即時副本頁面上設定轉出設定時，即可使用新的轉出設定。

### 从同步中排除属性和节点类型 {#excluding-properties-and-node-types-from-synchronization}

您可以配置多个支持相应同步操作的 OSGi 服务，以便它们不会影响特定的节点类型和属性。例如，與AEM內部功能相關的許多屬性和子節點不應包含在即時副本中。 僅應複製與頁面使用者相關的內容。

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

下表列出您可以指定要排除的節點的同步化動作。 此表格提供要使用「Web主控台」設定的服務名稱，以及使用存放庫節點進行設定的PID。

| 同步操作 | Web 控制台中的服务名称 | 服务 PID |
|---|---|---|
| contentcopy | CQ MSM 内容复制操作 | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | CQ MSM 内容删除操作 | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentupdate | CQ MSM 内容更新操作 | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | CQ MSM 页面移动操作 | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesupdate | CQ MSM 引用更新操作 | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

下表描述了您可以配置的属性：

<table>
 <tbody>
  <tr>
   <th>Web主控台屬性/ OSGi屬性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><p>排除的節點型別</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>匹配要从同步操作中排除的节点类型的正则表达式.</td>
  </tr>
  <tr>
   <td><p>排除的段落项</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>匹配要从同步操作中排除的段落项的正则表达式.</td>
  </tr>
  <tr>
   <td><p>排除的页面属性</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>匹配要从同步操作中排除的页面属性的正则表达式.</td>
  </tr>
  <tr>
   <td><p>忽略的 Mixin 节点类型</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>僅適用於CQ MSM內容更新動作。 符合要從同步化動作中排除的mixin節點型別名稱的規則運算式。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在Classic UI中，LiveCopy頁面的「頁面屬性」對話方塊中顯示的鎖定圖示不反映「排除的頁面屬性」屬性的設定。 鎖定圖示甚至會針對從同步化動作中排除的屬性而顯示。

>[!NOTE]
>
>在觸控最佳化的UI中，另請參閱 [在頁面屬性上設定MSM鎖定（觸控最佳化UI）](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui).

#### CQ MSM內容更新動作 — 排除 {#cq-msm-content-update-action-exclusions}

預設會排除數個屬性和節點型別，這些屬性和節點型別會在的OSGi設定中定義 **CQ MSM內容更新動作**，下 **排除的頁面屬性**.

依預設，轉出時排除符合下列規則運算式的屬性（即未更新）：

![chlimage_1](assets/chlimage_1.png)

您可以根据需要更改定义排除列表的表达式。

例如，如果您希望将页面&#x200B;**标题**&#x200B;包含在考虑转出的更改中，请从排除项中删除 `jcr:title`。例如，使用正则表达式：

`jcr:(?!(title)$).*`

### 配置同步以更新引用 {#configuring-synchronization-for-updating-references}

您可以配置多个 OSGi 服务以支持与更新引用相关的对应同步操作。

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

下表列出您可以為其指定參照更新的同步化動作。 此表格提供要使用「Web主控台」設定的服務名稱，以及使用存放庫節點進行設定的PID。

<table>
 <tbody>
  <tr>
   <th>Web主控台屬性/ OSGi屬性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><p>跨嵌套 Live Copy 更新引用</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>僅適用於CQ MSM參考更新動作。 選取此選項（Web主控台）或將此布林值屬性設為true （存放庫設定）可取代以位於最頂端LiveCopy分支內之任何資源為目標的參照。</td>
  </tr>
  <tr>
   <td><p>更新引用页面</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>僅適用於CQ MSM頁面移動動作。 選取此選項（Web主控台）或將此布林值屬性設為 <code>true</code> （存放庫設定）更新任何參照，以使用原始頁面來參照LiveCopy頁面。</td>
  </tr>
 </tbody>
</table>

## 指定要使用的转出配置 {#specifying-the-rollout-configurations-to-use}

MSM可讓您指定一般使用的轉出設定集，並視需要覆寫特定即時副本的轉出設定。 MSM 提供了多个位置来指定要使用的转出配置。位置會決定設定是否套用至特定的即時副本。

以下是可指定要使用的轉出設定的位置清單，說明MSM如何決定要將哪些轉出設定用於即時副本：

* **[即時副本頁面屬性](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page)：** 當即時副本頁面設定為使用一個或多個轉出設定時，MSM會使用這些轉出設定。
* **[Blueprint頁面屬性](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page)：** 當即時副本以Blueprint為基礎，且即時副本頁面未設定轉出設定時，將使用與Blueprint來源頁面關聯的轉出設定。
* **即時副本父頁面屬性：** 當即時副本頁面和Blueprint來源頁面均未設定轉出設定時，將使用套用至即時副本頁面父頁面的轉出設定。
* **[系統預設值](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration)：** 當無法確定即時副本父頁面的轉出設定時，將使用系統預設轉出設定。

例如，藍圖使用We.Retail參考網站作為來源內容。 從Blueprint建立網站。 下列清單中的每個專案都說明關於轉出設定的使用不同情境：

* 所有Blueprint頁面或即時副本頁面均未設定為使用轉出設定。 MSM會對所有即時副本頁面使用系統預設轉出設定。
* We.Retail參考網站的根頁面已設定好數個轉出設定。 MSM會對所有即時副本頁面使用這些轉出設定。
* We.Retail參考網站的根頁面已設定好數個轉出設定，而即時副本網站的根頁面已設定好不同的轉出設定。 MSM會使用在即時副本網站的根頁面上設定的轉出設定。

### 为 Live Copy 页面设置转出配置 {#setting-the-rollout-configurations-for-a-live-copy-page}

使用轉出設定來設定即時副本頁面，以便在來源頁面轉出時使用。 子页面默认情况下会继承该配置。當您設定要使用的轉出設定時，將會覆寫即時副本頁面從其父頁面繼承的設定。

您也可以在以下情況下為即時副本頁面設定轉出設定： [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page).

1. 使用 **網站** 控制檯以選取即時副本頁面。
1. 从工具栏中选择&#x200B;**属性**。
1. 打开 **Live Copy** 选项卡。

   **配置**&#x200B;部分将显示页面继承的转出配置。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 如果需要，可调整 **Live Copy 继承**&#x200B;标记。如果勾選，即時副本設定將在所有子項上都有效。

1. 清除 **從父項繼承轉出設定** 屬性，然後從清單中選取一或多個轉出設定。

   選取的轉出設定會顯示在下拉式清單下方。

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 按一下或點選 **儲存**.

### 設定Blueprint頁面的轉出設定 {#setting-the-rollout-configuration-for-a-blueprint-page}

使用轉出設定來設定Blueprint頁面，以便在轉出Blueprint頁面時使用。

請注意，Blueprint頁面的子頁面會繼承設定。 當您設定要使用的轉出設定時，可能會覆寫頁面從其父項繼承的設定。

1. 使用&#x200B;**站点**&#x200B;控制台选择 Blueprint 的根页面。
1. 从工具栏中选择&#x200B;**属性**。
1. 打开 **Blueprint** 选项卡。
1. 使用下拉选择器选择一个或多个&#x200B;**转出配置**。
1. 使用&#x200B;**保存**&#x200B;持久存储您的更新。

### 设置系统默认转出配置 {#setting-the-system-default-rollout-configuration}

指定要作為系統預設值的轉出組態。 若要指定預設值，請設定OSGi服務：

* **Day CQ WCM即時關係管理員**
服務PID為 
`com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用下列任一專案設定服務： [網頁主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [存放庫節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* 在 Web 控制台中，要配置的属性名称是默认转出配置。
* 使用存储库节点，要配置的属性的名称是 `liverelationshipmgr.relationsconfig.default`。

将此属性值设置为要用作系统默认值的转出配置的路径。默认值为 `/libs/msm/wcm/rolloutconfigs/default`，这是&#x200B;**标准转出配置**。
