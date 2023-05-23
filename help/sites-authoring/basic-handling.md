---
title: 使用AEM作者環境時的基本處理
description: 熟悉如何導覽AEM及其基本用法
uuid: c78ef9da-e0bd-47be-a410-9cf2ae71749a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 21181a6f-b434-40ed-8eb1-ebdfc98964dd
docset: aem65
exl-id: ef1a3997-feb4-4cb0-9396-c8335b69bb10
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '2973'
ht-degree: 48%

---

# 基本处理{#basic-handling}

>[!NOTE]
>
>* 此頁面旨在概述使用AEM製作環境時的基本處理方式。 它使用&#x200B;**站点**&#x200B;控制台作为基础。
>
>* 部分功能並未在所有主控台中提供，而其他功能可能也在某些主控台中提供。 有關個別主控台及其相關功能的特定資訊，將在其他頁面上詳細說明。
>* 用户在整个 AEM 环境中都可以使用各种键盘快捷键，尤其是在[使用控制台](/help/sites-authoring/keyboard-shortcuts.md)和[编辑页面](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)时。
>


## 快速入门 {#getting-started}

### 触屏优化 UI {#a-touch-enabled-ui}

AEM使用者介面已啟用觸控功能。 触屏界面允许您使用触屏，通过点按、触控并按住及轻扫之类的手势与软件进行交互。這與傳統案頭介面使用滑鼠動作（例如按一下、連按兩下、按一下滑鼠右鍵和滑鼠懸停滑鼠）的操作方式相反。

由於AEM UI支援觸控功能，因此您可以在觸控裝置（例如行動裝置或平板電腦）上使用觸控手勢，並在傳統桌上型裝置上使用滑鼠動作。

### 首要步骤 {#first-steps}

