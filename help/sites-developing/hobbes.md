---
title: 测试UI
seo-title: 测试UI
description: AEM为AEM UI提供了自动化测试的框架
seo-description: AEM为AEM UI提供了自动化测试的框架
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---


# 测试UI{#testing-your-ui}

>[!NOTE]
>
>从AEM 6.5开始，已弃用hobbes.js UI测试框架。 Adobe不打算对其进行进一步的增强，并建议客户使用Selenium自动化。
>
>See [Deprecated and Removed Features](/help/release-notes/deprecated-removed-features.md).

AEM为AEM UI提供了自动化测试的框架。 使用框架，您可以直接在Web浏览器中编写和运行UI测试。 该框架提供了用于创建测试的javascript API。

AEM测试框架使用Hobbes.js，这是一个用Javascript编写的测试库。 Hobbes.js框架是作为开发过程的一部分为测试AEM而开发的。 该框架现在可供公众使用，用于测试AEM应用程序。

>[!NOTE]
>
>有关API的完整详 [细信息](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html) ，请参阅Hobbes.js文档。

## 测试结构 {#structure-of-tests}

在AEM中使用自动测试时，以下术语是重要的，需要了解：

| 操作 | 操 **作** 是网页上的特定活动，如单击链接或按钮。 |
|---|---|
| 测试用例 | 测 **试案例** 是由一个或多个操作组成的特定情 **况**。 |
| 测试套件 | 测 **试套件** 是一组相关测试用例， **它们一** 起测试特定的用例。 |

## 执行测试 {#executing-tests}

### 查看测试套件 {#viewing-test-suites}

打开测试控制台，查看已注册的测试套件。 “Tests（测试）”面板包含测试套件及其测试用例的列表。

通过全局导航->工 **具>操作->测试导航到工具控制台**。

![chlimage_1-63](assets/chlimage_1-63.png)

打开控制台时，测试套件将列在左侧，并提供一个选项以按顺序运行所有测试套件。 右侧显示的带有方格背景的空间是测试运行时显示页面内容的占位符。

![chlimage_1-64](assets/chlimage_1-64.png)

### 运行单个测试套件 {#running-a-single-test-suite}

测试套件可以单独运行。 运行测试套件时，页面会随着测试用例及其操作的执行而发生更改，测试结果会在测试完成后显示。 图标表示结果。

复选标记图标指示通过的测试：

![](do-not-localize/chlimage_1-2.png)

“X”图标表示测试失败：

![](do-not-localize/chlimage_1-3.png)

运行测试套件：

1. 在“Tests（测试）”面板中，单击或点按要运行的测试用例的名称，以展开“Actions（操作）”的详细信息。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 单击或点按“ **运行测试** ”按钮。

   ![](do-not-localize/chlimage_1-4.png)

1. 测试执行时，占位符将替换为页面内容。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 点按或单击说明以打开“结果”面板，查看测试用例 **的结果** 。 点按或单击“结果”面板中的测试用例 **名称** ，将显示所有详细信息。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 运行多个测试 {#running-multiple-tests}

测试套件按其在控制台中的显示顺序顺序执行。 您可以深入测试，查看详细结果。

![chlimage_1-68](assets/chlimage_1-68.png)

1. 在“Tests（测试）”面板上，点 **按或单击** “Run all tests(运行所有测试 **)”按钮，或** 者单击要运行的测试套件标题下的“Run tests（运行测试）”按钮。

   ![](do-not-localize/chlimage_1-5.png)

1. 要视图每个测试用例的结果，请点按或单击测试用例的标题。 点按或单击“结果”面板中的测试名 **称** ，将显示所有详细信息。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 创建和使用简单的测试套件 {#creating-and-using-a-simple-test-suite}

以下过程会指导您使用We.Retail内容创建和执 [行测试套件](/help/sites-developing/we-retail.md)，但您可以轻松修改测试以使用其他网页。

有关创建自己的测试套件的完整详细信息，请 [参阅Hobbes.js API文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html)。

1. 打开CRXDE Lite。 ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 右键单击文件夹， `/etc/clientlibs` 然后单击“ **创建”>“创建文件夹”**。 键入 `myTests` 名称，然后单击“确 **定”**。
1. 右键单击文件夹， `/etc/clientlibs/myTests` 然后单击“ **创建”>“创建节点**”。 使用以下属性值，然后单击“确 **定”**:

   * 名称: `myFirstTest`
   * 类型: `cq:ClientLibraryFolder`

1. 将以下属性添加到myFirstTest节点：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | `categories` | String[] | `granite.testing.hobbes.tests` |
   | `dependencies` | String[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**AEM Forms**
   >
   >
   >要测试自适应表单，请向类别和依赖项添加以下值。 例如：
   >
   >
   >**类别**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**相关性**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 单击“ **全部保存**”。
1. 右键单击该节 `myFirstTest` 点，然后单 **击创建>创建文件**。 命名文件， `js.txt` 然后单 **击确定**。
1. 在文件 `js.txt` 中，输入以下文本：

   ```
   #base=.
   myTestSuite.js
   ```

1. 单击 **“全部保** 存”，然后关闭 `js.txt` 文件。
1. 右键单击该节 `myFirstTest` 点，然后单 **击创建>创建文件**。 命名文件， `myTestSuite.js` 然后单 **击确定**。
1. 将以下代码复制到文 `myTestSuite.js` 件，然后保存文件：

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

1. 导航到测 **试控** 制台以尝试测试套件。
