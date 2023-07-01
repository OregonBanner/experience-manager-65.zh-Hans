---
title: 测试您的UI
description: AEM提供了一个框架，用于实现AEM UI测试的自动化
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# 测试您的UI{#testing-your-ui}

>[!NOTE]
>
>从AEM 6.5开始，弃用hobbes.js UI测试框架。 Adobe不打算对其做进一步增强，因此建议客户使用Selenium自动化功能。
>
>参见 [已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md).

AEM提供了一个框架，用于实现AEM UI测试的自动化。 使用该框架，您可以直接在Web浏览器中编写和运行UI测试。 该框架提供了用于创建测试的JavaScript API。

AEM测试框架使用以JavaScript编写的测试库Hobbes.js。 Hobbes.js框架是为了在开发过程中测试AEM而开发的。 该框架现在可公开用于测试您的AEM应用程序。

>[!NOTE]
>
>请参阅Hobbes.js [文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html) 以了解API的完整详细信息。

## 测试结构 {#structure-of-tests}

在AEM中使用自动测试时，请务必了解以下术语：

| 操作 | An **操作** 是网页上的特定活动，例如单击链接或按钮。 |
|---|---|
| 测试用例 | A **测试用例** 是一种特定情况，可以由一个或多个 **操作**. |
| 测试套件 | A **测试套件** 是一组相关 **测试用例** 共同测试特定用例。 |

## 执行测试 {#executing-tests}

### 查看测试包 {#viewing-test-suites}

打开测试控制台以查看注册的测试包。 测试面板包含测试包及其测试用例的列表。

通过以下方式导航到“工具”控制台： **全局导航 — >工具>操作 — >测试**.

![chlimage_1-63](assets/chlimage_1-63.png)

打开控制台时，左侧列出测试包，并附带按顺序运行所有测试包的选项。 带有方格背景的右侧显示的空间是一个占位符，用于在测试运行时显示页面内容。

![chlimage_1-64](assets/chlimage_1-64.png)

### 运行单个测试包 {#running-a-single-test-suite}

测试包可以单独运行。 运行测试包时，页面会随着测试用例及其操作的执行而发生更改，并且在测试完成后显示结果。 图标指示结果。

复选标记图标表示已通过测试：

![复选标记图标。](do-not-localize/chlimage_1-2.png)

“X”图标表示测试失败：

![圆环内由X表示的失败测试图标。](do-not-localize/chlimage_1-3.png)

要运行测试包，请执行以下操作：

1. 在测试面板中，单击或点按要运行的测试用例的名称以展开操作的详细信息。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 单击 **运行测试**.

   ![“运行测试”按钮的图像，由圆圈内面向右的指针指示。](do-not-localize/chlimage_1-4.png)

1. 在执行测试时，占位符会被替换为页面内容。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 通过点按或单击描述以打开 **结果** 面板。 在中点击或单击测试用例的名称 **结果** 面板显示所有详细信息。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 运行多个测试 {#running-multiple-tests}

测试包将按照它们在控制台中的显示顺序依次执行。 您可以深入到测试中查看详细结果。

![chlimage_1-68](assets/chlimage_1-68.png)

1. 在测试面板上，点按或单击 **运行所有测试** 按钮或 **运行测试** 按钮时，单击要运行的测试包标题下方的“测试包”按钮。

   ![“Run all tests（运行所有测试）”按钮和“Run tests（运行测试）”按钮的图像，由圆圈内面向右的指针指示。](do-not-localize/chlimage_1-5.png)

1. 要查看每个测试用例的结果，请单击测试用例的标题。 单击中测试的名称 **结果** 面板显示所有详细信息。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## 创建和使用简单的测试套件 {#creating-and-using-a-simple-test-suite}

以下过程会逐步引导您使用创建和执行测试包 [We.Retail内容](/help/sites-developing/we-retail.md)，但您可以轻松地将测试修改为使用其他网页。

有关创建您自己的测试包的完整详细信息，请参阅 [Hobbes.js API文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html).

1. 打开CRXDE Lite。 ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. 右键单击 `/etc/clientlibs` 文件夹并单击 **“创建”>“创建文件夹”**. 类型 `myTests` 名称，然后单击 **确定**.
1. 右键单击 `/etc/clientlibs/myTests` 文件夹并单击 **创建>创建节点**. 使用以下属性值，然后单击 **确定**：

   * 名称: `myFirstTest`
   * 类型: `cq:ClientLibraryFolder`

1. 将以下属性添加到myFirstTest节点：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | `categories` | String[] | `granite.testing.hobbes.tests` |
   | `dependencies` | String[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**仅限AEM Forms**
   >
   >
   >要测试自适应表单，请将以下值添加到类别和依赖关系。 例如：
   >
   >
   >**类别**： `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**依赖关系**： `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 单击 **全部保存**.
1. 右键单击 `myFirstTest` 节点并单击 **“创建”>“创建文件”**. 为文件命名 `js.txt` 并单击 **确定**.
1. 在 `js.txt` 文件，输入以下文本：

   ```
   #base=.
   myTestSuite.js
   ```

1. 单击 **全部保存** 然后关闭 `js.txt` 文件。
1. 右键单击 `myFirstTest` 节点并单击 **“创建”>“创建文件”**. 为文件命名 `myTestSuite.js` 并单击 **确定**.
1. 将以下代码复制到 `myTestSuite.js` 文件，然后保存文件：

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

1. 导航到 **测试** 控制台以试用您的测试套件。
