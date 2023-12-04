---
title: 将规则应用于自适应表单字段
seo-title: Apply rules to adaptive form fields
description: 创建规则以将交互性、业务逻辑和智能验证添加到自适应表单。
seo-description: Create rules to add interactivity, business logic, and smart validations to an adaptive form.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# 教程：将规则应用于自适应表单字段 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教程是 [创建您的第一个自适应表单](/help/forms/using/create-your-first-adaptive-form.md) 系列。 Adobe建议按时间顺序关注系列，以了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

您可以使用规则将交互性、业务逻辑和智能验证添加到自适应表单。 自适应表单具有内置规则编辑器。 规则编辑器提供了与引导式导览类似的拖放功能。 拖放方法是创建规则的最快、最简单的方法。 规则编辑器还为有兴趣测试其编码技能或将规则提升到更高层次的用户提供了一个代码窗口。

要了解有关规则编辑器的更多信息，请访问 [自适应Forms规则编辑器](/help/forms/using/rule-editor.md).

在本教程结束时，您将学习如何创建规则以：

* 调用表单数据模型服务以从数据库中检索数据
* 调用表单数据模型服务以向数据库添加数据
* 运行验证检查并显示错误消息

本教程每个部分末尾的交互式GIF图像可帮助您动态学习和验证所构建表单的功能。

## 步骤1：从数据库中检索客户记录 {#retrieve-customer-record}

通过执行以下操作来创建表单数据模型 [创建表单数据模型](/help/forms/using/create-form-data-model.md) 文章。 现在，您可以使用规则编辑器调用Forms数据模型服务，以检索信息并将其添加到数据库。

每个客户都分配有一个唯一的客户ID号，这有助于在数据库中识别相关的客户数据。 以下过程使用客户ID从数据库中检索信息：

1. 打开自适应表单进行编辑。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 选择 **[!UICONTROL 客户ID]** 字段并选择 **[!UICONTROL 编辑规则]** 图标。 将打开“规则编辑器”窗口。
1. 选择 **[!UICONTROL +创建]** 图标以添加规则。 该操作将打开可视编辑器。

   在可视编辑器中， **[!UICONTROL 时间]** 语句默认处于选中状态。 此外，表单对象(在本例中， **[!UICONTROL 客户ID]**)，从中启动规则编辑器，并在 **[!UICONTROL 时间]** 语句。

1. 选择 **[!UICONTROL 选择状态]** 下拉并选择 **[!UICONTROL 已更改]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

1. 在 **[!UICONTROL 则]** 语句，选择 **[!UICONTROL 调用服务]** 从 **[!UICONTROL 选择操作]** 下拉菜单。
1. 选择 **[!UICONTROL 检索送货地址]** 来自的服务 **[!UICONTROL 选择]** 下拉菜单。
1. 拖放 **[!UICONTROL 客户ID]** “表单对象”选项卡中的字段 **[!UICONTROL 放置对象或在此选择]** 中的字段 **[!UICONTROL 输入]** 盒子。

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 拖放 **[!UICONTROL 客户ID、姓名、送货地址、省/市/自治区以及邮政编码]** “表单对象”选项卡中的字段 **[!UICONTROL 放置对象或在此选择]** 中的字段 **[!UICONTROL 输出]** 盒子。

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   选择 **[!UICONTROL 完成]** 以保存规则。 在规则编辑器窗口中，选择 **[!UICONTROL 关闭]**.

1. 预览自适应表单。 在中输入ID **[!UICONTROL 客户ID]** 字段。 该表单现在可以从数据库中检索客户详细信息。

   ![retrieve-information](assets/retrieve-information.gif)

## 步骤2：将更新的客户地址添加到数据库 {#updated-customer-address}

从数据库中检索到客户详细信息后，您可以更新送货地址、省/市和邮政编码。 以下过程调用表单数据模型服务将客户信息更新到数据库：

1. 选择 **[!UICONTROL 提交]** 字段并选择 **[!UICONTROL 编辑规则]** 图标。 将打开“规则编辑器”窗口。
1. 选择 **[!UICONTROL 提交 — 单击]** 规则并选择 **[!UICONTROL 编辑]** 图标。 此时会显示用于编辑“提交”规则的选项。

   ![submit规则](assets/submit-rule.png)

   在WHEN选项中， **[!UICONTROL 提交]** 和 **[!UICONTROL 已单击]** 已选择选项。

   ![已单击submit](assets/submit-is-clicked.png)

