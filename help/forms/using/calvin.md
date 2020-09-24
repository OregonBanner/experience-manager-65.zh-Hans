---
title: 自动测试自适应表单
seo-title: 自动测试自适应表单
description: 使用Calvin，您可以在CRXDE中创建测试用例，并直接在Web浏览器中运行UI测试，以彻底测试您的自适应表单。
seo-description: 使用Calvin，您可以在CRXDE中创建测试用例，并直接在Web浏览器中运行UI测试，以彻底测试您的自适应表单。
uuid: 7bf4fc8f-96df-4407-8d10-cf18880518bd
contentOwner: gtalwar
content-type: reference
topic-tags: adaptive_forms, develop
discoiquuid: 1cb54c8a-9322-4b5a-b5a7-0eef342cee54
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 1%

---


# 自动测试自适应表单{#automate-testing-of-adaptive-forms}

## 概述 {#overview}

自适应表单是客户互动不可或缺的一部分。 测试自适应表单时，必须对表单进行每次更改，例如推出新的修复包或更改表单中的规则。 但是，功能测试自适应表单及其中的每个字段可能都很繁琐。

Calvin允许您在Web浏览器中自动测试自适应表单。 卡尔文 [利用霍布](/help/sites-developing/hobbes.md)斯公司的用户界面来运行测试，并提供以下工具：

* 用于创建测试的JavaScript API。
* 用于运行测试的用户界面。

使用Calvin，您可以在CRXDE中创建测试用例，并直接在Web浏览器中运行UI测试，以彻底测试自适应表单的以下方面：

<table>
 <tbody>
  <tr>
   <td><strong>要测试的自适应表单方面</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>自适应表单的预填体验</td>
   <td>
    <ul>
     <li>表单是否按预期方式预填充，取决于数据模型的类型？</li>
     <li>表单对象的默认值是否按预期方式预填充？</li>
    </ul> </td>
  </tr>
  <tr>
   <td>提交自适应表单的体验</td>
   <td>
    <ul>
     <li>提交时是否生成了正确的数据？</li>
     <li>提交期间表单是否在服务器上重新验证？</li>
     <li>是否为正在执行的表单配置了提交操作？</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>表达式规则</p> <p> </p> </td>
   <td>
    <ul>
     <li>与表单对象关联的表达式，如在退出字段后执行脚本（在执行相关UI操作后执行）吗？<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>验证</td>
   <td>
    <ul>
     <li>执行操作后，字段验证是否按预期执行？</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>延迟加载</p> <p> </p> </td>
   <td>
    <ul>
     <li>单击选项卡（或面板的任何导航项）后，是否会根据延迟加载配置从服务器获取HTML?</li>
    </ul></td>
  </tr>
  <tr>
   <td><p>UI交互</p> </td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html#toc2__anchor" target="_blank">测试与自适应表单对象的UI交互</a></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 前提条件 {#prerequisites}

在使用本文创建测试用例之前，您需要了解以下内容：

