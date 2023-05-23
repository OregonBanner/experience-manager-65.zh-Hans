---
title: 使用者管理與安全性
description: 瞭解AEM中的使用者管理和安全性。
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: Security
source-git-commit: 3430897fc98aecbcf6cc7bf6bdc9b3df24e92366
workflow-type: tm+mt
source-wordcount: '5398'
ht-degree: 1%

---

# 使用者管理與安全性{#user-administration-and-security}

本章說明如何設定及維護使用者授權，並說明在AEM中驗證和授權如何運作背後的理論。

## AEM中的使用者和群組 {#users-and-groups-in-aem}

本節將更詳細地說明各種實體和相關概念，以幫助您設定易於維護的使用者管理概念。

### 用户 {#users}

使用者使用其帳戶登入AEM。 每個使用者帳戶都是獨一無二的，其中包含基本帳戶詳細資料以及指派的許可權。

使用者通常是群組的成員，這可以簡化這些許可權和/或許可權的配置。

### 组 {#groups}

群組是使用者的集合、其他群組或兩者。 這些集合都稱為群組的成員。

它們的主要目的是透過減少要更新的實體數目來簡化維護流程，因為對群組所做的變更會套用到群組的所有成員。 群組通常反映：

* 應用程式內的角色；例如允許瀏覽內容的人，或允許貢獻內容的人。
* 您自己的組織；您可能想要擴充角色，以便在來自不同部門的貢獻者限制在內容樹狀結構中的不同分支時，加以區分。

因此，群組通常保持穩定，而使用者則更頻繁地來來往。

透過規劃和乾淨的結構，群組的使用可反映您的結構，為您提供清晰的概觀和有效率的更新機制。

### 內建使用者和群組 {#built-in-users-and-groups}

AEM WCM會安裝數個使用者和群組。 在安裝後第一次存取「安全性主控台」時，會顯示這些集合。

下表列出每個專案及：

* 簡短說明
* 有關必要變更的任何建議

*變更所有預設密碼* （若您未在某些情況下刪除帳戶本身）。

<table>
 <tbody>
  <tr>
   <td>用户 ID</td>
   <td>类型</td>
   <td>描述</td>
   <td>建議</td>
  </tr>
  <tr>
   <td><p>管理员</p> <p>預設密碼： admin</p> </td>
   <td>用户</td>
   <td><p>具有完整存取許可權的系統管理帳戶。</p> <p>此帳戶用於AEM WCM和CRX之間的連線。</p> <p>如果您意外刪除此帳戶，會在存放庫重新啟動時重新建立（在預設設定中）。</p> <p>管理帳戶是AEM平台的必要專案。 因此，無法刪除此帳戶。</p> </td>
   <td><p>Adobe建議您變更此使用者帳戶的預設密碼。</p> <p>最好在安裝時進行，不過之後可進行。</p> <p>注意：請勿將此帳戶與CQ Servlet Engine的管理員帳戶混淆。</p> </td>
  </tr>
  <tr>
   <td><p>匿名</p> <p> </p> </td>
   <td>用户</td>
   <td><p>保留對執行個體的未經驗證存取的預設許可權。 根據預設，此帳戶具有最低的存取許可權。</p> <p>如果您不小心刪除此帳戶，會在啟動時重新建立。 無法永久刪除，但可以停用。</p> </td>
   <td>請避免刪除或停用此帳戶，因為它會對作者執行個體的運作產生負面影響。 如果安全性需求要求您刪除它，請務必先正確測試它對您系統的影響。</td>
  </tr>
  <tr>
   <td><p>作者</p> <p>預設密碼：作者</p> </td>
   <td>用户</td>
   <td><p>允許寫入/content的作者帳戶。 包含投稿人和瀏覽者許可權。</p> <p>可以當做網站管理員，因為它可以存取整個/content樹狀結構。</p> <p>此帳戶不是內建使用者，而是其他Geometrixx示範使用者</p> </td>
   <td><p>Adobe建議將帳戶完全刪除，或是變更預設密碼。</p> <p>最好在安裝時進行，不過之後可進行。</p> </td>
  </tr>
  <tr>
   <td>管理員</td>
   <td>组</td>
   <td><p>為其所有成員授予管理員許可權的群組。 僅允許管理員編輯此群組。</p> <p>具有完整存取許可權。</p> </td>
   <td>即使您在節點上設定「deny-everyone」，管理員仍可存取節點</td>
  </tr>
  <tr>
   <td>content-author</td>
   <td>组</td>
   <td><p>負責內容編輯的群組。 需要讀取、修改、建立和刪除許可權。</p> </td>
   <td>只要您新增讀取、修改、建立和刪除許可權，就可以使用專案特定的存取許可權來建立您自己的內容作者群組。</td>
  </tr>
  <tr>
   <td>投稿人</td>
   <td>组</td>
   <td><p>允許使用者寫入內容的基本許可權（如僅功能）。</p> <p>不會將任何許可權配置給/content樹狀結構。 必須為個別群組或使用者配置。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam-users</td>
   <td>组</td>
   <td>適用於典型AEM Assets使用者的現成可用參考群組。 此群組的成員擁有啟用資產和集合上傳/共用的適當許可權。</td>
   <td> </td>
  </tr>
  <tr>
   <td>每個人</td>
   <td>组</td>
   <td><p>AEM中的每個使用者都是群組所有者的成員，即使您可能沒有在所有工具中看到群組或成員資格關係。</p> <p>此群組可視為預設許可權，因為它可用於為所有人套用許可權，即使使用者將在未來建立。</p> </td>
   <td><p>請勿修改或刪除此群組。</p> <p>修改此帳戶會有其他安全性影響。</p> </td>
  </tr>
  <tr>
   <td>標籤管理員</td>
   <td>组</td>
   <td>允許編輯標籤的群組。</td>
   <td> </td>
  </tr>
  <tr>
   <td>user-administrator</td>
   <td>组</td>
   <td>授權使用者管理，即建立使用者和群組的權利。</td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流程編輯器</td>
   <td>组</td>
   <td>允許建立和修改工作流程模型的群組。</td>
   <td> </td>
  </tr>
  <tr>
   <td>workflow-users</td>
   <td>组</td>
   <td><p>參與工作流程的使用者必須是群組workflow-users的成員。 賦予使用者/etc/workflow/instances的完整存取權，以便他們可以更新工作流程例項。</p> <p>該群組包含在標準安裝中，但您必須手動將使用者新增到該群組。</p> </td>
  </tr>
 </tbody>
