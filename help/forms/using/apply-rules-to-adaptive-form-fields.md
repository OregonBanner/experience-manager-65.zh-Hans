---
title: “请勿发布教程：将规则应用于自适应表单字段”
seo-title: 将规则应用于自适应表单字段
description: 创建规则，将交互性、业务逻辑和智能验证添加到自适应表单。
seo-description: 创建规则，将交互性、业务逻辑和智能验证添加到自适应表单。
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
translation-type: tm+mt
source-git-commit: e3ecf724cdfcd20ef4c089605e644ad10ef1221b
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# 教程：将规则应用于自适应表单字段 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教程是创建第一个自 [适应表单系列中的一个步骤](/help/forms/using/create-your-first-adaptive-form.md) 。 Adobe建议按照时间顺序按照该系列进行操作，以了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

您可以使用规则向自适应表单添加交互性、业务逻辑和智能验证。 自适应表单具有内置规则编辑器。 规则编辑器提供拖放功能，类似于导览。 拖放方法是创建规则最快、最简单的方法。 规则编辑器还为有兴趣测试其编码技能或将规则提升到更高级别的用户提供了一个代码窗口。

您可以在自适应Forms规则编辑器中进一步 [了解规则编辑器](/help/forms/using/rule-editor.md)。

在教程结束时，您将学习如何创建规则以：

* 调用表单数据模型服务以从数据库检索数据
* 调用表单数据模型服务以向数据库添加数据
* 运行验证检查并显示错误消息

教程每个部分结尾的交互式GIF图像可以帮助您学习和验证正在构建的表单的功能。

## 第1步：从数据库检索客户记录 {#retrieve-customer-record}

您通过遵循创建表单数据模型文 [章创建表单数据模型](/help/forms/using/create-form-data-model.md) 。 现在，您可以使用规则编辑器调用Forms数据模型服务来检索信息并将信息添加到数据库。

每个客户都会获得一个唯一的客户ID编号，这有助于识别数据库中的相关客户数据。 以下过程使用客户ID从数据库检索信息：

1. 打开自适应表单进行编辑。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 点按客 **[!UICONTROL 户ID]** 字段，然后点 **[!UICONTROL 按编辑规则]** 图标。 “规则编辑器”(Rule Editor)窗口将打开。
1. 点按+ **[!UICONTROL 创建]** 图标以添加规则。 它打开可视编辑器。

   在可视编辑器中，默认 **[!UICONTROL 情况下]** ，选择WHEN语句。 此外，在WHEN语句中指定从其 **[!UICONTROL 中启动规则]**&#x200B;编辑器的表单对象(本例中为客 **[!UICONTROL 户ID]** )。

1. 点按选 **[!UICONTROL 择状态]** 下拉框，选择 **[!UICONTROL 被更改]**。

   ![当自定义更改时](assets/whencustomeridischanged.png)

