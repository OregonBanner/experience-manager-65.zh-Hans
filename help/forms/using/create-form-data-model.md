---
title: “教程：创建表单数据模型“
seo-title: 创建表单数据模型教程
description: 创建表单数据模型
seo-description: 创建表单数据模型
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Tutorial: Create form data model {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是“创建您的第一个自 [适应表单”系列中的一个步骤](../../forms/using/create-your-first-adaptive-form.md) 。 建议按照时间顺序按照这一系列来了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

AEM Forms数据集成模块允许您从不同的后端数据源(如AEM用户用户档案、RESTful Web服务、基于SOAP的Web服务、OData服务和关系数据库)创建表单数据模型。 您可以在表单数据模型中配置数据模型对象和服务，并将其与自适应表单关联。 自适应表单字段绑定到数据模型对象属性。 通过这些服务，您可以预填自适应表单并将提交的表单数据写入数据模型对象。

有关表单数据集成和表单数据模型的更多信息，请参 [阅AEM表单数据集成](../../forms/using/data-integration.md)。

本教程将指导您逐步准备、创建、配置表单数据模型并将其与自适应表单相关联。 在本教程的结尾，您将能够：

* [将MySQL数据库配置为数据源](#config-database)
* [使用MySQL数据库创建表单数据模型](#create-fdm)
* [配置表单数据模型](#config-fdm)
* [测试表单数据模型](#test-fdm)

表单数据模型将类似于：

![form-data-model_l](assets/form-data-model_l.png)

**答：** 已配置数 **据源B。** 数据源模式 **C.** Available services **D.** 数据模型对 **象E。** 配置的服务

## 前提条件 {#prerequisites}

在开始之前，请确保您具有以下各项：

* MySQL数据库，其示例数据在创建第一个自适应表单的“先决条件” [部分中指定](../../forms/using/create-your-first-adaptive-form.md)
* MySQL JDBC驱动程序的OSGi捆绑，如捆绑JDBC数 [据库驱动程序中所述](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* 如第一个教程创建自适应表单中 [所述的自适应表单](/help/forms/using/create-adaptive-form.md)

## 第1步：将MySQL数据库配置为数据源 {#config-database}

您可以配置不同类型的数据源以创建表单数据模型。 在本教程中，我们将配置您配置的MySQL数据库，并填充示例数据。 有关其他受支持数据源的信息以及如何配置它们，请参 [阅AEM Forms数据集成](../../forms/using/data-integration.md)。

执行以下操作以配置MySQL数据库：

1. 将MySQL数据库的JDBC驱动程序作为OSGi包安装：

   1. 以管理员身份登录到AEM Forms作者实例，然后转到AEM Web控制台包。 默认URL为 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。

   1. 点按 **安装／更新**。 出现 **“上传／安装包** ”对话框。

   1. 点按 **选择文件** ，浏览并选择MySQL JDBC驱动程序OSGi包。 选择 **开始包** 和刷新包 **，然后点**&#x200B;按安装或更新 ****。 确保Oracle Corporation的MySQL JDBC驱动程序处于活动状态。 已安装驱动程序。

1. 将MySQL数据库配置为数据源：

   1. 转到AEM Web控制台，网址为 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 找到 **Apache Sling Connection池化DataSource配置** 。 点按以在编辑模式下打开配置。
   1. 在配置对话框中，指定以下详细信息：

      * **数据源名称：** 您可以指定任何名称。 例如，指定 **WeRetailMySQL**。
      * **DataSource服务属性名称**:指定包含DataSource名称的服务属性的名称。 在将数据源实例注册为OSGi服务时指定它。 例如， **datasource.name**。
      * **JDBC驱动程序类**:指定JDBC驱动程序的Java类名。 对于MySQL数据库，指 **定com.mysql.jdbc.Driver**。
      * **JDBC连接URI**:指定数据库的连接URL。 对于在端口3306和模式weretail上运行的MySQL数据库，URL为： `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用户名：** 数据库用户名。 需要使JDBC驱动程序能够与数据库建立连接。
      * **密码：** 数据库的口令。 需要使JDBC驱动程序能够与数据库建立连接。
      * **借阅测试：** 启用“借 **阅时测试** ”选项。
      * **返回时测试：** 启用“ **返回时测试** ”选项。
      * **验证查询:** 指定SQL SELECT查询以验证池中的连接。 查询必须至少返回一行。 例如，从客 **户详细信息中选择***。
      * **事务隔离**:将该值设置 **为READ_COMMITTED**。
      将其他属性保留为默 [认值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) ，然后点 **按保存**。
   此时会创建与以下配置类似的配置。

   ![关系数据库——数据源——配置](assets/relational-database-data-source-configuration.png)

## Step 2: Create form data model {#create-fdm}

AEM Forms提供了一个直观的用户界面，用 [于从配置的数据源创建表单](data-integration.md) 数据模型。 您可以在表单数据模型中使用多个数据源。 对于我们的用例，我们将使用已配置的MySQL数据源。

执行以下操作以创建表单数据模型：

1. 在AEM作者实例中，导航到“表 **单** ”>“ **数据集成”**。
1. Tap **Create** > **Form Data Model**.
1. 在“创建表单数据模型”对话框中，指定 **表单数据模** 型的名称。 例如， **customer-shipping-billing-details**。 点按下 **一步**。
1. 选择数据源屏幕列表所有已配置的数据源。 选择 **WeRetailMySQL** 数据源，然后点按 **创建**。

   ![数据源选择](assets/data-source-selection.png)

将创 **建客户送货——结帐——详细信息** （表单数据模型）。

## 第3步：配置表单数据模型 {#config-fdm}

配置表单数据模型涉及：

* 添加数据模型对象和服务
* 为数据模型对象配置读写服务

执行以下操作以配置表单数据模型：

1. 在AEM作者实例上，导航到“表 **单** ”>“ **数据集成”**。 默认URL为 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 此处 **列出您之前创建的客户送货——结帐-** -详细信息表单数据模型。 在编辑模式下打开它。

   所选数据源 **WeRetailMySQL** 是在表单数据模型中配置的。

   ![default-fdm](assets/default-fdm.png)

1. 展开WeRailMySQL数据源树。 从Weretail **>** customerdetails **模式中选择以下数据模型对象和服** 务以形成数据模型：

   * **数据模型对象**:

      * id
      * 名称
      * shippingAddress
      * 城市
      * 状态
      * zipcode
   * **服务:**

      * 获取
      * 更新
   点按 **添加选定项** ，将选定数据模型对象和服务添加到表单数据模型。

   ![WeRetail模式](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC数据源的默认获取、更新和插入服务是随附表单数据模型的现成功能。

1. 为数据模型对象配置读和写服务。

   1. 选择客户 **详细信息** ，然后点按编辑 **属性**。
   1. 从 **读取** “服务”下拉菜单中选择获取。 将自 **动添加** id参数，该参数是customerdetails数据模型对象中的主键。 点 ![按aem_6_3_edit](assets/aem_6_3_edit.png) ，然后按如下配置参数。

      ![read-default](assets/read-default.png)

   1. 同样，选择 **“更新** ”作为“写入服务”。 customerdetails **对象将** added as argument as automatically. 参数配置如下。

      ![write-default](assets/write-default.png)

      按如下方式添加 **和配置** id参数。

      ![id-arg](assets/id-arg.png)

   1. 点按 **完成** ，以保存数据模型对象属性。 然后，点按保 **存** ，以保存表单数据模型。

      get **** 和 **** update服务将添加为数据模型对象的默认服务。

      ![数据模型对象](assets/data-model-object.png)

1. 转到“服 **务** ”选项卡，配 **置获取****和更新** 服务。

   1. 选择 **get服务** ，然后点按编 **辑属性**。 属性对话框打开。
   1. 在“编辑属性”对话框中指定以下内容：

      * **标题**:指定服务的标题。 例如：检索送货地址。
      * **说明**:指定包含服务的详细功能的说明。 例如：

         此服务从MySQL数据库检索送货地址和其他客户详细信息

      * **输出模型对象**:选择包含客户数据的模式。 例如：

         客户详细信息模式

      * **返回数组**:禁用“返 **回数组** ”选项。
      * **参数**:选择名为 **ID的参数**。
      点按&#x200B;**完成**。已配置从MySQL数据库检索客户详细信息的服务。

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 选择更新 **服务** ，然后点按编 **辑属性**。 属性对话框打开。

   1. 在“编辑属性”对话框中指定以下内容：

      * **标题**:指定服务的标题。 例如，更新送货地址。
      * **说明**:指定包含服务的详细功能的说明。 例如：

         此服务更新MySQL数据库中的送货地址和相关字段

      * **输入模型对象**:选择包含客户数据的模式。 例如：

         客户详细信息模式

      * **输出类型**:选择 **BOOLEAN**。

      * **参数**:选择名为 **ID的参数** ，并选 **择客户详细信息**。
      点按&#x200B;**完成**。MySQL **数据库中** ，用于更新客户详细信息的更新服务已配置。

      ![shiiping-address-update](assets/shiiping-address-update.png)



配置表单数据模型中的数据模型对象和服务。 您现在可以测试表单数据模型。

## Step 4: Test form data model {#test-fdm}

您可以测试数据模型对象和服务，以验证表单数据模型是否配置正确。

执行以下操作以运行测试：

1. 转到“模 **型** ”选项卡，选择 **Customerdetails** 数据模型对象，然后点按 **测试模型对象**。
1. 在“测 **试模型／服务** ”窗口中，从“选择模型／服务”下拉框中选择“读取模型对象” **，然后从“****** 选择模型／服务”下拉框中选择“读取模型对象”。
1. 在customerdetails **部分** ，为配置的MySQL数据库中存在的 **id参数指定一个值，然后点按** 测试 ****。

   将获取与指定ID关联的客户详细信息并在“输出”部 **分中显示** ，如下所示。

   ![测试读取模型](assets/test-read-model.png)

1. 同样，您也可以测试Write模型对象和服务。

   在以下示例中，更新服务成功更新了数据库中id 7102715的地址详细信息。

   ![测试写模型](assets/test-write-model.png)

   现在，如果您再次测试id 7107215的读模型服务，它将获取并显示更新后的客户详细信息，如下所示。

   ![已更新](assets/read-updated.png)