* 使用Hobbes创建测试套件和执行测试用例 [。](https://docs.adobe.com/docs/en/aem/6-3/develop/components/hobbes.html)
* [霍布斯JavaScript API](https://docs.adobe.com/docs/en/aem/6-2/develop/ref/test-api/index.html)
* [Calvin JavaScript API](https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html)

## 示例：使用Hobbes作为测试框架为自适应表单创建测试套件 {#example-create-a-test-suite-for-an-adaptive-form-using-hobbes-as-testing-framework}

以下示例将指导您创建测试套件以测试多个自适应表单。 您需要为需要测试的每个表单创建单独的测试用例。 通过执行与以下步骤类似的步骤并在步骤11中修改JavaScript代码，您可以创建自己的测试套件来测试自适应表单。

1. 在Web浏览器中转到CRXDE Lite: `https://'[server]:[port]'/crx/de`.
1. 右键单击/etc/clientlibs子文件夹，然后单击“ **创建** ”> **“创建节点**”。 输入名称（此处为afTestRegistration），将节点类型指定为cq:ClientLibraryFolder，然后单击“确 **定”。**

   clientlibs文件夹包含应用程序（JS和Init）的注册方面。 建议您在clientlibs文件夹中注册特定于某个表单的所有Hobbes测试套件对象。

1. 在新创建的节点（此处为afTestRegistration）中指定以下属性值，然后单击“全 **部保存”**。 这些属性帮助霍布斯将文件夹识别为测试文件。 要将此客户端库作为其他客户端库的依赖关系重复使用，请将其命名为granite.testing.calvin.tests。

<table>
 <tbody>
  <tr>
   <td>属性</td>
   <td>类型</td>
   <td>值</td>
  </tr>
  <tr>
   <td><p>类别</p> </td>
   <td><p>String[]</p> </td>
   <td><p>granite.testing.hobbes.tests、granite.testing.calvin.tests</p> </td>
  </tr>
  <tr>
   <td><p>依赖</p> </td>
   <td><p>String[]</p> </td>
   <td><p>granite.testing.hobbes.testrunner、granite.testing.calvin、apps.testframework.all</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>granite.testing.calvin.af clientlib包含所有自适应表单API。 这些API是卡尔文命名空间的一部分。

![1_aftestregistration](assets/1_aftestregistration.png)

1. 右键单击测试节点(此处为 **afTestRegistration)** ，然后单击 **创建** > **创建文件**。 将文件命名为js.txt并单击“ **确定**”。
1. 在js.txt文件中，添加以下文本：

   ```javascript
   #base=.
   js.txt
   ```

1. 单 **击“全部** 保存”，然后关闭js.txt文件。
1. 右键单击测试节点(此处为 **afTestRegistration)** ，然后单 **击“创建** ” **>“**&#x200B;创建文件”。 命名文件init.js，然后单击“ **确定**”。
1. 将以下代码复制到init.js文件，然后单击“全 **部保存**”:

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm = new hobs.TestSuite("Adaptive Form - Demo Test", {
           path: '/etc/clientlibs/afTestRegistration/init.js',
           register: true
       });
    // window.testsuites.testForm1 = new hobs.TestSuite("testForm1");
   }(window, window.hobs));
   ```

   以上代码创建名为Adaptive Form - **Demo Test的测试套件**。 要创建具有不同名称的测试套件，请相应地更改该名称。

1. 单 **击“创** 建” **>“创建节点** ”，为要测试的每个表单在clientlib文件夹下创建一个节点。 此示例使用名为testForm **的节点** ，测试名为testForm的自适 **应表单**。 指定以下属性，然后单击“ **确定**”:

   * 名称：testForm（您的表单名称）
   * 类型：cq:ClientLibraryFolder

1. 将以下属性添加到新创建的节点（此处为testForm）以测试自适应表单：

   | **属性** | **类型** | **值** |
   |---|---|---|
   | 类别 | String[] | granite.testing.hobbes.tests、granite.testing.hobbes.tests.testForm |
   | 依赖 | String[] | granite.testing.calvin.tests |

   >[!NOTE]
   >
   >此示例使用对客户端lib granite.testing.calvin.tests的依赖项来更好地管理。 此示例还添加一个客户端lib类别&quot;granite.testing.hobbes.tests.testForm&quot;，以根据需要重用此客户端lib。

   ![2_testformproperties](assets/2_testformproperties.png)

1. 右键单击为测试表单创建的文件夹（此处为testForm），然后选择“创 **建** ”> **“创建文件**”。 将文件命名为scriptingTest.js，并将以下代码添加到文件中，然后单击“全 **部保存”。**

   要使用以下代码测试其他自适应表单，请在navigateTo（行11、36和62） **中更改** 表单的路径和名称，以及相应的测试用例。 有关用于测试表单和表单对象不同方面的API的更多信息，请参 [阅Calvin API](https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html)。

   ```javascript
   (function(window, hobs) {
       'use strict';
   
    var ts = new hobs.TestSuite("Script Test", {
           path: '/etc/clientlibs/testForm/scriptingTest.js',
     register: false
    })
   
       .addTestCase(new hobs.TestCase("Checking execution of calculate script")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/testForm.html?wcmmode=disabled")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel1.textbox1");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel1.textbox", "5");
           })
           // if the calculate expression was setting "textbox1" value to "5", let's also check that
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel1.textbox1", "Calculate");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel1.textbox1");
           })
           .asserts.isTrue(function () {
               return calvin.model("panel1.textbox1").value == "5"
           })
       )
   
       .addTestCase(new hobs.TestCase("Calculate script Test")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/cal/demoform.html?wcmmode=disabled&dataRef=crx:///content/forms/af/cal/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
   
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel2.panel1488218690733.downPayment");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel2.panel1488218690733.priceProperty", "1000000");
           })
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel2.panel1488218690733.downPayment", "Calculate");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel2.panel1488218690733.downPayment");
           })
           .asserts.isTrue(function () {
               // if the calculate expression was setting "downPayment" value to "10000", let's also check that
      return calvin.model("panel2.panel1488218690733.downPayment").value == 10000
           })
       )
   
       .addTestCase(new hobs.TestCase("Checking execution of Value commit script")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/cal/demoform.html?wcmmode=disabled&dataRef=crx:///content/forms/af/cal/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
   
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel2.panel1488218690733.priceProperty");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel2.panel1488218690733.priceProperty", "100");
           })
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel2.panel1488218690733.priceProperty", "Value Commit");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel2.panel1488218690733.priceProperty");
           })
           .asserts.isTrue(function () {
            // if the value commit expression was setting "textbox1488215618594" value to "0", let's also check that
               return calvin.model("panel2.panel1488218690733.textbox1488215618594").value == 0
           })
       );
   
    // register the test suite with testForm
     window.testsuites.testForm.add(ts);
   
    }(window, window.hobs));
   ```

   将创建测试用例。 继续运行测试用例，通过Hobbes测试自适应表单。 有关运行测试用例的步骤，请参 [阅使用自动测试在UI测试中执行测试](/help/sites-developing/hobbes.md)。

您还可以在附加的文件SampleTestPackage.zip中安装该包，以获得与示例中所述步骤相同的结果：使用Hobbes作为测试框架为自适应表单创建测试套件。

[获取文件](assets/sampletestpackage.zip)

## 使用自动测试测试您的UI {#testing-your-ui-using-automated-tests}

### 运行单个测试套件 {#running-a-single-test-suite}

测试套件可以单独运行。 运行测试套件时，页面会随着测试用例及其操作的执行而发生更改，测试结果会在测试完成后显示。 图标表示结果。

复选标记图标指示通过的测试： ![选中标记](assets/checkmark.png)

“X”图标表示测试失败： ![交叉](assets/cross.png)

运行测试套件：

1. 在“Tests（测试）”面板中，单击或点按要运行的测试用例的名称，以展开“Actions（操作）”的详细信息。

   ![1_tapnameoftestcase](assets/1_tapnameoftestcase.png)

1. 单击或点按运行测试按钮。 ![runtestcase](assets/runtestcase.png)

   ![2_clickrun](assets/2_clickrun.png)

1. 测试执行时，占位符将替换为页面内容。

   ![3_pagecontent](assets/3_pagecontent.png)

1. 点按或单击说明以打开“结果”面板，查看测试用例的结果。 点按或单击“结果”面板中的测试用例名称会显示所有详细信息。

   ![4_reviewresults](assets/4_reviewresults.png)

测试AEM自适应表单的步骤与测试AEM UI的步骤类似。 有关测试自适应表单的更多信息，请参阅测试UI [中的以下主题](https://helpx.adobe.com//experience-manager/6-3/help/sites-developing/hobbes.html):

* 查看测试套件
* 运行多个测试

## 术语表 {#glossary}

<table>
 <tbody>
  <tr>
   <td><strong>术语</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><p>测试套件</p> </td>
   <td><p>测试套件是相关测试用例的集合。</p> </td>
  </tr>
  <tr>
   <td><p>测试用例</p> </td>
   <td><p>测试用例表示用户使用您的UI执行的任务。 将测试用例添加到测试套件以测试用户执行的活动。</p> </td>
  </tr>
  <tr>
   <td><p>操作</p> </td>
   <td><p>动作是在UI中执行手势的方法，如单击按钮或用值填充输入框。</p> <p>thower.actions.Wistanes、thower.actions.Core和thower.utils.af类的方法是可在测试中使用的操作。 所有操作都同步执行。</p> </td>
  </tr>
  <tr>
   <td><p>创作或发布环境</p> </td>
   <td><p>通常，表单可以在创作或发布环境中进行测试。 在发布环境的情况下，默认情况下，执行测试的权限受到限制。 这是因为与测试运行程序相关的所有客户端库都位于JCR结构的/libs中。</p> </td>
  </tr>
 </tbody>
</table>

