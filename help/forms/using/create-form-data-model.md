---
title: “教程：创建表单数据模型“”
seo-title: 创建表单数据模型教程
description: 创建表单数据模型
seo-description: 创建表单数据模型
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 1%

---


# Tutorial: Create form data model {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是创建第一个自 [适应表单系列中的一个步骤](../../forms/using/create-your-first-adaptive-form.md) 。 建议按照时间顺序按照系列来了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

AEM数 [!DNL Forms] 据集成模块允许您从不同的后端数据源(如AEM用户用户档案、RESTful Web服务、基于SOAP的Web服务、OData服务和关系型数据库)创建表单数据模型。 您可以在表单数据模型中配置数据模型对象和服务，并将其与自适应表单关联。 自适应表单字段绑定到数据模型对象属性。 这些服务使您能够预填自适应表单并将提交的表单数据写入数据模型对象。

有关表单数据集成和表单数据模型的更多信息，请参 [阅AEM Forms数据集成](../../forms/using/data-integration.md)。

本教程将指导您逐步准备、创建、配置表单数据模型并将其与自适应表单关联。 在本教程的结尾，您将能够：

* [将MySQL数据库配置为数据源](#config-database)
* [使用MySQL数据库创建表单数据模型](#create-fdm)
* [配置表单数据模型](#config-fdm)
* [测试表单数据模型](#test-fdm)

表单数据模型将类似于：

![form-data-model_l](assets/form-data-model_l.png)

**A.配置** 的数 **据源** B.数据 **源模式** C.Available Services **D.Data****** Model对象E.Configured Services

## 前提条件 {#prerequisites}

在开始之前，请确保您具有以下各项：

* [!DNL MySQL] 数据库，示例数据如创建第一个自适应表单的“ [先决条件”部分中所述](../../forms/using/create-your-first-adaptive-form.md)
* 如捆绑JDBC数 [!DNL MySQL] 据库驱动程序中 [所述，OSGi bundle for JDBC driver](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* 如第一个教程创建自适应表 [单中所述](/help/forms/using/create-adaptive-form.md)

## 第1步：将MySQL数据库配置为数据源 {#config-database}

您可以配置不同类型的数据源以创建表单数据模型。 对于本教程，我们将配置您配置并填充示例数据的MySQL数据库。 有关其他受支持数据源以及如何配置数据源的信息，请参 [阅AEM Forms数据集成](../../forms/using/data-integration.md)。

执行以下操作以配置数 [!DNL MySQL] 据库：

1. 将数据库的JDBC驱 [!DNL MySQL] 动程序作为OSGi捆绑包安装：

   1. 以管理员身 [!DNL Forms] 份登录到AEM作者实例，并转到AEM web控制台包。 默认URL为 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。

   1. 点按 **[!UICONTROL 安装／更新]**。 将显 [!UICONTROL 示“上传／安装包] ”对话框。

   1. 点按 **[!UICONTROL 选择文件]** ，浏览并选择JDBC驱动 [!DNL MySQL] 程序OSGi捆绑包。 选择 **[!UICONTROL 开始包]** 和刷 **[!UICONTROL 新包]**，然后点 **[!UICONTROL 按安装或更新]**。 确保“JDBC [!DNL Oracle Corporation's] 驱动程序” [!DNL MySQL] 处于活动状态。 已安装驱动程序。

1. 将数 [!DNL MySQL] 据库配置为数据源：

   1. 转到AEM Web控制台，网 [址为](https://localhost:4502/system/console/configMgr)https://localhost:4502/system/console/configMgr。
   1. 找到 **Apache Sling Connection池化DataSource配置** 。 点击以在编辑模式下打开配置。
   1. 在配置对话框中，指定以下详细信息：

      * **数据源名称：** 您可以指定任何名称。 例如，指定 **WeRetailMySQL**。
      * **DataSource服务属性名称**:指定包含DataSource名称的服务属性的名称。 将数据源实例注册为OSGi服务时指定它。 例如， **datasource.name**。
      * **JDBC驱动程序类**:指定JDBC驱动程序的Java类名称。 对于 [!DNL MySQL] 数据库， **请指定com.mysql.jdbc.Driver**。
      * **JDBC连接URI**:指定数据库的连接URL。 对于 [!DNL MySQL] 在端口3306和模式weretail上运行的数据库，URL为： `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用户名：** 数据库的用户名。 需要启用JDBC驱动程序以建立与数据库的连接。
      * **密码：** 数据库的口令。 需要启用JDBC驱动程序以建立与数据库的连接。
      * **借阅测试：** 启用“ **[!UICONTROL 借阅时测试]** ”选项。
      * **返回时测试：** 启用“ **[!UICONTROL 返回时测试]** ”选项。
      * **验证查询:** 指定SQL SELECT查询以验证池中的连接。 查询必须至少返回一行。 例如，从 **客户详细信息中选择***。
      * **事务隔离**:将该值设 **置为READ_COMMITTED**。

         保留其他属性并 [点按](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) “保 **[!UICONTROL 存”]**。

         将创建与以下配置类似的配置。

         ![关系型数据库——数据源——配置](assets/relational-database-data-source-configuration.png)

## Step 2: Create form data model {#create-fdm}

AEM提 [!DNL Forms] 供直观的用户界面， [用于从配置的数据源创建表](data-integration.md) 单数据模型。 您可以在表单数据模型中使用多个数据源。 对于我们的用例，我们将使用配置的 [!DNL MySQL] 数据源。

执行以下操作以创建表单数据模型：

1. 在AEM创作实例中，导航到 **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**。
1. Tap **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.
1. 在“创建表单数据模型”对话框中， **指定表** 单数据模型的名称。 例如， **customer-shipping-billing-details**。 点按 **[!UICONTROL 下一步]**。
1. 选择数据源屏幕列表所有已配置的数据源。 选择 **WeRetailMySQL** 数据源并点按 **[!UICONTROL 创建]**。

   ![数据源选择](assets/data-source-selection.png)

将创 **建客户——发运——结帐——详细** -表单数据模型。

## 第3步：配置表单数据模型 {#config-fdm}

配置表单数据模型涉及：

* 添加数据模型对象和服务
* 为数据模型对象配置读写服务

执行以下操作以配置表单数据模型：

1. 在AEM创作实例上，导航到 **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**。 默认URL为 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 此处 **列出您之前创建的** customer-shipping-billing-details表单数据模型。 在编辑模式下打开它。

   所选数据源 **WeRetailMySQL** 是在表单数据模型中配置的。

   ![default-fdm](assets/default-fdm.png)

1. 展开WeRailMySQL数据源树。 从Weretail > Customerdetails模式中选择以 **下数据模型** 对 **象和服务** ，以形成数据模型：

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

   点按 **添加选定** ，以将选定数据模型对象和服务添加到表单数据模型。

   ![WeRetail模式](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC数据源的默认get、update和insert服务是随附表单数据模型的现成提供。

1. 为数据模型对象配置读和写服务。

   1. 选择客 **户详细信** 息数据模型对象，然后点 **[!UICONTROL 按编辑属性]**。
   1. 从 **[!UICONTROL 读取]** 服务下拉菜单中选择获取。 将自 **动添加** id参数，该参数是customerdetails数据模型对象中的主键。 点 ![按aem_6_3_edit](assets/aem_6_3_edit.png) ，然后按如下配置参数。

      ![read-default](assets/read-default.png)

   1. 同样，选 **[!UICONTROL 择]** “更新”作为“写入服务”。 customerdetails **对象将** 作为参数自动添加。 参数配置如下。

      ![write-default](assets/write-default.png)

      按如下方式添 **加和** 配置id参数。

      ![id-arg](assets/id-arg.png)

   1. 点按 **[!UICONTROL 完成]** ，以保存数据模型对象属性。 然后，点按 **[!UICONTROL 保存]** ，以保存表单数据模型。

      get **[!UICONTROL 和]** update服 **** 务将作为数据模型对象的默认服务添加。

      ![数据模型对象](assets/data-model-object.png)

1. 转到“服 **[!UICONTROL 务]** ”选项卡， **[!UICONTROL 配置]** get **** 和update services。

   1. 选择get服 **[!UICONTROL 务]** ，然后点 **[!UICONTROL 按编辑属性]**。 属性对话框打开。
   1. 在“编辑属性”对话框中指定以下内容：

      * **标题**:指定服务的标题。 例如：检索送货地址。
      * **描述**:指定包含服务的详细功能的说明。 例如：

         此服务从数据库检索发运地址和其他客户详细 [!DNL MySQL] 信息

      * **输出模型对象**:选择包含客户数据的模式。 例如：

         客户详细信息模式

      * **返回数组**:禁用“ **返回数组** ”选项。
      * **参数**:选择名为 **ID的参数**。

      点按&#x200B;**[!UICONTROL 完成]**。已配置从MySQL数据库检索客户详细信息的服务。

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 选择更新 **[!UICONTROL 服务]** ，然后点 **[!UICONTROL 按编辑属性]**。 属性对话框打开。

   1. 在“编辑属性”对 [!UICONTROL 话框中指定] :

      * **标题**:指定服务的标题。 例如，更新发运地址。
      * **描述**:指定包含服务的详细功能的说明。 例如：

         此服务更新MySQL数据库中的送货地址和相关字段

      * **输入模型对象**:选择包含客户数据的模式。 例如：

         客户详细信息模式

      * **输出类型**:选择 **布尔**。

      * **参数**:选择名为ID **和** customerdetails **的参数**。
      点按&#x200B;**[!UICONTROL 完成]**。已配 **[!UICONTROL 置用于]** 更新数据库中客户详细信息 [!DNL MySQL] 的更新服务。

      ![shiiping-address-update](assets/shiiping-address-update.png)



配置表单数据模型中的数据模型对象和服务。 您现在可以测试表单数据模型。

## Step 4: Test form data model {#test-fdm}

您可以测试数据模型对象和服务，以验证表单数据模型配置是否正确。

执行以下操作以运行测试：

1. 转到“模 **[!UICONTROL 型]** ”选项卡，选择 **customerdetails** 数据模型对象，然 **[!UICONTROL 后点按测试模型对象]**。
1. 在“测 [!UICONTROL 试模型／服务] ”窗口中，从“选 **[!UICONTROL 择模型／服务”]** 下拉菜单中选择“读取模型对象 **** ”。
1. 在customerdetails **部分** ，为已配置数据库中 **存在的** id参数指定一个值， [!DNL MySQL] 然后点按 **[!UICONTROL 测试]**。

   将提取与指定ID关联的客户详细信息并在“输 **[!UICONTROL 出]** ”部分中显示，如下所示。

   ![测试读取模型](assets/test-read-model.png)

1. 同样，您也可以测试Write模型对象和服务。

   在以下示例中，更新服务成功更新数据库中id 7102715的地址详细信息。

   ![测试——写模型](assets/test-write-model.png)

   现在，如果您再次测试id 7107215的读取模型服务，它将获取并显示更新的客户详细信息，如下所示。

   ![已更新](assets/read-updated.png)
