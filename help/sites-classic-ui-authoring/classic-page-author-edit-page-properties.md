---
title: 編輯頁面屬性
description: 頁面的屬性可能會因頁面的性質而異。 例如，某些頁面可能已連線至即時副本，而其他頁面未連線，因此即時副本資訊將可酌情使用。
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 26%

---

# 编辑页面属性{#editing-page-properties}

您可以为页面定义所需的属性。这些属性会因页面性质而异。例如，某些页面可能会连接到 Live Copy，而其他页面则可能不会，Live Copy 信息将在适当情况下才可用。

## 页面属性 {#page-properties}

屬性分佈於數個索引標籤中：

### 基本 {#basic}

* **标题**

   頁面的標題會顯示在各種位置。 例如， **網站** 索引標籤清單和 **網站** 卡片/清單檢視。

   这是必填字段。

* **标记**

   您可以在此處更新選取方塊中的清單，從頁面新增或移除標籤：

   * 选择标记后，它会列在选择框下。您可以使用“x”从此列表中移除标记。
   * 可通过在空白选择框中键入名称输入全新标记。

      當您按下Enter鍵時，實際將會建立新標籤。 然後，新標籤將顯示在方塊中，右側有一個小星號，表示它是新標籤。

   * 使用下拉列表功能，可从现有标记中进行选择。
   * 當您將滑鼠移到選取方塊中的標籤專案上時，會出現x；這可用來移除此頁面的該標籤。

* **隐藏导航**

   切換開關可指示頁面在頁面導覽中顯示或隱藏。

* **页面标题**

   頁面上使用的標題。

* **导航标题**

   您可以指定個別標題以在導覽中使用（例如，如果您想要更簡潔的內容）。 如果為空， **標題** 將會使用。

* **子标题**

   頁面上使用的副標題。

* **描述**

   頁面的說明、用途或您要新增的任何其他詳細資訊。

* **开始时间**

   啟動已發佈頁面的日期和時間。 發佈後，此頁面將保持休眠狀態，直到指定的時間。

   對於您要立即發佈的頁面（一般情境），請將這些欄位留空。

* **结束时间**

   已發佈頁面將停用的時間。

   同樣地，請將這些欄位留空，以便您立即發佈頁面。

* **虚 URL**

   可讓您輸入此頁面的虛名URL。 這可讓您擁有更短且更有表現力的URL。

   例如，如果虛名URL設為w `elcome`至路徑/所識別的頁面 `v1.0/startpage`網站h `ttp://example.com,` 然後h `ttp://example.com/welcome`會是h的虛名URL `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >虚 URL：
   >
   >* 必須是唯一的，因此您應該注意該值尚未被其他頁面使用。
   >* 不支援規則運算式模式。


* **重定向虚 URL**

   指示您是否希望页面使用虚 URL。

### 高级 {#advanced}

* **语言**

   頁面語言。

* **重定向**

   指出此頁面應該自動重新導向的頁面。

* **Design**

   指出 [設計](/help/sites-developing/designer.md) 用於此頁面。

* **别名**

   指定要用於此頁面的別名。

* **启用已关闭的用户组**

   啟用（或停用）使用 [封閉式使用者群組](/help/sites-administering/cug.md) (CUG)。

* **登录页面**

   用於登入的頁面。

* **公认组**

   有資格登入CUG的群組。

* **领域**

   CUG的領域名稱。

* **导出配置**

   指定匯出設定。

### 缩略图 {#thumbnail}

* **页面缩略图**

   顯示頁面縮圖影像。 您可以：

   * **生成预览**

      產生頁面預覽，以做為縮圖使用。

   * **上传图像**

      上傳要當作縮圖的影像。

### Cloud Service {#cloud-services}

* **Cloud Service**

   定義屬性 [雲端服務](/help/sites-developing/extending-cloud-config.md).

### 个性化 {#personalization}

* **个性化**

   选择一个[品牌以指定定位的范围](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。

### 权限 {#permissions}

* **許可權** （觸控最佳化的UI）

   檢視 [有效許可權和新增許可權](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   在中定義Blueprint頁面的屬性 [多網站管理](/help/sites-administering/msm.md). 控制將修改傳播至即時副本的情況。

### Live Copy {#live-copy}

* **Live Copy**

   在中定義即時副本頁面的屬性 [多網站管理](/help/sites-administering/msm.md). 控制從Blueprint傳播修改的情況。

### 站点结构 {#site-structure}

* 提供具有全站点功能的页面的链接，例如&#x200B;**注册页面**、**脱机页面**&#x200B;以及其他。

## 编辑页面属性 {#editing-page-properties-2}

### 編輯特定頁面的頁面屬性 {#editing-page-properties-for-a-specific-page}

頁面屬性可定義頁面的各種屬性，例如標題，當這些屬性出現在網站和其他專案上時。

1. 開啟您要編輯的頁面。

1. 在sidekick中開啟 **頁面** 索引標籤然後選取 **頁面屬性……**

   這會開啟含有多個索引標籤的對話方塊。

1. 進行您需要的變更，然後按一下 **確定** 以儲存。
