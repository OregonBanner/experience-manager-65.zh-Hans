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
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 3%

---


# 创建自定义表单映射{#creating-custom-form-mappings}

在Adobe Campaign中创建自定义表时，您可能希望在AEM中构建一个映射到该自定义表的表单。

本文档介绍如何创建自定义表单映射。 完成此文档中的步骤后，您将为用户提供一个事件页面，在该页面中，用户可以注册即将到来的事件。 然后，您通过Adobe Campaign跟进这些用户。

## 前提条件 {#prerequisites}

您需要安装以下组件：

* Adobe Experience Manager
* Adobe Campaign Classic

有关详细信息，请参阅[将AEM与Adobe Campaign Classic集成](/help/sites-administering/campaignonpremise.md)。

## 创建自定义表单映射 {#creating-custom-form-mappings-2}

要创建自定义表单映射，您需要遵循以下高级步骤，以下各节将详细介绍这些步骤：

1. 创建自定义表。
1. 扩展&#x200B;**seed**&#x200B;表。
1. 创建自定义映射。
1. 根据自定义映射创建投放。
1. 在AEM中构建表单，它将使用创建的投放。
1. 提交表单以对其进行测试。

### 在Adobe Campaign{#creating-the-custom-table-in-adobe-campaign}中创建自定义表

开始，方法是在Adobe Campaign中创建自定义表。 在此示例中，我们使用以下定义创建事件表：

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

创建事件表后，运行&#x200B;**更新数据库结构向导**&#x200B;以创建表。

### 扩展种子表{#extending-the-seed-table}

在Adobe Campaign中，点按／单击&#x200B;**添加**&#x200B;以创建&#x200B;**种子地址(nms)**&#x200B;表的新扩展。

![chlimage_1-194](assets/chlimage_1-194.png)

现在，使用&#x200B;**事件**&#x200B;表中的字段扩展&#x200B;**种子**&#x200B;表：

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

之后，运行&#x200B;**更新数据库向导**&#x200B;以应用更改。

### 创建自定义目标映射{#creating-custom-target-mapping}

在&#x200B;**管理/活动管理** t中，转到&#x200B;**目标映射**&#x200B;并添加新的T **目标映射。**

>[!NOTE]
>
>确保对&#x200B;**内部名称**&#x200B;使用有意义的名称。

![chlimage_1-195](assets/chlimage_1-195.png)

### 创建自定义投放模板{#creating-a-custom-delivery-template}

在此步骤中，您将添加一个使用创建的&#x200B;**投放模板**&#x200B;的目标映射。

在&#x200B;**资源／模板**&#x200B;中，导航到投放模板并重复现有AEM投放。 单击&#x200B;**To**&#x200B;时，选择创建事件&#x200B;**目标映射**。

![chlimage_1-196](assets/chlimage_1-196.png)

### 在AEM {#building-the-form-in-aem}中构建表单

在AEM中，确保已在&#x200B;**页面属性**&#x200B;中配置Cloud Service。

然后，在&#x200B;**Adobe Campaign**&#x200B;选项卡中，选择在[创建自定义投放模板](#creating-a-custom-delivery-template)中创建的投放。

![chlimage_1-197](assets/chlimage_1-197.png)

配置字段时，请确保为表单字段指定唯一的元素名称。

配置字段后，您需要手动更改映射。

在CRXDE-lite中，转到&#x200B;**jcr:content**（页面）节点，将&#x200B;**acMapping**&#x200B;值更改为&#x200B;**目标映射**&#x200B;的内部名称。

![chlimage_1-198](assets/chlimage_1-198.png)

在表单的配置中，确保选中复选框以创建非现有表单

![chlimage_1-199](assets/chlimage_1-199.png)

### 提交表单{#submitting-the-form}

您现在可以提交表单并在Adobe Campaign端验证是否保存了这些值。

![chlimage_1-200](assets/chlimage_1-200.png)

## 疑难解答 {#troubleshooting}

**&quot;元素&#39;@eventdate&#39;中值&#39;02/02/2015&#39;的类型无效(类型为&#39;文档(adb:[事件])&#39;的事件)&quot;**

提交表单时，此错误将记录在AEM的&#x200B;**error.log**&#x200B;中。

这是由于日期字段的格式无效。 解决方法是提供&#x200B;**yyyy-mm-dd**&#x200B;作为值。

