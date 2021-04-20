---
title: “教程：创建表单数据模型”
seo-title: 为交互通信创建表单数据模型
description: 为交互通信创建表单数据模型
seo-description: 为交互通信创建表单数据模型
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2749'
ht-degree: 0%

---


# 教程：创建表单数据模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是[创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md)系列中的一个步骤。 建议按照时间顺序按照该系列进行操作，以了解、执行和演示完整的教程用例。

## 关于教程{#about-the-tutorial}

AEM Forms数据集成模块允许您从不同的后端数据源(如AEM用户用户档案、RESTful Web服务、基于SOAP的Web服务、OData服务和关系数据库)创建表单数据模型。 您可以在表单数据模型中配置数据模型对象和服务，并将其与自适应表单关联。 自适应表单字段绑定到数据模型对象属性。 这些服务使您能够预填自适应表单并将提交的表单数据写入数据模型对象。

有关表单数据集成和表单数据模型的详细信息，请参阅[AEM Forms数据集成](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)。

本教程将指导您完成准备、创建、配置表单数据模型并将其与交互式通信关联的步骤。 在本教程的结尾，您将能够：

* [设置数据库](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [将MySQL数据库配置为数据源](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [创建表单数据模型](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [配置表单数据模型](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [测试表单数据模型](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

表单数据模型类似于以下内容：

![表单数据模型](assets/form_data_model_callouts_new.png)

**A.配** 置的数 **据源B.** 数据源 **模式** C.Available  **services** D.D.Data  **** model对象E.C.Configured Services

## 前提条件 {#prerequisites}

在开始之前，请确保您具备以下各项：

* MySQL数据库，其示例数据如[设置数据库](../../forms/using/create-form-data-model0.md#step-set-up-the-database)部分中所述。
* [捆绑JDBC数据库驱动程序](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)中说明的MySQL JDBC驱动程序的OSGi捆绑

## 第1步：设置数据库{#step-set-up-the-database}

数据库是创建交互式通信的必备工具。 本教程使用数据库来显示Interactive Communications的表单数据模型和持久性功能。 设置包含客户、帐单和调用表的数据库。
下图说明了客户表的示例数据：

![sample_data_cust](assets/sample_data_cust.png)

使用以下DDL语句在数据库中创建&#x200B;**customer**&#x200B;表。

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

使用以下DDL语句在数据库中创建&#x200B;**bills**&#x200B;表。

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

使用以下DDL语句在数据库中创建&#x200B;**调用**&#x200B;表。

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

**呼叫**&#x200B;表包括呼叫详细信息，如呼叫日期、呼叫时间、呼叫号码、呼叫持续时间和呼叫费用。 **customer**&#x200B;表使用“移动号码”(mobilenum)字段链接到呼叫表。 对于&#x200B;**customer**&#x200B;表中列出的每个移动号码，**调用**&#x200B;表中有多个记录。 例如，您可以引用&#x200B;**调用**&#x200B;表来检索&#x200B;**1457892541**&#x200B;移动号码的调用详细信息。

**bills**&#x200B;表包括账单详细信息，如账单日期、账单期间、每月费用和通话费。 **customer**&#x200B;表使用“清单计划”字段链接到&#x200B;**bills**&#x200B;表。 在&#x200B;**customer**&#x200B;表中有一个与每个客户关联的计划。 **bills**&#x200B;表包括所有现有计划的定价详细信息。 例如，您可以从&#x200B;**customer**&#x200B;表中检索&#x200B;**Sarah**&#x200B;的计划详细信息，并使用这些详细信息从&#x200B;**bills**&#x200B;表中检索定价详细信息。

## 第2步：将MySQL数据库配置为数据源{#step-configure-mysql-database-as-data-source}

您可以配置不同类型的数据源以创建表单数据模型。 在本教程中，您将配置已配置并填充示例数据的MySQL数据库。 有关其他受支持数据源以及如何配置数据源的信息，请参阅[AEM Forms数据集成](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)。

执行以下操作以配置MySQL数据库：

1. 将MySQL数据库的JDBC驱动程序作为OSGi包安装：

   1. 以管理员身份登录到AEM Forms作者实例，然后转到AEM Web控制台包。 默认URL为[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。
   1. 点按&#x200B;**安装/更新**。 将显示&#x200B;**上载/安装包**&#x200B;对话框。

   1. 点按&#x200B;**选择文件**&#x200B;以浏览并选择MySQL JDBC驱动程序OSGi包。 选择&#x200B;**开始包**&#x200B;和&#x200B;**刷新包**，然后点按&#x200B;**安装**&#x200B;或&#x200B;**更新**。 确保Oracle Corporation的MySQL JDBC驱动程序处于活动状态。 已安装驱动程序。

1. 将MySQL数据库配置为数据源：

   1. 转到位于[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)的AEM Web控制台。
   1. 找到&#x200B;**Apache Sling Connection Pooled DataSource**&#x200B;配置。 点按可在编辑模式下打开配置。
   1. 在配置对话框中，指定以下详细信息：

      * **数据源名称：** 您可以指定任何名称。例如，指定&#x200B;**MySQL**。

      * **DataSource服务属性名称**:指定包含DataSource名称的服务属性的名称。将数据源实例注册为OSGi服务时指定。 例如，**datasource.name**。

      * **JDBC驱动程序类**:指定JDBC驱动程序的Java类名。对于MySQL数据库，请指定&#x200B;**com.mysql.jdbc.Driver**。

      * **JDBC连接URI**:指定数据库的连接URL。对于在端口3306和模式 Teleca上运行的MySQL数据库，URL为：`jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用户名：** 数据库的用户名。需要启用JDBC驱动程序以与数据库建立连接。
      * **口令：** 数据库的口令。需要启用JDBC驱动程序以与数据库建立连接。
      * **借阅时测试：** 启用 **借阅** 测试。

      * **返回时测试：** 启用 **返回** 时测试。

      * **验证查询:** 指定SQL SELECT查询以验证池中的连接。查询必须至少返回一行。 例如，**从customer**&#x200B;中选择*。

      * **事务隔离**:将值设置 **为READ_COMMITTED**。
   将其他属性保留为默认值[值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)，然后点按&#x200B;**保存**。

   将创建与以下内容类似的配置。

   ![Apache配置](assets/apache_configuration_new.png)

## 第3步：创建表单数据模型{#step-create-form-data-model}

AEM Forms为[从配置的数据源创建表单数据模式](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l提供直观的用户界面。 您可以在表单数据模型中使用多个数据源。 对于本教程中的用例，您将使用MySQL作为数据源。

执行以下操作以创建表单数据模型：

1. 在AEM作者实例中，导航到&#x200B;**Forms** > **数据集成**。
1. 点按&#x200B;**创建** > **表单数据模型**。
1. 在“创建表单数据模型”向导中，为表单数据模型指定&#x200B;**名称**。 例如，**FDM_Create_First_IC**。 点按&#x200B;**下一步**。
1. 选择数据源屏幕会列表所有配置的数据源。 选择&#x200B;**MySQL**&#x200B;数据源，然后点按&#x200B;**创建**。

   ![MYSQL数据源](assets/fdm_mysql_data_source_new.png)

1. 单击&#x200B;**完成**。将创建&#x200B;**FDM_Create_First_IC**&#x200B;表单数据模型。

## 第4步：配置表单数据模型{#step-configure-form-data-model}

配置表单数据模型包括：

* [添加数据模型对象和服务](#add-data-model-objects-and-services)
* [为数据模型对象创建计算子属性](#create-computed-child-properties-for-data-model-object)
* [添加数据模型对象之间的关联](#add-associations-between-data-model-objects)
* [编辑数据模型对象属性](#edit-data-model-object-properties)
* [为数据模型对象配置服务](#configure-services)

### 添加数据模型对象和服务{#add-data-model-objects-and-services}

1. 在AEM作者实例上，导航到&#x200B;**Forms** > **数据集成**。 默认URL为[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 此处列出您之前创建的&#x200B;**FDM_Create_First_IC**&#x200B;表单数据模型。 选择它并点按&#x200B;**编辑**。

   选定的数据源&#x200B;**MySQL**&#x200B;显示在&#x200B;**数据源**&#x200B;窗格中。

   ![FDM的MYSQL数据源](assets/mysql_fdm_new.png)

1. 展开&#x200B;**MySQL**&#x200B;数据源树。 从&#x200B;**teleca**&#x200B;模式中选择以下数据模型对象和服务：

   * **数据模型对象**:

      * 比尔
      * 呼叫
      * 客户
   * **服务:**

      * 获取
      * 更新

   点按&#x200B;**添加选定**，将选定的数据模型对象和服务添加到表单数据模型。

   ![选择数据模型对象服务](assets/select_data_model_object_services_new.png)

   清单、调用和客户数据模型对象显示在&#x200B;**模型**&#x200B;选项卡的右侧窗格中。 获取和更新服务显示在&#x200B;**服务**&#x200B;选项卡中。

   ![数据模型对象](assets/data_model_objects_new.png)

### 为数据模型对象{#create-computed-child-properties-for-data-model-object}创建计算子属性

computed属性是根据规则或表达式计算其值的属性。 使用规则，您可以将计算属性的值设置为文本字符串、数字、数学表达式的结果或表单数据模型中其他属性的值。

根据用例，使用以下数学表达式在&#x200B;**bills**&#x200B;数据模型对象中创建&#x200B;**usagecharges**&#x200B;子计算属性：

* 使用费=通话费+电话会议费+短信费+移动互联网费+漫游国家+漫游国际+ VAS（所有这些属性都存在于帐单数据模型对象中）
有关**usagecharges**&#x200B;子计算属性的详细信息，请参阅[规划交互式通信](/help/forms/using/planning-interactive-communications.md)。

执行以下步骤为清单数据模型对象创建计算的子属性：

1. 选中&#x200B;**bills**&#x200B;数据模型对象顶部的复选框以将其选中，然后点按&#x200B;**创建子属性**。
1. 在&#x200B;**创建子属性**&#x200B;窗格中：

   1. 输入&#x200B;**usagecharges**&#x200B;作为子属性的名称。
   1. 启用&#x200B;**Computed**。
   1. 选择&#x200B;**浮动**&#x200B;作为类型，然后点按&#x200B;**完成**&#x200B;将子属性添加到&#x200B;**bills**&#x200B;数据模型对象。

   ![创建子属性](assets/create_child_property_new.png)

1. 点按&#x200B;**编辑规则**&#x200B;以打开规则编辑器。
1. 点按&#x200B;**创建**。将打开&#x200B;**设置值**&#x200B;规则窗口。
1. 从“选择选项”下拉列表中，选择&#x200B;**数学表达式**。

   ![使用费规则编辑器](assets/usage_charges_rule_editor_new.png)

1. 在数学表达式中，分别选择&#x200B;**callcharges**&#x200B;和&#x200B;**confcallcharges**&#x200B;作为第一和第二对象。 选择&#x200B;**加号**&#x200B;作为运算符。 在数学表达式中点按并点按&#x200B;**扩展表达式**&#x200B;以添加&#x200B;**smsccharges**、**internetcharges**、**roamingnational**、**roamingintnl**&#x200B;和&#x200B;**vas/>对象。**

   下图描述了规则编辑器中的数学表达式:

   ![使用费用规则](assets/usage_charges_rule_all_new.png)

1. 点按&#x200B;**完成**。规则将在规则编辑器中创建。
1. 点按&#x200B;**关闭**&#x200B;以关闭“规则编辑器”窗口。

### 添加数据模型对象{#add-associations-between-data-model-objects}之间的关联

定义数据模型对象后，您可以在它们之间构建关联。 关联可以是一对一或一对多。 例如，可以有多个与某个员工关联的依赖项。 它称为一对多关联，由1:n在连接关联数据模型对象的行上进行描绘。 但是，如果关联为给定的员工ID返回唯一的员工姓名，则它称为一对一关联。

在将数据源中的关联数据模型对象添加到表单数据模型时，它们的关联将保留并显示为通过箭头线连接。

根据用例，在数据模型对象之间创建以下关联：

| 协会 | 数据模型对象 |
|---|---|
| 1:n | customer:calls（可以在每月账单中与客户关联多个呼叫） |
| 1:1 | 客户：帐单（一个帐单与特定月份的客户关联） |

请执行以下步骤以创建数据模型对象之间的关联：

1. 选中&#x200B;**customer**&#x200B;数据模型对象顶部的复选框以将其选中，然后点按&#x200B;**添加关联**。 将打开&#x200B;**添加关联**&#x200B;属性窗格。
1. 在&#x200B;**添加关联**&#x200B;窗格中：

   * 指定关联的标题。 它是可选字段。
   * 从&#x200B;**类型**&#x200B;下拉列表中选择&#x200B;**一至多**。

   * 从&#x200B;**模型对象**&#x200B;下拉列表中选择&#x200B;**调用**。

   * 从&#x200B;**服务**&#x200B;下拉列表中选择&#x200B;**get**。

   * 点按&#x200B;**添加**&#x200B;以将&#x200B;**customer**&#x200B;数据模型对象链接到使用属性调用&#x200B;****&#x200B;数据模型对象。 根据用例，调用数据模型对象必须链接到客户数据模型对象中的移动号码属性。 将打开&#x200B;**添加参数**&#x200B;对话框。

   ![添加关联](assets/add_association_new.png)

1. 在&#x200B;**添加参数**&#x200B;对话框中：

   * 从&#x200B;**名称**&#x200B;下拉列表中选择&#x200B;**mobilenum**。 mobile number属性是客户中可用并调用数据模型对象的通用属性。 因此，它用于在客户和调用数据模型对象之间创建关联。
对于客户数据模型对象中的每个可用移动号码，调用表中有多个可用的调用记录。

   * 为参数指定可选标题和说明。
   * 从&#x200B;**绑定到**&#x200B;下拉列表中选择&#x200B;**customer**。

   * 从&#x200B;**绑定值**&#x200B;下拉列表中选择&#x200B;**mobilenum**。

   * 点按&#x200B;**添加**。

   ![为参数添加关联](assets/add_association_argument_new.png)

   mobilenum属性显示在&#x200B;**Arguments**&#x200B;部分中。

   ![添加参数关联](assets/add_argument_association_new.png)

1. 点按&#x200B;**完成**，在客户和调用数据模型对象之间创建1:n关联。

   在创建客户与调用数据模型对象之间的关联后，在客户与清单数据模型对象之间创建1:1关联。

1. 选中&#x200B;**customer**&#x200B;数据模型对象顶部的复选框以将其选中，然后点按&#x200B;**添加关联**。 将打开&#x200B;**添加关联**&#x200B;属性窗格。
1. 在&#x200B;**添加关联**&#x200B;窗格中：

   * 指定关联的标题。 它是可选字段。
   * 从&#x200B;**类型**&#x200B;下拉列表中选择&#x200B;**一到一**。

   * 从&#x200B;**模型对象**&#x200B;下拉列表中选择&#x200B;**bills**。

   * 从&#x200B;**服务**&#x200B;下拉列表中选择&#x200B;**get**。 **billplan**&#x200B;属性（清单表的主键）已在&#x200B;**Arguments**部分中可用。
清单和客户数据模型对象分别使用开单计划（清单）和客户计划（客户）属性进行链接。 在这些属性之间创建一个绑定，以检索MySQL数据库中任何可用客户的计划详细信息。

   * 从&#x200B;**绑定到**&#x200B;下拉列表中选择&#x200B;**customer**。

   * 从&#x200B;**绑定值**&#x200B;下拉列表中选择&#x200B;**customerplan**。

   * 点按&#x200B;**完成**&#x200B;以在开单计划属性和customerplan属性之间创建绑定。

   ![添加客户帐单的关联](assets/add_association_customer_bills_new.png)

   下图描述了数据模型对象与用于在它们之间创建关联的属性之间的关联：

   ![fdm_associations](assets/fdm_associations.gif)

### 编辑数据模型对象属性{#edit-data-model-object-properties}

在创建客户与其他数据模型对象之间的关联后，编辑客户属性以定义从数据模型对象检索数据时所依据的属性。 基于用例，将移动号码用作从客户数据模型对象检索数据的属性。

1. 选中&#x200B;**customer**&#x200B;数据模型对象顶部的复选框以将其选中，然后点按&#x200B;**编辑属性**。 将打开&#x200B;**编辑属性**&#x200B;窗格。
1. 将&#x200B;**customer**&#x200B;指定为&#x200B;**顶级模型对象**。
1. 从&#x200B;**读取服务**&#x200B;下拉列表中选择&#x200B;**get**。
1. 在&#x200B;**参数**&#x200B;部分中：

   * 从&#x200B;**绑定到**&#x200B;下拉列表中选择&#x200B;**请求属性**。

   * 指定&#x200B;**mobilenum**&#x200B;作为绑定值。

1. 从&#x200B;**写入**&#x200B;服务下拉列表中选择&#x200B;**更新**。
1. 在&#x200B;**参数**&#x200B;部分中：

   * 对于&#x200B;**mobilenum**&#x200B;属性，从&#x200B;**绑定到**&#x200B;下拉列表中选择&#x200B;**customer**。

   * 从&#x200B;**绑定值**&#x200B;下拉列表中选择&#x200B;**mobilenum**。

1. 点按&#x200B;**完成**&#x200B;以保存属性。

   ![配置服务](assets/configure_services_customer_new.png)

1. 选中&#x200B;**调用**&#x200B;数据模型对象顶部的复选框以将其选中，然后点按&#x200B;**编辑属性**。 将打开&#x200B;**编辑属性**&#x200B;窗格。
1. 为&#x200B;**调用**&#x200B;数据模型对象禁用&#x200B;**顶级模型对象**。
1. 点按&#x200B;**完成**。

   重复步骤8 - 10，为&#x200B;**bills**&#x200B;数据模型对象配置属性。

### 配置服务{#configure-services}

1. 转到&#x200B;**服务**&#x200B;选项卡。
1. 选择&#x200B;**get**&#x200B;服务，然后点按&#x200B;**编辑属性**。 将打开&#x200B;**编辑属性**&#x200B;窗格。
1. 在&#x200B;**编辑属性**&#x200B;窗格中：

   * 输入可选标题和说明。
   * 从&#x200B;**输出模型对象**&#x200B;下拉列表中选择&#x200B;**customer**。

   * 点按&#x200B;**完成**&#x200B;以保存属性。

   ![编辑属性](assets/edit_properties_get_details_new.png)

1. 选择&#x200B;**update**&#x200B;服务，然后点按&#x200B;**编辑属性**。 将打开&#x200B;**编辑属性**&#x200B;窗格。
1. 在&#x200B;**编辑属性**&#x200B;窗格中：

   * 输入可选标题和说明。
   * 从&#x200B;**输入模型对象**&#x200B;下拉列表中选择&#x200B;**customer**。

   * 点按&#x200B;**完成**。
   * 点按&#x200B;**保存**&#x200B;以保存表单数据模型。

   ![更新服务属性](assets/update_service_properties_new.png)

## 第5步：测试表单数据模型和服务{#step-test-form-data-model-and-services}

您可以测试数据模型对象和服务，以验证表单数据模型配置是否正确。

执行以下操作以运行测试：

1. 转到&#x200B;**Model**&#x200B;选项卡，选择&#x200B;**customer**&#x200B;数据模型对象，然后点按&#x200B;**测试模型对象**。
1. 在&#x200B;**测试表单数据模型**&#x200B;窗口中，从&#x200B;**选择模型/服务**&#x200B;下拉列表中选择&#x200B;**读取模型对象**。
1. 在&#x200B;**Input**&#x200B;部分中，为配置的MySQL数据库中存在的&#x200B;**mobilenum**&#x200B;属性指定一个值，然后点按&#x200B;**Test**。

   将获取与指定mobilenum属性关联的客户详细信息并在“输出”部分中显示，如下所示。 关闭对话框。

   ![测试数据模型](assets/test_data_model_new.png)

1. 转到&#x200B;**服务**&#x200B;选项卡。
1. 选择&#x200B;**get**&#x200B;服务，然后点按&#x200B;**测试服务。**
1. 在&#x200B;**Input**&#x200B;部分中，为配置的MySQL数据库中存在的&#x200B;**mobilenum**&#x200B;属性指定一个值，然后点按&#x200B;**Test**。

   将获取与指定mobilenum属性关联的客户详细信息并在“输出”部分中显示，如下所示。 关闭对话框。

   ![测试服务](assets/test_service_new.png)

### 编辑并保存示例数据{#edit-and-save-sample-data}

表单数据模型编辑器允许您为表单数据模型中的所有数据模型对象属性（包括计算属性）生成示例数据。 它是一组随机值，与为每个属性配置的数据类型一致。 您还可以编辑和保存数据，即使重新生成示例数据，数据也会保留。

执行以下操作以生成、编辑和保存示例数据：

1. 在表单数据模型页上，点按&#x200B;**编辑示例数据**。 它会在“编辑示例数据”窗口中生成并显示示例数据。

   ![编辑示例数据](assets/edit_sample_data_new.png)

1. 在&#x200B;**编辑示例数据**&#x200B;窗口中，根据需要编辑数据，然后点按&#x200B;**保存**。 关上窗口。


