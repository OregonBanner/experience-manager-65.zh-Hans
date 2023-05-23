---
title: 將使用者資料中的資訊新增至表單提交中繼資料
seo-title: Adding information from user data to form submission metadata
description: 瞭解如何使用使用者提供的資料，將資訊新增至已提交表單的中繼資料。
seo-description: Learn how to add information to metadata of a submitted form with user provided data.
uuid: c3eea3c0-31f8-4bf8-b5cf-34f907bdbdba
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
feature: Adaptive Forms
exl-id: 5ca850e3-30f0-4384-b615-356dc3c2ad0d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# 將使用者資料中的資訊新增至表單提交中繼資料{#adding-information-from-user-data-to-form-submission-metadata}

您可以使用在表單元素中輸入的值，計算草稿或表單提交的中繼資料欄位。 中繼資料可讓您根據使用者資料篩選內容。 例如，使用者在您的表單名稱欄位中輸入John Doe。 您可以使用此資訊來計算中繼資料，該中繼資料可以將此提交分類在首字母縮寫JD下。

若要使用使用者輸入的值計算中繼資料欄位，請在中繼資料中新增表單的元素。 當使用者在該元素中輸入值時，指令碼會使用該值來計算資訊。 此資訊會新增至中繼資料。 將元素新增為中繼資料欄位時，需提供索引鍵。 索引鍵會新增為中繼資料中的欄位，而計算資訊會根據該索引鍵記錄。

例如，健康保險公司會發佈表單。 在此表單中，欄位會擷取一般使用者的年齡。 當有多位使用者提交表單後，客戶想要檢查特定年齡範圍內所有提交的表單。 額外的中繼資料可協助客戶，而不是處理隨著表單數量增加而複雜化的所有資料。 表單作者可以設定將一般使用者填入的屬性/資料儲存在最上層，以便進行最輕鬆的搜尋。 其他中繼資料是儲存在中繼資料節點最上層之使用者填寫的資訊，如作者所設定。

再來看看擷取電子郵件ID和電話號碼的表單的另一個範例。 當使用者匿名造訪此表單並放棄表單時，作者可以設定表單以自動儲存電子郵件ID和電話號碼。 此表單會自動儲存，而電話號碼和電子郵件ID會儲存在草稿的中繼資料節點中。 此設定的使用案例是銷售機會管理控制面板。

## 將表單元素新增至中繼資料 {#adding-form-elements-to-metadata}

執行以下步驟，在中繼資料中新增元素：

1. 在編輯模式中開啟最適化表單。\
   若要以編輯模式開啟您的表單，請在表單管理員中，選取您的表單並點選 **開啟**.
1. 在編輯模式中，選取元件，點選 ![欄位層級](assets/field-level.png) > **最適化表單容器**，然後點選 ![cmppr](assets/cmppr.png).
1. 在側邊欄中，按一下 **中繼資料**.
1. 在中繼資料區段中，按一下 **新增**.
1. 使用「中繼資料」標籤的「值」欄位來新增指令碼。 您新增的指令碼會從表單上的元素收集資料，並計算饋送至中繼資料的值。

   例如， **true** 如果輸入的年齡大於21歲，則會記錄在中繼資料中，並且 **false** 小於21時記錄。 在「中繼資料」標籤中輸入下列指令碼：

   `(agebox.value >= 21) ? true : false`

   ![中繼資料指令碼](assets/add-element-metadata.png)

   在中繼資料標籤中輸入的指令碼

1. 单击&#x200B;**确定**。

使用者在選取為中繼資料欄位的元素中輸入資料後，計算的資訊會記錄在中繼資料中。 您可以在您設定儲存中繼資料的儲存庫中檢視中繼資料。

## 檢視更新的表單提交中繼資料： {#seeing-updated-form-nbsp-submission-metadata}

以上例為例，中繼資料會儲存在CRX存放庫中。 中繼資料看起來像這樣：

![元数据](assets/metadata_entry_new.png)

如果您在中繼資料中新增核取方塊元素，選取的值會儲存為逗號分隔字串。 例如，您在表單中新增核取方塊元件，並將其名稱指定為 `checkbox1`. 在核取方塊元件屬性中，您可新增值0、1和2的「駕駛執照」、「社會安全號碼」和「護照」專案。

![從核取方塊儲存多個值](assets/checkbox-metadata.png)

您選取最適化表單容器，然後在表單屬性中新增中繼資料索引鍵 `cb1` 哪些儲存 `checkbox1.value`，並發佈表單。 當客戶填寫表單時，客戶會在核取方塊欄位中選取「護照和社會安全號碼」選項。 值1和2在提交中繼資料的cb1欄位中儲存為1、2。

![在核取方塊欄位中選取多個值的中繼資料專案](assets/metadata-entry.png)

>[!NOTE]
>
>上述範例僅供學習之用。 請確定您在AEM Forms實作中設定的正確位置尋找中繼資料。
