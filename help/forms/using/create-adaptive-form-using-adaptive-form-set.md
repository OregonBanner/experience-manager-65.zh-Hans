---
title: 使用一組最適化表單建立最適化表單
seo-title: Create an adaptive form using a set of adaptive forms
description: 透過AEM Forms，將最適化表單集合在一起，以製作單一大型最適化表單，並瞭解其功能。
seo-description: With AEM Forms, bring adaptive forms together to author a single large adaptive form, and understand its features.
uuid: e52e4f90-8821-49ec-89ff-fbf07db69bd2
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 264aa8c0-ba64-4768-b3d1-1b9baa6b4d72
docset: aem65
feature: Adaptive Forms
exl-id: 4254c2cb-66cc-4a46-b447-bc5e32def7a0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# 使用一組最適化表單建立最適化表單{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## 概述 {#overview}

在工作流程中（例如開立銀行帳戶的應用程式），您的使用者會填寫多個表單。 與其要求他們填寫一組表格，您可以將表格棧疊在一起並建置大型表格（父級表格）。 將最適化表單新增至較大表單時，會新增為面板（子表單）。 新增一組子表單以建立父表單。 您可以根據使用者輸入顯示或隱藏面板。 父表單的按鈕（例如提交和重設）會覆寫子表單的按鈕。 若要在父表單中新增自適應表單，您可以從資產瀏覽器中拖放自適應表單（如自適應表單片段）。

可用的功能包括：

* 獨立製作
* 顯示/隱藏適當的表單
* 延遲載入

與使用個別元件建立父項表單相比，獨立編寫和延遲載入等功能可提供效能改善。

>[!NOTE]
>
>您不可以使用XFA型最適化表單/片段做為子表單或父表單。

## 幕後 {#behind-the-scenes}

您可以在父表單中新增XSD型最適化表單和片段。 上層表單的結構與 [任何最適化表單](../../forms/using/prepopulate-adaptive-form-fields.md). 將最適化表單新增為子表單時，它會新增為父表單中的面板。 繫結子表單的資料儲存在 `data`的根目錄 `afBoundData` 上層表單XML結構描述的部分。

例如，您的客戶填寫申請表。 表單的前兩個欄位是名稱和身分。 其XML為：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

您在應用程式中新增另一個表單，讓您的客戶填寫其辦公室地址。 子表單的結構描述根目錄為 `officeAddress`. 套用 `bindref` `/application/officeAddress` 或 `/officeAddress`. 若 `bindref`未提供，則子表單將新增為 `officeAddress` 子樹。 請參閱下列格式的XML：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

如果您插入其他可讓客戶提供住家地址的表單，請套用 `bindref` `/application/houseAddress or /houseAddress.`XML看起來像這樣：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

如果要保留與結構描述根相同的子根名稱( `Address`在此範例中)，使用索引的bindrefs。

例如，套用bindrefs `/application/address[1]` 或 `/address[1]` 和 `/application/address[2]` 或 `/address[2]`. 表單的XML為：

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

您可以使用變更最適化表單/片段的預設子樹狀結構 `bindRef` 屬性。 此 `bindRef` 屬性可讓您指定指向XML結構描述樹狀結構中某個位置的路徑。

如果子表單未繫結，其資料會儲存在 `data`的根目錄 `afUnboundData` 上層表單XML結構描述的部分。

您可以將最適化表單新增為子表單多次。 確保 `bindRef` 已適當修改，以便適用性表單的每個已使用例項指向資料根下的不同子根。

>[!NOTE]
>
>如果不同的表單/片段對應到相同的子根，資料會被覆寫。

## 使用資產瀏覽器將最適化表單新增為子表單 {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

執行以下步驟，使用資產瀏覽器將最適化表單新增為子表單。

1. 在編輯模式下開啟父表單。
1. 在側邊欄中，按一下 **資產** ![資產 — 瀏覽器](assets/assets-browser.png). 在Assets下，選取 **最適化表單** 下拉式清單。
   [ ![在Assets下選取最適化表單](assets/asset.png)](assets/asset-1.png)

1. 拖放您要新增為子表單的最適化表單。
   [ ![將最適化表單拖放至您的網站](assets/drag-drop.png)](assets/drag-drop-1.png)您拖放的最適化表單會新增為子表單。
