---
title: Adobe 分类
seo-title: Adobe Classifications
description: 瞭解Adobe分類。
seo-description: Learn about Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 7%

---

# Adobe 分类{#adobe-classifications}

Adobe分類會將分類資料匯出至 [Adobe Analytics](/help/sites-administering/adobeanalytics.md) 以排程方式進行。 匯出程式是 **com.adobe.cq.scheduled.exporter.Exporter**.

若要設定此專案：

1. 使用 **導覽**，選取 **工具**， **Cloud Services**，則 **舊版Cloud Services**.
1. 捲動至 **Adobe Analytics** 並選取 **顯示設定**.
1. 按一下 **[+]** Adobe Analytics設定旁的連結。

1. 在 **建立框架** 對話方塊：

   * 指定&#x200B;**标题**。
   * 您可選擇指定 **名稱**，適用於將架構詳細資料儲存在存放庫中的節點。
   * 選取 **Adobe Analytics分類**

   然後按一下 **建立**.

   ![建立框架對話方塊](assets/aa-25.png)

1. 此 **分類設定** 對話方塊會開啟以進行編輯。

   ![分類設定對話方塊](assets/aa-classifications-settings.png)

   屬性包括下列各項：

   | **字段** | **描述** |
   |---|---|
   | 启用 | 選取 **是** 以啟用「Adobe分類」設定。 |
   | 发生冲突时覆盖 | 選取 **是** 覆寫任何資料衝突。 根據預設，此設定為 **否**. |
   | 删除已处理的项目 | 若設為 **是**，會在匯出處理後刪除節點。 預設值為 **False**. |
   | 导出作业描述 | 輸入「Adobe分類」工作的說明。 |
   | 通知電子郵件 | 輸入Adobe分類通知的電子郵件地址。 |
   | 报表包 | 輸入要執行匯入工作的報表套裝。 |
   | 数据集 | 輸入要執行匯入作業的資料集關係ID。 |
   | 转换程序 | 從下拉式功能表中，選取轉換器實作。 |
   | 数据源 | 導覽至資料容器的路徑。 |
   | 导出时间表 | 選取匯出的排程。 預設為每30分鐘。 |

1. 按一下 **確定** 以儲存您的設定。

## 修改頁面大小 {#modifying-page-size}

系統會在頁面中處理記錄。 根據預設，「Adobe分類」會建立頁面大小為1000的頁面。

根據Adobe分類中的定義，頁面大小上限可25000，並可從Felix主控台修改。 在匯出期間，「Adobe分類」會鎖定來源節點，以防止同時進行修改。 節點會在匯出後、發生錯誤時或工作階段關閉時解除鎖定。

若要變更頁面大小：

1. 瀏覽至OSGI主控台，網址為 **https://&lt;host>：&lt;port>/system/console/configMgr** 並選取 **AdobeAEM分類匯出程式**.

   ![aa-26](assets/aa-26.png)

1. 更新 **匯出頁面大小** 視需要，然後按一下 **儲存**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>「Adobe分類」先前稱為「SAINT匯出工具」。

匯出工具可使用轉換器將匯出資料轉換為特定格式。 對於「Adobe分類」，為子介面 `SAINTTransformer<String[]>` 已提供實作轉換器介面。 此介面用於將資料型別限製為 `String[]` 供SAINTAPI使用，並具有標籤介面來尋找可供選取的此類服務。

在預設實作SAINTDefaultTransformer中，匯出程式來源的子資源會被視為記錄，而屬性名稱會被視為索引鍵，而屬性值則會被視為值。 此 **金鑰** 欄會自動新增為第一欄 — 其值將是節點名稱。 名稱空間屬性(包含 `:`)會被忽略。

*節點結構：*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * 產品=我的產品名稱（字串）
      * 價格= 120.90 （字串）
      * 大小= M （字串）
      * 顏色=黑色（字串）
      * Color^Code = 101 （字串）

**SAINT標題和記錄：**

| **键** | **产品** | **价格** | **大小** | **颜色** | **Color^Code** |
|---|---|---|---|---|---|
| 1 | 我的產品名稱 | 120.90 | M | black | 101 |

屬性包括下列各項：

<table>
 <tbody>
  <tr>
   <td><strong>屬性路徑</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>轉換器</td>
   <td>SAINTTransformer實作的類別名稱</td>
  </tr>
  <tr>
   <td>电子邮件</td>
   <td>通知電子郵件地址。</td>
  </tr>
  <tr>
   <td>報告套裝</td>
   <td>執行匯入作業的報表套裝ID。 </td>
  </tr>
  <tr>
   <td>資料集</td>
   <td>執行匯入作業的資料集關係ID。 </td>
  </tr>
  <tr>
   <td>说明</td>
   <td>工作說明。 <br /> </td>
  </tr>
  <tr>
   <td>覆盖</td>
   <td>標幟以覆寫資料衝突。 預設為 <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>checkdivision</td>
   <td>用於檢查報表套裝相容性的旗標。 預設為 <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>標幟以在匯出後刪除已處理的節點。 預設為 <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## 自動化Adobe分類匯出 {#automating-adobe-classifications-export}

您可以建立自己的工作流程，讓任何新的匯入都能啟動工作流程，以在中建立適當且結構正確的資料 **/var/export/** 以便將其匯出至「Adobe分類」。
