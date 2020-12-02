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


# 教程：将规则应用于自适应表单字段{#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教程是[创建第一个自适应表单](/help/forms/using/create-your-first-adaptive-form.md)系列中的一个步骤。 Adobe建议按照时间顺序按照该系列进行操作，以了解、执行和演示完整的教程用例。

## 关于教程{#about-the-tutorial}

您可以使用规则向自适应表单添加交互性、业务逻辑和智能验证。 自适应表单具有内置的规则编辑器。 规则编辑器提供拖放功能，类似于导览。 拖放方法是创建规则最快、最简单的方法。 规则编辑器还为有兴趣测试其编码技能或将规则提升到更高级别的用户提供了一个代码窗口。

可在[自适应Forms规则编辑器](/help/forms/using/rule-editor.md)中进一步了解规则编辑器。

在教程结束时，您将学习如何创建规则以：

* 调用表单数据模型服务以从数据库检索数据
* 调用表单数据模型服务以向数据库添加数据
* 运行验证检查并显示错误消息

教程每个部分结尾的交互式GIF图像可以帮助您学习和验证正在构建的表单的功能。

## 第1步：从数据库{#retrieve-customer-record}检索客户记录

您通过按照[创建表单数据模型](/help/forms/using/create-form-data-model.md)文章创建表单数据模型。 现在，您可以使用规则编辑器调用Forms数据模型服务来检索信息并将信息添加到数据库。

每个客户都会获得一个唯一的客户ID编号，这有助于识别数据库中的相关客户数据。 以下过程使用客户ID从数据库检索信息：

1. 打开自适应表单进行编辑。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 点按&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段，然后点按&#x200B;**[!UICONTROL 编辑规则]**&#x200B;图标。 “规则编辑器”(Rule Editor)窗口将打开。
1. 点按&#x200B;**[!UICONTROL +创建]**&#x200B;图标以添加规则。 它打开可视编辑器。

   在可视编辑器中，默认情况下选择&#x200B;**[!UICONTROL WHEN]**&#x200B;语句。 此外，在&#x200B;**[!UICONTROL WHEN]**&#x200B;语句中指定从中启动规则编辑器的表单对象（本例中为&#x200B;**[!UICONTROL 客户ID]**）。

1. 点按&#x200B;**[!UICONTROL 选择状态]**&#x200B;下拉框，选择&#x200B;**[!UICONTROL 已更改]**。

   ![当自定义更改时](assets/whencustomeridischanged.png)