1. 在 **[!UICONTROL 则]** 选项，选择 **[!UICONTROL +添加语句]** 选项。 选择 **[!UICONTROL 调用服务]** 从 **[!UICONTROL 选择操作]** 下拉菜单。
1. 选择 **[!UICONTROL 更新送货地址]** 来自的服务 **[!UICONTROL 选择]** 下拉菜单。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 拖放 **[!UICONTROL 送货地址、省/市/自治区以及邮政编码]** 中的字段 [!UICONTROL 表单对象] 选项卡中的对应tablename .property（例如customerdetails .shippingAddress） **[!UICONTROL 放置对象或在此选择]** 中的字段 **[!UICONTROL 输入]** 盒子。 以tablename为前缀的所有字段（例如，此用例中的customerdetails）用作更新服务的输入数据。 这些字段中提供的所有内容都会在数据源中进行更新。

   >[!NOTE]
   >
   >请勿拖放 **[!UICONTROL 名称]** 和 **[!UICONTROL 客户ID]** 字段到对应的tablename.property（例如，customerdetails.name）。 它有助于避免错误地更新客户的名称和ID。

1. 拖放 **[!UICONTROL 客户ID]** 中的字段 [!UICONTROL 表单对象] 选项卡中的标识字段 **[!UICONTROL 输入]** 盒子。 不带前缀表名的字段（例如，此使用案例中的customerdetails）用作更新服务的搜索参数。 此 **[!UICONTROL id]** 字段在此使用案例中唯一标识  **customerdetails**  表格。
1. 选择 **[!UICONTROL 完成]** 以保存规则。 在规则编辑器窗口中，选择 **[!UICONTROL 关闭]**.
1. 预览自适应表单。 检索客户的详细信息，更新送货地址，并提交表单。 再次检索同一客户的详细信息时，将显示更新的送货地址。

## 步骤3：（额外部分）使用代码编辑器运行验证并显示错误消息 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您应该对表单运行验证，以确保在表单中输入的数据正确，并且在数据不正确时显示错误消息。 例如，如果在表单中输入了不存在的客户ID，则会显示一条错误消息。

自适应表单为多个组件提供了内置的验证，例如可用于常见用例的电子邮件和数值字段。 对于高级用例，使用规则编辑器可在数据库返回零(0)记录（无记录）时显示错误消息。

以下过程说明如何创建规则，以在表单中输入的客户ID在数据库中不存在时显示错误消息。 规则还会聚焦并重置 **[!UICONTROL 客户ID]** 字段。 规则使用 [表单数据模型服务的dataIntegrationUtils API](/help/forms/using/invoke-form-data-model-services.md) 检查客户ID是否存在于数据库中。

1. 选择 **[!UICONTROL 客户ID]** 字段并选择 `Edit Rules` 图标。 此 [!UICONTROL 规则编辑器] 窗口打开。
1. 选择 **[!UICONTROL +创建]** 图标以添加规则。 该操作将打开可视编辑器。

   在可视编辑器中， **[!UICONTROL 时间]** 语句默认处于选中状态。 此外，表单对象(在本例中， **[!UICONTROL 客户ID]**)，从中启动规则编辑器，并在 **[!UICONTROL 时间]** 语句。

1. 选择 **[!UICONTROL 选择状态]** 下拉并选择 **[!UICONTROL 已更改]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

   在 **[!UICONTROL 则]** 语句，选择 **[!UICONTROL 调用服务]** 从 **[!UICONTROL 选择操作]** 下拉菜单。

1. 切换自 **[!UICONTROL 可视编辑器]** 到 **[!UICONTROL 代码编辑器]**. 开关控件位于窗口的右侧。 代码编辑器将打开，显示类似于以下内容的代码：

   ![代码编辑器](assets/code-editor.png)

1. 将输入变量部分替换为以下代码：

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. 替换 `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` 部分代码相同的内容：

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

1. 预览自适应表单。 输入不正确的客户ID。 出现错误消息。

   ![display-validation-error](assets/display-validation-error.gif)
