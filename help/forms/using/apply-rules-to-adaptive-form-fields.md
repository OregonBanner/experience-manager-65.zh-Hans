---
title: 将规则应用于自适应表单字段
seo-title: Apply rules to adaptive form fields
description: 创建规则以向自适应表单添加交互性、业务逻辑和智能验证。
seo-description: Create rules to add interactivity, business logic, and smart validations to an adaptive form.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: 63bc43bba88a42d62fb574bc8ce42470ac61d693
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---

# 教程：将规则应用于自适应表单字段 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教程是 [创建您的第一个自适应表单](/help/forms/using/create-your-first-adaptive-form.md) 系列。 Adobe建议按照时间顺序排列这些系列，以了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

您可以使用规则向自适应表单添加交互性、业务逻辑和智能验证。 自适应表单具有内置规则编辑器。 规则编辑器提供了拖放功能，与引导式导览类似。 拖放方法是创建规则最快、最简单的方法。 规则编辑器还为有兴趣测试其编码技能或将规则提升到更高级别的用户提供了一个代码窗口。

您可以在 [自适应Forms规则编辑器](/help/forms/using/rule-editor.md).

在教程结束时，您将学习如何创建规则以：

* 调用表单数据模型服务以从数据库检索数据
* 调用表单数据模型服务以向数据库添加数据
* 运行验证检查并显示错误消息

教程每个部分末尾的交互式GIF图像可帮助您即时学习和验证要构建的表单的功能。

## 步骤1:从数据库中检索客户记录 {#retrieve-customer-record}

通过按照 [创建表单数据模型](/help/forms/using/create-form-data-model.md) 文章。 现在，您可以使用规则编辑器调用Forms数据模型服务以检索信息并将信息添加到数据库。

每个客户都会分配一个唯一的客户ID号，这有助于识别数据库中的相关客户数据。 以下过程使用客户ID从数据库中检索信息：

1. 打开自适应表单进行编辑。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 点按 **[!UICONTROL 客户ID]** 字段，然后点按 **[!UICONTROL 编辑规则]** 图标。 将打开规则编辑器窗口。
1. 点按 **[!UICONTROL +创建]** 图标以添加规则。 此时将打开可视编辑器。

   在可视化编辑器中， **[!UICONTROL WHEN]** 语句。 此外，表单对象(在本例中， **[!UICONTROL 客户ID]**)中，将在 **[!UICONTROL WHEN]** 语句。

1. 点按 **[!UICONTROL 选择状态]** 下拉框并选择 **[!UICONTROL 已更改]**.

   ![when customidischanged](assets/whencustomeridischanged.png)

1. 在 **[!UICONTROL 然后]** 语句，选择 **[!UICONTROL 调用服务]** 从 **[!UICONTROL 选择操作]** 下拉菜单。
1. 选择 **[!UICONTROL 检索送货地址]** 服务 **[!UICONTROL 选择]** 下拉菜单。
1. 拖放 **[!UICONTROL 客户ID]** 字段 **[!UICONTROL 放置对象或选择此处]** 字段 **[!UICONTROL 输入]** 框中。

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 拖放 **[!UICONTROL 客户ID、名称、送货地址、州和邮政编码]** 字段 **[!UICONTROL 放置对象或选择此处]** 字段 **[!UICONTROL 输出]** 框中。

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   点按 **[!UICONTROL 完成]** 来保存规则。 在规则编辑器窗口中，点按 **[!UICONTROL 关闭]**.

1. 预览自适应表单。 在 **[!UICONTROL 客户ID]** 字段。 现在，表单可以从数据库中检索客户详细信息。

   ![检索信息](assets/retrieve-information.gif)

## 步骤2:将更新的客户地址添加到数据库 {#updated-customer-address}

在从数据库中检索客户详细信息后，您可以更新送货地址、状态和邮政编码。 以下过程会调用表单数据模型服务来将客户信息更新到数据库：

