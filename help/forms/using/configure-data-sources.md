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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---


# 配置数据源{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms数据集成允许您配置和连接到不同的数据源。 现成支持以下类型。 但是，只需少量自定义，您也可以集成其他数据源。

* 关系数据库- MySQL、Microsoft SQL Server、IBM DB2和Oracle RDBMS。
* AEM用户用户档案
* REST风格的Web服务
* 基于SOAP的Web服务
* OData服务

数据集成支持OAuth2.0、基本身份验证和API密钥现成身份验证类型，并允许为访问Web服务实现自定义身份验证。 在AEM cloud services中配置RESTful、基于SOAP和OData服务时，在AEM Web控制台中配置关系用户档案库的JDBC和AEM用户的连接器。

## 配置关系数据库 {#configure-relational-database}

您可以使用AEM Web Console配置配置关系数据库。 执行以下操作：

1. 转到AEM Web控制台，网址为https://server:host/system/console/configMgr。
1. 查找Apache **[!UICONTROL Sling Connection池化DataSource配置]** 。 点击以在编辑模式下打开配置。
1. 在配置对话框中，指定要配置的数据库的详细信息，如：

   * 数据源的名称
   * 存储数据源名称的数据源服务属性
   * JDBC驱动程序的Java类名
   * JDBC连接URI
   * 用于与JDBC驱动程序建立连接的用户名和密码

   >[!NOTE]
   >
   >请确保在配置数据源之前加密敏感信息，如口令。 要加密：
   >
   >    
   >    
   >    1. 转至https://&#39;[server]:[port]&#39;/system/console/crypto。
   >    1. 在纯文 **[!UICONTROL 本字段中]** ，指定要加密的口令或任何字符串，然后单击 **[!UICONTROL 保护]**。

   >    
   >    
   >    
   >加密的文本将显示在可在配置中指定的受保护文本字段中。

1. 启 **[!UICONTROL 用“借取时测]** 试”或“返回时测 **[!UICONTROL 试”]** ，以指定在从池借入或返回对象之前，分别验证对象。
1. 在“验证查询”字段中指 **[!UICONTROL 定SQL]** SELECT查询，以验证池中的连接。 查询必须至少返回一行。 根据您的数据库，指定以下任一选项：

   * 选择1（MySQL和MS SQL）
   * SELECT 1 from dual(Oracle)

1. 点按 **[!UICONTROL 保存]** ，以保存配置。

## 配置AEM用户用户档案 {#configure-aem-user-profile}

您可以使用AEM Web Console中的用户用户档案连接器配置配置AEM用户用户档案。 执行以下操作：

