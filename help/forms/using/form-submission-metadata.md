---
title: 将用户数据中的信息添加到表单提交元数据
seo-title: Adding information from user data to form submission metadata
description: 了解如何使用用户提供的数据将信息添加到已提交表单的元数据。
seo-description: Learn how to add information to metadata of a submitted form with user provided data.
uuid: c3eea3c0-31f8-4bf8-b5cf-34f907bdbdba
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
feature: Adaptive Forms
exl-id: 5ca850e3-30f0-4384-b615-356dc3c2ad0d
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---

# 将用户数据中的信息添加到表单提交元数据{#adding-information-from-user-data-to-form-submission-metadata}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

您可以使用在表单元素中输入的值来计算草稿或表单提交的元数据字段。 元数据允许您根据用户数据筛选内容。 例如，用户在表单的名称字段中输入John Doe。 您可以使用此信息计算元数据，该元数据可将此提交归入首字母JD下。

要使用用户输入的值计算元数据字段，请在元数据中添加表单的元素。 当用户在该元素中输入值时，脚本使用该值计算信息。 此信息会添加到元数据中。 将元素添加为元数据字段时，需要提供其键。 键将作为字段添加到元数据中，并且计算的信息将根据该键进行记录。

例如，健康保险公司发布表单。 在此表单中，字段捕获最终用户的年龄。 在许多用户提交表单后，客户希望检查特定年龄范围内的所有提交。 添加元数据可帮助客户，而不是处理所有随着表单数量的增加而变得复杂的数据。 表单作者可以配置最终用户填充的属性/数据存储在顶级，以便进行最轻松的搜索。 其他元数据是存储在元数据节点顶级的用户填写信息，如作者配置的那样。

再看一个捕获电子邮件ID和电话号码的表单示例。 当用户匿名访问此表单并放弃该表单时，作者可以配置表单以自动保存电子邮件ID和电话号码。 此表单会自动保存，并且电话号码和电子邮件ID会存储在草稿的元数据节点中。 此配置的用例是潜在客户管理仪表板。

## 将表单元素添加到元数据 {#adding-form-elements-to-metadata}

执行以下步骤以在元数据中添加元素：

1. 在编辑模式下打开自适应表单。\
   要在编辑模式下打开表单，请在表单管理器中，选择您的表单并点按 **打开**.
1. 在编辑模式下，选择一个组件，然后点按 ![字段级](assets/field-level.png) > **自适应表单容器**，然后点按 ![cmppr](assets/cmppr.png).
1. 在侧栏中，单击 **元数据**.
1. 在元数据部分中，单击 **添加**.
1. 使用“元数据”选项卡的“值”字段可添加脚本。 您添加的脚本从表单上的元素中收集数据，并计算提供给元数据的值。

   例如， **true** 如果输入的年龄大于21岁，则记录在元数据中，并且 **false** 小于21时记录。 在“元数据”选项卡中输入以下脚本：

   `(agebox.value >= 21) ? true : false`

   ![元数据脚本](assets/add-element-metadata.png)

   在“元数据”选项卡中输入的脚本

1. 单击&#x200B;**确定**。

用户在选定为元数据字段的元素中输入数据后，计算的信息将记录到元数据中。 您可以在配置为存储元数据的存储库中查看元数据。

## 查看更新的表单提交元数据： {#seeing-updated-form-nbsp-submission-metadata}

对于上述示例，元数据存储在CRX存储库中。 元数据如下所示：

![元数据](assets/metadata_entry_new.png)

如果在元数据中添加复选框元素，则选定的值将以逗号分隔的字符串形式存储。 例如，在表单中添加复选框组件，并将其名称指定为 `checkbox1`. 在复选框组件属性中，添加值0、1和2的“驾驶执照”、“社会保险号”和“护照”项目。

![从复选框中存储多个值](assets/checkbox-metadata.png)

选择自适应表单容器，然后在表单属性中添加元数据键 `cb1` 哪些存储 `checkbox1.value`，并发布表单。 当客户填写表单时，客户会在复选框字段中选择“护照和社会保险号码”选项。 值1和2在提交元数据的cb1字段中存储为1、2。

![在复选框字段中选择的多个值的元数据条目](assets/metadata-entry.png)

>[!NOTE]
>
>以上示例仅供学习之用。 确保按照AEM Forms实施中的配置，在正确的位置查找元数据。
