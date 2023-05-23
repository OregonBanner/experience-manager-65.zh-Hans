---
title: 許可權管理的主體檢視
seo-title: Principal View for Permissions Management
description: 瞭解有助於許可權管理的新觸控式UI介面。
seo-description: Learn about the new Touch UI interface that facilitates permissions management.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 1%

---

# 許可權管理的主體檢視{#principal-view-for-permissions-management}

## 概述 {#overview}

AEM 6.5引進了使用者和群組的許可權管理。 主要功能與傳統UI相同，但更加方便使用者且更有效率。

## 使用方法 {#how-to-use}

### 存取UI {#accessing-the-ui}

透過「安全性」下的「許可權」卡存取新的UI型許可權管理，如下所示：

![](assets/screen_shot_2019-03-17at63333pm.png)

新檢視可讓您更輕鬆地檢視所有已明確授予許可權的路徑中指定主體的整個許可權集和限制。 如此一來，您就不需要前往

CRXDE可管理進階許可權和限制。 它已在相同檢視中合併。 該檢視預設為「每個人」群組。

![](assets/unu-1.png)

有一個篩選器可讓使用者選取要檢視的主體型別 **使用者**， **群組**，或 **全部**&#x200B;並搜尋任何主體&#x200B;**.**

![](assets/image2019-3-20_23-52-51.png)

### 檢視主體許可權 {#viewing-permissions-for-a-principal}

左側框架可讓使用者向下捲動以尋找任何主參與者，或根據選取的篩選器搜尋「群組」或「使用者」，如下所示：

![](assets/doi-1.png)

按一下名稱會在右側顯示指派的許可權。 許可權窗格會顯示特定路徑上的存取控制專案清單以及設定的限制。

![](assets/trei-1.png)

### 新增主要專案的存取控制專案 {#adding-new-access-control-entry-for-a-principal}

按一下「新增ACE」按鈕，即可新增新的存取控制專案，以新增許可權。

![](assets/patru.png)

這會顯示以下視窗，下一步是選擇需要設定許可權的路徑。

![](assets/cinci-1.png)

在此處，我們選取要設定許可權的路徑 **dam-users**：

![](assets/sase-1.png)

選取路徑後，工作流程會返回此畫面，使用者可在其中從可用名稱空間選取一或多個許可權(例如 `jcr`， `rep` 或 `crx`)，如下所示。

您可以使用文字欄位進行搜尋，然後從清單中選取，以新增許可權。

>[!NOTE]
>
>如需完整的許可權和說明清單，請參閱 [此頁面](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

選取許可權清單後，使用者可以選擇許可權型別：拒絕或允許，如下所示。

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### 使用限制 {#using-restrictions}

除了指定路徑上的許可權清單和許可權型別之外，此畫面還允許新增細粒度存取控制的限制，如下所示：

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>如需每個限制含義的詳細資訊，請參閱 [Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

您可以選取限制型別、輸入值並按一下 **+** 圖示。

![](assets/sapte-1.png) ![](assets/opt-1.png)

新的ACE會反映在「存取控制清單」中，如下所示。 請注意 `jcr:write` 是包含下列專案的彙總許可權 `jcr:removeNode` 以上所新增，但並未在下方顯示為其涵蓋的內容 `jcr:write`.

### 編輯ACE {#editing-aces}

選取主參與者並選擇您要編輯的ACE，即可編輯「存取控制專案」。

舉例來說，我們可以編輯以下專案 **dam-users** 按一下右側的鉛筆圖示：

![新增限制](assets/image2019-3-21_0-35-39.png)

編輯畫面中會顯示預先選取的已設定ACE，按一下它們旁邊的交叉圖示可以刪除它們，或者可以為給定路徑新增許可權，如下所示。

![編輯專案](assets/noua-1.png)

在此處，我們將新增 `addChildNodes` 許可權： **dam-users** 在指定路徑上。

![](assets/image2019-3-21_0-45-35.png)

按一下「 」以儲存變更 **儲存** 按鈕，而變更將反映在**dam-users的新許可權中**如下所示：

![](assets/zece-1.png)

### 刪除ACE {#deleting-aces}

可以刪除存取控制專案，以移除授予特定路徑上主要者的所有許可權。 ACE旁的X圖示可用來刪除它，如下所示：

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### 傳統UI許可權組合 {#classic-ui-privilege-combinations}

請注意，新許可權UI明確使用基本許可權集，而不是預先定義的組合，這些組合併未真正反映授與的確切基礎許可權。

這會導致混淆，無法確定確切的設定內容。 下表列出從傳統UI的許可權組合與組成這些組合的實際許可權之間的對應：

<table>
 <tbody>
  <tr>
   <th>傳統UI許可權組合</th>
   <th>許可權UI許可權</th>
  </tr>
  <tr>
   <td>读取</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>创建</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>删除</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>读取 ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>编辑 ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>复制</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
