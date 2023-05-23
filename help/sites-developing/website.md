---
title: 建立功能完整的網站(JSP)
seo-title: Create a Fully-Featured Website (JSP)
description: 本教學課程可讓您使用AEM建立完整功能的網站
seo-description: This tutorial enables you to create a fully featured website with AEM
uuid: ec76ad5e-af6c-43ad-ae57-a4ae4ac7029f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 90bc05c9-e971-4e75-bc07-5e137c6c913e
docset: aem65
exl-id: d7cf843c-c837-4b97-b6c5-0fbd6793bdd4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4935'
ht-degree: 2%

---

# 建立功能完整的網站(JSP){#create-a-fully-featured-website-jsp}

>[!NOTE]
>
>本文介紹如何使用JSP並根據傳統UI建立網站。 Adobe建議您為網站運用最新的AEM技術，如文章所述 [開發AEM Sites快速入門](/help/sites-developing/getting-started.md).

本教學課程可讓您使用Adobe Experience Manager (AEM)建立完整功能的網站。 該網站將以通用網站為基礎，主要針對網頁開發人員。 所有開發都將在作者環境中進行。

本教學課程說明如何：

1. 安裝AEM。
1. 存取CRXDE Lite（開發環境）。
1. 以CRXDE Lite設定專案結構。
1. 建立作為建立內容頁面基礎的範本、元件和指令碼。
1. 先建立網站的根頁面，然後建立內容頁面。
1. 建立下列元件以便在您的頁面上使用：

   * 顶部导航
   * 列出子项
   * 徽标
   * 图像
   * Text-Image
   * 搜索

1. 包含各種基礎元件。

執行所有步驟後，您的頁面將如下所示：

![chlimage_1-24](assets/chlimage_1-24.png)

**下載最終結果**

若要隨附教學課程而非進行練習，請下載website-1.0.zip。 此檔案是包含本教學課程結果的AEM內容套件。 使用 [封裝管理員](/help/sites-administering/package-manager.md) 以將套件安裝到您的編寫執行個體。

**注意：** 安裝此套件將會覆寫您使用本教學課程建立的編寫執行個體上的任何資源。

網站內容套件

[获取文件](assets/website-1_0.zip)

## 安裝Adobe Experience Manager {#installing-adobe-experience-manager}

