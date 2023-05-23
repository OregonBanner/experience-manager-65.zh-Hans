---
title: 使用AEM建立及組織頁面
description: 如何使用AEM建立和管理頁面
exl-id: 74576e51-4b4e-464e-a0b8-0fae748a505d
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '2525'
ht-degree: 57%

---

# 创建和组织页面 {#creating-and-organizing-pages}

本節說明如何使用Adobe Experience Manager (AEM)建立和管理頁面，以便您之後可以 [建立內容](/help/sites-authoring/editing-content.md) 這些頁面上。

>[!NOTE]
>
>您的帳戶需要 [適當的存取許可權](/help/sites-administering/security.md) 和 [許可權](/help/sites-administering/security.md#permissions) ，以在頁面上執行建立、複製、移動、編輯和刪除等動作。
>
>如果您遇到任何问题，我们建议您与系统管理员联系。

>[!NOTE]
>
>可以使用“网站”控制台中的许多[键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md)来更有效地组织页面。

## 组织您的网站 {#organizing-your-website}

身為作者，您需要在AEM中組織您的網站。 這涉及建立和命名內容頁面，以便：

* 您可以轻松地在创作环境中找到这些页面
* 您站点的访客可以方便地在发布环境中浏览这些页面

您还可以使用[文件夹](#creating-a-new-folder)来帮助组织内容。

網站的結構可視為存放內容頁面的樹狀結構。 這些內容頁面的名稱會用來組成URL，而檢視頁面內容時會顯示標題。

以下顯示We.Retail網站的範例，其中健行短褲頁面( `desert-sky-shorts`)已存取：

* 作者環境
   `https://localhost:4502/editor.html/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

* 發佈環境
   `https://localhost:4503/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

根據您執行個體的設定，使用 `/content` 在發佈環境中可能是選用的。

```xml
 /content
 /we-retail
  /us
   /en
    /products
     /equipment
      /hiking
       /desert-sky-shorts
       /hiking-poles
       /...
      /running...
      /surfing...
      /...
     /seasonal...
     /...
    /about-us
    /experience
    /...
   /es...
  /de...
  /fr...
  /...
 /...
```

此结构可以从&#x200B;**站点**&#x200B;控制台中查看，您可以在此控制台中[导航浏览网站的各个页面](/help/sites-authoring/basic-handling.md#navigating)，并对页面执行一些操作。您还可以创建新站点和[新页面](#creating-a-new-page)。

无论在什么位置，您都可以在标题栏的痕迹导航中看到上级分支：

![caop-01](assets/caop-01.png)

### 页面命名惯例 {#page-naming-conventions}

在创建新页面时，需填写以下两个关键字段：

* **[标题](#title)**：

   * 它会在控制台中向用户显示并在编辑中的页面内容顶部显示。
   * 此字段为必填字段。

* **[名称](#name)**：

   * 用于生成 URI。
   * 此字段的用户输入是可选的。如果未指定，則會從標題衍生名稱。 请参阅以下部分[页面名称限制和最佳实践](/help/sites-authoring/managing-pages.md#page-name-restrictions-and-best-practices)，以获取详细信息。

#### 页面名称限制和最佳实践 {#page-name-restrictions-and-best-practices}

页面&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;可以单独创建，但相互关联：

* 建立頁面時，僅 **標題** 欄位為必填。 若否 **名稱** 會在建立頁面時提供，AEM會從標題的前64個字元產生名稱（觀察下列驗證）。 仅使用前 64 个字符是为了支持短页面名称的最佳实践。

* 如果作者手动指定了页面名称，则 64 字符限制不适用，但有关页面名称长度的其他技术限制可能适用。

>[!NOTE]
>
>在定义页面名称时，一个好的经验法则是保持页面名称简短，但尽可能表达到位且容易记忆，使读者容易理解。请参阅针对 `title` 元素的 [W3C 风格指南](https://www.w3.org/Provider/Style/TITLE.html)，以获取更多信息。
>
>另请注意，某些浏览器（例如旧版本的 IE）只能接受一定长度的 URL，因此还有技术原因需缩短页面名称。

创建新页面时，AEM [将依据 AEM 和 JCR 实行的惯例来验证页面名称](/help/sites-developing/naming-conventions.md)。

允许使用的字符最少包括：

* &#39;a&#39;到&#39;z&#39;
* &#39;A&#39;到&#39;Z&#39;
* &#39;0&#39;到&#39;9&#39;
* `_`（下划线）
* `-`（连字符/减号）

有关允许使用的所有字符的完整详细信息，请参阅[命名惯例](/help/sites-developing/naming-conventions.md)。

>[!NOTE]
>
>如果AEM執行於 [MongoMK持續性管理員部署](/help/sites-deploying/recommended-deploys.md)，頁面名稱上限為150個字元。

#### 标题 {#title}

如果您在创建新页面时只提供一个页面&#x200B;**标题**，AEM 将从此字符串派生页面&#x200B;**名称**[，并依据 AEM 和 JCR 实行的惯例验证此名称](/help/sites-developing/naming-conventions.md)。虽然将接受包含无效字符的&#x200B;**标题**&#x200B;字段，但派生的名称会将无效的字符替换掉。例如：

| 标题 | 衍生名稱 |
|---|---|
| Schon | schoen.html |
| SC%&amp;&#42;ç+ | sc---c-.html |

#### 名称 {#name}

如果您在创建新页面时提供页面&#x200B;**名称**，AEM 将依据 AEM 和 JCR 实行的惯例验证此名称。[](/help/sites-developing/naming-conventions.md)您在&#x200B;**名称**&#x200B;字段中无法提交无效的字符。當AEM偵測到無效字元時，該欄位將會反白顯示一則說明訊息。

![caop-02](assets/caop-02.png)

>[!NOTE]
>
>应避免使用 ISO-639-1 定义的双字母代码作为页面名称，除非该页面是语言根页面。
>
>另請參閱 [準備翻譯內容](/help/sites-administering/tc-prep.md) 以取得詳細資訊。

### 模板 {#templates}

在AEM中，範本會指定特殊型別的頁面。 範本將用作任何正在建立的新頁面的基礎。

範本會定義包含縮圖影像和其他屬性的頁面結構。 例如，您可以為產品頁面、網站地圖和聯絡資訊使用不同的範本。 範本由下列專案組成 [元件](#components).

AEM隨附多種現成可用的範本。 可用的範本視個別網站而定。 关键的字段如下：

* **标题**
在生成的网页上显示的标题。

* **名称**
在命名页面时使用。

* **模板**
可在生成新页面时使用的模板列表。

>[!NOTE]
>
>如果在您的实例中进行配置，[模板作者可以通过模板编辑器创建模板](/help/sites-authoring/templates.md)。

### 组件 {#components}

元件是AEM提供的元素，可供您新增特定型別的內容。AEM隨附一系列 [現成可用的元件](/help/sites-authoring/default-components-console.md) 提供完整功能的機種。其中包括：

* 文本
* 图像
* 幻灯片放映
* 视频
* 以及更多功能

建立並開啟頁面後，您可以 [使用元件新增內容](/help/sites-authoring/editing-content.md#insertinganewparagraph)，可從以下網址取得： [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#componentbrowser).

>[!NOTE]
>
>[组件控制台](/help/sites-authoring/default-components-console.md)提供了有关实例中相关组件的概述。

## 管理页面 {#managing-pages}

### 创建新页面 {#creating-a-new-page}

除非所有頁面都已預先為您建立，否則您必須先建立頁面，然後才能開始建立內容：

1. 開啟Sites主控台(例如 [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content))。
1. 导航到要创建新页面的位置。
1. 使用工具栏中的&#x200B;**创建**&#x200B;打开下拉选择器，然后从列表中选择&#x200B;**页**：

   ![caop-03](assets/caop-03.png)

1. 在向导的第一步中，您可以执行以下操作之一：

   * 选择要用于创建新页面的模板，然后单击/点按&#x200B;**下一步**&#x200B;以继续。

   * 单击/点按&#x200B;**取消**&#x200B;可中止该过程。

   ![caop-04](assets/caop-04.png)

1. 在向导的最后一步中，您可以执行以下操作之一：

   * 使用三个选项卡输入您希望对新页面指定的[页面属性](/help/sites-authoring/editing-page-properties.md)，然后单击/点按&#x200B;**创建**&#x200B;以实际创建页面。

   * 使用 **返回** 以返回範本選取範圍。

   主要欄位包括：

   * **标题**：

      * 這會向使用者顯示，且是強制性的。
   * **名称**：

      * 用于生成 URI。如果未指定，則會從標題衍生名稱。
      * 如果您在创建新页面时提供页面&#x200B;**名称**[，AEM 将依据 AEM 和 JCR 实行的惯例验证此名称。](/help/sites-developing/naming-conventions.md)

      * 您 **無法提交無效的字元** 在 **名稱** 欄位。 當AEM偵測到無效字元時，將會反白顯示欄位，並顯示說明訊息，指出需要移除/取代的字元。
   >[!NOTE]
   >
   >另請參閱 [頁面命名慣例](#page-naming-conventions).

   建立新頁面所需的最少資訊是 **標題**.

   ![caop-05](assets/caop-05.png)

1. 使用&#x200B;**创建**&#x200B;完成此过程并创建新页面。确认对话框将询问您是要立即&#x200B;**打开**&#x200B;该页面，还是返回控制台（**完成**）：

   ![chlimage_1-118](assets/chlimage_1-118.png)

   >[!NOTE]
   >
   >如果您在创建页面时使用的名称在该位置已经存在，则系统将通过附加一个编号来自动生成该名称的变体。例如，如果 `winter` 已经存在，则新页面将变为 `winter0`。

1. 如果返回控制台，则会看到新页面：

   ![caop-06](assets/caop-06.png)

>[!CAUTION]
>
>建立頁面後，無法變更其範本，除非您 [使用新範本建立啟動項](/help/sites-authoring/launches-creating.md#create-launch-with-new-template)，但會遺失任何已存在的內容。

### 打开页面进行编辑 {#opening-a-page-for-editing}

建立頁面或導覽至現有頁面（在主控台中）後，您可以開啟該頁面進行編輯：

1. 開啟 **網站** 主控台。
1. 瀏覽至找到您要編輯的頁面為止。
1. 使用以下任一方式選取您的頁面：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigatingandselectionmode)和工具栏

   然后，选择&#x200B;**编辑**&#x200B;图标：

   ![screen_shot_2018-03-22at105355](assets/screen_shot_2018-03-22at105355.png)

1. 此时将打开页面，您可以根据需要[编辑页面](/help/sites-authoring/editing-content.md#touchoptimizedui)。

>[!NOTE]
>
>只有在「預覽」模式中才能從頁面編輯器導覽至其他頁面，因為連結在「編輯」模式中無效。

### 複製和貼上頁面 {#copying-and-pasting-a-page}

您可以將頁面及其所有子頁面複製到新位置：

1. 在 **網站** 主控台，導覽至找到您要複製的頁面為止。
1. 使用以下任一方式選取您的頁面：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigatingandselectionmode)和工具栏

   然後 **複製** 頁面圖示：

   ![screen_shot_2018-03-22at105425](assets/screen_shot_2018-03-22at105425.png)

   >[!NOTE]
   >
   >如果您處於選取模式，這會在頁面複製後立即自動退出。

1. 导航到页面的新副本所在的位置。
1. 通过正右侧的下拉箭头可显示&#x200B;**粘贴**&#x200B;图标：

   ![粘贴](assets/paste-without-children.png)

   您可以：
   * 选择&#x200B;**粘贴**&#x200B;页面图标本身：将在此位置创建原始页面和任何子页面的副本。
   * 选择下拉箭头以显示&#x200B;**粘贴（不含子项）**&#x200B;选项。将在此位置创建原始页面的副本；不会复制子页面。

   >[!NOTE]
   >
   >如果您将页面复制到某个位置，而该位置已经存在名称与原始名称相同的页面，则系统将通过附加一个编号来自动生成该名称的变体。例如，如果 `winter` 已存在，则 `winter` 将变为 `winter1`。

### 移动或重命名页面 {#moving-or-renaming-a-page}

>[!NOTE]
>
>重新命名頁面也必須遵循 [頁面命名慣例](#page-naming-conventions) 指定新頁面名稱時。

>[!NOTE]
>
>頁面只能移至允許頁面所依據的範本位置。 请参阅[模板可用性](/help/sites-developing/templates.md#template-availability)以了解更多信息。

移動或重新命名頁面的程式基本相同，並由相同的精靈處理。 通过此向导，您可以：

* 重命名页面而不移动页面.
* 移动页面而不重命名页面.
* 同时移动和重命名页面.

AEM提供可更新任何內部連結的功能，這些連結會參照正在重新命名/移動的頁面。 您可以逐頁進行，以提供完整的彈性。

1. 瀏覽至找到您要移動的頁面為止。
1. 使用以下任一方式選取您的頁面：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigatingandselectionmode)和工具栏

   然後選取 **移動** 頁面圖示：

   ![screen_shot_2018-03-22at105534](assets/screen_shot_2018-03-22at105534.png)

   這將會開啟移動頁面精靈。

1. 從 **重新命名** 精靈的階段您可以：

   * 指定移动页面后您希望页面使用的名称，然后单击/点按&#x200B;**下一步**&#x200B;以继续。

   * 单击/点按&#x200B;**取消**&#x200B;可中止该过程。

   ![caop-07](assets/caop-07.png)

   如果您只移動頁面，頁面名稱可以維持不變。

   >[!NOTE]
   >
   >如果您将页面移动到某个位置，而该位置已经存在具有相同名称的页面，则系统将通过附加一个编号来自动生成该名称的变体。例如，如果 `winter` 已存在，则 `winter` 将变为 `winter1`。

1. 從 **選取目的地** 精靈的階段您可以：

   * 使用 [欄檢視](/help/sites-authoring/basic-handling.md#column-view) 若要導覽至頁面的新位置：

      * 通过单击目标的缩略图选择目标。
      * 单击&#x200B;**下一步**&#x200B;以继续。
   * 使用 **返回** 以返回頁面名稱規格。

   >[!NOTE]
   >
   >依預設，將會選取您要移動/重新命名的頁面的父頁面作為目的地。

   ![caop-08](assets/caop-08.png)

   >[!NOTE]
   >
   >如果您将页面移动到某个位置，而该位置已经存在具有相同名称的页面，则系统将通过附加一个编号来自动生成该名称的变体。例如，如果 `winter` 已存在，则 `winter` 将变为 `winter1`。

1. 如果页面已链接、已引用或者已发布，则详细信息将列出在&#x200B;**调整/重新发布**&#x200B;步骤中。

   您可以指明哪些页面应当相应地调整和/或重新发布。

   >[!NOTE]
   >
   >如果页面既未链接也未引用，则此步骤将不可用。

   ![caop-09](assets/caop-09.png)

1. 選取 **移動** 將會完成程式，並根據需要移動/重新命名頁面。

>[!NOTE]
>
>如果页面已发布，则移动页面将自动取消发布。 依預設，移動完成時會重新發佈它，但您可以取消核取 **重新發佈** 中的欄位 **調整/重新發佈** 步驟。

>[!NOTE]
>
>如果页面未经任何引用，则会跳过&#x200B;**调整/重新发布**&#x200B;步骤。

#### 异步操作 {#asynchronous-actions}

通常，页面移动或重命名操作会立即执行。此过程被视为同步处理，在操作完成之前，会阻止 UI 中的进一步操作。

但是，如果受影响的页数超过定义的限制，将异步处理操作，从而使用户能够不受页面移动或重命名操作的阻碍，在 UI 中继续创作。

* 在上面的最后一步中单击&#x200B;**移动**&#x200B;时，AEM 会检查配置的限制。
* 如果受影响的页数低于限制，将执行同步操作。
* 如果受影响的页数超过限制，将执行异步操作。
   * 用户必须定义何时应执行异步操作
      * **现在**：立即开始执行异步作业。
      * **稍后**：允许用户定义何时开始异步作业。

         ![异步页面移动](assets/asynchronous-page-move.png)

可在&#x200B;[**异步作业状态**&#x200B;功能板](/help/sites-administering/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)（位于&#x200B;**全局导航** -> **工具** -> **操作** -> **作业**）中查看异步作业的状态

>[!NOTE]
>
>如需有關非同步作業處理以及如何設定頁面移動/重新命名動作限制的進一步資訊，請參閱 [非同步作業](/help/sites-administering/asynchronous-jobs.md) 管理使用手冊的檔案。

>[!NOTE]
>
>非同步頁面移動處理需要AEM 6.5.3.0或更新版本。

### 删除页面 {#deleting-a-page}

1. 一直导航到能够看见要删除的页面为止。
1. 使用[选择模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)选择所需页面，然后使用工具栏中的&#x200B;**删除**。

   ![screen_shot_2018-03-22at105622](assets/screen_shot_2018-03-22at105622.png)

   >[!NOTE]
   >
   >为安全起见，**删除**&#x200B;页面图标不可用作快速操作。

1. 對話方塊將會要求確認，使用：

   * **取消** 中止動作
   * **刪除** 若要確認動作：

      * 如果頁面沒有引用，則會刪除該頁面。
      * 如果页面含有引用，则会出现一个消息框，告知您&#x200B;**一个或多个页面被引用**。您可以选择&#x200B;**强制删除**&#x200B;或&#x200B;**取消**。

>[!NOTE]
>
>如果頁面已發佈，則在刪除前會自動取消發佈。

### 锁定页面 {#locking-a-page}

您可以 [鎖定/解鎖頁面](/help/sites-authoring/editing-content.md#locking-a-page) 從主控台或編輯個別頁面時。 有關頁面是否已鎖定的資訊也會顯示在這兩個位置。

![screen_shot_2018-03-22at105713](assets/screen_shot_2018-03-22at105713.png) ![screen_shot_2018-03-22at105720](assets/screen_shot_2018-03-22at105720.png)

### 创建新文件夹 {#creating-a-new-folder}

您可以创建文件夹来帮助组织文件和页面。

>[!NOTE]
>
>資料夾也必須遵守 [頁面命名慣例](#page-naming-conventions) 指定新資料夾名稱時。

>[!CAUTION]
>
>* 資料夾只能直接在下建立 **網站** 或位於其他資料夾下。 無法在頁面下建立縮圖。
>* 可以对文件夹执行移动、复制、粘贴、删除、发布、取消发布和查看/编辑属性等标准操作。
>* 无法在 Live Copy 中选择文件夹。
>


1. 開啟 **網站** 主控台並導覽至所需位置。
1. 若要開啟選項清單，請選取 **建立** （從工具列）
1. 選取 **資料夾** 以開啟對話方塊。 您可在此输入&#x200B;**名称**&#x200B;和&#x200B;**标题**：

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 选择&#x200B;**创建**&#x200B;以创建文件夹。
