---
title: 创建自定义表单映射
seo-title: 创建自定义表单映射
description: 在Adobe Campaign中创建自定义表时，您可能希望在AEM中构建一个映射到该自定义表的表单
seo-description: 在Adobe Campaign中创建自定义表时，您可能希望在AEM中构建一个映射到该自定义表的表单
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 创建自定义表单映射{#creating-custom-form-mappings}

在Adobe Campaign中创建自定义表时，您可能希望在AEM中构建一个映射到该自定义表的表单。

本文档介绍如何创建自定义表单映射。 完成本文档中的步骤后，您将为用户提供一个活动页面，用户可在该页面注册即将开展的活动。 然后，您可以通过Adobe Campaign跟踪这些用户。

## 前提条件 {#prerequisites}

您需要安装以下软件：

* Adobe Experience Manager
* Adobe Campaign Classic

See [Integrating AEM with Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) for more information.

## 创建自定义表单映射 {#creating-custom-form-mappings-2}

要创建自定义表单映射，您需要执行以下高级步骤，以下各节将详细介绍这些步骤：

1. 创建自定义表。
1. 扩展 **种子表** 。
1. 创建自定义映射。
1. 根据自定义映射创建分发。
1. 在AEM中构建表单，该表单将使用创建的分发。
1. 提交表单以测试它。

### 在Adobe Campaign中创建自定义表 {#creating-the-custom-table-in-adobe-campaign}

首先，在Adobe Campaign中创建自定义表。 在此示例中，我们使用以下定义创建一个事件表：

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

创建事件表后，运行“更新数 **据库结构”向导** ，以创建表。

### 扩展种子表 {#extending-the-seed-table}

在Adobe Campaign中，点按／单 **击添加** ，以创建种子地址(nms) **表的新扩展** 。

![chlimage_1-194](assets/chlimage_1-194.png)

现在，使用事件表中 **的字段** ，扩展种 **子表** :

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

之后，运行“更 **新数据库”向导** ，以应用更改。

### 创建自定义目标映射 {#creating-custom-target-mapping}

在“ **管理／营销**&#x200B;活动管理”中，转 **到“目标映射** ”并添加新的“**目标映射”。**

>[!NOTE]
>
>确保对“内部名称”使用有意义 **的名称**。

![chlimage_1-195](assets/chlimage_1-195.png)

### 创建自定义交付模板 {#creating-a-custom-delivery-template}

在此步骤中，您将添加一个使用创建的 **Target映射的分发模板**。

在“ **资源／模板**”中，导航到“交付模板”并复制现有AEM交付。 单击“至” **时**，选择创建事件 **Target映射**。

![chlimage_1-196](assets/chlimage_1-196.png)

### 在AEM中构建表单 {#building-the-form-in-aem}

在AEM中，确保已在页面属性中配置了云 **服务**。

然后，在 **Adobe Campaign选项卡中** ，选择在创建自定义分发模 [板中创建的分发](#creating-a-custom-delivery-template)。

![chlimage_1-197](assets/chlimage_1-197.png)

配置字段时，请确保为表单字段指定唯一的元素名称。

配置字段后，您需要手动更改映射。

在CRXDE-lite中，转到 **jcr:content** (of the page)节点，将 **acMapping** value更改为 **Target映射的内部名称**。

![chlimage_1-198](assets/chlimage_1-198.png)

在表单的配置中，确保选中复选框以创建非现有表单

![chlimage_1-199](assets/chlimage_1-199.png)

### 提交表单 {#submitting-the-form}

您现在可以提交表单并在Adobe Campaign端验证是否保存了这些值。

![chlimage_1-200](assets/chlimage_1-200.png)

## 疑难解答 {#troubleshooting}

**&quot;元素&#39;@eventdate&#39;中值&#39;02/02/2015&#39;的类型无效(文档类型为&#39;Event([adb:event])&#39;)&quot;**

提交表单时，此错误会记录在AEM **的error.log** 中。

这是由于日期字段的格式无效所致。 解决方法是提 **供yyyy-mm-dd** 作为值。