</table>

## AEM中的許可權 {#permissions-in-aem}

AEM會使用ACL來判斷使用者或群組可以採取的動作，以及可以在何處執行這些動作。

### 許可權和ACL {#permissions-and-acls}

許可權定義誰可以對資源執行哪些動作。 許可權是以下專案的結果： [存取控制](#access-control-lists-and-how-they-are-evaluated) 評估。

您可以透過選取或清除個別AEM的核取方塊來變更授予/拒絕給特定使用者的許可權 [動作](security.md#actions). 核取記號表示允許動作。 沒有核取記號表示動作被拒絕。

格線中的核取記號也會指出使用者在AEM內的哪些位置有哪些許可權（即哪些路徑）。

### 操作 {#actions}

可以在頁面（資源）上執行動作。 您可以針對階層中的每個頁面，指定允許使用者在該頁面上採取的動作。 [許可權](#permissions-and-acls) 可讓您允許或拒絕動作。

<table>
 <tbody>
  <tr>
   <td><strong>操作 </strong></td>
   <td><strong>描述 </strong></td>
  </tr>
  <tr>
   <td>读取</td>
   <td>允許使用者讀取頁面及任何子頁面。</td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>修改頁面及任何子頁面上的現有內容。</li>
     <li>在頁面或任何子頁面上建立段落。</li>
    </ul> <p>在JCR層級，使用者可以編輯資源，方法是編輯其屬性、鎖定、版本設定、nt-modifications，並且他們對定義jcr：content子節點的節點具有完整的寫入許可權。 例如cq：Page、nt：file、cq：Asset。</p> </td>
  </tr>
  <tr>
   <td>创建</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>建立頁面或子頁面。</li>
    </ul> <p>若 <strong>修改</strong> 遭拒，jcr：content底下的子樹狀結構會遭到排除，因為建立jcr：content及其子節點會視為頁面修改。 此規則僅適用於定義jcr：content子節點的節點。</p> </td>
  </tr>
  <tr>
   <td>删除</td>
   <td><p>使用者可以：</p>
    <ul>
     <li>從頁面或任何子頁面刪除現有段落。</li>
     <li>刪除頁面或子頁面。</li>
    </ul> <p>若 <strong>修改</strong> 拒絕jcr：content底下的任何子樹狀結構會排除為移除jcr：content，且其子節點會視為頁面修改。 此規則僅適用於定義jcr：content子節點的節點。</p> </td>
  </tr>
  <tr>
   <td>读取 ACL</td>
   <td>使用者可以讀取頁面或子頁面的存取控制清單。</td>
  </tr>
  <tr>
   <td>编辑 ACL</td>
   <td>使用者可以修改頁面或任何子頁面的存取控制清單。</td>
  </tr>
  <tr>
   <td>复制</td>
   <td>使用者可以將內容復寫至其他環境（例如發佈環境）。 此許可權也會套用至任何子頁面。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM會自動在中產生角色指派（所有者、編輯者、檢視者）的使用者群組 [集合](/help/assets/manage-collections.md). 然而，手動為這類群組新增ACL可能會在AEM中帶來安全漏洞。 Adobe建議您避免手動新增ACL。

### 存取控制清單及其評估方式 {#access-control-lists-and-how-they-are-evaluated}

AEM WCM使用存取控制清單(ACL)來組織套用至不同頁面的許可權。

存取控制清單由個別許可權組成，用於決定套用這些許可權的順序。 清單會根據所考慮頁面的階層而形成。 然後會自下而上掃描此清單，直到找到可套用至頁面的第一個適當許可權為止。

>[!NOTE]
>
>範例中包含ACL。 建議您檢閱並確定適合您應用程式的專案。 若要檢閱包含的ACL，請前往 **CRXDE** 並選取 **存取控制** 標籤中選取下列節點：
>
>* `/etc/cloudservices`
>* `/home/users/we-retail`
>
>您的自訂應用程式可以設定其他關係的存取權，例如：
>
>* `*/social/relationships/friend/*`
>* 或 `*/social/relationships/pending-following/*`.
>
>當您建立社群專屬的ACL時，加入這些社群的成員可能會被授予額外的許可權。 例如，當使用者加入社群時： `/content/we-retail/us/en/community`

### 許可權狀態 {#permission-states}

>[!NOTE]
>
>若為CQ 5.3使用者：
>
>相較於舊版CQ， **建立** 和 **刪除** 若使用者必須僅修改頁面，則不應再授予。 請改為授予 **修改** 動作僅限您希望使用者能在現有頁面上建立、修改或刪除元件時。
>
>基於回溯相容性原因，動作測試不會針對定義節點採取特殊處理方式 **jcr：content** 納入考量。

| **操作** | **描述** |
|---|---|
| 允許（核取記號） | AEM WCM可讓使用者在此頁面或任何子頁面上執行動作。 |
| 拒絕（無核取標籤） | AEM WCM不允許使用者在此頁面或任何子頁面上執行動作。 |

這些許可權也會套用至任何子頁面。

如果許可權不是從父節點繼承，但至少有一個本機專案用於該節點，則會將以下符號附加至核取方塊。 本機專案是在CRX 2.2介面中建立的專案（目前只能在CRX中建立萬用字元ACL）。

對於指定路徑上的動作：

<table>
 <tbody>
  <tr>
   <td>* （星號）</td>
   <td>至少有一個本機專案（有效或無效）。 這些萬用字元ACL在CRX中定義。</td>
  </tr>
  <tr>
   <td>！ （驚歎號）</td>
   <td>目前至少有一個專案沒有作用。</td>
  </tr>
 </tbody>
</table>

當您將滑鼠游標停留在星號或驚歎號上時，工具提示會提供更多有關宣告專案的詳細資訊。 工具提示分為兩個部分：

<table>
 <tbody>
  <tr>
   <td>上半部</td>
   <td><p>列出有效專案。</p> </td>
  </tr>
  <tr>
   <td>下方</td>
   <td>列出可能會在樹狀結構中的其他位置產生效果的非有效專案（如特殊屬性所指示，具有限制專案範圍的對應ACE）。 或者，它是一個條目，其效果被在給定路徑或祖先節點定義的另一個條目撤銷。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>如果沒有為頁面定義許可權，則會拒絕所有動作。

以下是有關管理存取控制清單的建議：

* 不要直接將許可權指派給使用者。 僅將其指派給群組。

   這麼做可簡化維護作業，因為群組數量遠低於使用者數量，且波動性也較低。

* 如果您希望群組/使用者只能修改頁面，請勿授予他們建立或拒絕許可權。 僅授予他們修改和讀取許可權。
* 請謹慎使用「拒絕」。 儘可能使用「僅允許」。

   如果許可權套用的順序與預期順序不同，則使用deny可能會造成非預期的影響。 如果使用者是多個群組的成員，則一個群組的Deny陳述式可能會取消另一個群組的Allow陳述式，反之亦然。 發生這類事情時，很難提供概觀，並且容易導致無法預見的結果，而「允許指派」不會導致這類衝突。

   Adobe建議您使用「允許」而非「拒絕」，請參閱 [最佳實務](#best-practices).

在修改任一許可權之前，請務必瞭解其運作和相互關聯的方式。 請參閱說明AEM WCM的CRX檔案 [評估存取許可權](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated)以及設定存取控制清單的範例。

### 权限 {#permissions}

許可權可讓使用者和群組存取AEM頁面上的AEM功能。

您可以展開/收合節點，依路徑瀏覽許可權，並可追蹤至根節點的許可權繼承。

您可以選取或清除適當的核取方塊，以允許或拒絕許可權。

![cqsecuritypermissionstab](assets/cqsecuritypermissionstab.png)

### 檢視詳細的許可權資訊 {#viewing-detailed-permission-information}

除了格線檢視外，AEM還提供在指定路徑上所選使用者/群組的詳細許可權檢視。 詳細資料檢視提供額外資訊。

除了檢視資訊之外，您也可以包含或排除群組中的目前使用者或群組。 另請參閱 [新增許可權時新增使用者或群組](#adding-users-or-groups-while-adding-permissions). 此處所做的變更會立即反映在詳細檢視的上半部分。

若要存取「詳細資訊」檢視，請在 **許可權** 標籤，按一下 **詳細資料** 任何選取的群組/使用者和路徑。

![許可權詳細資料](assets/permissiondetails.png)

詳細資訊分為兩個部分：

<table>
 <tbody>
  <tr>
   <td>上半部</td>
   <td><p>重複您在樹狀格線中看到的資訊。 對於每個動作，圖示會顯示該動作是否被允許或拒絕：</p>
    <ul>
     <li>無圖示=無宣告專案</li>
     <li>（勾號） =宣告的動作（允許）</li>
     <li>(-) =宣告的動作（拒絕）</li>
    </ul> </td>
  </tr>
  <tr>
   <td>下方</td>
   <td><p>顯示執行下列作業的使用者和群組格線：</p>
    <ul>
     <li>為給定路徑宣告一個專案AND</li>
     <li>指定的可授權或是否為群組</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 模擬其他使用者 {#impersonating-another-user}

使用 [模擬功能](/help/sites-authoring/user-properties.md#user-settings)，使用者可以代表其他使用者工作。

也就是說，使用者帳戶可以指定可以使用其帳戶操作的其他帳戶。 例如，如果允許使用者B模擬使用者A，則使用者B可以使用使用者A的完整帳戶詳細資料進行動作。

此功能可讓模擬者帳戶完成任務，就好像他們正使用自己所模擬的帳戶一樣。 例如，在缺勤期間，或短期共用過多負載。

>[!NOTE]
>
>為了模擬非管理員使用者才能運作，模擬者（在上述案例中為user-B）必須在以下位置具有「讀取」許可權： `/home/users` 路徑。
>
>另請參閱 [AEM中的許可權](/help/sites-administering/security.md#permissions-in-aem).

>[!CAUTION]
>
>如果一個帳戶模擬另一個帳戶，則很難檢視。 當模擬開始和結束時，會在稽核記錄中建立一個專案，但其他記錄檔（例如存取記錄）不會保留事件上已發生模擬的資訊。 因此，如果使用者B模擬使用者A，則所有事件看起來都像是使用者A執行了它們。

>[!CAUTION]
>
>模拟用户身份时可以执行页面锁定。不過，以這種方式鎖定的頁面只能以被模擬的使用者或具有管理員許可權的使用者身分解除鎖定。
>
>无法通过模拟锁定页面的用户的身份来解锁页面。

### 最佳实践 {#best-practices}

以下說明使用許可權和許可權時的最佳實務：

| 规则 | 原因 |
|--- |--- |
| *使用群組* | 避免依個別使用者指派存取許可權。 提出此建議有幾個原因：<ul><li>您擁有的使用者比群組多，因此群組可簡化結構。</li><li>群組有助於提供所有帳戶的概觀。</li> <li>使用群組可簡化繼承作業。</li><li>使用者來了又走。 群組是長期的。</li></ul> |
| *為正面* | 請一律使用Allow陳述式來指定群組權利（儘可能使用）。 避免使用Deny陳述式。 系統會依順序評估群組，且可能依照使用者的不同方式定義順序。 換言之：您可能無法控制執行及評估陳述式的順序。 如果您只使用Allow陳述式，則順序無關緊要。 |
| *保持簡單* | 在設定新安裝時投入一些時間和思考是值得的。 套用清晰的結構可簡化持續的維護和管理工作，確保您目前的同事和未來的後續人員都能輕鬆瞭解實作的內容。 |
| *测试* | 使用測試安裝來練習並確保您瞭解各種使用者和群組之間的關係。 |
| *預設使用者/群組* | 務必在安裝後立即更新預設使用者和群組，以防止任何安全性問題。 |

## 管理使用者和群組 {#managing-users-and-groups}

使用者包括使用系統的人員和向系統提出請求的外來系統。

群組是一組使用者。

兩者都可以使用安全性主控台中的使用者管理功能進行設定。

### 使用安全性主控台存取使用者管理 {#accessing-user-administration-with-the-security-console}

您可以使用「安全性」主控台來存取所有使用者、群組和關聯的許可權。 本節中說明的所有程式都在此視窗中執行。

若要存取AEM WCM安全性，請執行下列任一項作業：

* 從「歡迎」畫面或AEM中的各種位置，按一下安全性圖示：

![](do-not-localize/wcmtoolbar.png)

* 直接導覽至 `https://<server>:<port>/useradmin`. 請確定您以管理員身分登入AEM。

下列視窗隨即顯示：

![cqsecuritypage](assets/cqsecuritypage.png)

左邊的樹狀結構列出目前系統中所有的使用者和群組。 您可以選取要顯示的欄、對欄的內容進行排序，甚至通過將欄標題拖到新位置來變更欄的顯示順序。

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

這些標籤可讓您存取各種設定：

<!-- ??? in table below. -->

| 制表符 | 描述 |
|--- |--- |
| 篩選方塊 | 篩選列出的使用者、群組或兩者的機制。 另請參閱 [篩選使用者和群組](#filtering-users-and-groups). |
| 隐藏用户 | 隱藏所有列出之使用者的切換開關，僅保留群組。 另請參閱 [隱藏使用者和群組](#hiding-users-and-groups). |
| 隐藏组 | 隱藏所有列出群組的切換開關，僅保留使用者。 另請參閱 [隱藏使用者和群組](#hiding-users-and-groups). |
| 编辑 | 可讓您建立和刪除以及啟用和停用使用者或群組的功能表。 另請參閱 [建立使用者和群組](#creating-users-and-groups) 和 [刪除使用者和群組](#deleting-users-and-groups). |
| 属性 | 列出包含電子郵件資訊、說明和名稱資訊的使用者或群組相關資訊。 也可讓您變更使用者的密碼。 另請參閱 [建立使用者和群組](#creating-users-and-groups)， [修改使用者和群組屬性](#modifying-user-and-group-properties) 和 [變更使用者密碼](#changing-a-user-password). |
| 组 | 列出所選使用者或群組所屬的所有群組。 您可以將選取的一或多個使用者指派給其他群組，或從群組中移除這些群組。 另請參閱 [群組](#adding-users-or-groups-to-a-group). |
| 成员 | 僅適用於群組。 列出特定群組的成員。 另請參閱 [成員](#members-adding-users-or-groups-to-a-group). |
| 权限 | 您可以將許可權分配給使用者或群組。 可讓您控制下列專案：<ul><li>與特定頁面/節點相關的許可權。 另請參閱 [設定許可權](#setting-permissions). </li><li>與建立和刪除頁面以及階層修改相關的許可權。???可讓您 [分配許可權](#settingprivileges)，例如階層修改，可讓您建立和刪除頁面，</li><li>相關許可權 [復寫許可權](#setting-replication-privileges) （通常從作者到發佈）。</li></ul> |
| 模拟者 | 可讓其他使用者模擬帳戶。 當您需要使用者代表另一個使用者行事時很有用。 另請參閱 [模擬使用者](#impersonating-another-user). |
| 首选项 | 集合 [群組或使用者的偏好設定](#setting-user-and-group-preferences). 例如，語言偏好設定。 |

### 篩選使用者和群組 {#filtering-users-and-groups}

您可以輸入篩選運算式來篩選清單，這會隱藏不符合運算式的所有使用者和群組。 您也可以使用隱藏使用者和群組 [隱藏使用者和隱藏群組](#hiding-users-and-groups) 按鈕。

若要篩選使用者或群組：

1. 在左邊的樹狀結構清單中，在提供的空白處輸入您的篩選運算式。 例如，輸入 **管理員** 顯示包含此字串的所有使用者和群組。
1. 按一下放大鏡以篩選清單。

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. 按一下 **x** 移除所有篩選器時。

### 隱藏使用者和群組 {#hiding-users-and-groups}

隱藏使用者或群組是另一種篩選系統中所有使用者和群組清單的方式。 有兩種切換機制。 按一下「隱藏使用者」會隱藏檢視中的所有使用者，而按一下「隱藏群組」則會隱藏檢視中的所有群組（您無法同時隱藏使用者和群組）。 若要使用篩選運算式來篩選清單，請參閱 [篩選使用者和群組](#filtering-users-and-groups).

若要隱藏使用者和群組：

1. 在 **安全性** 主控台，按一下 **隱藏使用者** 或 **隱藏群組**. 選取的按鈕會反白顯示。

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. 若要讓使用者或群組重新出現，請再次按一下對應的按鈕。

### 建立使用者和群組 {#creating-users-and-groups}

若要建立使用者或群組：

1. 在 **安全性** 主控台樹狀結構清單，按一下 **編輯** 然後 **建立使用者** 或 **建立群組**.

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. 根據您是要建立使用者還是群組，輸入所需的詳細資訊。

   * 如果您選取 **建立使用者，** 您輸入登入ID、名字和姓氏、電子郵件地址和密碼。 依預設，AEM會根據姓氏的第一個字母建立路徑，但您可以選取其他路徑。

   ![createuserdialog](assets/createuserdialog.png)

   * 如果您選取 **建立群組**，您可輸入群組ID和說明（選用）。

   ![creategroupdialog](assets/creategroupdialog.png)

1. 单击&#x200B;**创建**。您建立的使用者或群組會顯示在樹狀結構清單中。

### 刪除使用者和群組 {#deleting-users-and-groups}

若要刪除使用者或群組：

1. 在 **安全性** 控制檯中，選取您要刪除的使用者或群組。 如果要刪除多個專案，請按住Shift鍵並按一下，或按住Ctrl鍵並按一下以選取它們。
1. 按一下 **編輯，** 然後選取「刪除」。 AEM WCM會詢問您是否要刪除使用者或群組。
1. 按一下 **確定** 以確認或取消。

### 修改使用者和群組屬性 {#modifying-user-and-group-properties}

若要修改使用者和群組屬性：

1. 在 **安全性** console，連按兩下您要修改的使用者或群組名稱。

1. 按一下 **屬性** 標籤，進行必要的變更，然後按一下 **儲存**.

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>使用者的路徑會顯示在使用者屬性的底部。 無法修改。

### 變更使用者密碼 {#changing-a-user-password}

使用以下程式來修改使用者的密碼。

>[!NOTE]
>
>您無法使用「安全性」主控台來變更管理密碼。 若要變更管理員帳戶的密碼，請使用 [使用者主控台](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) Granite Operations所提供的資訊。
>
>如果您在JEE上使用AEM Forms，請勿使用下列指示變更密碼，而改用JEEAdmin Console上的AEM Forms (/adminui)變更密碼。

1. 在 **安全性** console，連按兩下您要變更密碼的使用者名稱。
1. 按一下 **屬性** 標籤（如果尚未啟用）。
1. 按一下 **設定密碼**. 「設定密碼」視窗會開啟，您可以在其中變更密碼。

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. 輸入新密碼兩次；由於新密碼未以純文字顯示，此動作用於確認 — 如果新密碼不符，系統會顯示錯誤。
1. 按一下 **設定** 以啟用帳戶的新密碼。

### 新增使用者或群組至群組 {#adding-users-or-groups-to-a-group}

AEM提供三種將使用者或群組新增至現有群組的不同方式：

* 當您在群組中時，您可以新增成員（使用者或群組）。
* 當您在成員中時，您可以將成員新增至群組。
* 處理許可權時，您可以將成員新增至群組。

### 群組 — 新增使用者或群組至群組 {#groups-adding-users-or-groups-to-a-group}

此 **群組** 索引標籤會顯示目前帳戶所屬的群組。 您可以使用它來將選取的帳戶新增至群組：

1. 連按兩下您要指派給群組的帳戶（使用者或群組）名稱。
1. 按一下 **群組** 標籤。 您會看到該帳戶已經屬於的群組清單。
1. 在樹狀結構清單中，按一下要新增至帳戶的群組名稱，然後將其拖曳至 **群組** 窗格。 （如果要新增多個使用者，請按住Shift鍵並按一下，或按住Control鍵並按一下這些名稱，然後拖曳它們。）

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. 按一下 **儲存** 以儲存變更。

### 成員 — 新增使用者或群組至群組 {#members-adding-users-or-groups-to-a-group}

此 **成員** 索引標籤僅適用於群組，並顯示哪些使用者和群組屬於目前群組。 您可以使用它來新增帳戶至群組：

1. 連按兩下要新增成員的群組名稱。
1. 按一下 **成員** 標籤。 您會看到已屬於此群組的成員清單。
1. 在樹狀結構清單中，按一下要新增至群組的成員名稱，然後將其拖曳至 **成員** 窗格。 （如果要新增多個使用者，請按住Shift鍵並按一下，或按住Control鍵並按一下這些名稱，然後拖曳它們。）

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. 按一下 **儲存** 以儲存變更。

### 新增許可權時新增使用者或群組 {#adding-users-or-groups-while-adding-permissions}

若要將成員新增至位於特定路徑的群組：

1. 連按兩下您要新增使用者的群組或使用者的名稱。

1. 按一下 **許可權** 標籤。

1. 導覽至您要新增許可權的路徑，然後按一下 **詳細資料**. 詳細資訊視窗的下半部分提供有關誰擁有該頁面許可權的資訊。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 選取「 」中的核取方塊 **會員** 欄中指定想要擁有該路徑許可權的成員。 清除您要移除其許可權之成員的核取方塊。 紅色三角形會出現在您變更的儲存格中。
1. 按一下 **確定** 以儲存變更。

### 從群組移除使用者或群組 {#removing-users-or-groups-from-groups}

AEM提供三種不同的方式可移除群組中的使用者或群組：

* 當您在群組設定檔中時，您可以移除成員（使用者或群組）。
* 當您在成員設定檔中時，您可以從群組移除成員。
* 處理許可權時，您可以從群組移除成員。

### 群組 — 從群組移除使用者或群組 {#groups-removing-users-or-groups-from-groups}

若要從群組移除使用者或群組帳戶：

1. 連按兩下您要從群組移除的群組或使用者帳戶名稱。
1. 按一下 **群組** 標籤。 您可以看到所選帳戶屬於哪些群組。
1. 在 **群組** 窗格，按一下您要從群組移除的使用者或群組名稱，然後按一下 **移除**. (如果您想要移除多個帳號，請按住Shift鍵並按一下，或按住Control鍵並按一下這些名稱，然後按一下 **移除**.)

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. 按一下 **儲存** 以儲存變更。

### 成員 — 從群組移除使用者或群組 {#members-removing-users-or-groups-from-groups}

若要從群組移除帳號，請執行下列動作：

1. 連按兩下您要從中移除成員的群組名稱。
1. 按一下 **成員** 標籤。 您會看到已屬於此群組的成員清單。
1. 在 **成員** 窗格，按一下您要從群組中移除的成員名稱，然後按一下 **移除**. (如果要移除多個使用者，請按住Shift鍵並按一下，或按住Control鍵並按一下這些名稱，然後按一下 **移除**.)

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. 按一下 **儲存** 以儲存變更。

### 新增許可權時移除使用者或群組 {#removing-users-or-groups-while-adding-permissions}

若要從特定路徑的群組中移除成員：

1. 連按兩下您要從中移除使用者的群組或使用者的名稱。

1. 按一下 **許可權** 標籤。

1. 導覽至您要移除許可權的路徑，然後按一下 **詳細資料**. 詳細資訊視窗的下半部分提供有關誰擁有該頁面許可權的資訊。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 選取「 」中的核取方塊 **會員** 欄中指定想要擁有該路徑許可權的成員。 清除您要移除其許可權之成員的核取方塊。 紅色三角形會出現在您變更的儲存格中。
1. 按一下 **確定** 以儲存變更。

### 使用者同步 {#user-synchronization}

當部署是 [發佈陣列](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，使用者和群組必須在所有發佈節點之間同步。

若要瞭解使用者同步以及如何啟用同步，請參閱 [使用者同步](/help/sites-administering/sync.md).

## 管理許可權 {#managing-permissions}

>[!NOTE]
>
>Adobe已針對許可權管理引入新的觸控式UI型主體檢視。 如需其使用方式的詳細資訊，請參閱 [此頁面](/help/sites-administering/touch-ui-principal-view.md).

本節說明如何設定許可權，包括復寫許可權。

### 設定許可權 {#setting-permissions}

許可權可讓使用者在特定路徑的資源上執行特定動作。 其中也包含建立或刪除頁面的功能。

若要新增、修改或刪除許可權：

1. 在 **安全性** console，連按兩下您要為或設定許可權的使用者或群組名稱 [搜尋節點](#searching-for-nodes).

1. 按一下 **許可權** 標籤。

   ![cquserpermissions](assets/cquserpermissions.png)

1. 在樹狀格線中，選取核取方塊以允許選取的使用者或群組執行動作，或清除核取方塊以拒絕選取的使用者或群組執行動作。 如需詳細資訊，請按一下 **詳細資料**.

1. 完成後，按一下 **儲存**.

### 設定復寫許可權 {#setting-replication-privileges}

復寫許可權是發佈內容的許可權，可為群組和使用者設定。

>[!NOTE]
>
>* 套用至群組的任何復寫許可權都會套用至該群組中的所有使用者。
>* 使用者的復寫許可權會取代群組的復寫許可權。
>* 允許復寫許可權的優先順序高於拒絕復寫許可權。 另請參閱 [AEM中的許可權](#permissions-in-aem) 以取得詳細資訊。
>


若要設定復寫許可權：

1. 從清單中選取使用者或群組，按兩下以開啟，然後按一下 **許可權**.
1. 在網格中，導覽至您希望使用者擁有復寫許可權的路徑，或 [搜尋節點。](#searching-for-nodes)

1. 在 **復寫** 資料欄，選取核取方塊以新增該使用者或群組的復寫許可權，或清除核取方塊以移除復寫許可權。 AEM會在您進行變更但尚未儲存的任何地方顯示紅色三角形。

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. 按一下 **儲存** 以儲存變更。

### 搜尋節點 {#searching-for-nodes}

新增或移除許可權時，您可以瀏覽或搜尋節點。

有兩種不同型別的路徑搜尋：

* 路徑搜尋 — 如果搜尋字串開頭為&quot;/&quot;，則會搜尋指定路徑的直接子節點：

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

在搜尋方塊中，您可以執行下列動作：

| 操作 | 作用 |
|--- |--- |
| 向右鍵 | 選取搜尋結果中的子節點 |
| 向下鍵 | 再次開始搜尋。 |
| 輸入（傳回）金鑰 | 選取子節點並將其載入樹狀格點 |

* 全文搜尋 — 如果搜尋字串的開頭不是&quot;/&quot;，則會在路徑&quot;/content&quot;下的所有節點上執行全文搜尋。

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

若要對路徑或全文檢索執行搜尋：

1. 在「安全性」主控台中，選取使用者或群組，然後按一下 **許可權** 標籤。

1. 在「搜尋」方塊中，輸入要搜尋的字詞。

### 模擬使用者 {#impersonating-users}

您可以指定一或多個允許模擬目前使用者的使用者。 此功能表示他們可以將其帳戶設定切換為目前使用者的並代表此使用者操作。

使用此功能時請務必謹慎，因為此功能可讓使用者執行其自己的使用者無法執行的動作。 模擬使用者時，系統會通知使用者他們未以自己的身分登入。

在多種情況下，您可能會想要使用此功能，包括：

* 如果您不在辦公室，您可以讓其他人在您不在時模擬您。 透過使用此功能，您可以確保某人擁有您的存取許可權，而您不需要修改使用者設定檔或提供密碼。
* 您可以將其用於偵錯。 例如，檢視網站如何尋找具有受限制存取許可權的使用者。 此外，如果使用者抱怨技術問題，您可以模擬該使用者來診斷和修正問題。

若要模擬現有使用者，請執行下列動作：

1. 在樹狀結構清單中，選取您要指派其他使用者進行模擬的人員名稱。 按兩下以開啟。
1. 按一下 **模擬者** 標籤。
1. 按一下您想要能夠模擬所選使用者的使用者。 將使用者（模擬者）從清單拖曳至模擬窗格。 名稱會顯示在清單中。

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. 单击“**保存**”。

### 設定使用者和群組偏好設定 {#setting-user-and-group-preferences}

若要設定使用者和群組偏好設定，包括語言、視窗管理和工具列偏好設定：

1. 在左側樹狀結構中選取您要變更其偏好設定的使用者或群組。 若要選取多個使用者或群組，請按Ctrl+按一下或Shift+按一下您的選取專案。
1. 按一下 **偏好設定** 標籤。

   ![cqsecuritypreferences](assets/cqsecuritypreferences.png)

1. 視需要對群組或使用者偏好設定進行變更，然後按一下 **儲存** 完成後。

### 設定具有管理其他使用者之許可權的使用者或管理員 {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

若要將使用者或管理員設定為具有刪除/啟用/停用其他使用者的許可權：

1. 將您要授與管理其他使用者的許可權的使用者新增至管理員群組，並儲存變更。

   ![cqsecurityaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. 在使用者的 **許可權** 索引標籤，導覽至「/」，然後在「復寫」欄中選取核取方塊以允許在「/」進行復寫，然後按一下 **儲存**.

   ![cqsecurityreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   選取的使用者現在可以停用、啟用、刪除和建立使用者。

### 擴充專案層級的許可權 {#extending-privileges-on-a-project-level}

如果您計畫實作應用程式特定的許可權，下列資訊會說明實作自訂許可權所必須知道的事項，以及如何在CQ中實作自訂許可權：

jcr-privileges的組合會涵蓋階層修改許可權。 復寫許可權已命名 **crx：replicate** 會連同其他許可權一起儲存/評估jcr存放庫。 但是，不會在jcr層級強制執行。

自訂許可權的定義與註冊是 [Jackrabbit API](https://jackrabbit.apache.org/oak/docs/security/privilege.html) 截至2.4版(另請參閱 [JCR-2887](https://issues.apache.org/jira/browse/JCR-2887))。 JCR存取控制管理會涵蓋進一步的用法，例如 [JSR 283](https://jcp.org/en/jsr/detail?id=283) （第16節）。 此外，Jackrabbit API還定義了數個擴充功能。

許可權註冊機制反映在UI中，位於 **存放庫設定**.

新（自訂）許可權的註冊本身受到必須在存放庫層級授與的內建許可權保護。 在JCR中：在ac mgt api中以「absPath」引數傳遞「null」，詳情請參閱jsr 333。 依預設， **管理員** 而且所有管理員成員都擁有該許可權。

>[!NOTE]
>
>雖然實作負責驗證和評估自訂許可權，但除非這些許可權是內建許可權的彙總，否則無法強制執行。
