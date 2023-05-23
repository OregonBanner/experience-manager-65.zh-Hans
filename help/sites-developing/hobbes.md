---
title: 測試您的UI
seo-title: Testing Your UI
description: AEM為AEM UI提供自動化測試框架
seo-description: AEM provides a framework for automating tests for your AEM UI
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 1%

---

# 測試您的UI{#testing-your-ui}

>[!NOTE]
>
>自AEM 6.5起，hobbes.js UI測試框架已過時。 Adobe不打算進一步增強功能，因此建議客戶使用Selenium自動化。
>
>另請參閱 [過時和移除的功能](/help/release-notes/deprecated-removed-features.md).

AEM為AEM UI提供自動化測試框架。 使用該架構，您可以直接在網頁瀏覽器中編寫和執行UI測試。 此架構提供用於建立測試的JavaScript API。

AEM測試架構使用Hobbes.js，這是以Javascript撰寫的測試程式庫。 開發Hobbes.js架構是為了在開發過程中測試AEM。 此架構現在可供公眾用來測試您的AEM應用程式。

>[!NOTE]
>
>請參閱Hobbes.js [檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html) 以取得API的完整詳細資料。

## 測試結構 {#structure-of-tests}

在AEM中使用自動化測試時，請務必瞭解下列詞語：

| 操作 | 一個 **動作** 是網頁上的特定活動，例如按一下連結或按鈕。 |
|---|---|
| 測試案例 | A **測試案例** 是一種特定情況，可能由一或多個 **動作**. |
| 測試套裝 | A **測試套裝** 是一組相關 **測試案例** 一起測試特定使用案例。 |

## 執行測試 {#executing-tests}

### 檢視測試套裝 {#viewing-test-suites}

開啟測試主控台，檢視已註冊的測試套裝。 「測試」面板包含測試套裝及其測試案例的清單。

透過以下方式導覽至「工具」主控台： **全域導覽 — >工具>操作 — >測試**.

![chlimage_1-63](assets/chlimage_1-63.png)

開啟主控台時，左側會列出測試套裝，以及可依序執行所有測試的選項。 右側顯示有格線背景的空格是測試執行時顯示頁面內容的預留位置。

![chlimage_1-64](assets/chlimage_1-64.png)

### 執行單一測試套裝 {#running-a-single-test-suite}

測試套裝可以個別執行。 當您執行測試套裝時，頁面會隨著測試案例及其動作的執行而變更，並且會在測試完成後顯示結果。 圖示會指出結果。

核取記號圖示表示測試通過：

![](do-not-localize/chlimage_1-2.png)

「X」圖示表示測試失敗：

![](do-not-localize/chlimage_1-3.png)

若要執行測試套裝：

1. 在「測試」面板中，按一下或點選您要執行的測試案例名稱，以展開動作的詳細資訊。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 按一下或點選 **執行測試** 按鈕。

   ![](do-not-localize/chlimage_1-4.png)

1. 測試執行時，預留位置會取代為頁面內容。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 點選或按一下說明以開啟測試案例的結果 **結果** 面板。 在中點選或按一下測試案例的名稱 **結果** 面板顯示所有詳細資料。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 執行多項測試 {#running-multiple-tests}

測試套裝會依顯示在主控台中的順序執行。 您可以深入研究測試以檢視詳細結果。

![chlimage_1-68](assets/chlimage_1-68.png)

1. 在「測試」面板上，點選或按一下 **執行所有測試** 按鈕或 **執行測試** 按鈕來設定您要執行之測試套裝的標題。

   ![](do-not-localize/chlimage_1-5.png)

1. 若要檢視每個測試案例的結果，請點選或按一下測試案例的標題。 在「 」中點選或按一下您的測試名稱 **結果** 面板顯示所有詳細資料。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 建立和使用簡單測試套裝 {#creating-and-using-a-simple-test-suite}

下列程式會逐步引導您使用建立和執行測試套裝 [We.Retail內容](/help/sites-developing/we-retail.md)，但您可以輕鬆修改測試，以使用不同的網頁。

如需建立您自己的測試套裝的完整詳細資訊，請參閱 [Hobbes.js API檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html).

1. 開啟CRXDE Lite。 ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 以滑鼠右鍵按一下 `/etc/clientlibs` 資料夾並按一下 **「建立」>「建立資料夾」**. 型別 `myTests` ，然後按一下 **確定**.
1. 以滑鼠右鍵按一下 `/etc/clientlibs/myTests` 資料夾並按一下 **建立>建立節點**. 使用以下屬性值，然後按一下 **確定**：

   * 名称: `myFirstTest`
   * 类型: `cq:ClientLibraryFolder`

1. 將下列屬性新增至myFirstTest節點：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | `categories` | 字符串[] | `granite.testing.hobbes.tests` |
   | `dependencies` | 字符串[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**僅限AEM Forms**
   >
   >
   >若要測試調適型表單，請將下列值新增至類別和相依性。 例如：
   >
   >
   >**類別**： `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**相依性**： `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 按一下 **全部儲存**.
1. 以滑鼠右鍵按一下 `myFirstTest` 節點並按一下 **「建立」>「建立檔案」**. 為檔案命名 `js.txt` 並按一下 **確定**.
1. 在 `js.txt` 檔案中，輸入下列文字：

   ```
   #base=.
   myTestSuite.js
   ```

1. 按一下 **全部儲存** 然後關閉 `js.txt` 檔案。
1. 以滑鼠右鍵按一下 `myFirstTest` 節點並按一下 **「建立」>「建立檔案」**. 為檔案命名 `myTestSuite.js` 並按一下 **確定**.
1. 將下列程式碼複製到 `myTestSuite.js` 檔案，然後儲存檔案：

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. 導覽至 **測試** 主控台以試用您的測試套裝。