1. 转到AEM Web控制台[:][https://&#39;]server:port&#39;system/console/configMgr。
1. 查找AEM Forms **[!UICONTROL 用户档案集成——用户连接器配置]** ，然后点按以在编辑模式下打开配置。
1. 在“用户用户档案连接器配置”对话框中，可以添加、删除或更新用户用户档案属性。 指定的属性将可用于表单数据模型中。 使用以下格式指定用户用户档案属性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   示例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >上例 **中的** *表示CRXDE结构中AEM用户用户档案 `profile/empLocation/` 中节点下的所有节点。 表单数据模型可以访问节点下 `city` 任何节点 `string` 中的类型属 `profile/empLocation/` 性。 但是，包含指定属性的节点必须采用一致的结构。

1. 点按 **[!UICONTROL 保存]** ，以保存配置。

## 为云服务配置配置文件夹 {#cloud-folder}

>[!NOTE]
为RESTful、SOAP和OData服务配置云服务，需要配置云服务文件夹。

AEM中的所有云服务配置都整合在AEM存储 `/conf` 库的文件夹中。 默认情况下，该 `conf` 文件夹包 `global` 含可在其中创建云服务配置的文件夹。 但是，您需要手动为云配置启用它。 您还可以在中创建其他文 `conf` 件夹，以创建和组织云服务配置。

要为云服务配置配置文件夹，请执行以下操作：

1. 转到“工 **[!UICONTROL 具”>“常规”>“配置浏览器”]**。
1. 执行以下操作以启用云配置的全局文件夹，或跳过此步骤，为云服务配置创建和配置其他文件夹。

   1. 在配置浏 **[!UICONTROL 览器中]**，选择文 `global` 件夹并点 **[!UICONTROL 按属性]**。

   1. 在配置 **[!UICONTROL 属性对话框中]** ，启用 **[!UICONTROL 云配置]**。

   1. 点按 **[!UICONTROL 保存并关闭]** ，以保存配置并退出对话框。

1. 在配置浏 **[!UICONTROL 览器中]**，点 **[!UICONTROL 按创建]**。
1. 在创 **[!UICONTROL 建配置]** 对话框中，指定文件夹的标题并启 **[!UICONTROL 用云配置]**。
1. 点按 **[!UICONTROL 创建]** ，以创建为云服务配置启用的文件夹。

## 配置REST风格的Web服务 {#configure-restful-web-services}

REST风格的Web服务可在Swagger定 [义文件中使用](https://swagger.io/specification/) JSON格式的Swagger规范或YAML格式进行描述。 要在AEM cloud services中配置REST风格的Web服务，请确保文件系统上有Swagger文件或文件托管的URL。

执行以下操作以配置RESTful服务：

1. 转至“工 **[!UICONTROL 具”>“Cloud Service”>“数据源]**”。 点按以选择要在其中创建云配置的文件夹。

   有关 [创建和配置云服务配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder) ，请参阅配置云服务配置的文件夹。

1. 点按 **[!UICONTROL 创建]** ，打开创 **[!UICONTROL 建数据源配置向导]**。 指定配置的名称和标题（可选），从“ **[!UICONTROL 服务类型]** ” **[!UICONTROL 下拉菜单中选择RESTful Service]** ，选择浏览并选择配置的缩略图，然后点按 **[!UICONTROL 下一步]**。
1. 为RESTful服务指定以下详细信息：

   * 从“Swagger源”下拉菜单中选择“URL”或“文件”，然后相应地指定Swagger URL到Swagger定义文件或从本地文件系统上传Swagger文件。
   * 根据Swagger源输入，以下字段预填充了值：

      * 方案： REST API使用的传输协议。 在下拉列表中显示的方案类型数取决于在Swagger源中定义的方案。
      * 主机： 提供REST API的主机的域名或IP地址。 这是必填字段。
      * 基本路径： 所有API路径的URL前缀。 它是可选字段。\
         如有必要，请编辑这些字段的预填充值。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证、API密钥或自定义身份验证）以访问RESTful服务，并相应地提供身份验证详细信息。

   如果选择 **[!UICONTROL API密钥]** ，则指定API密钥的值。 API密钥可以作为请求头或查询参数发送。 从“位置”下拉列表 **[!UICONTROL 中]** ，选择其中一个选项，并相应地在“参数名称”字段中指定标题或 **[!UICONTROL 查询参数]** 的名称。

1. 点 **[!UICONTROL 按创建]** ，为RESTful服务创建云配置。

## 配置SOAP Web服务 {#configure-soap-web-services}

使用Web服务描述语言(WSDL) [规范描述基于SOAP的Web服务](https://www.w3.org/TR/wsdl)。 要在AEM cloud services中配置基于SOAP的Web服务，请确保您具有Web服务的WSDL URL，并执行以下操作：

1. 转至“工 **[!UICONTROL 具”>“Cloud Service”>“数据源]**”。 点按以选择要在其中创建云配置的文件夹。

   有关 [创建和配置云服务配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder) ，请参阅配置云服务配置的文件夹。

1. 点按 **[!UICONTROL 创建]** ，打开创 **[!UICONTROL 建数据源配置向导]**。 指定配置的名称和标题（可选），从 **[!UICONTROL 服务类型]****[!UICONTROL 下拉菜单中选择SOAP Web Service]** ，选择浏览并选择配置的缩略图，然后点 **[!UICONTROL 按下一步]**。
1. 为SOAP Web服务指定以下内容：

   * Web服务的WSDL URL。
   * 服务端点. 在此字段中指定一个值以覆盖WSDL中提及的服务端点。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证、自定义身份验证或X509令牌）以访问SOAP服务，并相应地提供身份验证的详细信息。

      如果选择X509令牌作为身份验证类型，请配置X509证书。 有关详细信息，请参 [阅设置证书](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)。
在“密钥别名”字段中指定X509证书的 **[!UICONTROL KeyStore别名]** 。 在“Time To Live（到实时时间）”字段中指定身份验证请求保持有效 **[!UICONTROL 之前的时间(秒]** )。 （可选）选择对邮件正文或时间戳标题进行签名，或者同时对两者进行签名。

1. 点 **[!UICONTROL 按创建]** ，为SOAP Web服务创建云配置。

## 配置OData服务 {#config-odata}

OData服务由其服务根URL标识。 要在AEM cloud services中配置OData服务，请确保您具有该服务的服务根URL，并执行以下操作：

>[!NOTE]
有关配置Microsoft Dynamics 365的分步指南（联机或内部），请参 [阅Microsoft Dynamics OData配置](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 转至“工 **[!UICONTROL 具”>“Cloud Service”>“数据源]**”。 点按以选择要在其中创建云配置的文件夹。

   有关 [创建和配置云服务配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder) ，请参阅配置云服务配置的文件夹。

1. 点按 **[!UICONTROL 创建]** ，打开创 **[!UICONTROL 建数据源配置向导]**。 指定配置的名称和标题（可选），从“ **[!UICONTROL 服务类型]** ” **[!UICONTROL 下拉菜单中选择OData Service]** ，选择浏览并选择配置的缩略图，然后点按 **[!UICONTROL 下一步]**。
1. 为OData服务指定以下详细信息：

   * 要配置的OData服务的服务根URL。
   * 选择身份验证类型（无、OAuth2.0、基本身份验证或自定义身份验证）以访问OData服务，并相应地提供身份验证的详细信息。

   >[!NOTE]
   必须选择OAuth 2.0身份验证类型，以使用OData端点作为服务根连接Microsoft Dynamics服务。

1. 点 **按创建** ，为OData服务创建云配置。

## 后续步骤 {#next-steps}

您已配置数据源。 接下来，您可以创建表单数据模型；如果已经创建了没有数据源的表单数据模型，则可以将其与刚刚配置的数据源关联。 有关详 [细信息，请参阅](/help/forms/using/create-form-data-models.md) “创建表单数据模型”。
