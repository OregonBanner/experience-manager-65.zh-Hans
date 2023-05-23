---
title: 使用者、群組和存取許可權管理
seo-title: User, Group and Access Rights Administration
description: 瞭解AEM中的使用者、群組和存取許可權管理。
seo-description: Learn about user, group and access rights administration in AEM.
uuid: 26d7bb25-5a38-43c6-bd6a-9ddba582c60f
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 66674e47-d19f-418f-857f-d91cf8660b6d
docset: aem65
exl-id: 5808b8f9-9b37-4970-b5c1-4d33404d3a8b
feature: Security
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '3120'
ht-degree: 0%

---

# 使用者、群組和存取許可權管理{#user-group-and-access-rights-administration}

啟用CRX存放庫的存取權涉及幾個主題：

* [存取許可權](#how-access-rights-are-evaluated)  — 如何定義和評估這些引數的概念
* [使用者管理](#user-administration)  — 管理用於存取的個別帳戶
* [群組管理](#group-administration)  — 透過組成群組來簡化使用者管理
* [存取許可權管理](#access-right-management)  — 定義控制這些使用者和群組存取資源方式的原則

基本元素包括：

**使用者帳戶** CRX會根據使用者帳戶中保留的詳細資訊，識別及驗證使用者（由該人員或其他應用程式），以驗證存取權。

在CRX中，每個使用者帳戶都是工作區中的節點。 CRX使用者帳戶具有下列屬性：

* 它代表CRX的一名使用者。
* 它包含使用者名稱和密碼。
* 適用於該工作區。
* 不能有子使用者。 針對階層式存取許可權，您應使用群組。

* 您可以指定使用者帳戶的存取許可權。

   不過，為了簡化管理，我們建議（大多數情況下）您指派存取權給群組帳戶。 為每個個別使用者指派存取許可權會很快變得非常難以管理（只有一兩個執行個體存在時，某些系統使用者會例外）。

**群組帳戶** 群組帳戶是使用者和/或其他群組的集合。 這些可用來簡化管理，因為指派給群組的存取許可權變更會自動套用至該群組中的所有使用者。 使用者不必屬於任何群組，但通常屬於多個群組。

在CRX中，群組具有以下屬性：

* 它代表一組具有共同存取許可權的使用者。 例如，作者或開發人員。
* 適用於該工作區。
* 它可以有成員；這些成員可以是個人使用者或其他群組。
* 使用成員關係可達成階層式分組。 您無法將群組直接放在存放庫中另一個群組的下方。
* 您可以定義所有群組成員的存取許可權。

**存取許可權** CRX使用存取權來控制對存放庫特定區域的存取。

這是透過指派許可權來允許或拒絕存取存放庫中的資源（節點或路徑）來完成的。 由於可以指派各種許可權，因此必須評估這些許可權以確定哪個組合適用於目前的請求。

CRX可讓您設定使用者和群組帳戶的存取許可權。 然後會將相同的基本評估原則套用至兩者。

## 存取許可權的評估方式 {#how-access-rights-are-evaluated}

>[!NOTE]
>
>CRX實作 [JSR-283定義的存取控制](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).
>
>CRX存放庫的標準安裝設定為使用資源型存取控制清單。 這是JSR-283存取控制的一個可能實作，也是Jackrabbit提供的實作之一。

### 主體和主體 {#subjects-and-principals}

CRX在評估存取權時使用兩個關鍵概念：

* A **主體** 是擁有存取許可權的實體。 主要專案包括：

   * 使用者帳戶
   * 群組帳戶

      如果使用者帳戶屬於一個或多個群組，則它也會與每個群組主體相關聯。

* A **主旨** 用於代表要求的來源。

   它可用來合併適用於該請求的存取許可權。 這些擷取自：

   * 使用者主體

      您直接指派給使用者帳戶的許可權。

   * 與該使用者相關聯的所有群組主體

      指派給使用者所屬任何群組的所有權利。
   然後會使用結果來允許或拒絕存取要求的資源。

#### 編譯主旨的存取權清單 {#compiling-the-list-of-access-rights-for-a-subject}

在CRX中，主題相依於：

* 使用者主體
* 與該使用者相關聯的所有群組主體

適用於主體的存取權清單是以下列方式建構的：

* 您直接指派給使用者帳戶的許可權
* 加上指派給使用者所屬任何群組的所有權利

![chlimage_1-56](assets/chlimage_1-56.png)

>[!NOTE]
>
>* CRX在編譯清單時不會將任何使用者階層列入考量。
>* CRX只有在您將群組加入為其他群組成員時，才會使用群組階層。 群組許可權沒有自動繼承。
>* 您指定群組的順序不會影響存取許可權。
>


### 解決請求和存取許可權 {#resolving-request-and-access-rights}

當CRX處理請求時，會將來自主體的存取請求與存放庫節點上的存取控制清單進行比較：

所以，如果Linda要求更新 `/features` 節點存放庫結構：

![chlimage_1-57](assets/chlimage_1-57.png)

### 優先順序 {#order-of-precedence}

CRX中的存取權評估如下：

* 使用者主體一律優先於群組主體，不論下列專案為何：

   * 在存取控制清單中的順序
   * 它們在節點階層中的位置

* 對於指定的主體，指定節點上最多存在1個拒絕和1個允許專案。 實作一律會清除多餘的專案，並確保允許和拒絕專案中未列出相同的許可權。

>[!NOTE]
>
>此評估程式適用於標準CRX安裝的資源型存取控制。

舉兩個例子，其中一個是使用者 `aUser` 是群組的成員 `aGroup`：

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
       + grandChildNode
```

在上述案例中：

* `aUser` 未被授予寫入許可權 `grandChildNode`.

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
         + ace: aUser - deny - write
       + grandChildNode
```

在此案例中：

* `aUser` 未被授予寫入許可權 `grandChildNode`.
* 第二個ACE `aUser` 為備援。

在階層內和單一存取控制清單中，會根據多個群組主體的順序評估其存取許可權。

### 最佳实践 {#best-practices}

下表列出一些建議和最佳實務：

<table>
 <tbody>
  <tr>
   <td>建議……</td>
   <td>原因...</td>
  </tr>
  <tr>
   <td><i>使用群組</i></td>
   <td><p>避免依個別使用者指派存取許可權。 原因有幾個：</p>
    <ul>
     <li>您擁有的使用者比群組多，因此群組可簡化結構。</li>
     <li>群組有助於提供所有帳戶的概觀。</li>
     <li>使用群組可簡化繼承作業。</li>
     <li>使用者來了又走。 群組是長期的。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><i>為正面</i></td>
   <td><p>請一律使用Allow陳述式來指定群組主體的存取許可權（儘可能使用）。 避免使用Deny陳述式。</p> <p>在單一存取控制清單中，群組主體會依序在階層內和順序進行評估。</p> </td>
  </tr>
  <tr>
   <td><i>保持簡單</i></td>
   <td><p>花一些時間在設定新安裝時思考將獲得良好的回報。</p> <p>套用清晰的結構將簡化持續的維護和管理，確保您目前的同事和/或未來的後續人員都能輕鬆瞭解正在實作的內容。</p> </td>
  </tr>
  <tr>
   <td><i>测试</i></td>
   <td>使用測試安裝來練習並確保您瞭解各種使用者和群組之間的關係。</td>
  </tr>
  <tr>
   <td><i>預設使用者/群組</i></td>
   <td>務必在安裝後立即更新預設使用者和群組，以防止任何安全性問題。</td>
  </tr>
 </tbody>
</table>

## 使用者管理 {#user-administration}

標準對話方塊用於 **使用者管理**.

您必須登入適當的工作區，才能從以下兩個位置存取對話方塊：

* 此 **使用者管理** CRX主要主控台上的連結
* 此 **安全性** CRX Explorer的功能表

![chlimage_1-58](assets/chlimage_1-58.png)

**属性**

* **使用者ID**

   用於存取CRX的帳戶簡短名稱。

* **主體名稱**

   帳戶的全文名稱。

* **密码**

   使用此帳戶存取CRX時需要。

* **ntlmhash**

   自動指派給每個新帳戶，並在密碼變更時更新。

* 您可以定義名稱、型別和值來新增屬性。 按一下每個新屬性的「儲存」（綠色勾號符號）。

**组成员资格**

這會顯示帳戶所屬的所有群組。 「已繼承」欄表示由於另一個群組的成員資格而繼承的成員資格。

按一下GroupID （可用時）將會開啟 [群組管理](#group-administration) 代表該群組。

**模拟者**

使用「模擬」功能時，使用者可以代表其他使用者工作。

這表示使用者帳戶可以指定可與其帳戶一起操作的其他帳戶（使用者或群組）。 換言之，如果允許使用者B模擬使用者A，則使用者B可以使用使用者A的完整帳戶詳細資訊（包括ID、名稱和存取許可權）來採取行動。

這可讓模擬者帳戶完成工作，就像他們正使用自己所模擬的帳戶一樣；例如，在短期休假或共用過多負載時。

如果帳戶模擬其他帳戶，則很難檢視。 記錄檔中沒有任何關於事件發生模擬的資訊。 因此，如果使用者B模擬使用者A，則所有事件看起來都像是使用者A個人執行的。

### 建立使用者帳戶 {#creating-a-user-account}

1. 開啟 **使用者管理** 對話方塊。
1. 按一下 **建立使用者**.
1. 然後您可以輸入「屬性」：

   * **使用者ID** 用作帳戶名稱。
   * **密碼** 登入時需要。
   * **主體名稱** 以提供完整的文字名稱。
   * **中繼路徑** 可用來形成樹狀結構。

1. 按一下「儲存」(Save) （綠色勾號）。
1. 此對話方塊將會展開，讓您可以：

   1. 設定 **屬性**.
   1. 另請參閱 **群組成員資格**.
   1. 定義 **模擬者**.

>[!NOTE]
>
>在同時擁有大量下列專案的安裝中註冊新使用者時，有時會導致效能損失：
>
>* 用户
>* 擁有許多成員的群組
>


### 更新使用者帳戶 {#updating-a-user-account}

1. 使用 **使用者管理** 對話方塊開啟所有帳戶的清單檢視。
1. 瀏覽樹狀結構。
1. 按一下所需的帳戶以開啟以進行編輯。
1. 進行變更，然後按一下該專案的「儲存」（綠色勾號符號）。
1. 按一下 **關閉** 完成，或 **清單……** 以返回所有使用者帳號的清單。

### 移除使用者帳戶 {#removing-a-user-account}

1. 使用 **使用者管理** 對話方塊開啟所有帳戶的清單檢視。
1. 瀏覽樹狀結構。
1. 選取所需的帳戶，然後按一下 **移除使用者**；帳戶將會立即刪除。

>[!NOTE]
>
>這會將這個主體的節點從存放庫中移除。
>
>不會移除存取許可權專案。 這可確保歷史完整性。

### 定義屬性 {#defining-properties}

您可以定義 **屬性** 對於新帳戶或現有帳戶：

1. 開啟 **使用者管理** 適當帳戶的對話方塊。
1. 定義 **屬性** 名稱。
1. 選取 **型別** 下拉式清單中的。
1. 定義 **值**.
1. 按一下新屬性的「儲存」（綠色的按一下符號）。

現有屬性可使用垃圾桶符號刪除。

除了密碼之外，屬性無法編輯，必須刪除並重新建立。

#### 變更密碼 {#changing-the-password}

此 **密碼** 是一個特殊屬性，按一下 **變更密碼** 連結。

您也可以將密碼變更為您自己的使用者帳戶，從 **安全性** CRX Explorer中的功能表。

### 定義模擬者 {#defining-an-impersonator}

您可以為新帳戶或現有帳戶定義「模擬者」：

1. 開啟 **使用者管理** 適當帳戶的對話方塊。
1. 指定要允許模擬該帳戶的帳戶。

   您可以使用「瀏覽……」來選取現有帳戶。

1. 按一下新屬性的「儲存」（綠色勾號符號）。

## 群組管理 {#group-administration}

標準對話方塊用於 **群組管理**.

您必須登入適當的工作區，才能從以下兩個位置存取對話方塊：

* 此 **群組管理** CRX主要主控台上的連結
* 此 **安全性** CRX Explorer的功能表

![chlimage_1-8](assets/chlimage_1-8.jpeg)

**属性**

* **群組ID**

   群組帳戶的簡短名稱。

* **主體名稱**

   群組帳戶的全文名稱。

* 您可以定義名稱、型別和值來新增屬性。 按一下每個新屬性的「儲存」（綠色勾號符號）。

* **成员**

   您可以將使用者或其他群組新增為此群組的成員。

**组成员资格**

這會顯示目前群組帳戶所屬的所有群組。 「已繼承」欄表示由於另一個群組的成員資格而繼承的成員資格。

按一下GroupID會開啟該群組的對話方塊。

**成员**

列出屬於目前群組成員的所有帳戶（使用者和/或群組）。

此 **已繼承** 欄指出由於另一個群組的成員資格而繼承的成員資格。

>[!NOTE]
>
>當所有者、編輯者或檢視者角色指派給任何資產資料夾的使用者時，就會建立新群組。 群組名稱的格式為 `mac-default-<foldername>` 針對每個已定義角色的資料夾。

### 建立群組帳戶 {#creating-a-group-account}

1. 開啟 **群組管理** 對話方塊。
1. 按一下 **建立群組**.
1. 然後您可以輸入「屬性」：

   * **主體名稱** 以提供完整的文字名稱。
   * **中繼路徑** 可用來形成樹狀結構。

1. 按一下「儲存」(Save) （綠色勾號）。
1. 此對話方塊將會展開，讓您可以：

   1. 設定 **屬性**.
   1. 另請參閱 **群組成員資格**.
   1. 管理 **成員**.

### 更新群組帳戶 {#updating-a-group-account}

1. 使用 **群組管理** 對話方塊開啟所有帳戶的清單檢視。
1. 瀏覽樹狀結構。
1. 按一下所需的帳戶以開啟以進行編輯。
1. 進行變更，然後按一下該專案的「儲存」（綠色勾號符號）。
1. 按一下 **關閉** 完成，或 **清單……** 以返回所有群組帳號的清單。

### 移除群組帳戶 {#removing-a-group-account}

1. 使用 **群組管理** 對話方塊開啟所有帳戶的清單檢視。
1. 瀏覽樹狀結構。
1. 選取所需的帳戶，然後按一下 **移除群組**；帳戶將會立即刪除。

>[!NOTE]
>
>這會將這個主體的節點從存放庫中移除。
>
>不會移除存取許可權專案。 這可確保歷史完整性。

### 定義屬性 {#defining-properties-1}

您可以為新帳戶或現有帳戶定義屬性：

1. 開啟 **群組管理** 適當帳戶的對話方塊。
1. 定義 **屬性** 名稱。
1. 選取 **型別** 下拉式清單中的。
1. 定義 **值**.
1. 按一下新屬性的「儲存」（綠色勾號符號）。

現有屬性可使用垃圾桶符號刪除。

### 成员 {#members}

您可以將成員新增至目前群組：

1. 開啟 **群組管理** 適當帳戶的對話方塊。
1. 可以任选其一：

   * 輸入所需成員的名稱（使用者或群組帳戶）。
   * 或使用 **瀏覽……** 搜尋並選取您要新增的主參與者（使用者或群組帳戶）。

1. 按一下新屬性的「儲存」（綠色勾號符號）。

或是刪除具有垃圾桶符號的現有成員。

## 存取許可權管理 {#access-right-management}

使用 **存取控制** CRXDE Lite標籤中，您可以定義存取控制原則並指派相關許可權。

例如， **目前路徑** 在左窗格中選取所需的資源，在右下窗格中選取「存取控制」標籤：

![crx_accesscontrol_tab](assets/crx_accesscontrol_tab.png)

原則會根據下列專案分類：

* **適用的存取控制原則**

   可以套用這些原則。

   這些是可建立本機原則的原則。 選取並新增適用原則後，它就會變成本機原則。

* **本地访问控制策略**

   這些是您已套用的存取控制原則。 然後，您可以更新、排序或移除這些專案。

   本機原則將會覆寫從父項繼承的任何原則。

* **有效的访问控制策略**

   這些是目前對任何存取請求有效的存取控制原則。 它們會顯示衍生自本機原則以及從父項繼承的任何彙總原則。

### 原則選擇 {#policy-selection}

可以為以下專案選取原則：

* **当前路径**

   如上述範例所示，選取存放庫內的資源。 將顯示此「目前路徑」的原則。

* **存储库**

   選取存放庫層級存取控制。 例如，設定 `jcr:namespaceManagement` 許可權，只與存放庫相關，與節點無關。

* **主体**

   在存放庫中註冊的主體。

   您可以輸入 **主體** 命名欄位或按一下欄位右側的圖示以開啟 **選取主體** 對話方塊。

   這可讓您 **搜尋** 對於 **使用者** 或 **群組**. 從產生的清單中選取所需的主參與者，然後按一下 **確定** 將值帶回上一個對話方塊。

![crx_accesscontrol_selectprincipal](assets/crx_accesscontrol_selectprincipal.png)

>[!NOTE]
>
>若要簡化管理，建議您為群組帳戶指派存取許可權，而非個別使用者帳戶。
>
>管理幾個群組比管理許多使用者帳戶更容易。

### 特权 {#privileges}

新增存取控制專案時，可選取下列許可權(請參閱 [安全性API](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/security/Privilege.html) 以取得完整詳細資訊)：

<table>
 <tbody>
  <tr>
   <th><strong>許可權名稱</strong></th>
   <th><strong>控制許可權的……</strong></th>
  </tr>
  <tr>
   <td><code>jcr:read</code></td>
   <td>擷取節點並讀取其屬性及其值。</td>
  </tr>
  <tr>
   <td><code>rep:write</code></td>
   <td>這是jcr：write和jcr：nodeTypeManagement的jackrabbit特定彙總許可權。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:all</code></td>
   <td>這是包含所有其他預先定義許可權的彙總許可權。</td>
  </tr>
  <tr>
   <td><strong>高级</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>crx:replicate</code></td>
   <td>執行節點的復寫。</td>
  </tr>
  <tr>
   <td><code>jcr:addChildNodes</code></td>
   <td>建立節點的子節點。</td>
  </tr>
  <tr>
   <td><code>jcr:lifecycleManagement</code></td>
   <td>在節點上執行生命週期作業。</td>
  </tr>
  <tr>
   <td><code>jcr:lockManagement</code></td>
   <td>鎖定和解鎖節點；重新整理鎖定。</td>
  </tr>
  <tr>
   <td><code>jcr:modifyAccessControl</code></td>
   <td>修改節點的存取控制原則。</td>
  </tr>
  <tr>
   <td><code>jcr:modifyProperties</code></td>
   <td>建立、修改和移除節點屬性。</td>
  </tr>
  <tr>
   <td><code>jcr:namespaceManagement</code></td>
   <td>註冊、取消註冊和修改名稱空間定義。</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeDefinitionManagement</code></td>
   <td>將節點型別定義匯入至存放庫。</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeManagement</code></td>
   <td>新增和移除mixin節點型別，並變更節點的主要節點型別。 這也包括任何對Node.addNode和XML匯入方法的呼叫，這些方法明確指定新節點的mixin或主要型別。</td>
  </tr>
  <tr>
   <td><code>jcr:readAccessControl</code></td>
   <td>讀取節點的存取控制原則。</td>
  </tr>
  <tr>
   <td><code>jcr:removeChildNodes</code></td>
   <td>移除節點的子節點。</td>
  </tr>
  <tr>
   <td><code>jcr:removeNode</code></td>
   <td>移除節點。</td>
  </tr>
  <tr>
   <td><code>jcr:retentionManagement</code></td>
   <td>在節點上執行保留管理作業。</td>
  </tr>
  <tr>
   <td><code>jcr:versionManagement</code></td>
   <td>在節點上執行版本設定作業。</td>
  </tr>
  <tr>
   <td><code>jcr:workspaceManagement</code></td>
   <td>透過JCR API建立和刪除工作區。</td>
  </tr>
  <tr>
   <td><code>jcr:write</code></td>
   <td>此彙總許可權包含：<br /> - jcr：modifyProperties<br /> - jcr：addChildNodes<br /> - jcr：removeNode<br /> - jcr：removeChildNodes</td>
  </tr>
  <tr>
   <td><code>rep:privilegeManagement</code></td>
   <td>註冊新許可權。</td>
  </tr>
 </tbody>
</table>

### 註冊新許可權 {#registering-new-privileges}

您也可以註冊新許可權：

1. 在工具列中選取 **工具**，則 **許可權** 以顯示目前註冊的許可權。

   ![ac_privileges](assets/ac_privileges.png)

1. 使用 **登入許可權** 圖示(**+**)以開啟對話方塊並定義新許可權：

   ![ac_privilegeregister](assets/ac_privilegeregister.png)

1. 按一下 **確定** 以儲存。 現在即可選取許可權。

### 新增存取控制專案 {#adding-an-access-control-entry}

1. 選取您的資源並開啟 **存取控制** 標籤。

1. 若要新增 **本機存取控制原則**，按一下 **+** 圖示右側 **適用的存取控制原則** 清單：

   ![crx_accesscontrol_applicable](assets/crx_accesscontrol_applicable.png)

1. 新專案會出現在 **本機存取控制原則：**

   ![crx_accesscontrol_newlocal](assets/crx_accesscontrol_newlocal.png)

1. 按一下 **+** 圖示以新增專案：

   ![crx_accesscontrol_addentry](assets/crx_accesscontrol_addentry.png)

   >[!NOTE]
   >
   >目前需要因應措施，才能指定空字串。
   >
   >為此，您需要使用「」。

1. 定義存取控制原則並按一下 **確定** 以儲存。 您的新原則將：

   * 列於 **本機存取控制原則**
   * 變更將會反映在 **有效的存取控制原則**.

CRX將會驗證您的選擇；對於指定的主體，指定節點上最多1個拒絕和1個允許專案。 實作一律會清除多餘的專案，並確保允許和拒絕專案中未列出相同的許可權。

### 排序本機存取控制原則 {#ordering-local-access-control-policies}

清單中的順序表示套用原則的順序。

1. 在表格中： **本機存取控制原則** 選取所需的專案，並將其拖曳至表格中的新位置。

   ![crx_accesscontrol_reorder](assets/crx_accesscontrol_reorder.png)

1. 變更將顯示在的這兩個表格中 **本機** 和 **有效的存取控制原則**.

### 移除存取控制原則 {#removing-an-access-control-policy}

1. 在表格中： **本機存取控制原則** 按一下專案右側的紅色圖示(-)。
1. 此專案會從兩個表格中移除， **本機** 和 **有效的存取控制原則**.

### 測試存取控制原則 {#testing-an-access-control-policy}

1. 從CRXDE Lite工具列選取 **工具**，則 **測試存取控制……**.
1. 新的對話方塊會在右上方窗格開啟。 選取 **路徑** 和/或 **主體** 您想要測試的物件。
1. 按一下 **測試** 若要檢視選取範圍的結果，請執行下列動作：

   ![crx_accesscontrol_test](assets/crx_accesscontrol_test.png)
