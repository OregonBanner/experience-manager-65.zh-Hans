---
title: 使用SAP部署电子商务Commerce Cloud
description: 了解如何使用SAPCommerce Cloud部署电子商务。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>本页包含指向hybris网站的链接。 对于某些页面，您需要一个帐户才能登录。

## 使用SAP部署eCommerceCommerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下过程使用以下演示目录来说明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署 [必要的电子商务包](#packages-needed-for-ecommerce-with-hybris) 将提供电子商务框架的完整功能，以及随hybris实施（包括演示目录）提供的电子商务功能的参考实施

此功能可在英语（美国）分支( `/content/geometrixx-outdoors/en_US`)Geometrixx Outdoors站点：

* [产品信息](#productinformationwithcolorvariants) （酌情包含颜色变体）

* [购物车内容概述](#shoppingcartcontentoverview)
* [客户注册](#customersignup) 和 [客户登录](#customersignin)

* [访问hybris管理控制台](#accesstothehybrismanagementconsole)

### 技术要求 — hybris Server {#technical-requirements-hybris-server}

eCommerce Integration Framework的hybris扩展已更新，以支持Hybris 5（默认），同时保持与的向后兼容性 [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* 支持版本18.11及更高版本。
>* 您需要Java 7才能运行 [hybris 5服务器。](https://www.hybris.com/en/architecture-technology)
>* hybris add-on， [电信加速器](https://www.hybris.com/en/products/telecommunication)，则AEM扩展不支持。
>


### 具有hybris的eCommerce需要的包 {#packages-needed-for-ecommerce-with-hybris}

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
   * 用于说明hybris用法的引用实施( `geometrixx-outdoors/en_US`)

### 使用hybris安装eCommerce {#installation-of-ecommerce-with-hybris}

要安装完整的配置(使用演示目录、Geometrixx Outdoors)，基本步骤如下：

1. [安装AEM](/help/sites-deploying/deploy.md).
1. 安装Geometrixx全部包

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用安装演示内容包 [包管理器](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下载并构建您的hybris Server](#download-and-build-your-hybris-server).
1. 在电子商务引擎中构建目录：

   1. [设置Geometrixx室外商店](#setup-the-geometrixx-outdoors-store).

1. [作者](/help/sites-authoring/qg-page-authoring.md) 您在AEM中需要的任何补充页面。

>[!CAUTION]
>
>使用hybris服务器需要单独的hybris许可证。

>[!NOTE]
>
>对于开发人员 [API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可供下载。

### Download and Build your hybris Server {#download-and-build-your-hybris-server}

此过程中的步骤将下载并构建hybris服务器。 它还将进行hybris和cq之间连接所需的初始配置。 然后，该扩展将可在默认设置下使用。

>[!CAUTION]
>
>不支持低于5.5.1的Hybris版本。

>[!NOTE]
>
>要完成此操作，您需要 [Groovy](https://groovy-lang.org/) 安装在系统上。

1. 下载 **hybris Commerce Suite** 分发（从hybris下载网站）。

   >[!CAUTION]
   >
   >您需要一个帐户（来自hybris）才能访问此内容。

1. 将分发文件解压缩到所需位置(称为 &lt;hybris-root-directory>)。
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
   >按 `Return` （如果需要）。

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

1. 在您的浏览器中，导航到 **hybris管理控制台** at:

   [http://localhost:9002](http://localhost:9002)

1. 单击 **初始化** 然后确认初始化操作（因为它将删除现有数据）。

   将在控制台中显示进度，其中 `FINISHED` 表示已完成。

   >[!NOTE]
   >
   >根据您的系统，完成此过程可能需要几分钟时间。

### 设置Geometrixx Outdoors存储 {#setup-the-geometrixx-outdoors-store}

此过程将上载并配置演示存储 — 联机Geometrixx。

1. 启动hybris实例。 从命令行中，执行以下操作：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在您的浏览器中，导航到 **hybris管理控制台** at:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   使用以下凭据：
   * 用户名：管理员
   * 密码：nimda

1. 在侧栏导航中，展开 **系统** 和 **工具**. 然后选择 **导入** 打开 **向导：CSV导入** 窗口。
1. 在 **配置** 选项卡， **上传** 以下 **导入文件**:

[获取文件](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 设置 **区域设置** 至：

   `en_US - English (United States)`

1. 打开 **资源** 选项卡。
1. **上传** 以下 **Media-Zip**:

[获取文件](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 单击 **开始** 导入指定文件。 的 **结果** 选项卡将显示所有日志条目。

1. 单击 **完成** 以关闭导入窗口。

1. 在侧栏中，选择 **系统**，则 **工具**，则 **导入**.

1. **上传** 以下 **导入文件**:

[获取文件](/help/sites-deploying/assets/base-store.csv)

   对于hybris 5.7，请使用以下代码：

[获取文件](/help/sites-deploying/assets/base-store-5_7.csv)

1. 设置 **区域设置** 至：

   `en_US - English (United States)`

1. 单击 **开始** 导入指定文件。 的 **结果** 选项卡将显示所有日志条目。

1. 单击 **完成** 以关闭导入窗口。

1. 您现在可以使用产品座舱查看导入的目录和产品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
