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
translation-type: tm+mt
source-git-commit: e4d84b5c6f7d2bfcac942b0b685a8f1fd11274f0

---


# Tutorial: Create form data model{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是创建您的第一个交 [互式通信系列中的一个步骤](/help/forms/using/create-your-first-interactive-communication.md) 。 建议按照时间顺序按照这一系列来了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

AEM Forms数据集成模块允许您从不同的后端数据源(如AEM用户用户档案、RESTful Web服务、基于SOAP的Web服务、OData服务和关系数据库)创建表单数据模型。 您可以在表单数据模型中配置数据模型对象和服务，并将其与自适应表单关联。 自适应表单字段绑定到数据模型对象属性。 通过这些服务，您可以预填自适应表单并将提交的表单数据写入数据模型对象。

有关表单数据集成和表单数据模型的更多信息，请参 [阅AEM表单数据集成](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)。

本教程将指导您逐步准备、创建、配置表单数据模型并将其与交互式通信相关联。 在本教程的结尾，您将能够：

* [设置数据库](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [将MySQL数据库配置为数据源](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [创建表单数据模型](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [配置表单数据模型](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [测试表单数据模型](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

表单数据模型类似于以下内容：

![表单数据模型](assets/form_data_model_callouts_new.png)

**答：** 已配置数 **据源B。** 数据源模式 **C.** Available services **D.** 数据模型对 **象E。** 配置的服务

## 前提条件 {#prerequisites}

在开始之前，请确保您具有以下各项：

* MySQL数据库，其示例数据如“设置 [数据库”部分中所述](../../forms/using/create-form-data-model0.md#step-set-up-the-database) 。
* MySQL JDBC驱动程序的OSGi捆绑，如捆绑JDBC数 [据库驱动程序中所述](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## 第1步：设置数据库 {#step-set-up-the-database}

数据库是创建交互式通信的必备工具。 本教程使用数据库来显示Interactive Communications的表单数据模型和持久性功能。 设置包含客户、帐单和调用表的数据库。
下图说明了客户表的示例数据：

![sample_data_cust](assets/sample_data_cust.png)

使用以下DDL语句在数据库中 **创建** customer表。

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

使用以下DDL语句在数据库中 **创建** bills表。

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

使用以下DDL语句在数据库中 **创建** calls表。

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

呼 **叫表包括呼叫详细信息** ，例如呼叫日期、呼叫时间、呼叫号码、呼叫持续时间和呼叫费用。 客 **户表使用** “移动号码(mobilenum)”字段链接到呼叫表。 对于客户表中列出的每个 **手机** ，呼叫表中有多个 **记录** 。 例如，您可以通过引用调用表来检索 **1457892541** 移动号码的 **调用详细信息** 。

帐单 **表包括** 帐单详细信息，如帐单日期、帐单期间、每月费用和电话费。 客 **户表使用“清单计** 划 **** ”字段链接到清单表。 客户表中有一个与每位客户关联的 **计划** 。 清单 **表包括** 所有现有计划的定价详细信息。 例如，您可以从客户表中检索 **Sarah** 的计划详细信息，并 **使用这些详细信息从清单表中检索** 定价详细信息 **** 。

## 第2步：将MySQL数据库配置为数据源 {#step-configure-mysql-database-as-data-source}

您可以配置不同类型的数据源以创建表单数据模型。 在本教程中，您将配置已配置并填充示例数据的MySQL数据库。 有关其他受支持数据源的信息以及如何配置它们，请参 [阅AEM Forms数据集成](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)。

执行以下操作以配置MySQL数据库：

1. 将MySQL数据库的JDBC驱动程序作为OSGi包安装：

   1. 以管理员身份登录到AEM Forms作者实例，然后转到AEM Web控制台包。 默认URL为 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。
   1. 点按 **安装／更新**。 出现 **“上传／安装包** ”对话框。

   1. 点按 **选择文件** ，浏览并选择MySQL JDBC驱动程序OSGi包。 选择 **开始包** 和刷新包 **，然后点按安**&#x200B;装 **或******&#x200B;更新Reade Bundle。 确保Oracle Corporation的MySQL JDBC驱动程序处于活动状态。 已安装驱动程序。

1. 将MySQL数据库配置为数据源：

   1. 转到AEM Web控制台，网址为 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 找到 **Apache Sling Connection池化DataSource配置** 。 点按以在编辑模式下打开配置。
   1. 在配置对话框中，指定以下详细信息：

      * **数据源名称：** 您可以指定任何名称。 例如，指定 **MySQL**。

      * **DataSource服务属性名称**:指定包含DataSource名称的服务属性的名称。 在将数据源实例注册为OSGi服务时指定它。 例如， **datasource.name**。

      * **JDBC驱动程序类**:指定JDBC驱动程序的Java类名。 对于MySQL数据库，指 **定com.mysql.jdbc.Driver**。

      * **JDBC连接URI**:指定数据库的连接URL。 对于在端口3306和模式电话上运行的MySQL数据库，URL为： `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用户名：** 数据库用户名。 需要使JDBC驱动程序能够与数据库建立连接。
      * **密码：** 数据库的口令。 需要使JDBC驱动程序能够与数据库建立连接。
      * **借阅测试：** 启用“借 **阅时测试** ”选项。

      * **返回时测试：** 启用“ **返回时测试** ”选项。

      * **验证查询:** 指定SQL SELECT查询以验证池中的连接。 查询必须至少返回一行。 例如，从 **客户中选择***。

      * **事务隔离**:将该值设置 **为READ_COMMITTED**。
   将其他属性保留为默 [认值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) ，然后点 **按保存**。

   此时会创建与以下配置类似的配置。

   ![Apache配置](assets/apache_configuration_new.png)

## Step 3: Create form data model {#step-create-form-data-model}

AEM Forms提供了直观的用户界面，可 [从配置的数据源](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)创建表单数据模型。 您可以在表单数据模型中使用多个数据源。 对于本教程中的用例，您将使用MySQL作为数据源。

执行以下操作以创建表单数据模型：

1. 在AEM作者实例中，导航到“表 **单** ”>“ **数据集成”**。
1. Tap **Create** > **Form Data Model**.
1. 在“创建表单数据模型”向导中，指定表 **单数据模** 型的名称。 例如， **FDM_Create_First_IC**。 点按下 **一步**。
1. 选择数据源屏幕列表所有已配置的数据源。 选 **择MySQL** 数据源并点 **按创建**。

   ![MYSQL数据源](assets/fdm_mysql_data_source_new.png)

1. 单击&#x200B;**完成**。将 **创建FDM_Create_First_IC** 表单数据模型。

## 第4步：配置表单数据模型 {#step-configure-form-data-model}

配置表单数据模型包括：

* [添加数据模型对象和服务](#add-data-model-objects-and-services)
* [为数据模型对象创建计算子属性](#create-computed-child-properties-for-data-model-object)
* [添加数据模型对象之间的关联](#add-associations-between-data-model-objects)
* [编辑数据模型对象属性](#edit-data-model-object-properties)
* [为数据模型对象配置服务](#configure-services)

### 添加数据模型对象和服务 {#add-data-model-objects-and-services}

1. 在AEM作者实例上，导航到“表 **单** ”>“ **数据集成”**。 默认URL为 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 此处 **列出您之前创建的FDM_Create_First_IC** 表单数据模型。 选择它并点按 **编辑**。

   选定的数据 **源MySQL** 显示在“数 **据源** ”窗格中。

   ![FDM的MYSQL数据源](assets/mysql_fdm_new.png)

1. 展开 **MySQL数据源树** 。 从电信模式中选择以下数据模型对象 **和服务** :

   * **数据模型对象**:

      * 票据
      * 呼叫
      * 客户
   * **服务:**

      * 获取
      * 更新
   点按 **添加选定项** ，将选定的数据模型对象和服务添加到表单数据模型。

   ![选择数据模型对象服务](assets/select_data_model_object_services_new.png)

   清单、调用和客户数据模型对象显示在“模型”选项卡的右侧窗 **格中** 。 获取和更新服务显示在“服务”选 **项卡** 。

   ![数据模型对象](assets/data_model_objects_new.png)

### 为数据模型对象创建计算的子属性 {#create-computed-child-properties-for-data-model-object}

计算属性是根据规则或表达式计算其值的属性。 使用规则，您可以将计算属性的值设置为表单数据模型中的文本字符串、数字、数学表达式的结果或其他属性的值。

根据用例，使用以下数 **学表达式** ，在清单数据模型对 **** 象中创建Usagecharges子计算属性：

* 使用费=通话费+电话通话费+短信费+移动互联网费+漫游国家+漫游国际+ VAS（所有这些属性都存在于帐单数据模型对象中）有关 **usagecharges** child计算属性的详细信息，请参 [阅计划交互通信](/help/forms/using/planning-interactive-communications.md)。

执行以下步骤以为清单数据模型对象创建计算的子属性：

1. 选中清单数据模型对象顶部的复 **选框** ，选择该对象，然后点按创建 **子属性**。
1. 在“创建 **子属性** ”窗格中：

   1. 输 **入usagecharges** 作为子属性的名称。
   1. 启用 **计算**。
   1. 选择 **浮动** ，作为类型，然后点按完 **成** ，将子属性添加到 **** 清单数据模型对象。
   ![创建子属性](assets/create_child_property_new.png)

1. 点按 **编辑规则** ，以打开规则编辑器。
1. 点按&#x200B;**创建**。“设 **置值** ”规则窗口打开。
1. 从“选择选项”下拉菜单中，选择“数学 **表达式”**。

   ![使用费规则编辑器](assets/usage_charges_rule_editor_new.png)

1. 在数学表达式中，分别 **选择调用** , **并将调用** callcarges作为第一和第二对象。 选择 **加号** ，作为运算符。 在数学表达式内点击并点击扩展 **表达式** ，以将 **、互**&#x200B;连电荷、National **************** 、RoamingNational、RoamingInternit、RoamingIntintIntent、AmingVas对象添加到表达式中。

   下图描述了规则编辑器中的数学表达式:

   ![使用费用规则](assets/usage_charges_rule_all_new.png)

1. 点按&#x200B;**完成**。规则将在规则编辑器中创建。
1. 点按 **关闭** ，以关闭规则编辑器窗口。

### 添加数据模型对象之间的关联 {#add-associations-between-data-model-objects}

定义数据模型对象后，您可以在它们之间构建关联。 关联可以是一对一或一对多。 例如，可以有多个与某个员工关联的依赖项。 它称为一对多关联，由连接相关数据模型对象的线上的1:n描述。 但是，如果某个关联为给定的员工ID返回唯一的员工姓名，则它称为一对一关联。

将数据源中的关联数据模型对象添加到表单数据模型时，它们的关联将保留并显示为通过箭头线连接。

根据用例，在数据模型对象之间创建以下关联：

| 协会 | 数据模型对象 |
|---|---|
| 1:n | 客户：呼叫（每月帐单中可以与客户关联多个呼叫） |
| 1:1 | 客户：帐单（一个帐单与特定月份的客户关联） |

请执行以下步骤以创建数据模型对象之间的关联：

1. 选中客户数据模型对象顶部的复 **选框** ，将其选中并点按添加 **关联**。 此时将 **打开“添加关联** ”属性窗格。
1. 在“添加 **关联** ”窗格中：

   * 指定关联的标题。 它是一个可选字段。
   * 从“ **类型** ”下拉 **** 列表中选择“一对多”。

   * 从“ **模型对象** ”(Model Object **** )下拉列表中选择调用。

   * 从 **服务****下拉列表** 中选择“获取”。

   * 点 **按添加** ，链接 **客户数据模型对** 象以使用属性调 **** 用数据模型对象。 根据用例，调用数据模型对象必须链接到客户数据模型对象中的移动号码属性。 “添 **加参数** ”(Add Argument)对话框打开。
   ![添加关联](assets/add_association_new.png)

1. 在“添 **加参数** ”对话框中：

   * 从 **名称****下拉列表** 中选择mobilenum。 移动号码属性是客户中可用的公用属性，它调用数据模型对象。 结果，它用于在客户和调用数据模型对象之间创建关联。
对于客户数据模型对象中的每个可用移动号码，呼叫表中有多个可用的呼叫记录。

   * 为参数指定可选标题和说明。
   * 从 **绑定到****下拉列表中选** 择客户。

   * 从“ **绑定值** ”下 **拉列表中选择** mobilenum。

   * 点按 **添加**。
   ![为参数添加关联](assets/add_association_argument_new.png)

   mobilenum属性显示在“参数” **部分** 。

   ![添加参数关联](assets/add_argument_association_new.png)

1. 点按 **完成** ，在客户和调用数据模型对象之间创建1:n关联。

   在客户与调用数据模型对象之间建立关联后，在客户与清单数据模型对象之间建立1:1关联。

1. 选中客户数据模型对象顶部的复 **选框** ，将其选中并点按添加 **关联**。 此时将 **打开“添加关联** ”属性窗格。
1. 在“添加 **关联** ”窗格中：

   * 指定关联的标题。 它是一个可选字段。
   * 从 **类型下拉列表** ，选 **择一** 个到一个。

   * 从“ **模型对象** ”(Model Object **** )下拉列表中选择清单。

   * 从 **服务****下拉列表** 中选择“获取”。 “ **参数** ”部分中已提供帐单计划属性，该属性是帐单表的主要 **键** 。
清单和客户数据模型对象分别使用清单计划（清单）和客户计划（客户）属性进行链接。 在这些属性之间创建一个绑定，以检索MySQL数据库中任何可用客户的计划详细信息。

   * 从 **绑定到****下拉列表中选** 择客户。

   * 从“ **绑定值****”(Binding Value** )下拉列表中选择Customerplan。

   * 点按 **完成** ，以在开单计划和客户计划属性之间创建绑定。
   ![为客户帐单添加关联](assets/add_association_customer_bills_new.png)

   下图描述了数据模型对象与用于创建它们之间关联的属性之间的关联：

   ![fdm_associations](assets/fdm_associations.gif)

### 编辑数据模型对象属性 {#edit-data-model-object-properties}

在创建客户与其他数据模型对象之间的关联后，编辑客户属性以定义从数据模型对象检索数据时所基于的属性。 根据用例，使用移动号码作为属性从客户数据模型对象检索数据。

1. 选中客户数据模型对象顶部的复 **选框** ，将其选中并点按编辑 **属性**。 此时将 **打开“编辑属性** ”窗格。
1. 将 **customer** 指定为 **顶级模型对象**。
1. 从 **读取****服务下拉** 列表中选择获取。
1. 在“参 **数** ”部分：

   * 从“ **绑定到** ”下 **拉列表中选择** “请求属性”。

   * 指定 **mobilenum** 作为绑定值。

1. 从 **Write** **Service下拉列表中选** 择更新。
1. 在“参 **数** ”部分：

   * 对于 **mobilenum** 属性，从“绑定到”(Binding To **)下拉列表中** 选择customer **** 。

   * 从“ **绑定值** ”下 **拉列表中选择** mobilenum。

1. 点按 **完成** ，以保存属性。

   ![配置服务](assets/configure_services_customer_new.png)

1. 选中调用数据模型对象顶部的复 **选框** ，将其选中并点按编辑 **属性**。 此时将 **打开“编辑属性** ”窗格。
1. 为调用数 **据模型对象禁用“顶****级模型** ”对象。
1. 点按&#x200B;**完成**。

   重复步骤8 - 10，为清单数据模 **型对象** 配置属性。

### 配置服务 {#configure-services}

1. 转到“服 **务** ”选项卡。
1. 选择 **get服务** ，然后点按编 **辑属性**。 此时将 **打开“编辑属性** ”窗格。
1. 在“编辑 **属性** ”窗格中：

   * 输入可选标题和说明。
   * 从“ **输出模** 型对象 **** ”下拉列表中选择客户。

   * 点按 **完成** ，以保存属性。
   ![编辑属性](assets/edit_properties_get_details_new.png)

1. 选择更新 **服务** ，然后点按编 **辑属性**。 此时将 **打开“编辑属性** ”窗格。
1. 在“编辑 **属性** ”窗格中：

   * 输入可选标题和说明。
   * 从“ **输入模** 型对象”(Input Model Object **** )下拉列表中选择客户。

   * 点按&#x200B;**完成**。
   * 点按 **保存** ，以保存表单数据模型。
   ![更新服务属性](assets/update_service_properties_new.png)

## 第5步：测试表单数据模型和服务 {#step-test-form-data-model-and-services}

您可以测试数据模型对象和服务，以验证表单数据模型是否配置正确。

执行以下操作以运行测试：

1. 转到“模 **型** ”选项卡，选择 **customer** 数据模型对象，然后点按 **测试模型对象**。
1. 在“测 **试表单数据模型********** ”窗口中，从“选择模型／服务”下拉列表中选择“读取模型对象”。
1. 在“输 **入** ”部分中，为已配置的MySQL数据库中存在的 **mobilenum** 属性指定一个值，然后点按 **测试**。

   将获取与指定mobilenum属性关联的客户详细信息并在“输出”部分中显示，如下所示。 关闭对话框。

   ![测试数据模型](assets/test_data_model_new.png)

1. 转到“服 **务** ”选项卡。
1. 选择 **get服务** ，然后点 **按测试服务。**
1. 在“输 **入** ”部分中，为已配置的MySQL数据库中存在的 **mobilenum** 属性指定一个值，然后点按 **测试**。

   将获取与指定mobilenum属性关联的客户详细信息并在“输出”部分中显示，如下所示。 关闭对话框。

   ![测试服务](assets/test_service_new.png)

### 编辑和保存示例数据 {#edit-and-save-sample-data}

表单数据模型编辑器允许您为表单数据模型中的所有数据模型对象属性（包括计算属性）生成示例数据。 它是一组随机值，它们符合为每个属性配置的数据类型。 您还可以编辑和保存数据，即使重新生成示例数据，数据也会保留。

执行以下操作以生成、编辑和保存示例数据：

1. 在表单数据模型页面上，点按编 **辑示例数据**。 它会在“编辑示例数据”窗口中生成并显示示例数据。

   ![编辑范例数据](assets/edit_sample_data_new.png)

1. 在“ **编辑示例数据** ”窗口中，根据需要编辑数据，然后点按 **保存**。 关闭窗口。


