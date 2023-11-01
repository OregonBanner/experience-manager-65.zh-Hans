---
title: 创建自定义表单映射
seo-title: Creating Custom Form Mappings
description: 在Adobe Campaign中创建自定义表时，您可能希望在AEM中构建映射到该自定义表的表单
seo-description: When you create a custom table in Adobe Campaign, you may want to build a form in AEM that maps to that custom table
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# 创建自定义表单映射{#creating-custom-form-mappings}

在Adobe Campaign中创建自定义表时，您可能希望在AEM中构建映射到该自定义表的表单。

本文档介绍如何创建自定义表单映射。 当您完成本文档中的步骤时，将为用户提供事件页面，用户可在其中注册即将举行的事件。 然后，您可以通过Adobe Campaign跟进这些用户。

## 前提条件 {#prerequisites}

您需要安装以下软件：

* Adobe Experience Manager
* Adobe Campaign Classic

请参阅 [将AEM与Adobe Campaign Classic集成](/help/sites-administering/campaignonpremise.md) 以了解更多信息。

## 创建自定义表单映射 {#creating-custom-form-mappings-2}

要创建自定义表单映射，您需要按照以下各节中详述的这些高级步骤进行操作：

1. 创建自定义表。
1. 扩展 **种子** 表格。
1. 创建自定义映射。
1. 根据自定义映射创建投放。
1. 在AEM中构建表单，该表单将使用创建的投放。
1. 提交表单以进行测试。

### 在Adobe Campaign中创建自定义表 {#creating-the-custom-table-in-adobe-campaign}

首先，在Adobe Campaign中创建自定义表。 在此示例中，我们使用以下定义来创建事件表：

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

创建事件表后，运行 **更新数据库结构向导** 以创建表。

### 扩展种子表 {#extending-the-seed-table}

在Adobe Campaign中，点按/单击 **添加** 要创建 **种子地址(nms)** 表格。

![chlimage_1-194](assets/chlimage_1-194.png)

现在，使用 **事件** 表以扩展 **种子** 表：

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

之后，运行 **更新数据库向导** 以应用更改。

### 创建自定义目标映射 {#creating-custom-target-mapping}

在 **管理/营销活动管理** t，转到 **目标映射** 并添加新的T **目标映射。**

>[!NOTE]
>
>请确保对以下内容使用有意义的名称： **内部名称**.

![chlimage_1-195](assets/chlimage_1-195.png)

### 创建自定义投放模板 {#creating-a-custom-delivery-template}

在此步骤中，您将添加一个使用所创建的 **目标映射**.

在 **资源/模板**，导航到投放模板并复制现有AEM投放。 当您单击 **至**，选择创建事件 **目标映射**.

![chlimage_1-196](assets/chlimage_1-196.png)

### 在AEM中构建表单 {#building-the-form-in-aem}

在AEM中，确保您已在中配置Cloud Service **页面属性**.

然后，在 **Adobe Campaign** 选项卡，选择在中创建的投放 [创建自定义投放模板](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

配置字段时，请确保为表单字段指定唯一的元素名称。

配置字段后，您需要手动更改映射。

在CRXDE-Lite中，转到 **jcr：content** （属于页面）节点，并更改 **acMapping** 的内部名称的值 **目标映射**.

![chlimage_1-198](assets/chlimage_1-198.png)

在表单的配置中，确保选中要创建的复选框（如果不存在）

![chlimage_1-199](assets/chlimage_1-199.png)

### 提交表单 {#submitting-the-form}

您现在可以提交表单，并在Adobe Campaign端验证值是否已保存。

![chlimage_1-200](assets/chlimage_1-200.png)

## 疑难解答 {#troubleshooting}

**“元素‘@eventdate’的值‘02/02/2015’的类型无效(类型为‘Event ([adb：event])&#39;)”**

提交表单时，此错误将记录在 **error.log** 在AEM中。

这是由于日期字段的格式无效。 解决方法是提供 **yyyy-mm-dd** 作为值。
