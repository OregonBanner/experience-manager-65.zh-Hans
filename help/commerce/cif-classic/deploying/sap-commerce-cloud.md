---
title: SAPCommerce Cloud
seo-title: SAPCommerce Cloud
description: 了解如何使用SAPCommerce Cloud部署电子商务。
seo-description: 了解如何使用SAPCommerce Cloud部署电子商务。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>This page contains links to the hybris website. 对于某些页面，您需要一个帐户才能登录。

## 使用SAPCommerce Cloud{#deploying-ecommerce-with-sap-commerce-cloud}部署电子商务

>[!NOTE]
>
>以下过程使用以下演示目录来说明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署[必需的eCommerce packages](#packages-needed-for-ecommerce-with-hybris)将提供eCommerce framework的完整功能，以及随hybris implementation(including a demonstration catalog)一起提供的eCommerce功能的引用实现

它位于Geometrixx Outdoors站点的英语（美国）分支(`/content/geometrixx-outdoors/en_US`)下：

* [产品信息](#productinformationwithcolorvariants) （如果适用，请提供颜色变体）

* [购物车内容概述](#shoppingcartcontentoverview)
* [客户登](#customersignup) 录 [和客户登录](#customersignin)

* [Access to the hybris management console](#accesstothehybrismanagementconsole)

### Technical Requirements - hybris Server {#technical-requirements-hybris-server}

The hybris extension of the eCommerce Integration Framework has been updated to support Hybris 5(as default), while maintaining backward compatibility with [ Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* 支持版本18.11及更高版本。
>* 您需要Java 7才能运行[hybris 5服务器。](https://www.hybris.com/en/architecture-technology)
>* AEM extension不支持hybris add-on， the [Telco Accelerator](https://www.hybris.com/en/products/telecommunication)。

>



### Packages Neededed for eCommerce with hybris {#packages-needed-for-ecommerce-with-hybris}

要安装电子商务功能，您需要：

* Your hybris server
* AEM eCommerce framework:

   * 这是标准AEM安装的一部分

* AEM Geometrixx-all包：

   * `cq-geometrixx-all-pkg`

* AEM hybris content packages:

   * `cq-hybris-content-6.3.2`
   * hybris-specific API实现
   * `cq-geometrixx-hybris-content-6.3.2`
   * a reference implementation to illustrate use of hybris(`geometrixx-outdoors/en_US`)

### Installation of eCommerce with hybris {#installation-of-ecommerce-with-hybris}

要安装完整的配置(使用演示目录，Geometrixx Outdoors)，基本步骤如下：

1. [安装AEM](/help/sites-deploying/deploy.md)。
1. 安装Geometrixx全包

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用[包管理器](/help/sites-administering/package-manager.md)安装演示内容包：

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Download and build your hybris Server](#download-and-build-your-hybris-server).
1. 在电子商务引擎中构建目录：

   1. [设置Geometrixx室外商店](#setup-the-geometrixx-outdoors-store)。

1. [在](/help/sites-authoring/qg-page-authoring.md) AEM中创作所需的任何补充页面。

>[!CAUTION]
>
>Use of the hybris server requires a separate hybris license.

>[!NOTE]
>
>对于开发人员[API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)也可下载。

### Download and Build your hybris Server {#download-and-build-your-hybris-server}

此过程中的步骤将下载并构建hybris server。 It will also make the initial configurations required for the connections between hybris and cq. 然后，该扩展将可用于默认设置。

>[!CAUTION]
>
>不支持早于5.5.1的Hybris版本。

>[!NOTE]
>
>要完成此操作，您需要在系统上安装[Groovy](https://groovy-lang.org/)。

1. 从hybris下载站点下载&#x200B;**hybris Commerce Suite** distribution。

   >[!CAUTION]
   >
   >You will need an account(from hybris)to access this.

1. 将分发文件解压缩到所需位置（称为&lt;hybris-root-directory>）。
1. 在命令行中，执行以下操作：

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
   >`ant clean all`
   >
   >根据需要按`Return`。

1. 将以下文件下载到您提取的hybris分发的根文件夹，

   ```
       <hybris-root-directory>
   ```


   [获取文件](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >For hybris 5.6.0 and later， please use the following setup.groovy.

   5.6.0及更高版本

   [获取文件](/help/sites-deploying/assets/setup-1.groovy)

1. 在命令行中，执行以下操作：

   * update of the hybris server(as required by the extension)
   * 重新生成hybris server with modified configuration
   * 开始服务器

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >根据您的系统，完成其中几个步骤可能需要几分钟。

1. 在您的浏览器中，导航到&#x200B;**hybris administration console**，网址为：

   [http://localhost:9002](http://localhost:9002)

1. 单击&#x200B;**初始化**，然后确认初始化操作（因为它将删除现有数据）。

   进度将显示在控制台上，`FINISHED`表示完成。

   >[!NOTE]
   >
   >根据您的系统，可能需要几分钟才能完成此操作。

### 设置Geometrixx Outdoors存储{#setup-the-geometrixx-outdoors-store}

此过程将上载并配置演示存储 — 在线Geometrixx。

1. 开始 your hybris instance. 在命令行中，执行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的浏览器中，导航到&#x200B;**hybris management console**，网址为：

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   使用以下凭据：
   * 用户名：管理
   * 密码：nimda

1. 在侧栏导航中，展开&#x200B;**System**&#x200B;和&#x200B;**Tools**。 然后选择&#x200B;**导入**&#x200B;以打开&#x200B;**向导：CSV Import**&#x200B;窗口。
1. 在&#x200B;**配置**&#x200B;选项卡中，**上载**&#x200B;以下&#x200B;**导入文件**:

   [获取文件](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 将&#x200B;**区域设置**&#x200B;设置为：

   `en_US - English (United States)`

1. 打开&#x200B;**资源**&#x200B;选项卡。
1. **上** 载以 **下Media-Zip**:

   [获取文件](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 单击&#x200B;**开始**&#x200B;以导入指定的文件。 **Result**&#x200B;选项卡将显示所有日志条目。

1. 单击&#x200B;**完成**&#x200B;以关闭导入窗口。

1. 在提要栏中，选择&#x200B;**System**，然后选择&#x200B;**Tools**，然后选择&#x200B;**Import**。

1. **上** 载以下 **导入文件**:

   [获取文件](/help/sites-deploying/assets/base-store.csv)

   For hybris 5.7, please use the following:

   [获取文件](/help/sites-deploying/assets/base-store-5_7.csv)

1. 将&#x200B;**区域设置**&#x200B;设置为：

   `en_US - English (United States)`

1. 单击&#x200B;**开始**&#x200B;以导入指定的文件。 **Result**&#x200B;选项卡将显示所有日志条目。

1. 单击&#x200B;**完成**&#x200B;以关闭导入窗口。

1. 您现在可以使用产品驾驶舱来视图导入的目录和产品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
