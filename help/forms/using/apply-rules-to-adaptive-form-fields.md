---
title: 将规则应用于自适应表单字段
seo-title: 将规则应用于自适应表单字段
description: 创建规则以向自适应表单添加交互性、业务逻辑和智能验证。
seo-description: 创建规则以向自适应表单添加交互性、业务逻辑和智能验证。
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: 63bc43bba88a42d62fb574bc8ce42470ac61d693
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 0%

---

# 教程：将规则应用于自适应表单字段 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教程是[创建您的第一个自适应表单](/help/forms/using/create-your-first-adaptive-form.md)系列中的一个步骤。 Adobe建议按照时间顺序排列这些系列，以了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

您可以使用规则向自适应表单添加交互性、业务逻辑和智能验证。 自适应表单具有内置规则编辑器。 规则编辑器提供了拖放功能，与引导式导览类似。 拖放方法是创建规则最快、最简单的方法。 规则编辑器还为有兴趣测试其编码技能或将规则提升到更高级别的用户提供了一个代码窗口。

您可以在[自适应Forms规则编辑器](/help/forms/using/rule-editor.md)中了解有关规则编辑器的更多信息。

在教程结束时，您将学习如何创建规则以：

* 调用表单数据模型服务以从数据库检索数据
* 调用表单数据模型服务以向数据库添加数据
* 运行验证检查并显示错误消息

教程每个部分末尾的交互式GIF图像可帮助您即时学习和验证所构建表单的功能。

## 步骤1:从数据库中检索客户记录 {#retrieve-customer-record}

您通过按照[创建表单数据模型](/help/forms/using/create-form-data-model.md)文章创建表单数据模型。 现在，您可以使用规则编辑器调用Forms数据模型服务以检索信息并将信息添加到数据库。

每个客户都会分配一个唯一的客户ID号，这有助于识别数据库中的相关客户数据。 以下过程使用客户ID从数据库中检索信息：

1. 打开自适应表单进行编辑。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 点按&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段，然后点按&#x200B;**[!UICONTROL 编辑规则]**&#x200B;图标。 将打开规则编辑器窗口。
1. 点按&#x200B;**[!UICONTROL +创建]**&#x200B;图标以添加规则。 此时将打开可视编辑器。

   在可视编辑器中，默认选中&#x200B;**[!UICONTROL WHEN]**&#x200B;语句。 此外，在&#x200B;**[!UICONTROL WHEN]**&#x200B;语句中，还指定了从中启动规则编辑器的表单对象（在本例中为&#x200B;**[!UICONTROL 客户ID]**）。

1. 点按&#x200B;**[!UICONTROL 选择状态]**&#x200B;下拉列表，然后选择&#x200B;**[!UICONTROL 已更改]**。

   ![when customidischanged](assets/whencustomeridischanged.png)

1. 在&#x200B;**[!UICONTROL THEN]**&#x200B;语句中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 调用服务]**。
1. 从&#x200B;**[!UICONTROL Select]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Retrieve Shipping Address]**&#x200B;服务。
1. 将“表单对象”选项卡中的&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段拖放到&#x200B;**[!UICONTROL 拖放对象或在**[!UICONTROL  INPUT ]**框中选择此处]**&#x200B;字段。

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 将“表单对象”选项卡中的&#x200B;**[!UICONTROL 客户ID、名称、送货地址、状态和邮政编码]**&#x200B;字段拖放到&#x200B;**[!UICONTROL 拖放对象，或在**[!UICONTROL  OUTPUT ]**框中选择]**&#x200B;字段。

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   点按&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。 在规则编辑器窗口中，点按&#x200B;**[!UICONTROL 关闭]**。

1. 预览自适应表单。 在&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段中输入ID。 现在，表单可以从数据库中检索客户详细信息。

   ![检索信息](assets/retrieve-information.gif)

## 步骤2:将更新的客户地址添加到数据库 {#updated-customer-address}

在从数据库中检索客户详细信息后，您可以更新送货地址、状态和邮政编码。 以下过程会调用表单数据模型服务来将客户信息更新到数据库：

