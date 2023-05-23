---
title: 內容頁面的回應式佈局
description: Adobe Experience Manager可讓您為頁面實現回應式版面。
uuid: 4db45d78-9fca-4251-b504-ae3481fd9a8b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 668d1a8a-c757-4c9f-833f-e5dada4d0384
exl-id: 760b8419-5cf8-49c5-8d4f-6691f5256c53
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 52%

---

# 响应式布局{#responsive-layout}

AEM可讓您透過使用 **配置容器** 元件。

這提供了段落系統，可讓您在回應式格線中定位元件。 此格點可根據裝置/視窗大小和格式重新排列版面。 此组件可与&#x200B;[**布局**&#x200B;模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)配合使用，让您能够根据设备创建和编辑响应式布局。

配置容器：

* 提供水準對齊格點的功能，以及將元件並排放置到格點中並定義它們何時應摺疊/重排的功能。
* 使用預先定義的中斷點（例如用於手機、平板電腦等） 可讓您定義相關裝置/方向的必要內容行為。

   * 例如，您可以自訂元件大小，或是否在特定裝置上可看見元件。

* 可巢狀化以允許欄控制項。

之後，使用者便可使用模擬器檢視特定裝置的內容呈現方式。

>[!CAUTION]
>
>雖然「版面容器」元件可在傳統UI中使用，但其完整功能僅在觸控式UI中提供並支援。

AEM 使用一组机制为页面实现响应式布局：

