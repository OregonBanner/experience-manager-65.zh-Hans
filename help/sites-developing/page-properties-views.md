---
title: 自訂頁面屬性檢視
seo-title: Customizing Views of Page Properties
description: 每個頁面都有一組您可以視需要編輯的屬性
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# 自訂頁面屬性檢視{#customizing-views-of-page-properties}

每個頁面都有一組 [屬性](/help/sites-authoring/editing-page-properties.md) 使用者可以檢視和編輯的專案；建立頁面（建立檢視）時需要某些專案，稍候可以檢視和編輯（編輯檢視）。 這些頁面屬性會透過對話方塊( `cq:dialog`)。

>[!CAUTION]
>
>傳統UI中不提供自訂頁面屬性檢視。

每個頁面屬性的預設狀態為：

* 在建立檢視中隱藏(例如 **建立頁面** 精靈)

* 可在編輯檢視中使用(例如 **檢視屬性**)

如果需要任何變更，則必須明確設定欄位。 這是使用適當的節點屬性來完成的：

* 建立檢視中可用的頁面屬性(例如 **建立頁面** 精靈)：

   * 名称: `cq:showOnCreate`
   * 类型: `Boolean`

* 編輯檢視中可用的頁面屬性(例如 **檢視**/**編輯**) **屬性** option)：

   * 名称: `cq:hideOnEdit`
   * 类型: `Boolean`

例如，請參閱「 」下分組欄位的設定 **更多標題和說明** 於 **基本** Foundation Page元件的索引標籤。 這些專案會顯示在 **建立頁面** 精靈為 `cq:showOnCreate` 已設為 `true`：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>請參閱 [擴充頁面屬性教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) 以取得自訂頁面屬性的指南。

## 設定頁面屬性 {#configuring-your-page-properties}

您也可以設定頁面元件的對話方塊並套用適當的節點屬性，以設定可用的欄位。

例如，根據預設， [**建立頁面** 精靈](/help/sites-authoring/managing-pages.md#creating-a-new-page) 顯示分組在下列位置的欄位： **更多標題和說明**. 若要隱藏這些專案，請設定：

1. 在下建立您的頁面元件 `/apps`.
1. 建立覆寫(使用 *對話方塊差異* 提供者： [Sling資源合併](/help/sites-developing/sling-resource-merger.md))，適用於 `basic` 頁面元件的區段；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >如需參考，請參閱：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   不過，您 ***必須*** 不變更中的任何專案 `/libs` 路徑。
   這是因為 `/libs` 下次升級執行個體時會被覆寫（而您在套用hotfix或feature pack時很可能會被覆寫）。
   設定和其他變更的建議方法是：
   1. 重新建立所需專案（即該專案存在於中） `/libs`)下 `/apps`
   1. 進行任何變更 `/apps`


1. 設定 `path` 屬性： `basic` 指向基本標籤的覆寫（另請參閱下一個步驟）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 建立「 」的覆寫 `basic` - `moretitles` 對應路徑下的區段；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 套用適當的節點屬性：

   * **名称**: `cq:showOnCreate`
   * **类型**: `Boolean`
   * **值**: `false`

   此 **更多標題和說明** 區段將不再顯示於 **建立頁面** 精靈。

>[!NOTE]
設定要與即時副本一起使用的頁面屬性時，請參閱 [在頁面屬性上設定MSM鎖定](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) 以取得更多詳細資料。

## 頁面屬性的設定範例 {#sample-configuration-of-page-properties}

此範例示範 [Sling資源合併](/help/sites-developing/sling-resource-merger.md)；包括使用 [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). 它也會說明這兩種功能的使用 `cq:showOnCreate` 和 `cq:hideOnEdit`.

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-page-dialog專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