1. 在THEN语 **[!UICONTROL 句中]** ，从“选 **[!UICONTROL 择操作”下]** 拉列表中选择 **[!UICONTROL “调]** 用服务”。
1. 从“选 **[!UICONTROL 择]** ”下拉框中 **[!UICONTROL 选择]** “检索发运地址”服务。
1. 将客户ID字段从表 **[!UICONTROL 单对象]** 选项卡拖放到 **[!UICONTROL Drop对象，或在INPUT框中选择]****[!UICONTROL “此处]** 字段”。

   ![dropojectstoinputfield-retriedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 将“客户ID”、“名 **[!UICONTROL 称”、“发运地址”、“状态”和“邮政编码]** ”字段从“表单对象”选项卡拖放 **[!UICONTROL 到“拖放”对象，或在“输出”框中选]** 择此处 **** 字段。

   ![dropobjectstooutputfield-retrieddata](assets/dropobjectstooutputfield-retrievedata.png)

   点按 **[!UICONTROL 完成]** ，以保存规则。 在规则编辑器窗口中，点按 **[!UICONTROL 关闭]**。

1. 预览自适应表单。 在客户ID字段中输入 **[!UICONTROL 一个ID]** 。 表单现在可以从数据库检索客户详细信息。

   ![检索信息](assets/retrieve-information.gif)

## 第2步：将更新的客户地址添加到数据库 {#updated-customer-address}

从数据库检索客户详细信息后，您可以更新送货地址、状态和邮政编码。 以下过程调用表单数据模型服务将客户信息更新到数据库：

1. 选择提 **[!UICONTROL 交]** 字段，然后点 **[!UICONTROL 按编辑规则]** 图标。 “规则编辑器”(Rule Editor)窗口将打开。
1. 选择提 **[!UICONTROL 交——单击规]** 则，然后点 **[!UICONTROL 按编辑]** 图标。 此时将显示编辑提交规则的选项。

   ![提交规则](assets/submit-rule.png)

   在WHEN选项中，已 **[!UICONTROL 选择]** “提 **[!UICONTROL 交”和“已]** 单击”选项。

   ![submit-is clicked](assets/submit-is-clicked.png)

1. 在THEN选 **[!UICONTROL 项中]** ，点按 **[!UICONTROL +添加语句选项]** 。 从选 **[!UICONTROL 择操作]** 下拉 **[!UICONTROL 菜单中选择调]** 用服务。
1. 从“选 **[!UICONTROL 择]** ”下拉菜单中选择 **[!UICONTROL “更新发]** 运地址”服务。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropojectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 将Shipping Address、 **[!UICONTROL State和Zip Code]** field从Form Objects选项卡拖放到Drop对象的相应表名。property（例如，customerdetails .shippingAddress）或在INPUT Box中选择 [!UICONTROL Here] Field(此处 ******** 地址、状态和邮政编码)。 以表名（例如，此用例中的customerdetails）为前缀的所有字段用作更新服务的输入数据。 这些字段中提供的所有内容都将在数据源中更新。

   >[!NOTE]
   >
   >请勿将Name和Customer ID **[!UICONTROL 字段拖]****[!UICONTROL 放到相应]** 的tablename.property（例如，customerdetails.name）。 它有助于避免错误地更新客户的名称和ID。

1. 将“客户ID”字 **[!UICONTROL 段从]** “表单对 [!UICONTROL 象”选项卡拖放到] “输入”框的 **[!UICONTROL id字段]** 。 没有前缀表名的字段（例如，此用例中的customerdetails）用作更新服务的搜索参数。 此用 **[!UICONTROL 例中的]** id字段唯一标识customerdetails表中 **的记录** 。
1. 点按 **[!UICONTROL 完成]** ，以保存规则。 在规则编辑器窗口中，点按 **[!UICONTROL 关闭]**。
1. 预览自适应表单。 检索客户的详细信息、更新送货地址并提交表单。 再次检索同一客户的详细信息时，将显示更新的发运地址。

## 第3步：（奖励部分）使用代码编辑器运行验证并显示错误消息 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您应对表单运行验证，以确保在表单中输入的数据正确无误，并在数据不正确时显示错误消息。 例如，如果在表单中输入了非现有客户ID，则应显示一条错误消息。

自适应表单提供了多个具有内置验证功能的组件，例如，电子邮件和数字字段，您可以将这些字段用于常见用例。 对高级用例使用规则编辑器，例如，当数据库返回零(0)条记录（无记录）时，显示错误消息。

下面的过程说明了如何创建规则，如果在表单中输入的客户ID在数据库中不存在，则显示错误消息。 该规则还将焦点置于客户ID字 **[!UICONTROL 段并重置]** 。 该规则使 [用表单数据模型服务的dataIntegrationUtils API](/help/forms/using/invoke-form-data-model-services.md) ，检查数据库中是否存在客户ID。

1. 点按客 **[!UICONTROL 户ID]** 字段，然后点 `Edit Rules` 按图标。 将打 [!UICONTROL 开“规则编辑] ”窗口。
1. 点按+ **[!UICONTROL 创建]** 图标以添加规则。 它打开可视编辑器。

   在可视编辑器中，默认 **[!UICONTROL 情况下]** ，选择WHEN语句。 此外，在WHEN语句中指定从其 **[!UICONTROL 中启动规则]**&#x200B;编辑器的表单对象(本例中为客 **[!UICONTROL 户ID]** )。

1. 点按选 **[!UICONTROL 择状态]** 下拉框，选择 **[!UICONTROL 被更改]**。

   ![当自定义更改时](assets/whencustomeridischanged.png)

   在THEN语 **[!UICONTROL 句中]** ，从“选 **[!UICONTROL 择操作”下]** 拉列表中选择 **[!UICONTROL “调]** 用服务”。

1. 从可视 **[!UICONTROL 编辑器切换]** 到代 **[!UICONTROL 码编辑器]**。 开关控件在窗口的右侧。 此时将打开代码编辑器，其中显示与以下内容类似的代码：

   ![代码编辑器](assets/code-editor.png)

1. 将输入变量部分替换为以下代码：

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. 将该部 `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` 分替换为以下代码：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. 预览自适应表单。 输入错误的客户ID。 出现错误消息。

   ![display-validation-error](assets/display-validation-error.gif)

