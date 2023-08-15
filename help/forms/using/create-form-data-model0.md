---
title: “教程：在AEM Forms中创建表单数据模型”
description: 为交互式通信创建表单数据模型
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2737'
ht-degree: 0%

---

# 教程：在AEM Forms中创建表单数据模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是 [创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建议按时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

AEM Forms数据集成模块允许您从不同的后端数据源(如AEM用户配置文件、RESTful Web服务、基于SOAP的Web服务、OData服务和关系数据库)创建表单数据模型。 您可以在表单数据模型中配置数据模型对象和服务，并将其与自适应表单关联。 自适应表单字段绑定到数据模型对象属性。 这些服务使您能够预填充自适应表单并将提交的表单数据写回数据模型对象。

有关表单数据集成和表单数据模型的更多信息，请参阅 [AEM Forms数据集成](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

本教程将指导您完成准备、创建、配置表单数据模型并将其与交互式通信关联的步骤。 在本教程结束时，您将能够：

* [设置数据库](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [将MySQL数据库配置为数据源](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [创建表单数据模型](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [配置表单数据模型](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [测试表单数据模型](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

表单数据模型类似于以下内容：

![表单数据模型](assets/form_data_model_callouts_new.png)

**答：** 配置的数据源 **B.** 数据源架构 **C.** 可用服务 **D.** 数据模型对象 **E.** 配置的服务

## 前提条件 {#prerequisites}

在开始之前，请确保您具备以下条件：

* 包含示例数据的MySQL数据库，如 [设置数据库](../../forms/using/create-form-data-model0.md#step-set-up-the-database) 部分。
* 用于MySQL JDBC驱动程序的OSGi包，如中所述 [捆绑JDBC数据库驱动程序](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## 步骤1：设置数据库 {#step-set-up-the-database}

数据库是创建交互式通信所必需的。 本教程使用数据库来显示表单数据模型和交互式通信的持久性功能。 设置包含客户、清单和调用表的数据库。
下图说明了customer表的示例数据：

![示例_data_cust](assets/sample_data_cust.png)

使用以下DDL语句创建 **客户** 表中的数据。

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

使用以下DDL语句创建 **帐单** 表中的数据。

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

使用以下DDL语句创建 **调用** 表中的数据。

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

此 **调用** 该表包括呼叫详细信息，如呼叫日期、呼叫时间、呼叫编号、呼叫持续时间和呼叫费用。 此 **客户** 表使用手机号码(mobilenum)字段链接到呼叫表。 对于 **客户** 表中，存在多条记录 **调用** 表格。 例如，您可以检索 **1457892541** 手机号码(通过引用 **调用** 表格。

此 **帐单** 该表包括开单详细信息，如开单日期、开单期间、每月费用和呼叫费用。 此 **客户** 表链接到 **帐单** 使用“清单计划”字段的表格。 有一个计划与中的每位客户相关联 **客户** 表格。 此 **帐单** 该表包括所有现有计划的定价详细信息。 例如，您可以检索计划详细信息 **Sarah** 从 **客户** 表，并使用这些详细信息从 **帐单** 表格。

## 步骤2：将MySQL数据库配置为数据源 {#step-configure-mysql-database-as-data-source}

您可以配置不同类型的数据源来创建表单数据模型。 在本教程中，您将配置已配置并填充了示例数据的MySQL数据库。 有关其他受支持的数据源以及如何配置这些数据源的信息，请参阅 [AEM Forms数据集成](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

执行以下操作以配置MySQL数据库：

1. 以OSGi捆绑包形式安装MySQL数据库的JDBC驱动程序：

   1. 以管理员身份登录AEM Forms创作实例，然后转到AEM Web控制台包。 默认URL为 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. 点按 **安装/更新**. An **上传/安装包** 出现对话框。

   1. 点按 **选择文件** 浏览并选择MySQL JDBC驱动程序OSGi包。 选择 **开始捆绑包** 和 **刷新包**，然后点击 **安装** 或 **更新**. 确保Oracle公司的MySQL JDBC驱动程序处于活动状态。 已安装驱动程序。

1. 将MySQL数据库配置为数据源：

   1. 转到位于的AEM Web控制台 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 定位 **Apache Sling连接池化数据源** 配置。 点按以在编辑模式下打开配置。
   1. 在配置对话框中，指定以下详细信息：

      * **数据源名称：** 您可以指定任意名称。 例如，指定 **MySQL**.

      * **数据源服务属性名称**：指定包含DataSource名称的服务属性的名称。 在将数据源实例注册为OSGi服务时指定它。 例如， **数据源名称**.

      * **JDBC驱动程序类**：指定JDBC驱动程序的Java类名。 对于MySQL数据库，请指定 **com.mysql.jdbc.Driver**.

      * **JDBC连接URI**：指定数据库的连接URL。 对于在端口3306和模式teleca上运行的MySQL数据库，URL为： `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用户名：** 数据库的用户名。 必须启用JDBC驱动程序才能与数据库建立连接。
      * **密码：** 数据库的密码。 必须启用JDBC驱动程序才能与数据库建立连接。
      * **借入测试：** 启用 **借阅测试** 选项。

      * **回访时测试：** 启用 **回访时测试** 选项。

      * **验证查询：** 指定一个SQL SELECT查询来验证池中的连接。 查询必须至少返回一行。 例如， **选择 &#42; 来自客户**.

      * **事务隔离**：将值设置为 **读取已提交**.

   将其他属性保留为默认值 [值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) 并点击 **保存**.

   将创建类似于以下内容的配置。

   ![Apache配置](assets/apache_configuration_new.png)

## 步骤3：创建表单数据模型 {#step-create-form-data-model}

AEM Forms提供了一个直观的用户界面，用于 [创建表单数据模式](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l来自配置的数据源。 您可以在表单数据模型中使用多个数据源。 对于本教程中的用例，您将使用MySQL作为数据源。

执行以下操作以创建表单数据模型：

1. 在AEM创作实例中，导航到 **Forms** > **数据集成**.
1. 点按 **创建** > **表单数据模型**.
1. 在创建表单数据模型向导中，指定 **name** 用于表单数据模型。 例如， **FDM_Create_First_IC**. 点按 **下一个**.
1. 选择数据源屏幕列出了所有已配置的数据源。 选择 **MySQL** 数据源并点按 **创建**.

   ![MYSQL数据源](assets/fdm_mysql_data_source_new.png)

1. 单击&#x200B;**完成**。此 **FDM_Create_First_IC** 创建表单数据模型。

## 步骤4：配置表单数据模型 {#step-configure-form-data-model}

配置表单数据模型包括：

* [添加数据模型对象和服务](#add-data-model-objects-and-services)
* [创建数据模型对象的计算子属性](#create-computed-child-properties-for-data-model-object)
* [添加数据模型对象之间的关联](#add-associations-between-data-model-objects)
* [编辑数据模型对象属性](#edit-data-model-object-properties)
* [为数据模型对象配置服务](#configure-services)

### 添加数据模型对象和服务 {#add-data-model-objects-and-services}

1. 在AEM创作实例上，导航到 **Forms** > **数据集成**. 默认URL为 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. 此 **FDM_Create_First_IC** 此处列出了您之前创建的表单数据模型。 选择并点击 **编辑**.

   所选数据源 **MySQL** 显示在 **数据源** 窗格。

   ![适用于FDM的MYSQL数据源](assets/mysql_fdm_new.png)

1. 展开 **MySQL** 数据源树。 从中选择以下数据模型对象和服务 **teleca** 架构：

   * **数据模型对象**：

      * 帐单
      * 调用
      * 客户

   * **服务:**

      * get
      * 更新

   点按 **添加选定项** 将选定的数据模型对象和服务添加到表单数据模型。

   ![选择数据模型对象服务](assets/select_data_model_object_services_new.png)

   清单、呼叫和客户数据模型对象显示在右侧窗格中的 **模型** 选项卡。 获取和更新服务将显示在 **服务** 选项卡。

   ![数据模型对象](assets/data_model_objects_new.png)

### 为数据模型对象创建计算子属性 {#create-computed-child-properties-for-data-model-object}

计算属性是根据规则或表达式计算其值的属性。 使用规则，您可以将计算属性的值设置为文本字符串、数字、数学表达式的结果或表单数据模型中其他属性的值。

根据用例，创建 **使用费用** 中的子计算属性 **帐单** 数据模型对象使用以下数学表达式：

* 使用费=呼叫费用+会议呼叫费用+ SMS费用+移动互联网费用+漫游国家+漫游国际+ VAS（所有这些属性都存在于帐单数据模型对象中）有关 **使用费用** 子计算属性，请参见 [规划交互式通信](/help/forms/using/planning-interactive-communications.md).

执行以下步骤，为清单数据模型对象创建计算子属性：

1. 选中顶部的复选框 **帐单** 要选择并点按的数据模型对象 **创建子属性**.
1. 在 **创建子属性** 窗格：

   1. 输入 **使用费用** 作为子资产的名称。
   1. 启用 **已计算**.
   1. 选择 **浮动** 作为类型并点击 **完成** 将子属性添加到 **帐单** 数据模型对象。

   ![创建子属性](assets/create_child_property_new.png)

1. 点按 **编辑规则** 以打开规则编辑器。
1. 点按&#x200B;**创建**。此 **设置值** 规则窗口将打开。
1. 从选择选项下拉列表中，选择 **数学表达式**.

   ![使用费规则编辑器](assets/usage_charges_rule_editor_new.png)

1. 在数学表达式中，选择 **callcharges** 和 **confcallcharges** 分别作为第一和第二对象。 选择 **加** 作为运算符。 在数学表达式中点按，然后点按 **扩展表达式** 添加 **smscharges**， **网间费用**， **roamingnational**， **roamingintel**、和 **vas** 表达式中的对象。

   下图描述了规则编辑器中的数学表达式：

   ![使用费用规则](assets/usage_charges_rule_all_new.png)

1. 点按 **完成**. 将在规则编辑器中创建规则。
1. 点按 **关闭** 关闭“规则编辑器”窗口。

### 在数据模型对象之间添加关联 {#add-associations-between-data-model-objects}

定义数据模型对象后，您可以建立它们之间的关联。 关联可以是一对一或一对多。 例如，可以有多个与员工关联的家属。 它称为一对多关联，在连接关联的数据模型对象的行上以1：n表示。 但是，如果关联为给定员工ID返回唯一的员工姓名，则称为一对一关联。

当您将数据源中的关联数据模型对象添加到表单数据模型时，它们的关联将保留并以箭头线连接的方式显示。

根据用例，在数据模型对象之间创建以下关联：

| 关联 | 数据模型对象 |
|---|---|
| 1：n | 客户：呼叫（每个月可以将多个呼叫与客户关联） |
| 1:1 | 客户：帐单（一个帐单与特定月份的客户关联） |

执行以下步骤来创建数据模型对象之间的关联：

1. 选中顶部的复选框 **客户** 要选择并点按的数据模型对象 **添加关联**. 此 **添加关联** 属性窗格打开。
1. 在 **添加关联** 窗格：

   * 指定关联的标题。 它是一个可选字段。
   * 选择 **一对多** 从 **类型** 下拉列表。

   * 选择 **调用** 从 **模型对象** 下拉列表。

   * 选择 **get** 从 **服务** 下拉列表。

   * 点按 **添加** 以链接 **客户** 数据模型对象到 **调用** 数据模型对象。 根据用例，调用数据模型对象必须链接到客户数据模型对象中的手机号码属性。 此 **添加参数** 对话框打开。

   ![添加关联](assets/add_association_new.png)

1. 在 **添加参数** 对话框：

   * 选择 **mobilenum** 从 **名称** 下拉列表。 手机号码属性是客户中可用的一个常用属性，可调用数据模型对象。 因此，它用于在customer和calls数据模型对象之间创建关联。
对于客户数据模型对象中可用的每个移动设备号码，“呼叫”表中都有多个可用的呼叫记录。

   * 为参数指定可选标题和描述。
   * 选择 **客户** 从 **绑定到** 下拉列表。

   * 选择 **mobilenum** 从 **捆绑值** 下拉列表。

   * 点按 **添加**.

   ![为参数添加关联](assets/add_association_argument_new.png)

   mobilenum属性显示在 **参数** 部分。

   ![添加参数关联](assets/add_argument_association_new.png)

1. 点按 **完成** 在customer和calls数据模型对象之间创建1：n关联。

   在客户和调用数据模型对象之间创建关联后，在客户和清单数据模型对象之间创建1:1关联。

1. 选中顶部的复选框 **客户** 要选择并点按的数据模型对象 **添加关联**. 此 **添加关联** 属性窗格打开。
1. 在 **添加关联** 窗格：

   * 指定关联的标题。 它是一个可选字段。
   * 选择 **一对一** 从 **类型** 下拉列表。

   * 选择 **帐单** 从 **模型对象** 下拉列表。

   * 选择 **get** 从 **服务** 下拉列表。 此 **billplan** 属性，即bills表的主键，在 **参数** 部分。
清单和客户数据模型对象分别使用billplan (bills)和customerplan (customer)属性链接。 创建这些属性之间的绑定以检索MySQL数据库中任何可用客户的计划详细信息。

   * 选择 **客户** 从 **绑定到** 下拉列表。

   * 选择 **customerplan** 从 **捆绑值** 下拉列表。

   * 点按 **完成** 创建billplan和customerplan属性之间的绑定。

   ![添加客户帐单关联](assets/add_association_customer_bills_new.png)

   下图描述了数据模型对象与用于创建它们之间的关联的属性之间的关联：

   ![fdm_associations](assets/fdm_associations.gif)

### 编辑数据模型对象属性 {#edit-data-model-object-properties}

在客户与其他数据模型对象之间创建关联后，编辑客户属性以定义属性，数据将基于此属性从数据模型对象中检索。 根据用例，使用手机号码作为属性，从客户数据模型对象中检索数据。

1. 选中顶部的复选框 **客户** 要选择并点按的数据模型对象 **编辑属性**. 此 **编辑属性** 窗格打开。
1. 指定 **客户** 作为 **顶级模型对象**.
1. 选择 **get** 从 **读取服务** 下拉列表。
1. 在 **参数** 部分：

   * 选择 **请求属性** 从 **绑定到** 下拉列表。

   * 指定 **mobilenum** 作为绑定值。

1. 选择 **更新** 从 **写入** “服务”下拉列表。
1. 在 **参数** 部分：

   * 对象 **mobilenum** 属性，选择 **客户** 从 **绑定到** 下拉列表。

   * 选择 **mobilenum** 从 **捆绑值** 下拉列表。

1. 点按 **完成** 以保存属性。

   ![配置服务](assets/configure_services_customer_new.png)

1. 选中顶部的复选框 **调用** 要选择并点按的数据模型对象 **编辑属性**. 此 **编辑属性** 窗格打开。
1. 禁用 **顶级模型对象** 对象 **调用** 数据模型对象。
1. 点按 **完成**.

   重复步骤8 - 10以配置属性 **帐单** 数据模型对象。

### 配置服务 {#configure-services}

1. 转到 **服务** 选项卡。
1. 选择 **get** 服务和点击 **编辑属性**. 此 **编辑属性** 窗格打开。
1. 在 **编辑属性** 窗格：

   * 输入可选标题和描述。
   * 选择 **客户** 从 **输出模型对象** 下拉列表。

   * 点按 **完成** 以保存属性。

   ![编辑属性](assets/edit_properties_get_details_new.png)

1. 选择 **更新** 服务和点击 **编辑属性**. 此 **编辑属性** 窗格打开。
1. 在 **编辑属性** 窗格：

   * 输入可选标题和描述。
   * 选择 **客户** 从 **输入模型对象** 下拉列表。

   * 点按 **完成**.
   * 点按 **保存** 以保存表单数据模型。

   ![更新服务属性](assets/update_service_properties_new.png)

## 步骤5：测试表单数据模型和服务 {#step-test-form-data-model-and-services}

您可以测试数据模型对象和服务，以验证是否正确配置了表单数据模型。

执行以下操作以运行测试：

1. 转到 **模型** 选项卡，选择 **客户** 数据模型对象，然后点按 **测试模型对象**.
1. 在 **测试表单数据模型** 窗口，选择 **读取模型对象** 从 **选择模型/服务** 下拉列表。
1. 在 **输入** 部分，指定值 **mobilenum** 已配置的MySQL数据库中存在的属性，然后点击 **测试**.

   将会获取与指定的mobilenum属性关联的客户详细信息，并显示在“输出”部分中，如下所示。 关闭对话框。

   ![测试数据模型](assets/test_data_model_new.png)

1. 转到 **服务** 选项卡。
1. 选择 **get** 服务和点击 **测试服务。**
1. 在 **输入** 部分，指定值 **mobilenum** 已配置的MySQL数据库中存在的属性，然后点击 **测试**.

   将会获取与指定的mobilenum属性关联的客户详细信息，并显示在“输出”部分中，如下所示。 关闭对话框。

   ![测试服务](assets/test_service_new.png)

### 编辑并保存示例数据 {#edit-and-save-sample-data}

表单数据模型编辑器允许您为表单数据模型中的所有数据模型对象属性（包括计算属性）生成示例数据。 它是一组符合为每个属性配置的数据类型的随机值。 您还可以编辑并保存数据，即使重新生成示例数据也会保留这些数据。

执行以下操作以生成、编辑和保存示例数据：

1. 在表单数据模型页面上，点按 **编辑示例数据**. 它在“编辑示例数据”窗口中生成并显示示例数据。

   ![编辑示例数据](assets/edit_sample_data_new.png)

1. 在 **编辑示例数据** 窗口，根据需要编辑数据，然后点击 **保存**. 关闭窗口。