1. 在&#x200B;**[!UICONTROL THEN]**&#x200B;语句中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 调用服务]**。
1. 从&#x200B;**[!UICONTROL 选择]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 检索送货地址]**&#x200B;服务。
1. 将&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段从“表单对象”选项卡拖放到&#x200B;**[!UICONTROL 拖放对象，或在**[!UICONTROL  INPUT ]**框中选择此处]**&#x200B;字段。

   ![dropojectstoinputfield-retriedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 将“表单对象”选项卡中的&#x200B;**[!UICONTROL 客户ID、名称、送货地址、状态和邮政编码]**&#x200B;字段拖放到&#x200B;**[!UICONTROL 拖放对象，或在**[!UICONTROL  OUTPUT ]**框中选择此处]**&#x200B;字段。

   ![dropobjectstooutputfield-retrieddata](assets/dropobjectstooutputfield-retrievedata.png)

   点按&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。 在规则编辑器窗口中，点按&#x200B;**[!UICONTROL 关闭]**。

1. 预览自适应表单。 在&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段中输入ID。 表单现在可以从数据库检索客户详细信息。

   ![检索信息](assets/retrieve-information.gif)

## 第2步：将更新的客户地址添加到数据库{#updated-customer-address}

从数据库检索客户详细信息后，您可以更新送货地址、状态和邮政编码。 以下过程调用表单数据模型服务将客户信息更新到数据库：

1. 选择&#x200B;**[!UICONTROL 提交]**&#x200B;字段，然后点按&#x200B;**[!UICONTROL 编辑规则]**&#x200B;图标。 “规则编辑器”(Rule Editor)窗口将打开。
1. 选择&#x200B;**[!UICONTROL 提交——单击]**&#x200B;规则，然后点按&#x200B;**[!UICONTROL 编辑]**&#x200B;图标。 此时将显示编辑提交规则的选项。

   ![提交规则](assets/submit-rule.png)

   在WHEN选项中，已选择&#x200B;**[!UICONTROL Submit]**&#x200B;和&#x200B;**[!UICONTROL 选项。]**

   ![submit-is clicked](assets/submit-is-clicked.png)

1. 在&#x200B;**[!UICONTROL THEN]**&#x200B;选项中，点按&#x200B;**[!UICONTROL +添加语句]**&#x200B;选项。 从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 调用服务]**。
1. 从&#x200B;**[!UICONTROL 选择]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 更新送货地址]**&#x200B;服务。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropojectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 将[!UICONTROL 表单对象]选项卡中的&#x200B;**[!UICONTROL 发运地址、状态和邮政编码]**&#x200B;字段拖放到&#x200B;**[!UICONTROL 投入**[!UICONTROL &#x200B;输入&lt;a6&lt;a>中&lt;a6/>对象&lt;a3/>的相应表名属性（例如customerdetails .shippingAddress）或在此处选择&#x200B;]**字段7/>。]**&#x200B;以表名（例如，此用例中的customerdetails）为前缀的所有字段用作更新服务的输入数据。 这些字段中提供的所有内容都将在数据源中更新。

   >[!NOTE]
   >
   >请勿将&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段拖放到相应的tablename.property（例如customerdetails.name）。 它有助于避免错误地更新客户的名称和ID。

1. 将[!UICONTROL 表单对象]选项卡中的&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段拖放到&#x200B;**[!UICONTROL INPUT]**&#x200B;框中的id字段。 没有前缀表名的字段（例如，此用例中的customerdetails）用作更新服务的搜索参数。 此用例中的&#x200B;**[!UICONTROL id]**&#x200B;字段唯一标识&#x200B;**customerdetails**&#x200B;表中的记录。
1. 点按&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。 在规则编辑器窗口中，点按&#x200B;**[!UICONTROL 关闭]**。
1. 预览自适应表单。 检索客户的详细信息、更新送货地址并提交表单。 再次检索同一客户的详细信息时，将显示更新的发运地址。

## 第3步：（奖励部分）使用代码编辑器运行验证并显示错误消息{#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您应对表单运行验证，以确保在表单中输入的数据正确无误，并在数据不正确时显示错误消息。 例如，如果在表单中输入了非现有客户ID，则应显示一条错误消息。

自适应表单提供了多个具有内置验证功能的组件，例如，电子邮件和数字字段，您可以将这些字段用于常见用例。 对高级用例使用规则编辑器，例如，当数据库返回零(0)条记录（无记录）时，显示错误消息。

下面的过程说明了如何创建规则，以在表单中输入的客户ID在数据库中不存在时显示错误消息。 规则还将焦点置于&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段并重置。 该规则使用表单数据模型服务[的dataIntegrationUtils API，检查数据库中是否存在客户ID。](/help/forms/using/invoke-form-data-model-services.md)

1. 点按&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段，然后点按`Edit Rules`图标。 将打开[!UICONTROL 规则编辑器]窗口。
1. 点按&#x200B;**[!UICONTROL +创建]**&#x200B;图标以添加规则。 它打开可视编辑器。

   在可视编辑器中，默认情况下选择&#x200B;**[!UICONTROL WHEN]**&#x200B;语句。 此外，在&#x200B;**[!UICONTROL WHEN]**&#x200B;语句中指定从中启动规则编辑器的表单对象（本例中为&#x200B;**[!UICONTROL 客户ID]**）。

1. 点按&#x200B;**[!UICONTROL 选择状态]**&#x200B;下拉框，选择&#x200B;**[!UICONTROL 已更改]**。

   ![当自定义更改时](assets/whencustomeridischanged.png)

   在&#x200B;**[!UICONTROL THEN]**&#x200B;语句中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 调用服务]**。

1. 从&#x200B;**[!UICONTROL 可视编辑器]**&#x200B;切换到&#x200B;**[!UICONTROL 代码编辑器]**。 开关控件在窗口的右侧。 此时将打开代码编辑器，其中显示与以下内容类似的代码：

   ![代码编辑器](assets/code-editor.png)

1. 将输入变量部分替换为以下代码：

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. 将`guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)`部分替换为以下代码：

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

