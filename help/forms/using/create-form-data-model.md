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
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 1%

---

# 教程：创建表单数据模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是[创建您的第一个自适应表单](../../forms/using/create-your-first-adaptive-form.md)系列中的一个步骤。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

## 关于教程{#about-the-tutorial}

AEM [!DNL Forms]数据集成模块允许您从不同的后端数据源(如AEM用户配置文件、RESTful Web服务、基于SOAP的Web服务、OData服务和关系数据库)创建表单数据模型。 您可以在表单数据模型中配置数据模型对象和服务，并将其与自适应表单相关联。 自适应表单字段绑定到数据模型对象属性。 利用这些服务，您可以预填自适应表单，并将提交的表单数据写回数据模型对象。

有关表单数据集成和表单数据模型的更多信息，请参阅[AEM Forms数据集成](../../forms/using/data-integration.md)。

本教程将指导您完成准备、创建、配置表单数据模型并将其与自适应表单相关联的步骤。 在本教程结束时，您将能够：

* [将MySQL数据库配置为数据源](#config-database)
* [使用MySQL数据库创建表单数据模型](#create-fdm)
* [配置表单数据模型](#config-fdm)
* [测试表单数据模型](#test-fdm)

表单数据模型将类似于以下内容：

![form-data-model_l](assets/form-data-model_l.png)

**A.** 配置的数 **据源B.** 数据源架构 **C.** 可用服务 **D.** 数据模型对象 **E.** 配置的服务

## 前提条件 {#prerequisites}

在开始之前，请确保您具有以下功能：

* [!DNL MySQL] 数据库，其中包含首个自适应表单的先决条件部分 [中所述的示例数据](../../forms/using/create-your-first-adaptive-form.md)
* [!DNL MySQL] JDBC驱动程序的OSGi包，如[捆绑JDBC数据库驱动程序](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)中所述
* 如第一个教程[创建自适应表单](/help/forms/using/create-adaptive-form.md)中所述

## 步骤1:将MySQL数据库配置为数据源{#config-database}

您可以配置不同类型的数据源以创建表单数据模型。 在本教程中，我们将配置您配置并填充示例数据的MySQL数据库。 有关其他受支持数据源及其配置方式的信息，请参阅[AEM Forms数据集成](../../forms/using/data-integration.md)。

请执行以下操作以配置[!DNL MySQL]数据库：

1. 将[!DNL MySQL]数据库的JDBC驱动程序安装为OSGi包：

   1. 以管理员身份登录AEM [!DNL Forms]创作实例，然后转到AEM Web控制台包。 默认URL为[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。

   1. 点按&#x200B;**[!UICONTROL Install/Update]**。 出现[!UICONTROL 上载/安装包]对话框。

   1. 点按&#x200B;**[!UICONTROL 选择文件]**&#x200B;以浏览并选择[!DNL MySQL] JDBC驱动程序OSGi包。 选择&#x200B;**[!UICONTROL 启动包]**&#x200B;和&#x200B;**[!UICONTROL 刷新包]**，然后点按&#x200B;**[!UICONTROL 安装或更新]**。 确保[!DNL MySQL]的[!DNL Oracle Corporation's] JDBC驱动程序处于活动状态。 已安装驱动程序。

1. 将[!DNL MySQL]数据库配置为数据源：

   1. 转到位于[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)的AEM Web控制台。
   1. 找到&#x200B;**Apache Sling连接池化数据源**&#x200B;配置。 点按以在编辑模式下打开配置。
   1. 在配置对话框中，指定以下详细信息：

      * **数据源名称：** 可以指定任何名称。例如，指定&#x200B;**WeRetailMySQL**。
      * **数据源服务属性名称**:指定包含数据源名称的服务属性的名称。在将数据源实例注册为OSGi服务时指定。 例如， **datasource.name**。
      * **JDBC驱动程序类**:指定JDBC驱动程序的Java类名称。对于[!DNL MySQL]数据库，请指定&#x200B;**com.mysql.jdbc.Driver**。
      * **JDBC连接URI**:指定数据库的连接URL。对于在端口3306和模式weretail上运行的[!DNL MySQL]数据库，URL为：`jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用户名：** 数据库的用户名。需要启用JDBC驱动程序来建立与数据库的连接。
      * **密码：** 数据库的密码。需要启用JDBC驱动程序来建立与数据库的连接。
      * **借用时测试：** 启用“借 **[!UICONTROL 用时测]** 试”选项。
      * **回访时测试：** 启用回 **[!UICONTROL 访时]** 测试。
      * **验证查询：** 指定SQL SELECT查询以验证池中的连接。查询必须至少返回一行。 例如， **从customerdetails**&#x200B;中选择*。
      * **事务隔离**:将值设置为 **READ_COMMITTED**。

         将其他属性保留为默认的[值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)，然后点按&#x200B;**[!UICONTROL Save]**。

         将创建与以下类似的配置。

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## 步骤2:创建表单数据模型{#create-fdm}

AEM [!DNL Forms]提供直观的用户界面，用于[从配置的数据源创建表单数据模型](data-integration.md)。 您可以在表单数据模型中使用多个数据源。 对于我们的用例，我们将使用配置的[!DNL MySQL]数据源。

执行以下操作以创建表单数据模型：

1. 在AEM创作实例中，导航到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**。
1. 点按&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 表单数据模型]**。
1. 在创建表单数据模型对话框中，为表单数据模型指定&#x200B;**名称**。 例如，**customer-shipping-billing-details**。 点按&#x200B;**[!UICONTROL Next]**。
1. “选择数据源”屏幕列出了所有已配置的数据源。 选择&#x200B;**WeRetailMySQL**&#x200B;数据源，然后点按&#x200B;**[!UICONTROL 创建]**。

   ![数据源选择](assets/data-source-selection.png)

将创建&#x200B;**customer-shipping-billing-details**&#x200B;表单数据模型。

## 步骤3:配置表单数据模型{#config-fdm}

配置表单数据模型涉及：

* 添加数据模型对象和服务
* 为数据模型对象配置读写服务

执行以下操作以配置表单数据模型：

1. 在AEM创作实例上，导航至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**。 默认URL为[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 此处列出了您之前创建的&#x200B;**customer-shipping-billing-details**&#x200B;表单数据模型。 在编辑模式下将其打开。

   所选数据源&#x200B;**WeRetailMySQL**&#x200B;在表单数据模型中配置。

   ![default-fdm](assets/default-fdm.png)

1. 展开WeRailMySQL数据源树。 从&#x200B;**weretail** > **customerdetails**&#x200B;架构中选择以下数据模型对象和服务以形成数据模型：

   * **数据模型对象**:

      * id
      * name
      * shippingAddress
      * 城市
      * 状态
      * 邮政编码
   * **服务:**

      * get
      * 更新

   点按&#x200B;**添加选定项** ，将选定的数据模型对象和服务添加到表单数据模型。

   ![WeRetail架构](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC数据源的默认获取、更新和插入服务是随表单数据模型一起提供的。

1. 为数据模型对象配置读和写服务。

   1. 选择&#x200B;**customerdetails**&#x200B;数据模型对象，然后点按&#x200B;**[!UICONTROL 编辑属性]**。
   1. 从读取服务下拉列表中选择&#x200B;**[!UICONTROL get]**。 将自动添加&#x200B;**id**&#x200B;参数，该参数是customerdetails数据模型对象中的主键。 点按![aem_6_3_edit](assets/aem_6_3_edit.png)并按如下配置参数。

      ![读 — 默认](assets/read-default.png)

   1. 同样，选择&#x200B;**[!UICONTROL update]**&#x200B;作为写服务。 **customerdetails**&#x200B;对象将自动添加为参数。 参数的配置如下所示。

      ![write-default](assets/write-default.png)

      按如下方式添加和配置&#x200B;**id**&#x200B;参数。

      ![id-arg](assets/id-arg.png)

   1. 点按&#x200B;**[!UICONTROL 完成]**&#x200B;以保存数据模型对象属性。 然后，点按&#x200B;**[!UICONTROL Save]**&#x200B;以保存表单数据模型。

      将&#x200B;**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL update]**&#x200B;服务添加为数据模型对象的默认服务。

      ![数据模型 — 对象](assets/data-model-object.png)

1. 转到&#x200B;**[!UICONTROL Services]**&#x200B;选项卡，并配置&#x200B;**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL update]**&#x200B;服务。

   1. 选择&#x200B;**[!UICONTROL get]**&#x200B;服务，然后点按&#x200B;**[!UICONTROL 编辑属性]**。 此时将打开属性对话框。
   1. 在编辑属性对话框中指定以下内容：

      * **标题**:指定服务的标题。例如：检索送货地址。
      * **描述**:指定包含服务详细功能的描述。例如：

         此服务从[!DNL MySQL]数据库中检索送货地址和其他客户详细信息

      * **输出模型对象**:选择包含客户数据的架构。例如：

         customerdetail架构

      * **返回数组**:禁用返 **回** 数组选项。
      * **参数**:选择名为ID **的参数**。

      点按&#x200B;**[!UICONTROL 完成]**。已配置从MySQL数据库检索客户详细信息的服务。

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 选择&#x200B;**[!UICONTROL update]**&#x200B;服务，然后点按&#x200B;**[!UICONTROL 编辑属性]**。 此时将打开属性对话框。

   1. 在[!UICONTROL 编辑属性]对话框中指定以下内容：

      * **标题**:指定服务的标题。例如，更新发运地址。
      * **描述**:指定包含服务详细功能的描述。例如：

         此服务更新MySQL数据库中的送货地址和相关字段

      * **输入模型对象**:选择包含客户数据的架构。例如：

         customerdetail架构

      * **输出类型**:选择 **布尔值**。

      * **参数**:选择名为ID和 **** customerdetails **的参数**。
      点按&#x200B;**[!UICONTROL 完成]**。配置了&#x200B;**[!UICONTROL 更新]**&#x200B;服务以更新[!DNL MySQL]数据库中的客户详细信息。

      ![shiiping-address-update](assets/shiiping-address-update.png)



配置表单数据模型中的数据模型对象和服务。 您现在可以测试表单数据模型。

## 步骤4:测试表单数据模型{#test-fdm}

您可以测试数据模型对象和服务，以验证表单数据模型是否配置正确。

执行以下操作以运行测试：

1. 转到&#x200B;**[!UICONTROL Model]**&#x200B;选项卡，选择&#x200B;**customerdetails**&#x200B;数据模型对象，然后点按&#x200B;**[!UICONTROL 测试模型对象]**。
1. 在[!UICONTROL 测试模型/服务]窗口中，从&#x200B;**[!UICONTROL 选择模型/服务]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 读取模型对象]**。
1. 在&#x200B;**customerdetails**&#x200B;部分中，为配置的[!DNL MySQL]数据库中存在的&#x200B;**id**&#x200B;参数指定值，然后点按&#x200B;**[!UICONTROL 测试]**。

   将获取与指定ID关联的客户详细信息，并将其显示在&#x200B;**[!UICONTROL Output]**&#x200B;部分中，如下所示。

   ![测试读取模型](assets/test-read-model.png)

1. 同样，您也可以测试Write模型对象和服务。

   在以下示例中，更新服务成功更新了数据库中ID 7102715的地址详细信息。

   ![测试 — 写入模型](assets/test-write-model.png)

   现在，如果您再次测试id 7107215的读取模型服务，它将获取并显示更新后的客户详细信息，如下所示。

   ![已读更新](assets/read-updated.png)
