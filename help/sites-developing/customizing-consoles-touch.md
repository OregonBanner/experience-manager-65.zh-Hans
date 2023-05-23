---
title: 自訂主控台
seo-title: Customizing the Consoles
description: AEM提供各種機制，讓您能夠自訂編寫執行個體的主控台
seo-description: AEM provides various mechanisms to enable you to customize the consoles of your authoring instance
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---

# 自訂主控台 {#customizing-the-consoles}

>[!CAUTION]
>
>本檔案說明如何在現代、觸控式UI中自訂主控台，且不適用於傳統UI。

AEM提供各種機制，讓您能夠自訂主控台(以及 [頁面製作功能](/help/sites-developing/customizing-page-authoring-touch.md))。

* Clientlibs Clientlibs可讓您擴充預設實作以實現新功能，同時重複使用標準函式、物件和方法。 自訂時，您可以在下建立自己的clientlib `/apps.` 例如，它可以儲存自訂元件所需的程式碼。

* 覆蓋圖覆蓋圖以節點定義為基礎，可讓您覆蓋標準功能(在 `/libs`)的自訂功能(位於 `/apps`)。 建立覆蓋時不需要1:1的原始副本，因為Sling資源合併允許繼承。

您可以透過多種方式使用這些來擴充AEM主控台。 下面會覆蓋一個小的選取範圍（高階）。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 使用和建立 [clientlibs](/help/sites-developing/clientlibs.md).
>* 使用和建立 [覆蓋](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>



>[!CAUTION]
>
>您 ***必須*** 不變更中的任何專案 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時會被覆寫（而您在套用hotfix或feature pack時很可能會被覆寫）。
>
>設定和其他變更的建議方法是：
>
>1. 重新建立所需專案（即該專案存在於中） `/libs`)下 `/apps`
>
>1. 進行任何變更 `/apps`

>


例如，下列位置位於 `/libs` 結構可以重疊：

* 主控台（任何以Granite UI頁面為基礎的控制檯）；例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>請參閱知識庫文章， [疑難排解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以取得進一步的提示和工具。

## 自訂主控台的預設檢視 {#customizing-the-default-view-for-a-console}

您可以自訂主控台的預設檢視（欄、卡片、清單）：

1. 您可以從下列位置覆蓋所需專案，以重新排序檢視：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一個專案將是預設值。

   可用的節點與可用的檢視選項相關：

   * `column`
   * `card`
   * `list`

1. 例如，在清單的覆蓋中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定義下列屬性：

   * **名称**: `sling:orderBefore`
   * **类型**: `String`
   * **值**: `column`

### 將新動作新增至工具列 {#add-new-action-to-the-toolbar}

1. 您可以建置自己的元件，並包含自訂動作的對應使用者端程式庫。 例如， **提升至Twitter** 動作時間：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然後，即可將此連結至主控台上的工具列專案：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在選擇模式中：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 將工具列動作限制在特定群組 {#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自訂演算條件來覆蓋標準動作，並施加演算前必須滿足的特定條件。

   例如，建立元件以根據群組控制轉譯條件：

   `/apps/myapp/components/renderconditions/group`

1. 若要將這些套用至Sites主控台上的「建立網站」動作：

   `/libs/wcm/core/content/sites`

   建立覆蓋：

   `/apps/wcm/core/content/sites`

1. 然後新增動作的rendercondition：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此節點上的屬性，您可以定義 `groups` 有權執行特定動作；例如， `administrators`

### 自訂清單檢視中的欄 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>此功能已針對文字欄位欄位進行最佳化；對於其他資料型別，可以覆蓋 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` 在 `/apps`.

若要自訂清單檢視中的欄：

1. 覆蓋可用欄的清單。

   * 在節點上：

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 新增欄或移除現有欄。
   另請參閱 [使用覆蓋（和Sling資源合併）](/help/sites-developing/overlays.md) 以取得詳細資訊。

1. 選擇性：

   * 如果您想要插入其他資料，您需要撰寫 [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) 搭配
      `pageInfoProviderType` 属性.

   例如，請參閱下方的附加類別/套件（來自GitHub）。

1. 您現在可以在清單檢視的欄配置器中選取欄。

### 篩選資源 {#filtering-resources}

使用主控台時，常見的使用案例是使用者必須從資源（例如頁面、元件、資產等）中進行選擇。 例如，這可採取清單的形式，作者必須從中選擇專案。

為了將清單保持在合理的大小並與使用案例相關，可採用自訂述詞的形式實施篩選器。 另請參閱 [本文](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) 以取得詳細資訊。
