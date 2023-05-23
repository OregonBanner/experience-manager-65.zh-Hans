---
title: 配置和配置浏览器
description: 瞭解AEM設定，以及這些設定如何管理AEM中的工作區設定。
exl-id: 1be5849b-748c-48e8-afa8-35a9026c27b3
source-git-commit: 84b16dd1a60f731b568dd87ef89699875cb86596
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 6%

---

# 配置和配置浏览器 {#configuration-browser}

AEM設定可管理AEM中的設定，並作為工作區。

## 什么是配置？ {#what-is-a-configuration}

可以從兩個不同的觀點來考慮設定。

* [管理員](#configurations-administrator) 使用設定作為AEM內的工作區，以定義和管理設定群組。
* [開發人員](#configurations-developer) 使用實作設定的基礎設定機制，以在AEM中儲存和查詢設定。

摘要：從管理員的觀點來看，設定是您建立工作區以管理AEM中設定的方式，而開發人員應瞭解AEM如何使用和管理存放庫中的這些設定。

無論您如何認為，設定在AEM中有兩個主要用途：

* 設定可為特定使用者群組啟用某些功能。
* 設定會定義這些功能的存取權。

## 管理員設定 {#configurations-administrator}

AEM管理員和作者可以將設定視為工作區。 藉由實作這些功能的存取許可權，這些工作區可用來將設定群組及其關聯內容收集在一起，以供組織使用。

可為AEM中的許多不同功能建立設定。

* [云配置](/help/sites-administering/configurations.md)
* [上下文中心區段](/help/sites-administering/segmentation.md)
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [可编辑模板](/help/sites-authoring/templates.md)

### 示例 {#administrator-example}

例如，管理員可以為可編輯的範本建立兩個設定。

* WKND — 一般
* WKND-Magazine

然後，管理員可以使用WKND-General設定建立一般頁面範本，然後使用WKND-Magazine底下的雜誌專用範本。

然後，管理員可以將WKND-General與WKND網站的所有內容相關聯。 不過，WKND-Magazine設定只會與雜誌網站相關聯。

藉由執行下列動作：

* 內容作者為雜誌建立新頁面時，作者可以選擇一般範本(WKND-General)或雜誌範本(WKND-Magazine)。
* 當內容作者為網站中其他非雜誌部分建立新頁面時，作者只能從一般範本(WKND-General)中選擇。

類似設定不僅適用於可編輯的範本，也可用於雲端設定、ContextHub區段和內容片段模型。

### 使用設定瀏覽器 {#using-configuration-browser}

設定瀏覽器可讓管理員輕鬆建立、管理及設定AEM中設定的存取許可權。

>[!NOTE]
>
>只有在您的使用者擁有 `admin` 權利。 `admin` 為了指派存取權給設定或修改設定，也需要許可權。

#### 创建配置 {#creating-a-configuration}

使用設定瀏覽器，在AEM中建立新設定非常簡單。

1. 登入AEMas a Cloud Service，並從主功能表選取 **工具** -> **一般** -> **設定瀏覽器**.
1. 点按或单击&#x200B;**创建**。
1. 提供配置的&#x200B;**标题**&#x200B;和&#x200B;**名称**。

   ![创建配置](assets/configuration-create.png)

   * **标题**&#x200B;应为描述性的。
   * **名称**&#x200B;将成为存储库中的节点名称。
      * 它会根据标题自动生成，并根据 [AEM 命名约定](/help/sites-developing/naming-conventions.md)进行调整。
      * 如有必要可以调整。
1. 檢查您要允許的設定型別。
   * [云配置](/help/sites-administering/configurations.md)
   * [上下文中心區段](/help/sites-administering/segmentation.md)
   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [可编辑模板](/help/sites-authoring/templates.md)
1. 点按或单击&#x200B;**创建**。

>[!TIP]
>
>設定可以巢狀。

#### 編輯設定及其存取許可權 {#access-rights}

如果您將設定視為工作區，可以對這些設定設定設定存取許可權，以強制誰可以存取這些工作區，誰則不能存取。

1. 登入AEMas a Cloud Service，並從主功能表選取 **工具** -> **一般** -> **設定瀏覽器**.
1. 選取您要修改的設定，然後點選或按一下 **屬性** 工具列中的。
1. 選取您要新增至設定的任何其他功能
   >[!NOTE]
   >
   >建立設定後，無法取消選取功能。
1. 使用 **有效許可權** 按鈕以檢視角色及其目前授與設定的許可權矩陣。
   ![有效許可權視窗](assets/configuration-effective-permissions.png)
1. 若要指派新許可權，請在 **選取使用者或群組** 中的欄位 **新增許可權** 區段。
   * 此  **選取使用者或群組** 欄位可根據現有使用者和角色提供自動完成功能。
1. 從自動完成結果中選取適當的使用者或角色。
   * 您可以選取多個使用者或角色。
1. 檢查所選使用者或角色應具有的存取選項，然後按一下 **新增**.
   ![將存取權新增至設定](assets/configuration-edit.png)
1. 重複這些步驟以選取使用者或角色，並視需要指派其他存取許可權。
1. 點選或按一下 **儲存並關閉** 完成後。

## 開發人員設定 {#configurations-developer}

作為開發人員，請務必瞭解AEMas a Cloud Service如何處理設定，以及它如何處理設定解析。

### 設定與內容分離 {#separation-of-config-and-content}

雖然 [管理員和使用者可能會將設定視為工作區](#configurations-administrator) 若要管理不同的設定和內容，請務必瞭解設定和內容是由AEM在存放庫中個別儲存和管理的。

* `/content` 是所有內容的首頁。
* `/conf` 是所有設定的首頁。

內容透過參考其關聯設定 `cq:conf` 屬性。 AEM會根據內容和內容內容執行查詢 `cq:conf` 屬性以尋找適當的設定。

### 示例 {#developer-example}

在此範例中，假設您有一些對DAM設定感興趣的應用程式程式碼。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有設定查詢的起點是內容資源，通常位於下的某個位置 `/content`. 這可能是頁面、頁面內的元件、資產或DAM資料夾。 這是我們尋找適用於此內容的正確設定的實際內容。

現在使用 `Conf` 物件時，我們可以擷取我們感興趣的特定組態專案。 在此案例中為 `dam/imageserver`，此為與下列專案相關之設定的集合： `imageserver`. 此 `getItem` 呼叫傳回 `ValueMap`. 然後我們會閱讀 `bgkcolor` 字串屬性，並提供「FFFFFF」預設值，以防屬性（或整個設定專案）不存在。

現在來看看對應的JCR內容：

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

在此範例中，我們假設這裡有WKND特定的DAM資料夾以及對應的設定。 從該資料夾開始 `/content/dam/wknd`，我們會看到有一個名為的字串屬性 `cq:conf` 會參照應該套用至子樹狀結構的設定。 屬性通常設定在 `jcr:content` 資產資料夾或頁面的URL。 這些 `conf` 連結是明確的，因此只要檢視CRXDE中的內容，就能輕鬆追蹤連結。

跳入 `/conf`，我們會依循參考資料檢視 `/conf/wknd` 節點。 此為設定。 請注意，其查詢對應用程式程式碼是完全透明的。 範常式式碼從未有專屬參照，而是隱藏在 `Conf` 物件。 要套用哪個設定，需透過JCR內容完全控制。

我們看到設定包含固定名稱 `settings` 包含實際專案的節點，包括 `dam/imageserver` 在我們的案例中需要。 此類專案可視為「設定檔案」，通常以 `cq:Page` 包含 `jcr:content` 儲存實際內容。

最後，我們會看到屬性 `bgkcolor` 程式碼範例所需的專案。 此 `ValueMap` 我們從「 」回來 `getItem` 根據頁面的 `jcr:content` 節點。

### 設定解析度 {#configuration-resolution}

上述基本範例顯示單一設定。 但在許多情況下，您會想要有不同的設定，例如預設全域設定、每個品牌的不同設定，以及子專案的特定設定。

為了支援此功能，AEM中的設定查閱具有繼承和遞補機制，其優先順序如下：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * 參考自以下專案的特定設定： `cq:conf` 中的某處 `/content`
   * 階層是任意的，而且可以像您的網站結構一樣設計，知道這一點不是應用程式程式碼的事
   * 可由具有設定許可權的使用者在執行階段變更
1. `/conf/<siteconfig>/<parentconfig>`
   * 周遊後援設定的父項
   * 可由具有設定許可權的使用者在執行階段變更
1. `/conf/<siteconfig>`
   * 周遊後援設定的父項
   * 可由具有設定許可權的使用者在執行階段變更
1. `/conf/global`
   * 系統全域設定
   * 通常為安裝的全域預設值
   * 設定者 `admin` 角色
   * 可由具有設定許可權的使用者在執行階段變更
1. `/apps`
   * 應用程式預設值
   * 已透過應用程式部署修正
   * 在執行階段為唯讀
1. `/libs`
   * AEM產品預設值
   * 僅可由Adobe變更，不允許專案存取
   * 已透過應用程式部署修正
   * 在執行階段為唯讀

### 使用設定 {#using-configurations}

AEM中的設定是以Sling內容感知設定為基礎。 Sling套件組合提供的服務API可用於取得內容感知設定。 內容感知設定是與內容資源或資源樹狀結構相關的設定 [如上一個範例所述。](#developer-example)

如需內容感知設定、範例及使用方式的詳細資訊， [請參閱Sling檔案。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web主控台 {#confmgr-web-console}

為了進行偵錯和測試，我們提供 **ConfMgr** Web主控台： `https://<host>:<port>/system/console/conf`，可顯示指定路徑/專案的設定。

![ConfMgr](assets/configuration-confmgr.png)

只要提供：

* **内容路径**
* **项目**
* **用户**

按一下 **解決** 檢視已解析的設定，並接收將解析這些設定的範常式式碼。

### 內容感知設定Web主控台 {#context-aware-web-console}

為了進行偵錯和測試，我們提供 **內容感知設定** Web主控台： `https://<host>:<port>/system/console/slingcaconfig`，可查詢存放庫中的內容感知設定並檢視其屬性。

![內容感知設定Web主控台](assets/configuration-context-aware-console.png)

只要提供：

* **内容路径**
* **設定名稱**

按一下 **解決** 以擷取所選組態的關聯內容路徑和屬性。