1. 选择&#x200B;**[!UICONTROL Submit]**&#x200B;字段，然后点按&#x200B;**[!UICONTROL 编辑规则]**&#x200B;图标。 将打开规则编辑器窗口。
1. 选择&#x200B;**[!UICONTROL 提交 — 单击]**&#x200B;规则，然后点按&#x200B;**[!UICONTROL 编辑]**&#x200B;图标。 此时会显示用于编辑提交规则的选项。

   ![submit-rule](assets/submit-rule.png)

   在WHEN选项中，已选择&#x200B;**[!UICONTROL Submit]**&#x200B;和&#x200B;**[!UICONTROL 已单击]**&#x200B;选项。

   ![已单击提交](assets/submit-is-clicked.png)

1. 在&#x200B;**[!UICONTROL THEN]**&#x200B;选项中，点按&#x200B;**[!UICONTROL +添加语句]**&#x200B;选项。 从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 调用服务]**。
1. 从&#x200B;**[!UICONTROL 选择]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 更新送货地址]**&#x200B;服务。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 从[!UICONTROL 表单对象]选项卡中，将&#x200B;**[!UICONTROL 发送地址、状态和邮政编码]**&#x200B;字段拖放到&#x200B;**[!UICONTROL 放置对象的相应表名.property（例如customerdetails .shippingAddress）中，或在**[!UICONTROL  INPUT ]**框中选择]**&#x200B;字段。 所有前缀为tablename的字段（例如，此用例中的customerdetails）都用作更新服务的输入数据。 这些字段中提供的所有内容都将在数据源中更新。

   >[!NOTE]
   >
   >请勿将&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Customer ID]**&#x200B;字段拖放到相应的tablename.property（例如customerdetails.name）中。 这有助于避免错误更新客户的名称和ID。

1. 将&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段从[!UICONTROL 表单对象]选项卡拖放到&#x200B;**[!UICONTROL INPUT]**&#x200B;框中的id字段。 没有前缀表名的字段（例如，此用例中的customerdetails）用作更新服务的搜索参数。 此用例中的&#x200B;**[!UICONTROL id]**&#x200B;字段唯一标识&#x200B;**customerdetails**&#x200B;表中的记录。
1. 点按&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。 在规则编辑器窗口中，点按&#x200B;**[!UICONTROL 关闭]**。
1. 预览自适应表单。 检索客户详细信息、更新送货地址并提交表单。 再次检索同一客户的详细信息时，将显示更新的发运地址。

## 步骤3:（附加部分）使用代码编辑器运行验证和显示错误消息 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您应该对表单运行验证，以确保在表单中输入的数据正确无误，并在数据不正确时显示错误消息。 例如，如果在表单中输入了非现有客户ID，则应显示一条错误消息。

自适应表单提供了多个具有内置验证的组件，例如可用于常见用例的电子邮件和数字字段。 例如，当数据库返回零(0)条记录（无记录）时，使用规则编辑器来显示错误消息。

以下过程说明如何创建规则，以在表单中输入的客户ID在数据库中不存在时显示错误消息。 该规则还会将焦点引向并重置&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段。 规则使用表单数据模型服务](/help/forms/using/invoke-form-data-model-services.md)的dataIntegrationUtils API来检查数据库中是否存在客户ID。[

1. 点按&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段，然后点按`Edit Rules`图标。 将打开[!UICONTROL 规则编辑器]窗口。
1. 点按&#x200B;**[!UICONTROL +创建]**&#x200B;图标以添加规则。 此时将打开可视编辑器。

   在可视编辑器中，默认选中&#x200B;**[!UICONTROL WHEN]**&#x200B;语句。 此外，在&#x200B;**[!UICONTROL WHEN]**&#x200B;语句中，还指定了从中启动规则编辑器的表单对象（在本例中为&#x200B;**[!UICONTROL 客户ID]**）。

1. 点按&#x200B;**[!UICONTROL 选择状态]**&#x200B;下拉列表，然后选择&#x200B;**[!UICONTROL 已更改]**。

   ![when customidischanged](assets/whencustomeridischanged.png)

   在&#x200B;**[!UICONTROL THEN]**&#x200B;语句中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 调用服务]**。

1. 从&#x200B;**[!UICONTROL Visual Editor]**&#x200B;切换到&#x200B;**[!UICONTROL 代码编辑器]**。 开关控件在窗口的右侧。 此时将打开代码编辑器，其中显示与以下内容类似的代码：

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

   ![显示验证错误](assets/display-validation-error.gif)
