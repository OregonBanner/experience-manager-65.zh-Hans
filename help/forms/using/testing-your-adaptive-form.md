---
title: “教程：测试自适应表单”
seo-title: “教程：测试自适应表单”
description: 使用自动测试功能一次测试多个自适应表单。
seo-description: 使用自动测试功能一次测试多个自适应表单。
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
feature: 自适应表单
exl-id: 343e2e0b-d5ef-4f01-b3d6-45f90e2430fd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 3%

---

# 教程：测试自适应表单{#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

本教程是[创建您的第一个自适应表单](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的一个步骤。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

自适应表单准备就绪后，务必要先测试自适应表单，然后再将其转出给最终用户。 您可以手动测试每个字段（功能测试），或自动测试自适应表单。 当您有多个自适应表单时，手动测试所有自适应表单的每个字段将是一项艰巨的任务。

AEM [!DNL Forms]提供测试框架Calvin，以自动测试自适应表单。 使用框架，您可以直接在Web浏览器中编写和运行UI测试。 该框架提供了用于创建测试的JavaScript API。 通过自动测试，您可以测试自适应表单的预填充体验、提交自适应表单的体验、表达式规则、验证、延迟加载和UI交互等。 本教程将指导您完成在自适应表单上创建和运行自动测试的步骤。 在本教程结束时，您将能够：

* [为自适应表单创建测试包](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [为自适应表单创建测试](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [运行为自适应表单创建的测试包和测试](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## 步骤1:创建测试包{#step-create-a-test-suite}

测试包包含一组测试用例。 您可以有多个测试包。 建议为每个表单分别使用一个测试包。 要创建测试包，请执行以下操作：

1. 以管理员身份登录到AEM [!DNL Forms]创作实例。 打开[!UICONTROL CRXDE Lite]。 您可以点按AEM徽标> **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**&#x200B;或在浏览器中打开[https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) URL以打开CRXDE Lite。

1. 在[!UICONTROL CRXDE Lite]中导航到/etc/clientlibs。 右键单击/etc/clientlibs子文件夹，然后单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 创建节点]**。 在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入&#x200B;**WeRetailFormTestCases**。 选择类型为&#x200B;**cq:ClientLibraryFolder**&#x200B;并单击&#x200B;**[!UICONTROL 确定]**。 它会创建一个节点。 您可以使用任何名称代替`WeRetailFormTestCases`。
1. 将以下属性添加到`WeRetailFormTestCases`节点，然后点按&#x200B;**[!UICONTROL 保存所有]**。

   <table>
    <tbody>
     <tr>
      <td><strong>属性</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>多个</strong></td>
      <td><strong>值</strong></td>
     </tr>
     <tr>
      <td>类别</td>
      <td>字符串</td>
      <td>启用</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     <tr>
      <td>依赖</td>
      <td>字符串</td>
      <td>启用</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.testrunner <br /> </li>
        <li>granite.testing.calvin <br /> </li>
        <li>apps.testframework.all</li>
       </ul> </td>
     </tr>
    </tbody>
   </table>

   确保将每个属性添加到单独的框中，如下所示：

   ![依赖](assets/dependencies.png)

1. 右键单击&#x200B;**[!UICONTROL WeRetailFormTestCases]**&#x200B;节点，单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 创建文件]**。 在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入`js.txt`并单击&#x200B;**[!UICONTROL 确定]**。
1. 打开js.txt文件进行编辑，添加以下代码并保存文件：

   ```text
   #base=.
    init.js
   ```

1. 在`WeRetailFormTestCases`节点中创建一个文件init.js 。 将以下代码添加到文件中，然后点按&#x200B;**[!UICONTROL 保存全部]**。

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm3 = new hobs.TestSuite("We retail - Tests", {
           path: '/etc/clientlibs/WeRetailFormTestCases/init.js',
           register: true
       });
    // window.testsuites.testForm2 = new hobs.TestSuite("testForm2");
   }(window, window.hobs));
   ```

   以上代码将创建一个名为&#x200B;**We retail - Tests**&#x200B;的测试包。

1. 打开AEM Testing UI(AEM > **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 测试]**)。 UI中列出了测试包 — **We retail - Tests** -。

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## 步骤2:创建一个测试用例以在自适应表单{#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}中预填充值

测试案例是一组用于测试特定功能的操作。 例如，预填表单的所有字段并验证几个字段，以确保输入正确的值。

操作是自适应表单上的特定活动，如单击按钮。 要创建测试用例和操作以验证每个自适应表单字段的用户输入，请执行以下操作：

1. 在[!UICONTROL CRXDE lite]中，导航到`/content/forms/af/create-first-adaptive-form`文件夹。 右键单击&#x200B;**[!UICONTROL create-first-adaptive-form]**&#x200B;文件夹节点，然后单击&#x200B;**[!UICONTROL 创建]**> **[!UICONTROL 创建文件]**。 在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入`prefill.xml`并单击&#x200B;**[!UICONTROL 确定]**。 将以下代码添加到该文件：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><afData>
     <afUnboundData>
       <data>
         <customer_ID>371767</customer_ID>
         <customer_Name>John Jacobs</customer_Name>
         <customer_Shipping_Address>1657 1657 Riverside Drive Redding</customer_Shipping_Address>
         <customer_State>California</customer_State>
         <customer_ZIPCode>096001</customer_ZIPCode>
        </data>
     </afUnboundData>
     <afBoundData>
       <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"/>
     </afBoundData>
   </afData>
   ```

1. 导航至 `/etc/clientlibs`. 右键单击`/etc/clientlibs`子文件夹，然后单击&#x200B;**[!UICONTROL 创建]** **[!UICONTROL 创建节点]**。

   在&#x200B;**[!UICONTROL Name]**&#x200B;字段中键入`WeRetailFormTests`。 选择类型`cq:ClientLibraryFolder`，然后单击&#x200B;**[!UICONTROL 确定]**。

1. 将以下属性添加到&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;节点。

   <table>
    <tbody>
     <tr>
      <td><strong>属性</strong></td>
      <td><strong>类型</strong></td>
      <td><strong>多个</strong></td>
      <td><strong>值</strong></td>
     </tr>
     <tr>
      <td>类别</td>
      <td>字符串</td>
      <td>启用</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.hobbes.tests.testForm</li>
       </ul> </td>
     </tr>
     <tr>
      <td>依赖</td>
      <td>字符串</td>
      <td>启用</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. 在&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;节点中创建文件js.txt。 将以下内容添加到文件中：

   ```shell
   #base=.
   prefillTest.js
   ```

   单击&#x200B;**[!UICONTROL Save All]**。

1. 在&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;节点中创建文件`prefillTest.js`。 将以下代码添加到文件中。 代码会创建一个测试用例。 测试用例会预填表单的所有字段，并验证一些字段以确保输入正确的值。

   ```javascript
   (function (window, hobs) {
       'use strict';
   
       var ts = new hobs.TestSuite("Prefill Test", {
           path: '/etc/clientlibs/WeRetailFormTests/prefillTest.js',
           register: false
       })
   
       .addTestCase(new hobs.TestCase("Prefill Test")
           // navigate to the testForm which is to be test
           .navigateTo("/content/forms/af/create-first-adaptive-form/shipping-address-add-update-form.html?wcmmode=disabled&dataRef=crx:///content/forms/af/create-first-adaptive-form/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ID").value == 371767;
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ZIPCode").value == 96001;
           })
       );
   
       // register the test suite with testForm
       window.testsuites.testForm3.add(ts);
   
   }(window, window.hobs));
   ```

   测试案例已创建并准备运行。 您可以创建测试案例以验证自适应表单的各个方面，例如检查计算脚本的执行情况、验证模式以及验证自适应表单的提交体验。 有关自适应表单测试各个方面的信息，请参阅自动测试自适应表单。

## 步骤3:在包或单个测试案例{#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}中运行所有测试

一个测试包可以有多个测试用例。 您可以一次或单独在测试包中运行所有测试用例。 运行测试时，图标会指示结果：

* 复选标记图标表示通过的测试：![save_icon](assets/save_icon.svg)
* “X”图标表示测试失败：![close-icon](assets/close-icon.svg)

1. 导航到AEM图标> **[!UICONTROL Tools]**> **[!UICONTROL Operations]**> **[!UICONTROL Testing]**
1. 要运行测试包的所有测试，请执行以下操作：

   1. 在[!UICONTROL 测试]面板中，点按&#x200B;**[!UICONTROL We retail - Tests(1)]**。 它扩展包以显示测试列表。
   1. 点按&#x200B;**[!UICONTROL 运行测试]**&#x200B;按钮。 测试执行时，屏幕右侧的空白区域将替换为自适应表单。

      ![运行全测试](assets/run-all-test.png)

1. 要从测试包运行单个测试，请执行以下操作：

   1. 在“测试”面板中，点按&#x200B;**[!UICONTROL We retail - Tests(1)]**。 它扩展包以显示测试列表。
   1. 点按&#x200B;**[!UICONTROL 预填充测试]** ，然后点按&#x200B;**[!UICONTROL 运行测试]**&#x200B;按钮。 测试执行时，屏幕右侧的空白区域将替换为自适应表单。

1. 点按测试名称预填充测试，以查看测试案例的结果。 此时将打开[!UICONTROL Result]面板。 点按[!UICONTROL Result]面板中的测试案例名称，以查看测试的所有详细信息。

   ![review-results](assets/review-results.png)

现在，自适应表单已准备好发布。