* [**布局容器**](#adding-a-layout-container-and-its-content-edit-mode)&#x200B;组件

   此组件在[组件浏览器](/help/sites-authoring/author-environment-tools.md#components-browser)中可用，而且提供了一个网格段落系统，让您能够在响应式网格内添加和放置组件。您也可以将此组件设置为页面上的默认段落系统。

* [**布局模式**](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

   将布局容器放置到页面上后，就可以使用&#x200B;**布局**&#x200B;模式在响应式网格内放置内容。

* [**模拟器**](#selecting-a-device-to-emulate)
模拟器让您能够创建并编辑响应式网站，这些网站可以根据设备/窗口大小，通过以交互方式调整组件大小来重新安排布局。随后，用户可以使用模拟器查看内容的呈现方式。

透過這些回應式格點機制，您可以：

* 根據裝置寬度（與裝置型別和方向相關），使用中斷點來定義不同的內容配置。
* 使用这些相同的断点和内容布局来确保您的内容可对桌面浏览器窗口的大小做出响应。
* 使用水平对齐网格功能，从而允许您将组件放入网格中，根据需要调整大小，定义它们何时应该折叠/重排成并排或上下放置的形式。
* 为特定设备布局隐藏组件。
* 实现列控件。

根据您的项目，可以将布局容器用作您页面的默认段落系统，或用作可通过组件浏览器添加到页面中的组件（或同时用作两者）。

>[!NOTE]
>
>Adobe 提供了响应式布局的 [GitHub 文档](https://adobe-marketing-cloud.github.io/aem-responsivegrid/)，前端开发人员可以参考该文档，以便在 AEM 之外使用 AEM 网格，例如在为将来的 AEM 站点创建静态 HTML 模型时。

>[!NOTE]
>
>通过对模板进行配置，可以启用上述机制。另請參閱 [設定回應式佈局](/help/sites-administering/configuring-responsive-layout.md) 以取得進一步資訊。

## 布局定义、设备模拟和断点 {#layout-definitions-device-emulation-and-breakpoints}

在创建网站内容时，您可能希望确保内容的显示方式适合用来查看内容的设备。

AEM可讓您根據裝置的寬度來定義版面：

* 模擬器可讓您在一系列裝置上模擬這些版面。 除设备类型以外，通过&#x200B;**旋转设备**&#x200B;选项选择的方向也可能会因宽度的改变而影响所选的断点。
* 断点是区分各种布局定义的分界点。

   * 断点可有效地定义任何使用特定布局的设备的最大宽度（以像素为单位）。
   * 断点通常适用于一系列选定的设备，具体视设备显示器的宽度而定。
   * 断点的范围会向左扩展，直至到达下一个断点。
   * 您无法明确地选择断点，选择设备和方向将会自动选择相应的断点。

**桌面**&#x200B;设备没有特定的宽度，因此它与默认的断点（即，高于上次所配置断点的所有断点）有关。

>[!NOTE]
>
>尽管可以为每台单独的设备定义断点，但这会大大增加定义和维护布局所需的工作量。

使用模擬器時，您會選取特定裝置來模擬和定義版面，相關的中斷點也會反白顯示。 您所做的任何配置變更都將適用於中斷點套用的其他裝置，亦即位於使用中中斷點標籤左側、但下一個中斷點標籤前的任何裝置。

例如，當您選取裝置時 **iPhone 6 Plus** （定義為540畫素的寬度）用於模擬和配置、中斷點 **電話** （定義為768畫素）也會啟動。 您對版面所做的任何變更 **IPHONE 6** 將適用於下的其他裝置 **電話** 中斷點，例如 **IPHONE 5** （定義為320畫素）。

![screen_shot_2018-03-23at084058](assets/screen_shot_2018-03-23at084058.png)

## 选择要模拟的设备 {#selecting-a-device-to-emulate}

1. 開啟必要頁面以進行編輯。 例如：

   `http://localhost:4502/editor.html/content/we-retail/us/en/experience.html`

1. 从顶部工具栏中选择&#x200B;**模拟器**&#x200B;图标：

   ![](do-not-localize/screen_shot_2018-03-23at084256.png)

1. 此时将打开模拟器工具栏。

   ![screen_shot_2018-03-23at084551](assets/screen_shot_2018-03-23at084551.png)

   模拟器工具栏会显示其他布局选项：

   * **旋轉裝置**  — 可讓您將裝置從垂直（縱向）方向旋轉至水準（橫向）方向，反之亦然。

   ![](do-not-localize/screen_shot_2018-03-23at084612.png) ![](do-not-localize/screen_shot_2018-03-23at084637.png)

   * **选择设备** - 从列表中定义要模拟的特定设备（请参阅下一步以了解详细信息）。

   ![](do-not-localize/screen_shot_2018-03-23at084743.png)

1. 若要選取要模擬的特定裝置，您可以：

   * 使用「選取裝置」圖示，並從下拉式選擇器中選取。
   * 点按/单击模拟器工具栏中的设备指示器。

   ![screen_shot_2018-03-23at084818](assets/screen_shot_2018-03-23at084818.png)

1. 选择特定设备后，您可以：

   * 查看选定设备的活动标记，如 **iPad。**
   * 查看相应[断点](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)的活动标记，如&#x200B;**平板电脑**。

   ![screen_shot_2018-03-23at084932](assets/screen_shot_2018-03-23at084932.png)

   * 藍色虛線代表 *摺頁* 針對選取的裝置(此處為 **IPHONE 6**)。

   ![screen_shot_2018-03-23at084947](assets/screen_shot_2018-03-23at084947.png)

   * 摺頁也可以視為分頁符號(不要與 [中斷點](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints))以取得詳細資訊。 為方便起見，此畫面會顯示在捲動前，使用者在裝置上看到的內容部分。
   * 如果模擬的裝置高度高於熒幕大小，則不會顯示折線。
   * 显示折页是为了方便作者查看，在已发布的页面上则不会显示折页。



## 添加布局容器及其内容（编辑模式） {#adding-a-layout-container-and-its-content-edit-mode}

**布局容器**&#x200B;是一个段落系统，该系统：

* 包含其他组件。
* 定義版面。
* 回應變更。

>[!NOTE]
>
>如果尚未提供，請 **配置容器** 必須明確 [已為段落系統/頁面啟動](/help/sites-administering/configuring-responsive-layout.md) (例如，使用 [**設計** 模式](/help/sites-authoring/default-components-designmode.md))。

1. 布局 **容器在组件浏览器中** ，可作为标准 [组件使用](/help/sites-authoring/author-environment-tools.md#components-browser)。 从此处，您可以将其拖动到页面上的所需位置，随后您将看到将组件拖动到 **此处占位符** 。
1. 然後，您可以將元件新增至版面容器。 這些元件將儲存實際內容：

   ![screen_shot_2018-03-23at085500](assets/screen_shot_2018-03-23at085500.png)

## 选择布局容器并对其执行操作（编辑模式） {#selecting-and-taking-action-on-a-layout-container-edit-mode}

与其他组件一样，您可以先选择布局容器，然后再对其执行剪切、复制、删除等操作（在&#x200B;**编辑**&#x200B;模式下）：

>[!CAUTION]
>
>由於版面容器是段落系統，刪除元件將會同時刪除版面格線以及容器內容納的所有元件（及其內容）。

1. 如果您將滑鼠移到格點預留位置上或點選格點，則會顯示動作選單。

   ![screen_shot_2018-03-23at085357](assets/screen_shot_2018-03-23at085357.png)

   您需要选择&#x200B;**父项**&#x200B;选项。

   ![](do-not-localize/screen_shot_2018-03-23at085417.png)

1. 如果配置元件為巢狀，請選取 **父級** 選項會顯示下拉式選取專案，讓您選取巢狀配置容器或其父項。

   當您將滑鼠移至下拉式清單中的容器名稱上時，其外框將顯示在頁面上。

   * 最低的巢狀配置容器將以黑色外框。
   * 下一個最低的巢狀配置容器將以深灰色顯示。
   * 每個後續容器都會以較淺的灰色陰影顯示。

   ![screen_shot_2018-03-23at085636](assets/screen_shot_2018-03-23at085636.png)

1. 此时将突出显示整个网格及其内容。在显示的操作工具栏中，您可以选择一项操作，例如&#x200B;**删除**。

   ![screen_shot_2018-03-23at085724](assets/screen_shot_2018-03-23at085724.png)

## 定义布局（布局模式） {#defining-layouts-layout-mode}

>[!NOTE]
>
>您可以为每个[断点](#layout-definitions-device-emulation-and-breakpoints)定义单独的布局（由模拟的设备类型和方向决定）。

要为通过布局容器实施的响应式网格配置布局，您需要使用&#x200B;**布局**&#x200B;模式。

可以通过两种方式启动&#x200B;**布局**&#x200B;模式。

* 使用[工具栏中的模式菜单](/help/sites-authoring/author-environment-tools.md#page-modes)并选择&#x200B;**布局**&#x200B;模式

   * 像切换到&#x200B;**编辑**&#x200B;模式或&#x200B;**定位**&#x200B;模式一样，选择&#x200B;**布局**&#x200B;模式。
   * **布局**&#x200B;模式会一直保持下去，直到您通过模式选择器选择其他模式后，才会离开&#x200B;**布局**&#x200B;模式。

* 時間 [編輯個別元件。](/help/sites-authoring/editing-content.md#edit-component-layout)

   * 藉由使用 **版面** 元件快速動作選單中的選項，您可以切換至 **版面** 模式。
   * **版面** 編輯元件時模式會持續存在並恢復為 **編輯** 模式，此時焦點會變更為另一個元件。

在版面配置模式中，您可以對格線執行各種動作：

* 使用藍點調整內容元件的大小。 調整大小一律靠齊格點。 當調整背景格點大小時，將顯示以協助對齊：

   ![screen_shot_2018-03-23at090140](assets/screen_shot_2018-03-23at090140.png)

   >[!NOTE]
   >
   >在调整&#x200B;**图像**&#x200B;等组件的大小时，其比例和比率将保持不变。

* 单击/点按内容组件后，您可以使用工具栏执行以下操作：

   * **父项**

      可讓您選取整個版面容器元件，以便對整體執行動作。

   * **浮动到新行**

      元件將會移至新的一行，視格線內的可用空間而定。

   * **隐藏组件**

      元件將變得不可見（可以從版面配置容器的工具列恢復）。
   ![screen_shot_2018-03-23at090246](assets/screen_shot_2018-03-23at090246.png)

* 在&#x200B;**布局**&#x200B;模式下，您可以点按/单击&#x200B;**将组件拖动到此处**&#x200B;来选择整个组件。這將會顯示此模式的工具列。

   根據版面配置元件和屬於它的元件的狀態，工具列會有不同的選項。 例如：

   * **父项** - 选择父组件。

   ![](do-not-localize/screen_shot_2018-03-23at090823.png)

   * **顯示隱藏的元件**  — 顯示所有或個別元件。 數字表示目前有多少個隱藏的元件。計數器顯示隱藏的元件數目。

   ![](do-not-localize/screen_shot_2018-03-23at091007.png)

   * **还原断点布局** - 还原到默认的布局。这意味着不再强制使用自定义布局。

   ![](do-not-localize/screen_shot_2018-03-23at091013.png)

   * **浮动到新行** - 在间距允许的情况下将组件向上移动一个位置。

   ![screen_shot_2018-03-23at090829](assets/screen_shot_2018-03-23at090829.png)

   * **隐藏组件** - 隐藏当前的组件。

   ![](do-not-localize/screen_shot_2018-03-23at090834.png)

   >[!NOTE]
   >
   >在以上示例中，浮动和隐藏操作之所以可用，是因为此布局容器嵌套在一个父布局容器内。

   * **取消隐藏组件**
选择父组件会显示包含 
**显示隐藏组件**&#x200B;选项的操作工具栏。 在此示例中，隐藏了两个组件。
   ![screen_shot_2018-03-23at091200](assets/screen_shot_2018-03-23at091200.png)

   选择&#x200B;**显示隐藏的组件**&#x200B;选项时，当前隐藏的组件将以蓝色显示在它们的原始位置。

   ![screen_shot_2018-03-23at091224](assets/screen_shot_2018-03-23at091224.png)

   选择&#x200B;**全部恢复**&#x200B;将取消隐藏所有隐藏的组件。