若要安裝用於開發網站的AEM執行個體，請依照設定 [具有作者和發佈執行個體的部署環境](/help/sites-deploying/deploy.md#author-and-publish-installs)，或執行 [一般安裝](/help/sites-deploying/deploy.md#default-local-install). 一般安裝包括下載AEM Quickstart JAR檔案、將license.properties檔案放在與JAR檔案相同的目錄中，以及連按兩下JAR檔案。

安裝AEM後，請按一下「歡迎」頁面上的「CRXDE Lite」連結來存取CRXDE Lite開發環境：

![chlimage_1-25](assets/chlimage_1-25.png)

>[!NOTE]
>
>使用預設連線埠在本機安裝的AEM編寫執行個體的CRXDE LiteURL為 [https://localhost:4502/crx/de/](https://localhost:4502/crx/de/).

### 在CRXDE Lite中設定專案結構 {#setting-up-the-project-structure-in-crxde-lite}

使用CRXDE Lite在存放庫中建立mywebsite應用程式結構：

1. 在CRXDE Lite左側的樹狀結構中，以滑鼠右鍵按一下 **`/apps`** 資料夾並按一下 **建立** > **建立** **資料夾**. 在 **建立資料夾** 對話方塊，輸入 `mywebsite` 作為資料夾名稱，然後按一下 **確定**.
1. 以滑鼠右鍵按一下 **`/apps/mywebsite`** 資料夾並按一下 **建立** > **建立資料夾**. 在 **建立資料夾** 對話方塊，輸入 `components` 作為資料夾名稱，然後按一下 **確定**.
1. 以滑鼠右鍵按一下 **`/apps/mywebsite`** 資料夾並按一下 **建立** > **建立資料夾**. 在 **建立資料夾** 對話方塊，輸入 `templates` 作為資料夾名稱，然後按一下 **確定**.

   樹狀結構中的結構現在看起來應該像這樣：

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 按一下 **全部儲存**.

### 設定設計 {#setting-up-the-design}

在本節中，您可使用「設計工具」建立應用程式的設計。 此設計會提供您網站的CSS和影像資源。

>[!NOTE]
>
>按一下以下連結以下載mywebsite.zip。 封存包含供您設計使用的static.css和影像檔案。

static.css檔案和影像範例

[获取文件](assets/mywebsite.zip)

1. 在AEM歡迎頁面上，按一下 **工具**. ([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html))

   ![chlimage_1-27](assets/chlimage_1-27.png)

1. 在資料夾樹狀結構中，選取 **設計** 資料夾，然後按一下 **新增** > **新頁面**. 型別 `mywebsite` 作為標題，然後按一下 **建立**.

1. 如果mywebsite專案未出現在表格中，請重新整理樹狀結構或表格。

1. [使用WebDAV](/help/sites-administering/webdav-access.md) 存取位於https://localhost:4502的URL，複製範例 `static.css` 檔案和 `images` 從下載的mywebsite.zip檔案中放入的資料夾 `/etc/designs/mywebsite` 資料夾。

   ![chlimage_1-28](assets/chlimage_1-28.png)

### 建立Contentpage範本、元件和指令碼 {#creating-the-contentpage-template-component-and-script}

在本節中，您將建立下列專案：

* 將在範例網站中用來建立內容頁面的內容頁面範本
* 用於呈現內容頁面的contentpage元件
* contentpage指令碼

#### 建立Contentpage範本 {#creating-the-contentpage-template}

建立範本以用作網站網頁的基礎。

範本會定義新頁面的預設內容。 複雜的網站可能會使用數個範本來建立網站中不同型別的頁面。 在本練習中，所有頁面都以一個簡單範本為基礎。

1. 在CRXDE Lite的資料夾樹狀結構中，按一下右鍵 `/apps/mywebsite/templates` 並按一下 **建立** > **建立範本**.

1. 在「建立範本」對話方塊中，輸入下列值，然後按一下 **下一個**：

   * **標籤**： contentpage
   * **標題**：我的網站內容頁面範本
   * **說明**：這是我的網站內容頁面範本
   * **資源型別：** mywebsite/components/contentpage

   使用「排名」屬性的預設值。

   ![chlimage_1-29](assets/chlimage_1-29.png)

   資源型別可識別轉譯頁面的元件。 在此情況下，使用contentpage範本建立的所有頁面都會由 `mywebsite/components/contentpage` 元件。

1. 若要指定可使用此範本的頁面路徑，請按一下加號按鈕並鍵入 `/content(/.*)?` 在出現的文字方塊中。 然後，按一下 **下一個**.

   ![chlimage_1-30](assets/chlimage_1-30.png)

   允許的路徑屬性值是 *規則運算式。* 路徑符合運算式的頁面可以使用範本。 在此情況下，規則運算式會比對 **/content** 資料夾和所有子頁面。

   當作者在/content下方建立頁面時， **contentpage** 範本會顯示在可用的範本清單中。

1. 按一下 **下一個** 在 **允許的父項** 和 **允許的子項** 面板並按一下 **確定**. 在CRXDE Lite中，按一下 **全部儲存**.

   ![chlimage_1-31](assets/chlimage_1-31.png)

#### 建立Contentpage元件 {#creating-the-contentpage-component}

建立 *元件* 會定義內容並轉譯使用contentpage範本的頁面。 元件的位置必須對應至contentpage範本的Resource Type屬性值。

1. 在CRXDE Lite中按一下滑鼠右鍵 `/apps/mywebsite/components` 並按一下 **建立** > **元件**.
1. 在 **建立元件** 對話方塊中，輸入下列屬性值：

   * **標籤**： contentpage
   * **標題**：我的網站內容頁面元件
   * **說明**：這是我的網站內容頁面元件

   ![chlimage_1-32](assets/chlimage_1-32.png)

   新元件的位置為 `/apps/mywebsite/components/contentpage`. 此路徑對應至內容頁面範本的資源型別（減去初始值） **`/apps/`** 路徑的一部分)。

   此通訊會將範本連線到元件，對網站的正確運作至關重要。

1. 按一下 **下一個** 直到對話方塊的「允許的子系」面板出現，然後按一下 **確定**. 在CRXDE Lite中，按一下 **全部儲存**.

   結構現在看起來像這樣：

   ![chlimage_1-33](assets/chlimage_1-33.png)

#### 開發Contentpage元件指令碼 {#developing-the-contentpage-component-script}

將程式碼新增至contentpage.jsp指令碼以定義頁面內容。

1. 在CRXDE Lite中，開啟檔案 `contentpage.jsp` 在 `/apps/mywebsite/components/contentpage`. 依預設，檔案包含下列程式碼：

   ```java
   <%--
   
     My Website Content Page Component component.
   
     This is My Website Content Page Component.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
       /* TODO add you code here */
   %>
   ```

1. 複製下列程式碼，並將其貼到預設程式碼之後的contentpage.jsp中：

   ```java
   <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
       pageEncoding="ISO-8859-1"%>
   <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
   "https://www.w3.org/TR/html4/loose.dtd">
   <html>
   <head>
   <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
   <title>My title</title>
   </head>
   <body>
   <div>My body</div>
   </body>
   </html>
   ```

1. 按一下 **全部儲存** 以儲存變更。

### 建立您的網站頁面和內容頁面 {#creating-your-website-page-and-content-pages}

在本節中，您將建立以下所有使用內容頁面範本的頁面：我的網站、英文、產品、服務和客戶。

1. 在AEM歡迎頁面([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html))，按一下「網站」。

   ![chlimage_1-34](assets/chlimage_1-34.png)

1. 在資料夾樹狀結構中，選取 **網站** 資料夾，然後按一下 **新增** > **新頁面**.
1. 在 **建立頁面** 視窗，輸入下列內容：

   * 标题: `My Website`
   * 名称: `mywebsite`
   * 選取 `My Website Content Page Template`

   ![chlimage_1-35](assets/chlimage_1-35.png)

1. 单击&#x200B;**创建**。在資料夾樹狀結構中，選取 **/Websites/My Website** 頁面並按一下 **新增** > **新頁面**.
1. 在「建立頁面」對話方塊中，輸入下列屬性值，然後按一下「建立」：

   * 標題：英文
   * 名稱： en
   * 選取「我的網站內容」頁面範本

1. 在資料夾樹狀結構中，選取 **/Websites/My網站/英文** 頁面並按一下 **新增**> **新頁面**.
1. 在 **建立頁面** 對話方塊，輸入以下屬性值，然後按一下 **建立**：

   * 標題：產品
   * 選取「我的網站內容」頁面範本

1. 在資料夾樹狀結構中，選取 **/Websites/My網站/英文** 頁面並按一下 **新增** > **新頁面**.
1. 在 **建立頁面** 對話方塊，輸入以下屬性值，然後按一下 **建立**：

   * 標題：服務
   * 選取「我的網站內容」頁面範本

1. 在資料夾樹狀結構中，選取 **/Websites/My網站/英文** 頁面並按一下 **新增** > **新頁面**.
1. 在 **建立頁面** 對話方塊，輸入以下屬性值，然後按一下 **建立**：

   * 標題：客戶
   * 選取「我的網站內容」頁面範本

   您的結構如下所示：

   ![chlimage_1-36](assets/chlimage_1-36.png)

1. 若要將您的頁面連結至mywebsite設計，請在CRXDE Lite中選取 `/content/mywebsite/en/jcr:content` 節點。 在「屬性」標籤上，為新屬性輸入下列值，然後按一下「新增」：

   * 名稱：cq：designPath
   * 型別：字串
   * 值： /etc/designs/mywebsite

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. 在新的網頁瀏覽器標籤或視窗中，開啟 [https://localhost:4502/content/mywebsite/en/products.html](https://localhost:4502/content/mywebsite/en/products.html) 若要檢視「產品」頁面：

   ![chlimage_1-38](assets/chlimage_1-38.png)

### 增強Contentpage指令碼 {#enhancing-the-contentpage-script}

本節說明如何使用AEM基礎元件指令碼及撰寫您自己的指令碼，來增強contentpage指令碼。

此 **產品** 頁面如下所示：

![chlimage_1](assets/chlimage_1.jpeg)

#### 使用Foundation頁面命令檔 {#using-the-foundation-page-scripts}

在本練習中，您需設定pagecontent元件，使其超型別成為AEM Page元件。 由於元件繼承其超型別的功能，因此您的頁面內容會繼承頁面元件的指令碼和屬性。

例如，在元件JSP程式碼中，您可以參照超級型別元件提供的指令碼，就像這些指令碼包含在元件中一樣。

1. 在CRXDE Lite中，將屬性新增至 `/apps/mywebsite/components/contentpage` 節點。

   1. 選取 `/apps/mywebsite/components/contentpage` 節點。
   1. 在「屬性」標籤底部，輸入以下屬性值，然後按一下「新增」：

      * **名稱：** sling：resourceSuperType
      * **型別：** 字串
      * **值：** foundation/components/page
   1. 按一下「儲存全部」。


1. 開啟 `contentpage.jsp` 下的檔案 `/apps/mywebsite/components/contentpage` 和以下列程式碼取代現有程式碼：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" contentType="text/html; charset=utf-8" %><%
   %><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
   <html>
   <cq:include script="head.jsp"/>
   <cq:include script="body.jsp"/>
   </html>
   ```

1. 儲存您的變更。
1. 在您的瀏覽器中，重新載入產品頁面。 如下所示：

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

   開啟頁面來源以檢視head.jsp和body.jsp指令碼產生的javascript和HTML元素。 下列指令碼片段會在您開啟頁面時開啟Sidekick：

   ```java
   CQ.WCM.launchSidekick("/content/mywebsite/en/products",
               {propsDialog: "/libs/foundation/components/page/dialog",
                  locked: false locked: false
                });
   ```

#### 使用您自己的指令碼 {#using-your-own-scripts}

您可以在此段落中建立數個指令碼，每個指令碼都會產生頁面內文的一部分。 接著，您可以在pagecontent元件中建立body.jsp檔案，覆寫AEM Page元件的body.jsp。 在body.jsp檔案中，您可以包含產生頁面內文不同部分的指令碼。

**秘訣：** 當元件包含與元件超型別中的檔案具有相同名稱和相對位置的檔案時，則稱為 *覆蓋*.

1. 在CRXDE Lite中建立檔案 `left.jsp` 在 `/apps/mywebsite/components/contentpage`：

   1. 以滑鼠右鍵按一下節點 `/apps/mywebsite/components/contentpage`，然後選取**建立**然後 **建立檔案**.

   1. 在視窗中，輸入 `left.jsp` 作為 **名稱** 並按一下 **確定**.

1. 編輯檔案 `left.jsp` 若要移除現有內容並取代為下列程式碼：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="left">
   <div>logo</div>
   <div>newslist</div>
   <div>search</div>
   </div>
   ```

1. 保存更改。
1. 在CRXDE Lite中建立檔案 `center.jsp` 在 `/apps/mywebsite/components/contentpage`：

   1. 以滑鼠右鍵按一下節點 `/apps/mywebsite/components/contentpage`，選取 **建立**，則 **建立檔案**.

   1. 在對話方塊中，輸入 `center.jsp` 作為 **名稱** 並按一下 **確定**.

1. 編輯檔案 `center.jsp` 移除現有內容並使用下列程式碼加以取代：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="center">
   <div>trail</div>
   <div>title</div>
   <div>parsys</div>
   </div>
   ```

1. 保存更改。
1. 在CRXDE Lite中建立檔案 `right.jsp` 在 `/apps/mywebsite/components/contentpage`：

   1. 以滑鼠右鍵按一下節點 `/apps/mywebsite/components/contentpage`，選取 **建立**，則 **建立檔案**.

   1. 在對話方塊中，輸入 `right.jsp` 作為 **名稱** 並按一下 **確定**.

1. 編輯檔案 `right.jsp` 若要移除現有內容並取代為下列程式碼：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="right">
   <div>iparsys</div>
   </div>
   ```

1. 保存更改。
1. 在CRXDE Lite中建立檔案 `body.jsp` 在 `/apps/mywebsite/components/contentpage`：
1. 編輯檔案 `body.jsp` 若要移除現有內容並取代為下列程式碼：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><body>
   <div id="CQ">
   <div class="topnav">topnav</div>
   <div class="content">
   <cq:include script="left.jsp" />
   <cq:include script="center.jsp" />
   <cq:include script="right.jsp" />
   </div>
   <div class="footer">
   <div class="toolbar">toolbar</div>
   </div>
   </div>
   </body>
   ```

1. 保存更改。
1. 在您的瀏覽器中，重新載入產品頁面。 如下所示：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 建立頂端導覽元件 {#creating-the-top-navigation-component}

在本節中，您會建立一個元件，顯示網站所有頂層頁面的連結，以方便導覽。 此元件內容會顯示在使用內容頁面範本建立的所有頁面頂端。

在頂端導覽元件(topnav)的第一個版本中，導覽專案僅為文字連結。 在第二個版本中，您會使用影像導覽連結來實作Topnav。

您的頂端導覽列如下：

![chlimage_1-39](assets/chlimage_1-39.png)

#### 建立頂端導覽元件 {#creating-the-top-navigation-component-1}

1. 在CRXDE Lite中按一下滑鼠右鍵 `/apps/mywebsite/components`，選取 **建立**，則 **建立元件**.
1. 在 **建立元件** 視窗，輸入下列內容：

   * **標籤**： `topnav`

   * **标题**: `My Top Navigation Component`

   * **描述**: `This is My Top Navigation Component`

1. 按一下 **下一個** 直到您進入最後一個視窗並按一下 **確定**. 儲存您的變更。

#### 建立含有文字連結的頂端導覽指令碼 {#creating-the-top-navigation-script-with-textual-links}

將轉譯指令碼新增至topnav，以產生子頁面的文字連結：

1. 在CRXDE Lite中，開啟檔案 `topnav.jsp` 在 `/apps/mywebsite/components/topnav`.
1. 複製並貼上下列程式碼以取代現有的程式碼：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
           com.day.text.Text,
           com.day.cq.wcm.api.PageFilter, com.day.cq.wcm.api.Page" %><%
       /* get starting point of navigation */
       Page navRootPage = currentPage.getAbsoluteParent(2);
       if (navRootPage == null && currentPage != null) {
       navRootPage = currentPage;
       }
       if (navRootPage != null) {
           Iterator<Page> children = navRootPage.listChildren(new PageFilter(request));
           while (children.hasNext()) {
               Page child = children.next();
               %><a href="<%= child.getPath() %>.html"><%=child.getTitle() %></a><%
           }
       }
   %>
   ```

#### 在Contentpage元件中包含頂端導覽 {#including-top-navigation-in-the-contentpage-component}

若要在內容頁面元件中包含topnav：

1. 在CRXDE Lite中，開啟 `body.jsp` 在 `/apps/mywebsite/components/contentpage`和取代：

   ```xml
   <div class="topnav">topnav</div>
   ```

   替换为:

   ```xml
   <cq:include path="topnav" resourceType="mywebsite/components/topnav" />
   ```

1. 保存更改。
1. 在您的瀏覽器中，重新載入產品頁面。 頂端導覽列示如下：

   ![chlimage_1-40](assets/chlimage_1-40.png)

#### 使用字幕增強頁面 {#enhancing-pages-with-subtitles}

頁面元件會定義屬性，讓您為頁面提供字幕。 新增提供頁面內容相關資訊的字幕。

1. 在您的瀏覽器中，開啟 **產品** 頁面。
1. 在Sidekick **頁面** 標籤，按一下 **頁面屬性**.
1. 在對話方塊的「基本」標籤上，展開 **更多標題和說明，** 和 **字幕** 屬性，型別 **我們的工作**. 单击&#x200B;**确定**。
1. 重複上述步驟以新增副標題 **關於我們的服務** 至 **服務** 頁面。
1. 重複上述步驟以新增副標題 **我們獲得的信任** 至 **客戶** 頁面。

   **秘訣：** 在CRXDE Lite中，選取/content/mywebsite/en/products/jcr：content節點以檢視是否已新增字幕屬性。

#### 使用影像連結增強頂端導覽 {#enhance-top-navigation-by-using-image-links}

增強Topnav元件的轉譯指令碼，以使用影像連結而非導覽控制項的超文字。 此影像包含連結目標的標題和副標題。

此練習示範 [Sling請求處理](/help/sites-developing/the-basics.md#sling-request-processing). topnav.jsp指令碼經過修改，可呼叫動態產生影像以用於頁面導覽連結的指令碼。 在本練習中，Sling會剖析影像來源檔案的URL，以決定用於轉譯影像的指令碼。

例如，產品頁面的影像連結來源可以是https://localhost:4502/content/mywebsite/en/products.navimage.png。 Sling會剖析此URL以判斷資源型別，以及用於轉譯資源的指令碼：

1. Sling決定要使用的資源路徑 `/content/mwebysite/en/products.png.`
1. Sling將此路徑與 `/content/mywebsite/en/products` 節點。
1. Sling決定 `sling:resourceType` 此節點的 `mywebsite/components/contentpage`.

1. Sling會在此元件中尋找最符合URL選擇器的指令碼( `navimage`)和副檔名( `png`)。

在本練習中，Sling會將這些URL與您建立的/apps/mywebsite/components/contentpage/navimage.png.java指令碼相符。

1. 在CRXDE Lite中，開啟 `topnav.jsp` 在 `/apps/mywebsite/components/topnav.`找出錨點元素的內容（第14行）：

   ```xml
   <%=child.getTitle() %>
   ```

1. 以下列程式碼取代錨點內容：

   ```xml
   <img alt="<%= child.getTitle() %>" src="<%= child.getPath() %>.navimage.png">
   ```

1. 保存更改。
1. 以滑鼠右鍵按一下 `/apps/mywebsite/components/contentpage` 節點並按一下 **建立** > **建立檔案**.
1. 在 **建立檔案** 視窗，作為 **名稱**，型別 `navimage.png.java`.

   .java副檔名會向Sling指出Apache Sling Scripting Java支援應該用於編譯指令碼和建立servlet。

1. 將下列程式碼複製到 `navimage.png.java.`此程式碼會擴充AbstractImageServlet類別：

   * [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 建立儲存目前資源屬性的ImageContext物件。
   * 資源的父頁面是從ImageContext物件擷取。 然後取得頁面標題和副標題。
   * [ImageHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ImageHelper.html) 用於從網站設計的navimage_bg.jpg檔案、頁面標題和頁面子標題產生影像。

   ```java
   package apps.mywebsite.components.contentpage;
   
   import java.awt.Color;
   import java.awt.Paint;
   import java.awt.geom.Rectangle2D;
   
   import java.io.IOException;
   import javax.jcr.RepositoryException;
   
   import com.day.cq.wcm.api.Page;
   import com.day.cq.wcm.api.PageManager;
   import com.day.cq.wcm.api.components.Component;
   import com.day.cq.wcm.api.designer.Designer;
   
   import com.day.cq.commons.SlingRepositoryException;
   import com.day.cq.wcm.commons.WCMUtils;
   import com.day.cq.wcm.commons.AbstractImageServlet;
   import com.day.cq.commons.ImageHelper;
   
   import com.day.image.Font;
   import com.day.image.Layer;
   
   import org.apache.sling.api.SlingHttpServletRequest;
   import org.apache.sling.api.SlingHttpServletResponse;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
   
   /**
     * Renders the navigation image
     */
   public class navimage_png extends AbstractImageServlet {
   
         protected Layer createLayer(ImageContext ctx)
                throws RepositoryException, IOException {
            PageManager pageManager = ctx.resolver.adaptTo(PageManager.class);
            Page currentPage = pageManager.getContainingPage(ctx.resource);
   
            /* constants for image appearance */
            int scale = 6;
            int paddingX = 24;
            int paddingY = 24;
            Color bgColor = new Color(0x004a565c, true);
   
            /* obtain the page title */
            String title = currentPage.getTitle();
            if (title == null) {
                title = currentPage.getName();
            }
   
            /* format the title text */
            title = title.toUpperCase();
            Paint titleColor = Color.WHITE;
            Font titleFont = new Font("Myriad Pro", 10 * scale, Font.BOLD);
            int titleBase = 10 * scale;
   
            /* obtain and format the page subtitle */
            String subtitle = currentPage.getProperties().get("subtitle", "");
            Paint subtitleColor = new Color(0xffa9afb1, true);
            Font subTitleFont = new Font("Tahoma", 7);
            int subTitleBase = 20;
   
            /* create a layer that contains the background image from the mywebsite design */
            Designer dg = ctx.resolver.adaptTo(Designer.class);
            String imgPath = new String(dg.getDesignPath(currentPage)+"/images/navimage_bg.jpg");
            Layer bg = ImageHelper.createLayer(ctx.resolver.resolve(imgPath));
   
            /* draw the title text (4 times bigger) */
            Rectangle2D titleExtent = titleFont.getTextExtent(0, 0, 0, 0, title, Font.ALIGN_LEFT, 0, 0);
            Rectangle2D subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
   
            /* ensure subtitleExtent is wide enough */
            if ( subtitle.length() > 0 ) {
                int titleWidth = (int)titleExtent.getWidth() / scale;
                if ( subtitleExtent.getWidth() > titleWidth && subtitleExtent.getWidth() + 2 * paddingX >
    bg.getWidth() ) {
                    int charWidth = (int)subtitleExtent.getWidth() / subtitle.length();
                    int maxWidth = (bg.getWidth() > titleWidth + 2  * paddingX ? bg.getWidth() - 2 * paddingX : titleWidth);
                    int len = (maxWidth - ( 2 * charWidth) ) / charWidth;
                    subtitle = subtitle.substring(0, len) + "...";
                    subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
                }
            }
            int width = Math.max((int) titleExtent.getWidth(), (int) subtitleExtent.getWidth());
           /* create the text layer */
            Layer text = new Layer(width, (int) titleExtent.getHeight() + 40, new Color(0x01ffffff, true));
            text.setPaint(titleColor);
            text.drawText(0, titleBase, 0, 0, title, titleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            text.resize(text.getWidth() / scale, text.getHeight() / scale);
            text.setX(0);
            text.setY(0);
   
            if (subtitle.length() > 0) {
                /* draw the subtitle normal sized */
                text.setPaint(subtitleColor);
                text.drawText(0, subTitleBase, 0, 0, subtitle, subTitleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            }
   
            /* merge the image and text layers */
            text.setY(paddingY);
            text.setX(paddingX);
            text.setBackgroundColor(bgColor);
   
            int bgWidth = bg.getWidth();
            if ( text.getWidth() + 2 * paddingX > bgWidth ) {
                bgWidth = text.getWidth() + 2 * paddingX;
                bg.resize(bgWidth, bg.getHeight());
            }
            bg.merge(text);
   
            return bg;
        }
    }
   ```

1. 保存更改。
1. 在您的瀏覽器中，重新載入產品頁面。 頂端導覽現在顯示如下：

   ![screen_shot_2012-03-07at10047pm](assets/screen_shot_2012-03-07at10047pm.png)

### 建立清單子元件 {#creating-the-list-children-component}

建立listchildren元件，此元件會產生包含頁面標題、說明和日期（例如產品頁面）的頁面連結清單。 連結的目標是目前頁面的子頁面，或是元件對話方塊中指定的根頁面的子頁面。

![chlimage_1-41](assets/chlimage_1-41.png)

#### 建立產品頁面 {#creating-product-pages}

在產品頁面下方建立兩個頁面。 對於每個說明兩個特定產品的頁面，您可以設定標題、說明和日期。

1. 在「網站」頁面的資料夾樹狀結構中，選取「網站/我的網站/英文/產品」專案，然後按一下「新增>新增頁面」。
1. 在對話方塊中輸入下列屬性值，然後按一下「建立」：

   * 標題：產品1。
   * 名稱： product1。
   * 選取我的網站內容頁面範本

1. 使用以下屬性值在Products底下建立另一個頁面：

   * 標題：產品2
   * 名稱： product2
   * 選取我的網站內容頁面範本

1. 在CRXDE Lite中，設定「產品1」頁面的說明和日期：

   1. 選取 `/content/mywebsite/en/products/product1/jcr:content` 節點。
   1. 在 **屬性** 索引標籤中，輸入下列值：

      * 名称: `jcr:description`
      * 类型: `String`
      * 价值: `This is a description of the Product 1!.`
   1. 按一下 **新增**.
   1. 在 **屬性** 索引標籤中，使用下列值建立另一個屬性：

      * 名稱：日期
      * 型別：字串
      * 值： 2008年2月14日
      * 按一下「新增」。
   1. 按一下「儲存全部」。



1. 在CRXDE Lite中，設定「產品2」頁面的說明和日期：

   1. 選取/content/mywebsite/en/products/product2/jcr：content節點。
   1. 在 **屬性** 索引標籤中，輸入下列值：

      * 名稱： jcr：description
      * 型別：字串
      * 值：這是產品2的說明！。
   1. 按一下 **新增**.
   1. 在相同文字方塊中，將先前的值取代為下列值：

      * 名稱：日期
      * 型別：字串
      * 值： 2012年5月11日
      * 按一下「新增」。
   1. 按一下「儲存全部」。



#### 建立清單子元件 {#creating-the-list-children-component-1}

若要建立listchildren元件：

1. 在CRXDE Lite中按一下滑鼠右鍵 `/apps/mywebsite/components`，選取 **建立**，則 **建立元件**.
1. 在對話方塊中輸入下列屬性值，然後按下一步：

   * 標籤： listchildren。
   * 標題：我的Listchildren元件。
   * 說明：這是我的清單子元件。

1. 繼續按「下一步」，直到「允許的子系」面板出現，然後按一下「確定」。

#### 建立清單子指令碼 {#creating-the-list-children-script}

為listchildren元件開發指令碼。

1. 在CRXDE Lite中，開啟檔案 `listchildren.jsp` 在 `/apps/mywebsite/components/listchildren`.
1. 將預設程式碼取代為下列程式碼：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
            com.day.cq.wcm.api.PageFilter"%><%
        /* Create a new Page object using the path of the current page */
         String listroot = properties.get("listroot", currentPage.getPath());
        Page rootPage = pageManager.getPage(listroot);
        /* iterate through the child pages and gather properties */
        if (rootPage != null) {
            Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
            while (children.hasNext()) {
                Page child = children.next();
                String title = child.getTitle() == null ? child.getName() : child.getTitle();
                String date = child.getProperties().get("date","");
                %><div class="item">
                <a href="<%= child.getPath() %>.html"><b><%= title %></b></a>
                <span><%= date %></code><br>
                <%= child.getProperties().get("jcr:description","") %><br>
                </div><%
            }
        }
    %>
   ```

1. 保存更改。

#### 建立清單子系對話方塊 {#creating-the-list-children-dialog}

建立用來設定listchildren元件屬性的對話方塊。

1. 在listchildren元件下建立對話方塊節點：

   1. 在CRXDE Lite中，以滑鼠右鍵按一下 `/apps/mywebsite/components/listchildren`節點並按一下 **建立** > **建立對話方塊**.

   1. 在對話方塊中，輸入下列屬性值，然後按一下確定

      * **標籤**： `dialog`

      * **標題**： `Edit Component` 並按一下 **確定**.

   ![screen_shot_2012-03-07at45818pm](assets/screen_shot_2012-03-07at45818pm.png)

   具有以下屬性：

   ![screen_shot_2012-03-07at50415pm](assets/screen_shot_2012-03-07at50415pm.png)

1. 選取 `/apps/mywebsite/components/listchildren/dialog/items/items/tab1` 節點。
1. 在「屬性」標籤中，變更 **標題** 屬性至 `List Children`

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. 選取tab1節點，然後按一下「建立>建立節點」，輸入下列屬性值，然後按一下「確定」：

   * 名稱：專案
   * 型別： cq：WidgetCollection

   ![screen_shot_2012-03-07at51018pm](assets/screen_shot_2012-03-07at51018pm.png)

1. 使用以下屬性值在items節點底下建立節點：

   * 名稱： listroot
   * 型別：cq：Widget

   ![screen_shot_2012-03-07at51031pm](assets/screen_shot_2012-03-07at51031pm.png)

1. 新增listroot節點的屬性，以將其設定為文字欄位。 下表中的每一列代表屬性。 完成後，按一下「儲存全部」。

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | 欄位標籤 | 字符串 | 列表根的路径 |
   | name | 字符串 | 。/listroot |
   | xtype | 字符串 | textfield |

   ![screen_shot_2012-03-07at51433pm](assets/screen_shot_2012-03-07at51433pm.png)

#### 在Contentpage元件中包含清單子項 {#including-list-children-in-the-contentpage-component}

若要在您的contentpage元件中包含listchildren元件，請依照下列步驟進行：

1. 在CRXDE Lite中，開啟檔案 `left.jsp` 在 `/apps/mywebsite/components/contentpage` 並找出下列程式碼（第4行）：

   ```xml
   <div>newslist</div>
   ```

1. 將該程式碼取代為下列程式碼：

   ```xml
   <cq:include path="newslist" resourceType="mywebsite/components/listchildren" />
   ```

1. 保存更改。

#### 檢視頁面中的清單子系 {#viewing-list-children-in-a-page}

若要檢視此元件的完整作業，您可以檢視「產品」頁面：

* 父頁面（「清單根的路徑」）未定義時。
* 定義父頁面（「清單根的路徑」）時。

1. 在您的瀏覽器中，重新載入產品頁面。 listchildren元件顯示如下：

   ![chlimage_1-43](assets/chlimage_1-43.png)

1. ![chlimage_1-44](assets/chlimage_1-44.png)

1. 作為清單根的路徑，請輸入： `/content/mywebsite/en`. 单击确定。現在頁面上的listchildren元件看起來如下所示：

   ![chlimage_1-45](assets/chlimage_1-45.png)

### 建立標誌元件 {#creating-the-logo-component}

建立可顯示公司標誌並提供網站首頁連結的元件。 元件包含設計模式對話方塊，以便屬性值儲存在網站設計(/etc/designs/mywebsite)中：

* 屬性值會套用至新增至使用設計之頁面的所有元件例項。
* 屬性可使用元件在使用設計的頁面上的任何例項進行設定。

您的設計模式對話方塊包含設定影像和連結路徑的屬性。 標誌元件會放置在網站中所有頁面的左上角。

其外觀如下：

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Adobe Experience Manager提供更完整的標誌元件( `/libs/foundation/components/logo`)。

#### 建立標誌元件節點 {#creating-the-logo-component-node}

若要建立標誌元件，請遵循下列步驟：

1. 在CRXDE Lite中按一下滑鼠右鍵/apps/mywebsite/components，然後選取 **建立**，則 **建立元件**.
1. 在「建立元件」對話方塊中輸入下列屬性值，然後按一下「下一步」：

   * 标签: `logo`.
   * 标题: `My Logo Component`.
   * 描述: `This is My Logo Component`.

1. 按一下「下一步」 ，直到到達對話方塊的最後一個面板，然後按一下 **確定**.

#### 建立標誌指令碼 {#creating-the-logo-script}

本節說明如何建立指令碼，以顯示含有首頁連結的標誌影像。

1. 在CRXDE Lite中，開啟檔案 `logo.jsp` 在 `/apps/mywebsite/components/logo`.
1. 下列程式碼會建立網站首頁的連結，並新增對標誌影像的參照。 將程式碼複製到 `logo.jsp`：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.text.Text,
                      com.day.cq.wcm.foundation.Image,
                      com.day.cq.commons.Doctype" %><%
       /* obtain the path for home */
       long absParent = currentStyle.get("absParent", 2L);
       String home = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);
       /* obtain the image */
       Resource res = currentStyle.getDefiningResource("imageReference");
       if (res == null) {
           res = currentStyle.getDefiningResource("image");
       }
       /* if no image use text link, otherwise draw the image */
       %>
   <a href="<%= home %>.html"><%
       if (res == null) {
           %>Home<%
       } else {
           Image img = new Image(res);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out);
       }
       %></a>
   ```

1. 保存更改。

#### 建立標誌設計對話方塊 {#creating-the-logo-design-dialog}

建立對話方塊，以在「設計」模式中設定您的標誌元件。 必須命名設計模式對話方塊節點 `design_dialog`.

1. 在標誌元件下建立對話方塊節點：

   1. 以滑鼠右鍵按一下 `/apps/mywebsite/components/logo` 節點並按一下 **建立** > **建立對話方塊**.

   1. 輸入下列屬性值，然後按一下「確定」：

      * **標籤：** `design_dialog`

      * **标题:** `Logo (Design)`

1. 以滑鼠右鍵按一下design_dialog分支中的tab1節點，然後按一下「刪除」。 按一下「儲存全部」。
1. 在 `design_dialog/items/items`節點，建立名為的新節點 `img` 型別 `cq:Widget`. 新增下列屬性，然後按一下「儲存全部」：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | fileNameParameter | 字符串 | 。/imageName |
   | fileReferenceParameter | 字符串 | 。/imageReference |
   | name | 字符串 | 。/图像 |
   | 标题 | 字符串 | 图像 |
   | xtype | 字符串 | html5smartimage |

   ![chlimage_1-47](assets/chlimage_1-47.png)

#### 建立標誌演算指令碼 {#creating-the-logo-render-script}

建立指令碼，擷取標誌影像並將其寫入頁面。

1. 以滑鼠右鍵按一下logo元件節點，然後按一下「建立>建立檔案」以建立名為img.java的GET檔。
1. 開啟檔案，將下列程式碼複製到檔案中，然後按一下「儲存全部」：

```java
package apps.mywebsite.components.logo;

import java.io.IOException;
import java.io.InputStream;

import javax.jcr.RepositoryException;
import javax.jcr.Property;
import javax.servlet.http.HttpServletResponse;

import com.day.cq.wcm.foundation.Image;
import com.day.cq.wcm.commons.RequestHelper;
import com.day.cq.wcm.commons.WCMUtils;
import com.day.cq.wcm.commons.AbstractImageServlet;
import com.day.cq.commons.SlingRepositoryException;
import com.day.image.Layer;
import org.apache.commons.io.IOUtils;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ValueMap;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

/**
 * Renders an image
 */
public class img_GET extends AbstractImageServlet {

    protected Layer createLayer(ImageContext c)
            throws RepositoryException, IOException {
        /* don't create the layer yet. handle everything later */
        return null;
    }

    protected void writeLayer(SlingHttpServletRequest req,
                              SlingHttpServletResponse resp,
                              ImageContext c, Layer layer)
            throws IOException, RepositoryException {

        Image image = new Image(c.resource);
        image.setItemName(Image.NN_FILE, "image");
        image.setItemName(Image.PN_REFERENCE, "imageReference");
        if (!image.hasContent()) {
            resp.sendError(HttpServletResponse.SC_NOT_FOUND);
            return;
        }
        /* get pure layer */
        layer = image.getLayer(false, false, false);

        /* do not re-encode layer, just spool */
        Property data = image.getData();
        InputStream in = data.getStream();
        resp.setContentLength((int) data.getLength());
        String contentType = image.getMimeType();
        if (contentType.equals("application/octet-stream")) {
            contentType=c.requestImageType;
        }
        resp.setContentType(contentType);
        IOUtils.copy(in, resp.getOutputStream());
        in.close();

        resp.flushBuffer();
    }
}
```

#### 將標誌元件新增至Contentpage元件 {#adding-the-logo-component-to-the-contentpage-component}

1. 在CRXDE Lite中，開啟 `left.jsp` 在 `/apps/mywebsite/components/contentpage file` 並找到下列程式碼行：

   ```xml
   <div>logo</div>
   ```

1. 將該程式碼取代為下列程式碼行：

   ```xml
   <cq:include path="logo" resourceType="mywebsite/components/logo" />
   ```

1. 保存更改。
1. 在您的瀏覽器中，重新載入產品頁面。 標誌看起來如下，但目前只顯示基礎連結：

   ![chlimage_1-48](assets/chlimage_1-48.png)

#### 設定頁面中的標誌影像 {#setting-the-logo-image-in-a-page}

本節說明如何使用設計模式對話方塊將影像設定為您的標誌。

1. 在瀏覽器中開啟「產品」頁面後，按一下Sidekick底部的「設計」按鈕以進入設計模式。

   ![](do-not-localize/chlimage_1-1.png)

1. 在「設計圖志列」中，按一下「編輯」以使用對話方塊來編輯圖志元件的設定。
1. 在對話方塊中，按一下「影像」標籤面板中的，瀏覽您從mywebsite.zip檔案擷取的logo.png影像，然後按一下「確定」。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 按一下Sidekick標題列上的三角形以返回「編輯」模式。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. 在CRXDE Lite中，前往下列節點以檢視儲存的屬性值：

   `/etc/designs/mywebsite/jcr:content/contentpage/logo`

### 包含階層連結元件 {#including-the-breadcrumb-component}

在本節中，您將包含階層連結（追蹤）元件，這是基礎元件之一。

1. 在CRXDE Lite中，瀏覽至 `/apps/mywebsite/components/contentpage`，開啟檔案 `center.jsp` 和取代：

   ```java
   <div>trail</div>
   ```

   替换为:

   ```xml
   <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
   ```

1. 保存更改。
1. 在您的瀏覽器中，重新載入 **產品1** 頁面。 軌跡元件看起來如下：

   ![chlimage_1-50](assets/chlimage_1-50.png)

### 包含標題元件 {#including-the-title-component}

在本節中，您將包含標題元件，這是基礎元件之一。

1. 在CRXDE Lite中，瀏覽至 `/apps/mywebsite/components/contentpage`，開啟檔案 `center.jsp` 和取代：

   ```xml
   <div>title</div>
   ```

   替换为:

   ```xml
   <cq:include path="title" resourceType="foundation/components/title" />
   ```

1. 保存更改。
1. 在您的瀏覽器中，重新載入產品頁面。 標題元件如下所示：

   ![chlimage_1-51](assets/chlimage_1-51.png)

   **注意**：您可以在編輯模式中設定不同的標題和型別/大小。

### 包含段落系統元件 {#including-the-paragraph-system-component}

段落系統(parsys)是網站的重要部分，因為它管理著段落清單。 它可讓作者將段落元件新增至頁面並提供結構。

將parsys元件（基礎元件之一）新增至contentpage元件。

1. 在CRXDE Lite中，瀏覽至 `/apps/mywebsite/components/contentpage`，開啟檔案 `center.jsp` 並找到下列程式碼行：

   ```xml
   <div>parsys</div>
   ```

1. 將這行程式碼取代為下列程式碼，然後儲存變更：

   ```xml
   <cq:include path="par" resourceType="foundation/components/parsys" />
   ```

1. 在瀏覽器中，重新整理「產品」頁面。 它現在具有parsys元件，如下所示：

   ![chlimage_1-52](assets/chlimage_1-52.png)

### 建立影像元件 {#creating-the-image-component}

建立可在段落系統中顯示影像的元件。 為了節省時間，影像元件會建立為商標元件的復本，並有一些屬性變更。

>[!NOTE]
>
>Adobe Experience Manager提供更完整的影像元件( `/libs/foundation/components/image`)。

#### 建立影像元件 {#creating-the-image-component-1}

1. 用滑鼠右鍵按一下 `/apps/mywebsite/components/logo` 節點，然後按一下「複製」。
1. 以滑鼠右鍵按一下 `/apps/mywebsite/components` 節點，然後按一下「貼上」。
1. 以滑鼠右鍵按一下 `Copy of logo` 節點，按一下「重新命名」，刪除現有文字並鍵入 `image`.

1. 選取 `image` 元件節點，並變更下列屬性值：

   * `jcr:title:` 我的影像元件。
   * `jcr:description`：這是我的影像元件。

1. 將屬性新增至 `image` 具有下列屬性值的節點：

   * 名稱： componentGroup
   * 型別：字串
   * 值： MyWeb站點

1. 在 `image` 節點，重新命名 `design_dialog` 節點至 `dialog`.

1. 重新命名 `logo.jsp` 至 `image.jsp.`

1. 開啟img.javaGET並將套件變更為 `apps.mywebsite.components.image`.

![chlimage_1-53](assets/chlimage_1-53.png)

#### 建立影像指令碼 {#creating-the-image-script}

本節說明如何建立影像指令碼。

1. 打开 `/apps/mywebsite/components/image/` `image.jsp`
1. 使用以下程式碼取代現有程式碼，然後儲存變更：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.cq.commons.Doctype,
                       com.day.cq.wcm.foundation.Image,
                       com.day.cq.wcm.api.components.DropTarget,
                       com.day.cq.wcm.api.components.EditConfig,
                       com.day.cq.wcm.commons.WCMUtils" %><%
    /* global.jsp provides access to the current resource through the resource object */
           Image img = new Image(resource);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out); %>
   ```

1. 保存更改。

#### 建立影像cq：editConfig節點 {#creating-the-image-cq-editconfig-node}

此 `cq:editConfig` 節點型別可讓您在編輯元件的屬性時設定元件的特定行為。

在此區段中，您可使用cq：editConfig節點將資產從「內容尋找器」拖曳至影像元件中。

1. 在CRXDE Lite的/apps/mywebsite/components/image節點下，建立新節點，如下所示：

   * 名稱：cq：editConfig。
   * 型別：cq：EditConfig。

1. 在節點cq：editConfig下，建立新節點，如下所示：

   * 名稱： cq：dropTargets。
   * 型別：cq：DropTargetConfig。

1. 在cq：dropTargets節點下，建立新節點，如下所示：

   * 名稱：影像。
   * 型別： nt：unstructured。

1. 在CRXDE中，設定屬性如下：

| 名称 | 类型 | 价值 |
|---|---|---|
| 接受 | 字符串 | image/(gif | jpeg | png) |
| 组 | 字符串 | 媒體 |
| propertyName | 字符串 | 。/imageReference |

![chlimage_1-54](assets/chlimage_1-54.png)

#### 新增圖示 {#adding-the-icon}

在本節中，您新增圖示，以便在Sidekick中列出影像元件時顯示在影像元件旁邊：

1. 在CRXDE Lite中，以滑鼠右鍵按一下檔案 `/libs/foundation/components/image/icon.png` 並選取 **複製。**
1. 以滑鼠右鍵按一下節點 `/apps/mywebsite/components/image` 並按一下 **貼上**，然後按一下 **全部儲存**.

#### 使用影像元件 {#using-the-image-component}

在本節中，您將檢視 **產品** 頁面，並將影像元件新增至段落系統。

1. 在您的瀏覽器中，重新載入 **產品** 頁面。
1. 在Sidekick中，按一下 **設計模式** 圖示。
1. 按一下「編輯」按鈕，編輯零件的設計對話方塊。
1. 在對話方塊中， **允許的元件** 會顯示；導覽至 **我的網站**，選取 **我的影像元件** 並按一下 **確定。**
1. 返回至 **編輯模式。**
1. 連按兩下parsys框架(開啟 **將元件或資產拖曳到這裡**)。 此 **插入新元件** 和 **Sidekick** 選取器如下所示：

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

### 包含工具列元件 {#including-the-toolbar-component}

在本節中，您將包含工具列元件，這是基礎元件之一。

在編輯模式和設計模式中，您都有幾個選項。

1. 在CRXDE Lite中，導覽至 `/apps/mywebsite/components/contentpage`，開啟 `body.jsp` 檔案並找出下列程式碼：

   ```java
   <div class="toolbar">toolbar</div>
   ```

1. 用下列程式碼取代該程式碼，然後儲存變更。

   ```java
   <cq:include path="toolbar" resourceType="foundation/components/toolbar"/>
   ```

1. 在「AEM網站」頁面的資料夾樹狀結構中，選取「網站/我的網站/英文」，然後按一下「新增>新增頁面」。 指定下列屬性值，然後按一下「建立」：

   * 標題：工具列
   * 選取我的網站內容頁面範本

1. 在頁面清單中，以滑鼠右鍵按一下「工具列」頁面，然後按一下「屬性」。 選取「在導覽中隱藏」，然後按一下「確定」。

   「在導覽中隱藏」選項可防止頁面出現在導覽元件中，例如topnav和listchildren。

1. 在「工具列」下，建立下列頁面：

   * 連絡人
   * 意見反應
   * 登录
   * 搜索

1. 在您的瀏覽器中，重新載入產品頁面。 如下所示：

   ![chlimage_1-55](assets/chlimage_1-55.png)

### 建立搜尋元件 {#creating-the-search-component}

在本節中，您將建立元件以搜尋網站上的內容。 此搜尋元件可放置在任何頁面的段落系統中（例如，在專門的搜尋結果頁面上）。

您的搜尋輸入方塊將會如下所示 **英文** 頁面：

![chlimage_1-56](assets/chlimage_1-56.png)

#### 建立搜尋元件 {#creating-the-search-component-1}

1. 在CRXDE Lite中按一下滑鼠右鍵 `/apps/mywebsite/components`，選取 **建立**，則 **建立元件**.
1. 使用對話方塊來設定元件：

   1. 在第一個面板中，指定下列屬性值：

      * 標籤：搜尋
      * 標題：我的搜尋元件
      * 說明：這是我的搜尋元件
      * 群組：我的網站
   1. 按「下一步」，然後再次按「下一步」。
   1. 在「允許的父項」面板上，按一下+按鈕並鍵入 `*/parsys`.
   1. 按一下「下一步」，然後按一下「確定」。


1. 按一下「儲存全部」。
1. 複製下列節點並貼到apps/mywebsite/components/search節點：

   * `/libs/foundation/components/search/dialog`
   * `` `/libs/foundation/components/search/i18n`

   * `/libs/foundation/components/search/icon.png`

1. 按一下「儲存全部」。

#### 建立搜尋指令碼 {#creating-the-search-script}

本節說明如何建立搜尋命令檔：

1. 開啟 `/apps/mywebsite/components/search/search.jsp` 檔案。
1. 將下列程式碼複製到 `search.jsp`：

   ```java
   <%@ page import="com.day.cq.wcm.foundation.Search,com.day.cq.tagging.TagManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   %><cq:setContentBundle/><%
       Search search = new Search(slingRequest);
   
       String searchIn = (String) properties.get("searchIn");
       String requestSearchPath = request.getParameter("path");
       if (searchIn != null) {
           /* only allow the "path" request parameter to be used if it
            is within the searchIn path configured */
           if (requestSearchPath != null && requestSearchPath.startsWith(searchIn)) {
               search.setSearchIn(requestSearchPath);
           } else {
               search.setSearchIn(searchIn);
           }
       } else if (requestSearchPath != null) {
           search.setSearchIn(requestSearchPath);
       }
   
       pageContext.setAttribute("search", search);
       TagManager tm = resourceResolver.adaptTo(TagManager.class);
   %><c:set var="trends" value="${search.trends}"/><%
   %><center>
     <form action="${currentPage.path}.html">
       <input size="41" maxlength="2048" name="q" value="${fn:escapeXml(search.query)}"/>
       <input value="<fmt:message key="searchButtonText"/>" type="submit" />
     </form>
   </center>
   <br/>
   <c:set var="result" value="${search.result}"/>
   <c:choose>
     <c:when test="${empty result && empty search.query}">
     </c:when>
     <c:when test="${empty result.hits}">
       <c:if test="${result.spellcheck != null}">
         <p><fmt:message key="spellcheckText"/> <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${result.spellcheck}"/></c:url>"><b><c:out value="${result.spellcheck}"/></b></a></p>
       </c:if>
       <fmt:message key="noResultsText">
         <fmt:param value="${fn:escapeXml(search.query)}"/>
       </fmt:message>
     </c:when>
     <c:otherwise>
       <p class="searchmeta">Results ${result.startIndex + 1} - ${result.startIndex + fn:length(result.hits)} of ${result.totalMatches} for <b>${fn:escapeXml(search.query)}</b>. (${result.executionTime} seconds)</p>
      <br/>
   
     <div class="searchresults">
       <div class="results">
         <c:forEach var="hit" items="${result.hits}" varStatus="status">
           <div class="hit">
           <a href="${hit.URL}">${hit.title}</a>
           <div class="excerpt">${hit.excerpt}</div>
          <div class="hiturl"> ${hit.URL}<c:if test="${!empty hit.properties['cq:lastModified']}"> - <c:catch><fmt:formatDate value="${hit.properties['cq:lastModified'].time}" dateStyle="medium"/></c:catch></c:if> - <a href="${hit.similarURL}"><fmt:message key="similarPagesText"/></a>
           </div></div>
         </c:forEach>
       </div>
         <br/>
   
        <div class="searchRight">
             <c:if test="${fn:length(trends.queries) > 0}">
                 <p><fmt:message key="searchTrendsText"/></p>
                 <div class="searchTrends">
                     <c:forEach var="query" items="${trends.queries}">
                         <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${query.query}"/></c:url>"><span style="font-size:${query.size}px"><c:out value="${query.query}"/></code></a>
                     </c:forEach>
                 </div>
             </c:if>
             <c:if test="${result.facets.languages.containsHit}">
                 <p>Languages</p>
                 <c:forEach var="bucket" items="${result.facets.languages.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value='<%= new java.util.Locale((String) pageContext.getAttribute("bucketValue")).getDisplayLanguage(request.getLocale()) %>'/>
                     <c:choose>
                         <c:when test="${param.language != null}">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.tags.containsHit}">
                 <p>Tags</p>
                 <c:forEach var="bucket" items="${result.facets.tags.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="tag" value="<%= tm.resolve((String) pageContext.getAttribute("bucketValue")) %>"/>
                     <c:if test="${tag != null}">
                         <c:set var="label" value="${tag.title}"/>
                         <c:choose>
                             <c:when test="<%= request.getParameter("tag") != null && java.util.Arrays.asList(request.getParameterValues("tag")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="tag" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                             <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="tag" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                         </c:choose><br/>
                     </c:if>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.mimeTypes.containsHit}">
                 <jsp:useBean id="fileTypes" class="com.day.cq.wcm.foundation.FileTypes"/>
                 <p>File types</p>
                 <c:forEach var="bucket" items="${result.facets.mimeTypes.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value="${fileTypes[bucket.value]}"/>
                     <c:choose>
                         <c:when test="<%= request.getParameter("mimeType") != null && java.util.Arrays.asList(request.getParameterValues("mimeType")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.lastModified.containsHit}">
                 <p>Last Modified</p>
                 <c:forEach var="bucket" items="${result.facets.lastModified.buckets}">
                     <c:choose>
                         <c:when test="${param.from == bucket.from && param.to == bucket.to}">${bucket.value} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/><c:if test="${bucket.from != null}"><cq:addParam name="from" value="${bucket.from}"/></c:if><c:if test="${bucket.to != null}"><cq:addParam name="to" value="${bucket.to}"/></c:if></cq:requestURL>">${bucket.value} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
   
         <c:if test="${fn:length(search.relatedQueries) > 0}">
   
          <br/><br/><div class="related">
           <fmt:message key="relatedSearchesText"/>
           <c:forEach var="rq" items="${search.relatedQueries}">
               <a href="${currentPage.path}.html?q=${rq}"><c:out value="${rq}"/></a>
           </c:forEach></div>
         </c:if>
         </div>
   
         <c:if test="${fn:length(result.resultPages) > 1}">
           <div class="pagination">
               <fmt:message key="resultPagesText"/>
           <c:if test="${result.previousPage != null}">
             <a href="${result.previousPage.URL}"><fmt:message key="previousText"/></a>
           </c:if>
           <c:forEach var="page" items="${result.resultPages}">
             <c:choose>
               <c:when test="${page.currentPage}">${page.index + 1}</c:when>
               <c:otherwise>
                 <a href="${page.URL}">${page.index + 1}</a>
               </c:otherwise>
             </c:choose>
           </c:forEach>
           <c:if test="${result.nextPage != null}">
             <a href="${result.nextPage.URL}"><fmt:message key="nextText"/></a>
           </c:if>
           </div>
         </c:if>
         </div>
   
     </c:otherwise>
   </c:choose>
   ```

1. 保存更改。

#### 在Contentpage元件中包含搜尋方塊 {#including-a-search-box-in-the-contentpage-component}

若要在內容頁面的左側區段中加入搜尋輸入方塊，請依照下列步驟進行：

1. 在CRXDE Lite中，開啟檔案 `left.jsp` 在 `/apps/mywebsite/components/contentpage` 並找出下列程式碼（第2行）：

   ```xml
   %><div class="left">
   ```

1. 插入下列程式碼 **早於** 該行：

   ```java
   %><%@ page import="com.day.text.Text"%><%
   %><% String docroot = currentDesign.getPath();
   String home = Text.getAbsoluteParent(currentPage.getPath(), 2);%><%
   ```

1. 找到下列程式碼行：

   ```xml
   <div>search</div>
   ```

1. 用下列程式碼取代該程式碼，然後儲存變更。

   ```java
   <div class="form_1">
        <form class="geo" action="<%= home %>/toolbar/search.html" id="form" >
             <p>
                  <input class="geo" type="text" name="q"><br>
                  <a href="<%= home %>/toolbar/search.html" class="link_1">advanced search</a>
             </p>
        </form>
   </div>
   ```

1. 在您的瀏覽器中，重新載入產品頁面。 搜尋元件如下所示：

   ![chlimage_1-57](assets/chlimage_1-57.png)

#### 在搜尋頁面中包含搜尋元件 {#including-the-search-component-in-the-search-page}

在本節中，您將搜尋元件新增至段落系統。

1. 在瀏覽器中，開啟「搜尋」頁面。
1. 在Sidekick中，按一下設計模式圖示。
1. 在「設計段落區塊」(Design of par block)中（在「搜尋」標題下），按一下「編輯」(Edit)。
1. 在對話方塊中，向下捲動至  **我的網站** 群組，選取 **我的搜尋元件** 並按一下 **確定**.
1. 在Sidekick上，按一下三角形以返回編輯模式。
1. 將My Search元件從Sidekick拖曳至parsys框架。 如下所示：

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. 導覽至您的產品頁面。 在輸入方塊中搜尋客戶，然後按Enter。 系統會將您重新導向至「搜尋」頁面。 切換到預覽模式：輸出的格式如下所示：

   ![chlimage_1-59](assets/chlimage_1-59.png)

### 包含Iparsys元件 {#including-the-iparsys-component}

在本節中，您將包含繼承段落系統(iparsys)元件，這是基礎元件之一。 此元件可讓您在父頁面上建立段落結構，並讓子頁面繼承段落。

對於此元件，您可以在編輯模式和設計模式中設定多個引數。

1. 在CRXDE Lite中，導覽至 `/apps/mywebsite/components/contentpage`，開啟檔案 `right.jsp` 和取代：

   ```java
   <div>iparsys</div>
   ```

   替换为:

   ```java
   <cq:include path="rightpar" resourceType="foundation/components/iparsys" />
   ```

1. 保存更改。
1. 在您的瀏覽器中，重新載入** Products**頁面。 整個頁面如下：

   ![chlimage_1-5](assets/chlimage_1-5.jpeg)
