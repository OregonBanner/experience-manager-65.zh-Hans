---
title: 配置数据源
seo-title: 配置数据源
description: 了解如何配置不同类型的数据源并利用它们创建表单数据模型。
seo-description: 了解如何配置不同类型的数据源并利用它们创建表单数据模型。
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 配置数据源{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms Data Integration允许您配置并连接到不同的数据源。 现成支持以下类型。 但是，由于很少进行自定义，您还可以集成其他数据源。

* 关系数据库- MySQL、Microsoft SQL Server、IBM DB2和Oracle RDBMS。
* AEM用户用户档案
* RESTful Web服务
* 基于SOAP的Web服务
* OData服务

数据集成支持OAuth2.0、基本身份验证和API密钥现成身份验证类型，并允许为访问Web服务实施自定义身份验证。 在AEM Cloud Services中配置RESTful、基于SOAP和OData服务时，在AEM Web控制台中配置关系数据库的JDBC和AEM用户用户档案的连接器。

## 配置关系数据库 {#configure-relational-database}

您可以使用AEM Web Console配置配置关系型数据库。 执行以下操作：

1. 转到AEM Web控制台，网址为https://server:host/system/console/configMgr。
1. 查找 **[!UICONTROL Apache Sling Connection池化DataSource配置]** 。 点按以在编辑模式下打开配置。
1. 在配置对话框中，指定要配置的数据库的详细信息，如：

   * 数据源的名称
   * 存储数据源名称的数据源服务属性
   * JDBC驱动程序的Java类名
   * JDBC连接URI
   * 用于与JDBC驱动程序建立连接的用户名和密码
   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >在配置数据源之前，请确保加密密码等敏感信息。 要加密：
   >
   >    
   >    
   >    1. 转到https://&#39;[server]:[port]&#39;/system/console/crypto。
   >    1. 在纯文 **[!UICONTROL 本字段中]** ，指定要加密的口令或任何字符串，然后单击 **[!UICONTROL 保护]**。
   >    
   >    
   >    
   >加密的文本将显示在可在配置中指定的“受保护文本”字段中。

1. 启 **[!UICONTROL 用“借阅时测试]** ”或“退回时测试” **** ，以指定在从池借阅对象或从池返回对象之前，将验证这些对象。
1. 在验证查询字段中指定SQL SELECT **[!UICONTROL 查询]** ，以验证池中的连接。 查询必须至少返回一行。 根据您的数据库，指定以下任一选项：

   * 选择1（MySQL和MS SQL）
   * SELECT 1（来自Oracle）

1. 点按 **[!UICONTROL 保存]** ，以保存配置。

## 配置AEM用户用户档案 {#configure-aem-user-profile}

您可以使用AEM Web Console中的用户用户档案连接器配置来配置AEM用户用户档案。 执行以下操作：

1. 转到位于https://&#39;[server]:[port]&#39;system/console/configMgr的AEM Web控制台。
1. 查找 **[!UICONTROL AEM Forms数据集成——用户用户档案连接器配置]** ，然后点按以在编辑模式下打开配置。
1. 在“用户用户档案连接器配置”对话框中，可以添加、删除或更新用户用户档案属性。 指定的属性将可用于表单数据模型中。 使用以下格式指定用户用户档案属性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   示例:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`
   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >上例 **中的*** ，表示CRXDE结构中AEM用户用户档案中 `profile/empLocation/` 节点下的所有节点。 这意味着表单数据模型可以访问节点下 `city` 任何节点中 `string` 存在的类型属 `profile/empLocation/` 性。 但是，包含指定属性的节点必须遵循一致的结构。

1. 点按 **[!UICONTROL 保存]** ，以保存配置。

## 为云服务配置文件夹 {#cloud-folder}

**注意**:为RESTful、SOAP和OData服务配置云服务文件夹需要配置。

AEM中的所有云服务配置都整合在AEM存储库 `/conf` 的文件夹中。 默认情况下，该文 `conf` 件夹包含您可 `global` 以在其中创建云服务配置的文件夹。 但是，您需要为云配置手动启用它。 您还可以在中创建其他文件夹， `conf` 以创建和组织云服务配置。

要为云服务配置配置文件夹，请执行以下操作：

1. 转到工具> **[!UICONTROL 常规>配置浏览器]**。
1. 执行以下操作以启用云配置的全局文件夹，或跳过此步骤以为云服务配置创建和配置另一个文件夹。

   1. 在配置浏 **[!UICONTROL 览器中]**，选择文件 `global` 夹并点按 **[!UICONTROL 属性]**。

   1. 在配置 **[!UICONTROL 属性对话框中]** ，启用 **[!UICONTROL 云配置]**。

   1. 点按 **[!UICONTROL 保存并关闭]** ，以保存配置并退出对话框。

1. 在配置浏 **[!UICONTROL 览器中]**，点按 **[!UICONTROL 创建]**。
1. 在创建 **[!UICONTROL 配置对话框中]** ，指定文件夹的标题并启用 **[!UICONTROL 云配置]**。
1. 点按 **[!UICONTROL 创建]** ，以创建为云服务配置启用的文件夹。

## 配置RESTful Web服务 {#configure-restful-web-services}

RESTful Web服务可在Swagger定义文件中使 [用JSON格式的Swagger规范](https://swagger.io/specification/) 或YAML格式进行描述。 要在AEM云服务中配置RESTful Web服务，请确保您的文件系统中有Swagger文件或文件托管的URL。

执行以下操作以配置RESTful服务：

1. 转到工 **[!UICONTROL 具>云服务>数据源]**。 点按以选择要在其中创建云配置的文件夹。

   有关 [为云服务配置创建和配置文件夹的信息](../../forms/using/configure-data-sources.md#cloud-folder) ，请参阅为云服务配置配置配置文件夹。

1. 点按 **[!UICONTROL 创建]** ，打开创 **[!UICONTROL 建数据源配置向导]**。 指定配置的名称和标题（可选），从“服务类型”下拉菜单中选择 **[!UICONTROL RESTful Service]** ，选择浏览并选择配置的缩略图，然后点按“下 **[!UICONTROL 一步]******”。
1. 为RESTful服务指定以下详细信息：

   * 从“Swagger源”下拉菜单中选择“URL”或“文件”，然后相应地将Swagger URL指定到Swagger定义文件，或从本地文件系统上传Swagger文件。
   * 根据Swagger源输入，以下字段预填充了值：

      * 方案：REST API使用的传输协议。 在下拉列表中显示的方案类型数取决于在Swagger源中定义的方案。
      * 主持人：提供REST API的主机的域名或IP地址。 这是必填字段。
      * 基本路径：所有API路径的URL前缀。 它是一个可选字段。\
         如有必要，请编辑这些字段的预填充值。
   * 选择身份验证类型— 无、OAuth2.0、基本身份验证、API密钥或自定义身份验证— 访问RESTful服务，并相应地提供身份验证详细信息。
   如果选择 **[!UICONTROL API密钥]** ，则指定API密钥的值。 API密钥可以作为请求头或查询参数发送。 从“位置”下拉列表中选择 **[!UICONTROL 其中一个选项]** ，并相应地在“参数名称”字段中指定标题的名称或 **[!UICONTROL 查询参数]** 。

1. 点 **[!UICONTROL 击创建]** ，以创建RESTful服务的云配置。

## 配置SOAP Web服务 {#configure-soap-web-services}

使用Web服务描述语言(WSDL)规范描述基于SOAP [的Web服务](https://www.w3.org/TR/wsdl)。 要在AEM云服务中配置基于SOAP的Web服务，请确保您拥有Web服务的WSDL URL，并执行以下操作：

1. 转到工 **[!UICONTROL 具>云服务>数据源]**。 点按以选择要在其中创建云配置的文件夹。

   有关 [为云服务配置创建和配置文件夹的信息](../../forms/using/configure-data-sources.md#cloud-folder) ，请参阅为云服务配置配置配置文件夹。

1. 点按 **[!UICONTROL 创建]** ，打开创 **[!UICONTROL 建数据源配置向导]**。 指定配置的名称和标题（可选），从“服务类型”下拉菜单中选择 **[!UICONTROL SOAP Web Service]** ，选择浏览并选择配置的缩略图，然后点按“下 **[!UICONTROL 一步]******”。
1. 为SOAP Web服务指定以下内容：

   * Web服务的WSDL URL。
   * 服务端点. 在此字段中指定一个值以覆盖WSDL中提到的服务端点。
   * 选择身份验证类型— 无、OAuth2.0、基本身份验证或自定义身份验证— 访问SOAP服务，并相应地提供身份验证的详细信息。

1. 点 **[!UICONTROL 击创建]** ，以创建SOAP Web服务的云配置。

## 配置OData服务 {#config-odata}

OData服务由其服务根URL标识。 要在AEM云服务中配置OData服务，请确保您具有该服务的服务根URL，并执行以下操作：

>[!NOTE]
有关配置Microsoft Dynamics 365的分步指南（联机或内部），请参阅 [Microsoft Dynamics OData配置](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 转到工 **[!UICONTROL 具>云服务>数据源]**。 点按以选择要在其中创建云配置的文件夹。

   有关 [为云服务配置创建和配置文件夹的信息](../../forms/using/configure-data-sources.md#cloud-folder) ，请参阅为云服务配置配置配置文件夹。

1. 点按 **[!UICONTROL 创建]** ，打开创 **[!UICONTROL 建数据源配置向导]**。 指定配置的名称和标题（可选），从“服务类型”下拉列表中选择 **[!UICONTROL OData Service]** ，选择浏览并选择配置的缩略图，然后点按“下 **[!UICONTROL 一步”]******。
1. 为OData服务指定以下详细信息：

   * 要配置的OData服务的服务根URL。
   * 选择身份验证类型— 无、OAuth2.0、基本身份验证或自定义身份验证— 访问OData服务，并相应地提供身份验证的详细信息。
   >[!NOTE]
   必须选择OAuth 2.0身份验证类型才能使用OData端点作为服务根连接Microsoft Dynamics服务。

1. 点 **按创建** ，以创建OData服务的云配置。

## 后续步骤 {#next-steps}

您已配置数据源。 接下来，您可以创建表单数据模型；如果您已经创建了没有数据源的表单数据模型，则可以将其与刚刚配置的数据源关联。 有关详 [细信息，请参阅创建表单数据模型](/help/forms/using/create-form-data-models.md) 。
