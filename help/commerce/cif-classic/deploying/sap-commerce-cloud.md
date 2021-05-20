---
title: SAPCommerce Cloud
seo-title: SAPCommerce Cloud
description: 了解如何使用SAPCommerce Cloud部署电子商务。
seo-description: 了解如何使用SAPCommerce Cloud部署电子商务。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>本页包含指向hybris网站的链接。 对于某些页面，您需要一个帐户才能登录。

## 使用SAPCommerce Cloud部署eCommerce {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下过程使用以下演示目录来说明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署[必要的电子商务包](#packages-needed-for-ecommerce-with-hybris)将提供电子商务框架的完整功能，以及随hybris实施（包括演示目录）提供的电子商务功能的引用实施

此功能位于Geometrixx Outdoors网站的英语（美国）分支(`/content/geometrixx-outdoors/en_US`)下：

* [产品信息](#productinformationwithcolorvariants) （适用时包含颜色变体）

* [购物车内容概述](#shoppingcartcontentoverview)
* [客户登](#customersignup) 录 [和客户登录](#customersignin)

* [访问hybris管理控制台](#accesstothehybrismanagementconsole)

### 技术要求 — hybris Server {#technical-requirements-hybris-server}

eCommerce Integration Framework的hybris扩展已更新，以支持Hybris 5（默认），同时保持与[Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris)的向后兼容性。

>[!NOTE]
>
>* 支持版本18.11及更高版本。
>* 您需要Java 7才能运行[hybris 5服务器。](https://www.hybris.com/en/architecture-technology)
>* AEM扩展不支持hybris附加组件[Telco Accelerator](https://www.hybris.com/en/products/telecommunication)。

>



### 具有hybris {#packages-needed-for-ecommerce-with-hybris}的eCommerce所需的包

要安装电子商务功能，您需要：

* 您的hybris服务器
* AEM电子商务框架：

   * 这是标准AEM安装的一部分

* AEMGeometrixx全部包：

   * `cq-geometrixx-all-pkg`

* AEM hybris content packages:

   * `cq-hybris-content-6.3.2`
   * hybris特定API实施
   * `cq-geometrixx-hybris-content-6.3.2`
   * 用于说明hybris用法的引用实施(`geometrixx-outdoors/en_US`)

### 使用hybris {#installation-of-ecommerce-with-hybris}安装eCommerce

要安装完整的配置(使用演示目录、Geometrixx Outdoors)，基本步骤如下：

1. [安装AEM](/help/sites-deploying/deploy.md)。
1. 安装Geometrixx全部包

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用[包管理器](/help/sites-administering/package-manager.md)安装演示内容包：

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下载并构建您的hybris Server](#download-and-build-your-hybris-server)。
1. 在电子商务引擎中构建目录：

   1. [设置Geometrixx室外商店](#setup-the-geometrixx-outdoors-store)。

1. [](/help/sites-authoring/qg-page-authoring.md) 创作您在AEM中需要的任何补充页面。

>[!CAUTION]
>
>使用hybris服务器需要单独的hybris许可证。

>[!NOTE]
>
>对于开发人员[API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)也可供下载。

### Download and Build your hybris Server {#download-and-build-your-hybris-server}

此过程中的步骤将下载并构建hybris服务器。 它还将进行hybris和cq之间连接所需的初始配置。 然后，该扩展将可在默认设置下使用。

>[!CAUTION]
>
>不支持低于5.5.1的Hybris版本。

>[!NOTE]
>
>要完成此操作，您需要在系统上安装[Groovy](https://groovy-lang.org/)。

1. 从hybris下载网站下载&#x200B;**hybris Commerce Suite**&#x200B;分发。

   >[!CAUTION]
   >
   >您需要一个帐户（来自hybris）才能访问此内容。

1. 将分发文件解压缩到所需位置（称为&lt;hybris-root-directory>）。
1. 从命令行中，执行以下操作：

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

1. 将以下文件下载到提取的hybris分发的根文件夹中，

   ```
       <hybris-root-directory>
   ```


[获取文件](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >对于hybris 5.6.0及更高版本，请使用以下setup.groovy。

   5.6.0及更高版本

[获取文件](/help/sites-deploying/assets/setup-1.groovy)

1. 从命令行中，执行以下操作：

   * 更新hybris server的配置（扩展所需）
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
   >根据您的系统，完成其中几个步骤可能需要几分钟时间。

1. 在您的浏览器中，导航到&#x200B;**hybris管理控制台**，其地址为：

   [http://localhost:9002](http://localhost:9002)

1. 单击&#x200B;**初始化**，然后确认初始化操作（因为它将删除现有数据）。

   控制台上将显示进度， `FINISHED`表示完成。

   >[!NOTE]
   >
   >根据您的系统，完成此过程可能需要几分钟时间。

### 设置Geometrixx Outdoors存储{#setup-the-geometrixx-outdoors-store}

此过程将上载并配置演示存储 — 联机Geometrixx。

1. 启动hybris实例。 从命令行中，执行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的浏览器中，导航到&#x200B;**hybris管理控制台**，其地址为：

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   使用以下凭据：
   * 用户名：管理员
   * 密码：nimda

1. 在侧栏导航中，展开&#x200B;**System**&#x200B;和&#x200B;**Tools**。 然后，选择&#x200B;**Import**&#x200B;以打开&#x200B;**向导：CSV导入**&#x200B;窗口。
1. 在&#x200B;**Configuration**&#x200B;选项卡中， **Upload**&#x200B;以下&#x200B;**Import file**:

[获取文件](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 将&#x200B;**区域设置**&#x200B;设置为：

   `en_US - English (United States)`

1. 打开&#x200B;**Resources**&#x200B;选项卡。
1. **** 上载以 **下Media-Zip**:

[获取文件](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 单击&#x200B;**开始**&#x200B;以导入指定的文件。 **Result**&#x200B;选项卡将显示所有日志条目。

1. 单击&#x200B;**Done**&#x200B;以关闭导入窗口。

1. 在侧栏中，选择&#x200B;**System**，然后选择&#x200B;**工具**，然后选择&#x200B;**Import**。

1. **** 上载以下导 **入文件**:

[获取文件](/help/sites-deploying/assets/base-store.csv)

   对于hybris 5.7，请使用以下代码：

[获取文件](/help/sites-deploying/assets/base-store-5_7.csv)

1. 将&#x200B;**区域设置**&#x200B;设置为：

   `en_US - English (United States)`

1. 单击&#x200B;**开始**&#x200B;以导入指定的文件。 **Result**&#x200B;选项卡将显示所有日志条目。

1. 单击&#x200B;**Done**&#x200B;以关闭导入窗口。

1. 您现在可以使用产品座舱查看导入的目录和产品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
