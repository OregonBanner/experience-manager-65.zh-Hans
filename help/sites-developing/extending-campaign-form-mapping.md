---
title: 建立自訂表單對應
seo-title: Creating Custom Form Mappings
description: 在Adobe Campaign中建立自訂表格時，您可能想要在AEM中建立對應至該自訂表格的表單
seo-description: When you create a custom table in Adobe Campaign, you may want to build a form in AEM that maps to that custom table
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# 建立自訂表單對應{#creating-custom-form-mappings}

在Adobe Campaign中建立自訂表格時，您可能想要在AEM中建立對應至該自訂表格的表單。

本檔案說明如何建立自訂表單對應。 完成本檔案中的步驟後，您將會為使用者提供事件頁面，讓他們註冊即將舉行的事件。 然後您可以透過Adobe Campaign跟進這些使用者。

## 前提条件 {#prerequisites}

您必須安裝下列專案：

* Adobe Experience Manager
* Adobe Campaign Classic

另請參閱 [將AEM與Adobe Campaign Classic整合](/help/sites-administering/campaignonpremise.md) 以取得詳細資訊。

## 建立自訂表單對應 {#creating-custom-form-mappings-2}

若要建立自訂表單對應，您必須依照以下各節中詳細說明的這些高階步驟操作：

1. 建立自訂表格。
1. 擴充 **種子** 表格。
1. 建立自訂對應。
1. 根據自訂對應建立傳遞。
1. 在AEM中建立表單，此表單將使用建立的傳送。
1. 提交表單以進行測試。

### 在Adobe Campaign中建立自訂表格 {#creating-the-custom-table-in-adobe-campaign}

首先，在Adobe Campaign中建立自訂表格。 在此範例中，我們使用以下定義來建立事件表格：

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

建立事件表格後，請執行 **更新資料庫結構精靈** 以建立表格。

### 延伸種子表 {#extending-the-seed-table}

在Adobe Campaign中，點選/按一下 **新增** 若要建立 **種子地址(nms)** 表格。

![chlimage_1-194](assets/chlimage_1-194.png)

現在，使用 **事件** 表格以擴充 **種子** 表格：

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

之後，執行 **更新資料庫精靈** 以套用變更。

### 建立自訂目標對應 {#creating-custom-target-mapping}

在 **管理/行銷活動管理** t，前往 **目標對應** 並新增一個T **目標對應。**

>[!NOTE]
>
>請務必使用有意義的名稱 **內部名稱**.

![chlimage_1-195](assets/chlimage_1-195.png)

### 建立自訂傳遞範本 {#creating-a-custom-delivery-template}

在此步驟中，您會新增使用建立的傳遞範本 **目標對應**.

在 **資源/範本**，導覽至傳遞範本並複製現有的AEM傳遞。 當您按一下 **至**，選取建立事件 **目標對應**.

![chlimage_1-196](assets/chlimage_1-196.png)

### 在AEM中建立表單 {#building-the-form-in-aem}

在AEM中，確定您已設定Cloud Service於 **頁面屬性**.

然後，在 **Adobe Campaign** 索引標籤中，選取在中建立的傳遞 [建立自訂傳遞範本](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

設定欄位時，請務必為表單欄位指定唯一的元素名稱。

設定欄位後，您需要手動變更對應。

在CRXDE-lite中，移至 **jcr：content** （頁面）節點並變更 **acMapping** 的內部名稱的值 **目標對應**.

![chlimage_1-198](assets/chlimage_1-198.png)

在表單的設定中，確定勾選核取方塊以建立（如果不存在）

![chlimage_1-199](assets/chlimage_1-199.png)

### 提交表單 {#submitting-the-form}

您現在可以提交表單，並在Adobe Campaign端驗證值是否已儲存。

![chlimage_1-200](assets/chlimage_1-200.png)

## 疑难解答 {#troubleshooting}

**「元素&#39;@eventdate&#39;的值&#39;02/02/2015&#39;的型別無效(型別為&#39;Event ([adb：event])&#39;)」**

提交表單時，此錯誤會記錄在 **error.log** 在AEM中。

這是由於日期欄位的格式無效。 因應措施是提供 **yyyy-mm-dd** 做為值。
