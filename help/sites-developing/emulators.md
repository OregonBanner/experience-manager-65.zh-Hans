---
title: 模拟器
seo-title: Emulators
description: AEM可讓作者在模擬一般使用者將檢視頁面的環境的模擬器中檢視頁面
seo-description: AEM enables authors to view a page in an emulator that simulates the environment in which an end-user will view the page
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 模拟器{#emulators}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM)可讓作者在模擬一般使用者將檢視頁面之環境的模擬器中，檢視頁面，例如在行動裝置或電子郵件使用者端中。

AEM模擬器架構：

* 在模擬的使用者介面(UI)中提供內容製作，例如行動裝置或電子郵件使用者端（用於製作電子報）。
* 根據模擬的UI調整頁面內容。
* 允許建立自訂模擬器。

>[!CAUTION]
>
>只有傳統UI支援此功能。

## 模擬器特性 {#emulators-characteristics}

模擬器：

* 是以ExtJS為基礎。
* 在頁面DOM上操作。
* 其外觀會透過CSS加以規範。
* 支援外掛程式（例如行動裝置旋轉外掛程式）。
* 僅對作者有效。
* 其基本元件位於 `/libs/wcm/emulator/components/base`.

### 模擬器如何轉換內容 {#how-the-emulator-transforms-the-content}

模擬器的運作方式是將內部HTML內容包裝在模擬器DIV中。 例如，下列html程式碼：

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

在模擬器啟動後，會轉換為下列html程式碼：

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

已新增兩個div標籤：

* 具有id的div `cq-emulator` 保持模擬器為整體和

* 具有id的div `cq-emulator-content` 代表頁面內容所在的裝置檢視區/畫面/內容區域。

新的CSS類別也會指派給新的模擬器div：它們代表目前模擬器的名稱。

模擬器的外掛程式可能會進一步擴充指派的CSS類別清單，如旋轉外掛程式的範例，根據目前的裝置旋轉插入「垂直」或「水準」類別。

如此一來，可藉由具有與模擬器div的ID和CSS類別相對應的CSS類別，來控制模擬器的完整外觀。

>[!NOTE]
>
>建議專案HTML將內文內容包裝在單一div中，就像上面的範例一樣。 如果內文內容包含多個標籤，可能會出現無法預測的結果。

### 行動模擬器 {#mobile-emulators}

現有的行動模擬器：

* 在/libs/wcm/mobile/components/emulators之下。
* 可透過JSON servlet在以下網址取得：

   http://localhost:4502/bin/wcm/mobile/emulators.json

當頁面元件依賴行動頁面元件時( `/libs/wcm/mobile/components/page`)，則模擬器功能會透過下列機制自動整合到頁面中：

* 行動頁面元件 `head.jsp` 包含裝置群組相關的模擬器初始元件（僅在製作模式下）以及裝置群組的轉譯CSS，透過：

   `deviceGroup.drawHead(pageContext);`

* 方法 `DeviceGroup.drawHead(pageContext)` 包含模擬器的init元件，也就是呼叫 `init.html.jsp` 模擬器元件的。 如果模擬器元件沒有自己的 `init.html.jsp` 並仰賴行動裝置基礎模擬器( `wcm/mobile/components/emulators/base)`，行動基本模擬器的init指令碼稱為( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`)。

* 行動基本模擬器的初始指令碼透過Javascript定義：

   * 為頁面定義的所有模擬器的設定(emulatorConfigs)
   * 模擬器管理員透過以下方式將模擬器的功能整合到頁面中：

      `emulatorMgr.launch(config)`;

      模擬器管理員的定義如下：

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 建立自訂行動模擬器 {#creating-a-custom-mobile-emulator}

若要建立自訂行動模擬器：

1. 以下 `/apps/myapp/components/emulators` 建立元件 `myemulator` (節點型別： `cq:Component`)。

1. 設定 `sling:resourceSuperType` 屬性至 `/libs/wcm/mobile/components/emulators/base`

1. 使用類別定義CSS使用者端資料庫 `cq.wcm.mobile.emulator` 對於模擬器外觀：名稱= `css`，節點型別= `cq:ClientLibrary`

   例如，您可以參照節點 `/libs/wcm/mobile/components/emulators/iPhone/css`

1. 如有需要，請定義JS使用者端程式庫，例如定義特定外掛程式：名稱= js，節點型別= cq：ClientLibrary

   例如，您可以參照節點 `/libs/wcm/mobile/components/emulators/base/js`

1. 如果模擬器支援外掛程式定義的特定功能（例如觸控捲動），請在模擬器下方建立設定節點：名稱= `cq:emulatorConfig`，節點型別= `nt:unstructured` 並新增定義外掛程式的屬性：

   * 名稱= `canRotate`，型別= `Boolean`，值= `true`：包含旋轉功能。

   * 名稱= `touchScrolling`，型別= `Boolean`，值= `true`：包含觸控捲動功能。
   您可以定義自己的外掛程式，以新增更多功能。