1. 选择 **[!UICONTROL 提交]** 字段，然后点按 **[!UICONTROL 编辑规则]** 图标。 将打开规则编辑器窗口。
1. 选择 **[!UICONTROL 提交 — 单击]** 规则并点按 **[!UICONTROL 编辑]** 图标。 此时会显示用于编辑提交规则的选项。

   ![submit-rule](assets/submit-rule.png)

   在WHEN选项中， **[!UICONTROL 提交]** 和 **[!UICONTROL 点击]** 选项。

   ![已单击提交](assets/submit-is-clicked.png)

1. 在 **[!UICONTROL 然后]** 选项，点按 **[!UICONTROL +添加语句]** 选项。 选择 **[!UICONTROL 调用服务]** 从 **[!UICONTROL 选择操作]** 下拉菜单。
1. 选择 **[!UICONTROL 更新送货地址]** 服务 **[!UICONTROL 选择]** 下拉菜单。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 拖放 **[!UICONTROL 送货地址、州和邮政编码]** 字段 [!UICONTROL 表单对象] 选项卡，指向 **[!UICONTROL 放置对象或选择此处]** 字段 **[!UICONTROL 输入]** 框中。 所有前缀为tablename的字段（例如，此用例中的customerdetails）都用作更新服务的输入数据。 这些字段中提供的所有内容都将在数据源中更新。

   >[!NOTE]
   >
   >请勿拖放 **[!UICONTROL 名称]** 和 **[!UICONTROL 客户ID]** 字段到相应的tablename.property（例如customerdetails.name）。 这有助于避免错误更新客户的名称和ID。

1. 拖放 **[!UICONTROL 客户ID]** 字段 [!UICONTROL 表单对象] 选项卡 **[!UICONTROL 输入]** 框中。 没有前缀表名的字段（例如，此用例中的customerdetails）用作更新服务的搜索参数。 的 **[!UICONTROL id]** 此用例中的字段唯一标识  **customerdetails**  表。
1. 点按 **[!UICONTROL 完成]** 来保存规则。 在规则编辑器窗口中，点按 **[!UICONTROL 关闭]**.
1. 预览自适应表单。 检索客户详细信息、更新送货地址并提交表单。 再次检索同一客户的详细信息时，将显示更新的发运地址。

## 步骤3:（附加部分）使用代码编辑器运行验证和显示错误消息 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您应该对表单运行验证，以确保在表单中输入的数据正确无误，并在数据不正确时显示错误消息。 例如，如果在表单中输入了非现有客户ID，则应显示一条错误消息。

自适应表单提供了多个具有内置验证的组件，例如可用于常见用例的电子邮件和数字字段。 例如，当数据库返回零(0)条记录（无记录）时，使用规则编辑器来显示错误消息。

以下过程说明如何创建规则，以在表单中输入的客户ID在数据库中不存在时显示错误消息。 该规则还会将焦点引到并重置 **[!UICONTROL 客户ID]** 字段。 规则使用 [表单数据模型服务的dataIntegrationUtils API](/help/forms/using/invoke-form-data-model-services.md) 来检查数据库中是否存在客户ID。

1. 点按 **[!UICONTROL 客户ID]** 字段，然后点按 `Edit Rules` 图标。 的 [!UICONTROL 规则编辑器] 窗口。
1. 点按 **[!UICONTROL +创建]** 图标以添加规则。 此时将打开可视编辑器。

   在可视化编辑器中， **[!UICONTROL WHEN]** 语句。 此外，表单对象(在本例中， **[!UICONTROL 客户ID]**)中，将在 **[!UICONTROL WHEN]** 语句。

1. 点按 **[!UICONTROL 选择状态]** 下拉框并选择 **[!UICONTROL 已更改]**.

   ![when customidischanged](assets/whencustomeridischanged.png)

   在 **[!UICONTROL 然后]** 语句，选择 **[!UICONTROL 调用服务]** 从 **[!UICONTROL 选择操作]** 下拉菜单。

1. 从 **[!UICONTROL 可视编辑器]** to **[!UICONTROL 代码编辑器]**. 开关控件在窗口的右侧。 此时将打开代码编辑器，其中显示与以下内容类似的代码：

   ![代码编辑器](assets/code-editor.png)

1. 将输入变量部分替换为以下代码：

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. 替换 `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` 部分，其代码如下：

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
