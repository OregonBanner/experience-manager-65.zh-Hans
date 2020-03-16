---
title: SAP Commerce Cloud
seo-title: SAP Commerce Cloud
description: 了解如何使用SAP Commerce Cloud部署电子商务。
seo-description: 了解如何使用SAP Commerce Cloud部署电子商务。
uuid: 26ace49c-02d2-4b49-a959-e033def89bd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: c5dcc90a-05d2-4701-a625-2b655ad0b458
docset: aem65
pagetitle: Deploying eCommerce with hybris
translation-type: tm+mt
source-git-commit: 9e39868768d2fc70f587b18d36042e742d5fae45

---


# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>此页包含指向hybris网站的链接。 对于某些页面，您需要帐户才能登录。

## 使用SAP Commerce Cloud部署电子商务 {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>AEM 6.5的连接器未就绪。

>[!NOTE]
>
>以下过程使用以下演示目录来说明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署必 [要的eCommerce packages](#packages-needed-for-ecommerce-with-hybris) will provide the full functionality of the eCommerce framework, as reference implementation of eCommerce functionality as provided with a hybris implementation(industion a demonstration catalog)

此选项位于Geometrixx Outdoors站点的英语（美国）分支( `/content/geometrixx-outdoors/en_US`)下：

* [产品信息](#productinformationwithcolorvariants) （如果适用，带有颜色变体）

* [购物车内容概述](#shoppingcartcontentoverview)
* [客户注册](#customersignup)[和客户登录](#customersignin)

* [访问hybris管理控制台](#accesstothehybrismanagementconsole)

### Technical Requirements - hybris Server {#technical-requirements-hybris-server}

The hybris extension of the eCommerce Integration Framework has been updated to support Hybris 5(as default)while maintaining backward compatibility with Hybris 4 <!--[Hybris 4](/help/sites-developing/hybris.md#developing-for-hybris). -->

>[!NOTE]
>
>* 支持最多包含OCC版本2的hybris 6.4。
>* 您需要Java 7才能运行 [hybris 5服务器。](https://www.hybris.com/en/architecture-technology)
>* AEM extension不支持hybris add-on, the [Telco Accelerator](https://www.hybris.com/en/products/telecommunication), is not supported.
>



### Packages Neededed for eCommerce with hybris {#packages-needed-for-ecommerce-with-hybris}

要安装电子商务功能，您需要：

* Your hybris server, available from [hybris](#configureandbuildthehybrisserver).
* AEM eCommerce framework:

   * 这是标准AEM安装的一部分

* AEM Geometrixx-all包：

   * `cq-geometrixx-all-pkg`

* AEM hybris content packages:&quot;

   * 
       &quot;
 cq-hybris-content-6.3.2     
    
    &quot;
   
   * hybris-specific API实现
   * `cq-geometrixx-hybris-content-6.3.2`
   * 用于说明use of hybris()的引用实 `geometrixx-outdoors/en_US`现


### eCommerce with hybris安装 {#installation-of-ecommerce-with-hybris}

要安装完全正式的配置（使用演示目录，Geometrixx Outdoors），基本步骤为：

1. [安装AEM](/help/sites-deploying/deploy.md)。
1. 安装Geometrixx-all包

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用包管理器安装演示内容 [包](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下载并构建您的hybris Server](#download-and-build-your-hybris-server)。
1. 在电子商务引擎中构建目录：

   1. [设置Geometrixx Outdoor Store](#setup-the-geometrixx-outdoors-store)。

1. [在AEM中](/help/sites-authoring/page-authoring.md) ，创作您需要的任何补充页面。

>[!CAUTION]
>
>Use of the hybris server requires a separate hybris license.

>[!NOTE]
>
>对于开发 [人员](/help/sites-developing/ecommerce.md#api-documentation) ，也可下载API文档。

### Download and Build your hybris Server {#download-and-build-your-hybris-server}

此过程中的步骤将下载并构建hybris服务器。 它还将使hybris和cq之间的连接需要初始配置。 然后，该扩展将可用于默认设置。

>[!CAUTION]
>
>不支持早于5.5.1的Hybris版本。

>[!NOTE]
>
>要完成此操作，您需要在 [系统上安](https://groovy-lang.org/) 装Groovy。

1. 从hybris下载站点下载**hybris Commerce Suite **distribution。

   >[!CAUTION]
   >
   >You will need an account(from hybris)to access this.

1. 将分发文件解压缩到所需位置（称为&lt;hybris-root-directory>）。
1. 从命令行执行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >执行时：
   >
   >
   >`ant clean all`
   >
   >
   >按 `Return` 需要。

1. 将以下文件下载到您提取的hybris分发的根文件夹，

   ```
       <<i>hybris-root-directory</i>>
   ```

   : 

   [获取文件](assets/setup.groovy)

   >[!NOTE]
   >
   >对于hybris 5.6.0和更高版本，请使用以下setup.groovy。

   5.6.0及更高版本

   [获取文件](assets/setup-1.groovy)

1. 在命令行中，执行以下操作：

   * 更新hybris server的配置(as required by the extension)
   * 使用修改的配置重新构建hybris服务器
   * 启动服务器

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >根据您的系统，完成这些步骤中的几个可能需要几分钟。

1. 在您的浏览器中，导航到 **hybris管理控制台** :

   [https://localhost:9002](https://localhost:9002)

1. 单击 **初始化** ，然后确认初始化操作（因为它将删除现有数据）。

   进度将显示在控制台上，并指示 `FINISHED` 完成。

   >[!NOTE]
   >
   >根据您的系统，完成此操作可能需要几分钟。

### 设置Geometrixx Outdoors Store {#setup-the-geometrixx-outdoors-store}

此过程将上传和配置演示商店- Geometrixx Online。

1. 启动您的hybris实例。 从命令行执行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的浏览器中，导航到 **hybris管理控制台** :

   [https://localhost:9002/hmc/hybris](https://localhost:9002/hmc/hybris)

1. 从提要栏导航中，解释 **System** and **Tools**。 然后选择 **导入** ，以打开向 **导：“CSV导入** ”窗口。
1. 在“配 **置** ”选项卡 **中** ，上传以 **下导**&#x200B;入文件：

   [获取文件](assets/geometrixx-outdoors-export.csv)

1. 将“区 **域设置** ”设置为：

   `en_US - English (United States)`

1. Open the **Resources** tab.
1. **上传** 以下 **Media-Zip**:

   [获取文件](assets/geometrixx-outdoors-images.zip)

1. 单击 **开始** ，以导入指定的文件。 “结 **果** ”选项卡将显示所有日志条目。

1. 单击 **完成** ，关闭导入窗口。

1. 从提要栏中，依次 **选择System**、 **Tools**、 **Import**。

1. **上传** 以下导 **入文件**:

   [Get File](assets/base-store.csv)For hybris 5.7, please use the following:

   [获取文件](assets/base-store-5_7.csv)

1. 将“区 **域设置** ”设置为：

   `en_US - English (United States)`

1. 单击 **开始** ，以导入指定的文件。 “结 **果** ”选项卡将显示所有日志条目。

1. 单击 **完成** ，关闭导入窗口。

1. 您现在可以使用产品驾驶舱来查看导入的目录和产品：

   [https://localhost:9002/productcockpit](https://localhost:9002/productcockpit)