登录后，您将立即转到[“导航”面板](#navigation-panel)。選取其中一個選項會開啟相應的主控台。

![bh-01](assets/bh-01.png)

>[!NOTE]
>
>为了使您更好地了解 AEM 的基本用法，本文档基于&#x200B;**站点**&#x200B;控制台进行了介绍。
>
>请单击或点按&#x200B;**站点**&#x200B;以开始操作。

### 产品导航 {#product-navigation}

每當使用者首次存取主控台時，就會啟動產品導覽教學課程。 请花上一分钟的时间，通过单击或点按通读该教程，以大致了解 AEM 的基本处理。

![bh-02](assets/bh-02.png)

单击或点按&#x200B;**下一步**&#x200B;以前进至概述的下一个页面。单击或点按&#x200B;**关闭**，或者单击或点按概述对话框外部可将其关闭。

除非您檢視所有投影片或核取選項，否則概觀會在您下次存取主控台時重新啟動 **不要再顯示**.

## 全局导航 {#global-navigation}

您可以使用全局导航面板在控制台之间导航。當您按一下或點選畫面左上方的Adobe Experience Manager連結時，就會以全熒幕下拉式清單的形式觸發此動作。

通过单击或点按&#x200B;**关闭**&#x200B;可关闭全局导航面板，以返回到您之前所在的位置。

![bh-03](assets/bh-03.png)

>[!NOTE]
>
>第一次登入時，您會看到 **導覽** 面板。

全局导航有两个面板，它们由屏幕左侧的图标来表示：

* **[导航](/help/sites-authoring/basic-handling.md#navigation-panel)** – 登录到 AEM 时由一个指南针图标
* **[工具](/help/sites-authoring/basic-handling.md#tools-panel)** – 由一个锤子图标来表示

這些面板上可用的選項說明如下。

### “导航”面板 {#navigation-panel}

「導覽」面板可讓您存取AEM主控台：

![bh-01](assets/bh-01.png)

当您在控制台和内容中导航时，浏览器选项卡的标题将更新以反映您的位置。

在“导航”中，可用的控制台有：

<table>
 <tbody>
  <tr>
   <td><strong>控制台</strong></td>
   <td><strong>用途</strong></td>
  </tr>
  <tr>
   <td>资源<br /> </td>
   <td>這些主控台可讓您匯入和 <a href="/help/assets/home.md">管理數位資產</a> 例如影像、影片、檔案和音訊檔案。 然後這些資產便可由同一AEM執行個體上執行的任何網站使用。 </td>
  </tr>
  <tr>
   <td>社区</td>
   <td>此主控台可讓您建立和管理 <a href="/help/communities/sites-console.md">社群網站</a> 的 <a href="/help/communities/overview.md#engagement-community">參與</a> 和 <a href="/help/communities/overview.md#enablement-community">啟用</a>.</td>
  </tr>
  <tr>
   <td>商务</td>
   <td>這可讓您管理與您的相關產品、產品目錄和訂單 <a href="/help/commerce/cif-classic/administering/ecommerce.md">商務</a> 網站。</td>
  </tr>
  <tr>
   <td>体验片段</td>
   <td>一個 <a href="/help/sites-authoring/experience-fragments.md">體驗片段</a> 是獨立的體驗，可以跨管道重複使用，也可以有變數，省去重複複製和貼上體驗或體驗片段的麻煩。</td>
  </tr>
  <tr>
   <td>Forms</td>
   <td>此主控台可讓您建立、管理及處理 <a href="/help/forms/home.md">表單和檔案</a>.</td>
  </tr>
  <tr>
   <td>个性化</td>
   <td>此主控台提供 <a href="/help/sites-authoring/personalization.md">用於編寫目標內容和呈現個人化體驗的工具架構</a>.</td>
  </tr>
  <tr>
   <td>项目</td>
   <td>此 <a href="/help/sites-authoring/touch-ui-managing-projects.md">專案主控台可讓您直接存取專案</a>. 專案是虛擬儀表板。 它們可用於建立團隊，然後授予該團隊存取資源、工作流程和任務的許可權，允許人員致力於共同目標。 <br /> </td>
  </tr>
  <tr>
   <td>Screens</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/authoring/setting-up-projects/creating-a-screens-project.html">Screens</a> 可讓您管理所有對外畫面，不管是任何大小、在任何位置。</td>
  </tr>
  <tr>
   <td>Sites</td>
   <td>Sites主控台可讓您 <a href="/help/sites-authoring/page-authoring.md">建立、檢視及管理網站</a> 在您的AEM執行個體上執行。 透過這些主控台，您可以建立、編輯、複製、移動和刪除網站頁面、開始工作流程以及發佈頁面。<br /> </td>
  </tr>
 </tbody>
</table>

### “工具”面板 {#tools-panel}

在「工具」面板中，側面板中的每個選項都包含一系列子選單。 此 [工具主控台](/help/sites-administering/tools-consoles.md) 您可以在此處存取許多專用工具和控制檯，協助您管理網站、數位資產和內容存放庫的其他方面。

![bh-04](assets/bh-04.png)

## 标题 {#the-header}

标题始终显示在屏幕顶部。 雖然無論您在系統中的何處，標頭中的大部分選項都保持不變，但有些選項是上下文特定的。

![bh-03](assets/bh-03.png)

* [全局导航](#navigatingconsolesandtools)

   选择 **Adobe Experience Manager** 链接可在各控制台之间进行导航。

   ![screen_shot_2018-03-23at103615](assets/screen_shot_2018-03-23at103615.png)

* [搜索](/help/sites-authoring/search.md)

   ![](do-not-localize/screen_shot_2018-03-23at103542.png)

   您还可以使用[快捷键](/help/sites-authoring/keyboard-shortcuts.md) `/`（正斜杠）从任何控制台中调用搜索。

* [解决方案](https://www.adobe.com/cn/experience-cloud.html)

   ![](do-not-localize/screen_shot_2018-03-23at103552.png)

* [帮助](#accessinghelptouchoptimizedui)

   ![](do-not-localize/screen_shot_2018-03-23at103547.png)

* [通知](/help/sites-authoring/inbox.md)

   ![](do-not-localize/screen_shot_2018-03-23at103558.png)

   此图标将带有一个标记，显示当前分配的未完成通知的数量。

   >[!NOTE]
   >
   >現成可用的AEM會預先載入指派給管理員使用者群組的管理任務。 另請參閱 [您的收件匣 — 立即可用的管理工作](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks) 以取得詳細資訊。

* [用户属性](/help/sites-authoring/user-properties.md)

   ![](do-not-localize/screen_shot_2018-03-23at103603.png)

* [边栏选择器](/help/sites-authoring/basic-handling.md#rail-selector)

   ![](do-not-localize/screen_shot_2018-03-23at103943.png)

   显示的选项取决于您当前所在的控制台。例如，在 **網站** 您可以選取「僅限內容」（預設值）、「時間軸」、「參照」或「篩選器」側面板。

   ![screen_shot_2018-03-23at104029](assets/screen_shot_2018-03-23at104029.png)

* 痕迹导航

   ![bh-05](assets/bh-05.png)

   痕迹导航位于边栏中间，且始终显示当前选定项的描述，它允许您在特定控制台内导航。在 Sites 控制台中，您可以导航浏览网站的各个级别。

   只要按一下階層連結文字，即可顯示下拉式清單，列出目前所選專案的階層層次。 按一下專案以跳至該位置。

   ![bh-06](assets/bh-06.png)

* Analytics時段選擇

   ![screen_shot_2018-03-23at104126](assets/screen_shot_2018-03-23at104126.png)

   這僅在清單檢視中可用。 另請參閱 [清單檢視](#list-view) 以取得詳細資訊。

* **创建**&#x200B;按钮

   ![screen_shot_2018-03-23at104301](assets/screen_shot_2018-03-23at104301.png)

   单击此按钮后，会根据当前的控制台/上下文显示相应的选项。

* [视图](/help/sites-authoring/basic-handling.md#viewingandselectingyourresourcescardlistcolumn)

   檢檢視示位於AEM工具列的最右側。 由於它也會指出目前檢視，因此會變更。 例如，在默认视图&#x200B;**列视图**&#x200B;中显示：

   ![bh-07](assets/bh-07.png)

   您可以在欄檢視、卡片檢視和清單檢視之間切換；在清單檢視中，它也會顯示檢視設定。

   ![bh-09](assets/bh-09.png)

* 键盘导航

   您可以只使用键盘导航网站。這會使用的標準瀏覽器功能 **標籤** 金鑰(或 **OPT+TAB**)，將您移動至頁面上 *可聚焦*.

   在 **Sites** 控制台中，添加了&#x200B;**跳至主要内容**&#x200B;的选项。當您看到時，它就會變得可見 *標籤* 透過「 」標頭選項，可讓您略過（產品）工具列中的標準元素，並直接前往主要內容，以加速導覽。

   ![bh-30](assets/bh-30.png)

## 访问帮助 {#accessing-help}

有各种可用的帮助资源：

* **主控台工具列**

   根據您的位置 **說明** 圖示會開啟適當的資源：

   ![bh-10](assets/bh-10.png)

* **导航**

   首次在系统中导航时，[系统会提供一系列幻灯片来介绍 AEM 导航知识](/help/sites-authoring/basic-handling.md#product-navigation)。

* **页面编辑器**

   第一次編輯頁面時，系統會以一系列投影片來介紹頁面編輯器。

   ![bh-11](assets/bh-11.png)

   与在首次访问任何控制台时浏览[产品导航概述](/help/sites-authoring/basic-handling.md#product-navigation)一样，浏览此概述。

   在&#x200B;[**页面信息**&#x200B;菜单中，可以随时通过选择&#x200B;**帮助**](/help/sites-authoring/author-environment-tools.md#accessing-help)&#x200B;来再次显示这些幻灯片。

* **工具主控台**

   通过&#x200B;**“工具”**&#x200B;控制台，还可以访问外部&#x200B;**资源**：

   * **檔案**
檢視網站體驗管理檔案

   * **開發人員資源**
開發人員資源和下載
   >[!NOTE]
   >
   >在控制台中，您可以随时使用热键 `?`（问号）访问提供的快捷键概述。
   >
   >如需所有鍵盤快速鍵的概觀，請參閱下列檔案：
   >
   >    * [用于编辑页面的键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   >    * [控制台的键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md)


## “操作”工具栏 {#actions-toolbar}

每當選取資源（例如頁面或資產）時，工具列中都會有附有說明文字的圖示來指示各種動作。 这些操作取决于以下要素：

* 当前控制台.
* 当前上下文.
* 是否处于[选择模式](#navigatingandselectionmode).

工具栏中可用的操作会发生更改，以反映您可对特定的选定项目执行的操作。

[选择资源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)的方式依视图而定。

由于某些窗口存在空间限制，因此工具栏的长度可能很快就会超过可用空间。如果发生此情况，将会显示额外的选项。单击或点按省略号（三个点或 **...**）会打开下拉选择器，其中包含所有剩余操作。例如，在 **Sites** 控制台中选择了一个页面之后：

![“操作”工具栏](assets/bh-12.png)

>[!NOTE]
>
>可用的個別圖示會記錄為與適當的主控台/功能/情境相關。

## 快速操作 {#quick-actions}

在[信息卡视图](#cardviewquickactions)中，某些操作以快速操作图标的形式呈现，同时也在工具栏中提供。快速動作圖示一次只適用於一個專案，您不需要預先選取。

当您将鼠标（桌面设备）悬停在资源信息卡上时，会见到快速操作。可用的快速動作取決於主控台和內容。 例如，下面是适用于 **Sites** 控制台中的页面的快速操作：

![bh-13](assets/bh-13.png)

## 查看和选择资源 {#viewing-and-selecting-resources}

从概念上讲，所有视图中的查看、导航和选择操作都相同，只是操作方法根据所使用的视图而略有差异。

在任意可用视图中，您都可以查看、导航和选择资源（以对其执行进一步操作），可通过右上方的图标选择各个视图：

* [列视图](#column-view)
* [信息卡视图](#card-view)

* [列表视图](#list-view)

>[!NOTE]
>
>依預設，AEM Assets不會在任何檢視中將資產的原始轉譯顯示為縮圖。 如果您是管理員，則可以使用覆蓋圖來設定AEM Assets，以將原始轉譯顯示為縮圖。

### 選取資源 {#selecting-resources}

选择特定的资源取决于视图和设备的组合：

<table>
 <tbody>
  <tr>
   <td> </td>
   <td>选择</td>
   <td>取消选择</td>
  </tr>
  <tr>
   <td>列视图<br /> </td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下縮圖</li>
     <li>行動裝置：<br /> 點選縮圖</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下縮圖</li>
     <li>行動裝置：<br /> 點選縮圖</li>
    </ul> </td>
  </tr>
  <tr>
   <td>卡片视图<br /> </td>
   <td>
    <ul>
     <li>案頭：<br /> 滑鼠懸停，然後使用核取記號快速動作</li>
     <li>行動裝置：<br /> 點選並按住卡片</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下卡片</li>
     <li>行動裝置：<br /> 點選卡片</li>
    </ul> </td>
  </tr>
  <tr>
   <td>列表视图</td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下縮圖</li>
     <li>行動裝置：<br /> 點選縮圖</li>
    </ul> </td>
   <td>
    <ul>
     <li>案頭：<br /> 按一下縮圖</li>
     <li>行動裝置：<br /> 點選縮圖</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 全选 {#select-all}

您可以通过单击控制台右上角的&#x200B;**“全选”**&#x200B;选项来选择任何视图中的所有项目。

* 在&#x200B;**信息卡视图**&#x200B;中，选择所有信息卡。
* 在 **清單檢視** 選取清單中的所有專案。
* 在&#x200B;**列视图**&#x200B;中，选择最左侧列中的所有项目。

![screen-shot_2019-03-05at094659](assets/screen-shot_2019-03-05at094659.png)

#### 取消全选 {#deselecting-all}

在任何情况下，当您选择项目时，即会在工具栏的右上角显示选定项目的计数。

您可以透過以下任一方式取消選取所有專案並退出選取模式：

* 按一下或點選 **X** 在計數旁邊，

* 或使用 **逸出**.

![bh-14](assets/bh-14.png)

在所有檢視中，如果您使用案頭裝置，只要點選鍵盤上的Esc鍵，即可選取所有專案。

#### 选择示例 {#selecting-example}

1. 例如在信息卡视图中：

   ![bh-15](assets/bh-15.png)

1. 在选择了某个资源后，顶部标题被[操作工具栏](#actionstoolbar)覆盖，通过该工具栏可访问当前适用于选定资源的操作。

   要退出选择模式，请选择右上角的 **X**，或者使用 **Esc** 键。

### 列视图 {#column-view}

![bh-16](assets/bh-16.png)

列视图允许通过一系列的层叠列，对内容树进行可视化导航。此檢視可讓您視覺化並周遊網站的樹狀結構。

在最左邊的欄中選取資源，會在右邊的欄中顯示子資源。 在右側欄中選取資源後，會在右側的其他欄中顯示子資源，依此類推。

* 您可以點選或按一下資源名稱或資源名稱右側的>形箭號，在樹狀結構中向上和向下導覽。

   * 點選或按一下時，資源名稱和V形符號會反白顯示。

   ![bh-17](assets/bh-17.png)

   * 已點按/已點按資源的子項會顯示在已點按/已點按資源右側的欄中。
   * 如果您點選或按一下沒有子系的資源名稱，其詳細資訊將顯示在最後一欄。


* 點選或按一下縮圖可選取資源。

   * 選取時，縮圖上將會覆蓋核取記號，並且資源名稱也會反白顯示。
   * 最后的列中将显示选定资源的详细信息。
   * 動作工具列將變為可用。

   ![bh-18](assets/bh-18.png)

   在欄檢視中選取頁面時，選取的頁面會連同下列詳細資訊顯示在最終欄中：

   * 页面标题
   * 頁面名稱（頁面URL的一部分）
   * 頁面所依據的範本
   * 修改詳細資料
   * 頁面語言
   * 出版物詳細資料


### 信息卡视图 {#card-view}

![bh-15-1](assets/bh-15-1.png)

* 信息卡视图显示各个项目在当前级别的信息信息卡。這些會提供下列資訊：

   * 页面内容的可视表示形式.
   * 页面标题.
   * 重要日期（例如上次編輯、上次發佈）。
   * 该页面是否被锁定、隐藏或是 Live Copy 的一部分.
   * （在适当时）您何时需要在工作流中采取相应的操作.

      * 指出所需動作的標籤，可能與 [收件匣](/help/sites-authoring/inbox.md).

* [快速動作](#quick-actions) 也可以在此檢視中使用，例如選取和常見動作，例如編輯。

   ![bh-13-1](assets/bh-13-1.png)

* 您可以通过点按/单击信息卡对树进行向下导航（注意避免快速操作），或使用[标题中的痕迹导航](/help/sites-authoring/basic-handling.md#the-header)再次向上导航。

### 列表视图 {#list-view}

![bh-19](assets/bh-19.png)

* 列表视图列出各项资源在当前级别的信息。
* 您可以通过点按/单击资源名称对树进行向下导航，并使用[标题中的痕迹导航](/help/sites-authoring/basic-handling.md#the-header)再次向上导航。

* 要轻松选择列表中的所有项目，请使用列表左上角的复选框。

   ![bh-20](assets/bh-20.png)

   * 選取清單中的所有專案時，此核取方塊會顯示為已核取。

      * 按一下或點選核取方塊以取消選取全部。
   * 僅選取部分專案時，會出現減號。

      * 按一下或點選核取方塊以選取全部。
      * 再次按一下或點選核取方塊以取消全選。


* 可使用位于“视图”按钮下方的&#x200B;**查看设置**&#x200B;选项选择要显示的列。下列欄可供顯示：

   * **名称** – 页面名称，在多语言创作环境中非常有用，因为它是页面 URL 的一部分，无论用户使用何种语言，都不会发生更改
   * **修改时间** – 上次修改日期和上次修改用户
   * **发布时间** – 发布状态
   * **模板** – 页面所基于的模板
   * **工作流** – 当前应用于页面的工作流。当您鼠标悬停或打开时间线时，会提供更多信息。

   * **頁面分析**
   * **不重複訪客**
   * **頁面逗留時間**

   ![bh-21](assets/bh-21.png)

   默认将显示&#x200B;**名称**&#x200B;列，它构成了页面 URL 的一部分。在某些情況下，作者可能需要存取不同語言的頁面，如果作者不知道頁面的語言，檢視頁面名稱（通常不會變更）會很有幫助。

* 可使用列表中每个项目最右侧的点状垂直栏更改项目的顺序。

   >[!NOTE]
   >
   >只有在 `jcr:primaryType` 值为 `sling:OrderedFolder` 的已排序文件夹内才能更改顺序。

   ![bh-22](assets/bh-22.png)

   单击或点按垂直选择栏并将项目拖到列表中的新位置。

   ![bh-23](assets/bh-23.png)

* 您可以使用「 」顯示適當的欄，以顯示Analytics資料。 **檢視設定** 對話方塊。

   您可以使用標頭右側的篩選選項來篩選過去30、90或365天的Analytics資料。

   ![bh-24](assets/bh-24.png)

## 边栏选择器 {#rail-selector}

**边栏选择器**&#x200B;位于窗口的左上角，会根据您当前的控制台显示相应的选项。

![bh-25](assets/bh-25.png)

例如，在站点中，您可以选择“仅限内容”（默认）、“内容树”、“时间轴”、“引用”或“筛选器”侧面板。

如果选择“仅限内容”，则只会显示边栏图标。如果选择其他任何选项，则边栏图标旁边会显示选项名称。

>[!NOTE]
>
>可使用[键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md)快速地在各边栏显示选项之间进行切换。

### 内容树 {#content-tree}

內容樹狀結構可用來快速導覽側面板中的網站階層，以及檢視目前資料夾中頁面的許多相關資訊。

通过将内容树侧面板与列表视图或信息卡视图结合使用，用户可以方便地查看项目的层次结构，并通过内容树侧面板在内容结构中轻松导航，还可以在列表视图中查看详细的页面信息。

![bh-26](assets/bh-26.png)

>[!NOTE]
>
>選取階層檢視中的專案後，可使用方向鍵來快速瀏覽階層。
>
>請參閱 [鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md) 以取得詳細資訊。

### 时间线 {#timeline}

時間軸可用於檢視和/或啟動所選資源上已發生的事件。 要打开时间线列，请使用边栏选择器：

通过时间线列可以：

* [查看与选定项目相关的各种事件。](#timelineviewevents)

   * 可以从下拉列表中选择事件类型：

      * [评论](#timelineaddingandviewingcomments)
      * 注释
      * 活动
      * [启动项](/help/sites-authoring/launches.md)
      * [版本](/help/sites-authoring/working-with-page-versions.md)
      * [工作流](/help/sites-authoring/workflows-applying.md)

         * 但以下各項除外 [暫時性工作流程](/help/sites-developing/workflows.md#transient-workflows) 因為沒有儲存這些專案的歷史記錄資訊
      * 和全部顯示


* [添加/查看有关选定项目的评论。](#timelineaddingandviewingcomments)**评论**&#x200B;框显示在事件列表的底部。键入评论后按回车键将记录该评论。在选择&#x200B;**评论**&#x200B;或&#x200B;**显示全部**&#x200B;时，将显示该评论。

* 特定的控制台还具有其他一些功能。例如，在“站点”控制台中，您可以：

   * [保存版本](/help/sites-authoring/working-with-page-versions.md#creatinganewversiontouchoptimizedui)。
   * [建立工作流](/help/sites-authoring/workflows-applying.md#startingaworkflowfromtherail).

这些选项可通过&#x200B;**评论**&#x200B;字段旁边的 V 形标记访问。

![bh-27](assets/bh-27.png)

### 引用 {#references}

**引用** 顯示所選資源的任何連線。 例如，在 **Sites** 控制台中，页面的[引用](/help/sites-authoring/author-environment-tools.md#showingpagereferences)会显示以下项目：

* [启动项](/help/sites-authoring/launches.md#launches-in-references-sites-console)
* [Live Copy](/help/sites-administering/msm-livecopy-overview.md#openingthelivecopyoverviewfromreferences)
* [语言副本](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)
* 内容引用：

   * 從其他頁面連結至所選頁面的連結
   * 參考元件在所選頁面中借用的內容和/或借出的內容

![bh-28](assets/bh-28.png)

### 过滤器 {#filter}

这将打开一个与[搜索](/help/sites-authoring/search.md)类似的面板，其中已设置相应的位置过滤器，允许您进一步筛选希望查看的内容。

![bh-29](assets/bh-29.png)
