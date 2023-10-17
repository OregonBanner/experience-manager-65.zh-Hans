---
title: 使用SAPCommerce Cloud部署电子商务
description: 了解如何使用SAPCommerce Cloud部署Adobe Experience Manager eCommerce。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# SAPCOMMERCE CLOUD{#sap-commerce-cloud}

>[!NOTE]
>
>本页包含指向hybris网站的链接。 对于某些页面，您需要帐户才能登录。

## 使用SAPCommerce Cloud部署eCommerce {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下过程使用下列演示目录来说明部署：
>
>`Geometrixx Outdoors Site English (US)`

部署 [必要的电子商务包](#packages-needed-for-ecommerce-with-hybris) 提供电子商务框架的完整功能，以及随hybris实施提供的电子商务功能的参考实施（包括演示目录）

可在英语（美国）分支( `/content/geometrixx-outdoors/en_US`Geometrixx Outdoors )，其网址为：

* [产品信息](#productinformationwithcolorvariants) （在适当的时候使用颜色变体）

* [购物车内容概述](#shoppingcartcontentoverview)
* [客户注册](#customersignup) 和 [客户登录](#customersignin)

* [访问hybris管理控制台](#accesstothehybrismanagementconsole)

### 技术要求 — hybris服务器 {#technical-requirements-hybris-server}

电子商务集成框架的hybris扩展已更新，以支持Hybris 5（作为默认），同时保持与的向后兼容性 [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* 支持版本18.11及更高版本。
>* 您需要Java™ 7来运行 [hybris 5服务器。](https://www.sap.com/products/crm.html)
* hybris附加模块 [电信加速器](https://www.sap.com/products/crm.html)AEM扩展不支持。
>

### 带有hybris的电子商务所需的包 {#packages-needed-for-ecommerce-with-hybris}

要安装电子商务功能，您需要：

* 您的hybris服务器
* AEM电子商务框架：

   * 这是标准AEM安装的一部分

* AEM全Geometrixx包：

   * `cq-geometrixx-all-pkg`

* AEM hybris内容包：

   * `cq-hybris-content-6.3.2`
   * 特定于hybris的API实施
   * `cq-geometrixx-hybris-content-6.3.2`
   * 用于说明使用hybris ( `geometrixx-outdoors/en_US`)

### 使用hybris安装电子商务 {#installation-of-ecommerce-with-hybris}

要安装完整的配置(使用演示目录、Geometrixx Outdoors)，基本步骤如下：

1. [安装AEM](/help/sites-deploying/deploy.md).
1. 安装全Geometrixx包

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. 使用安装演示内容包 [包管理器](/help/sites-administering/package-manager.md)：

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [下载并构建hybris服务器](#download-and-build-your-hybris-server).
1. 在电子商务引擎中构建目录：

   1. [设置Geometrixx户外商店](#setup-the-geometrixx-outdoors-store).

1. [作者](/help/sites-authoring/qg-page-authoring.md) AEM中所需的任何辅助页面。

>[!CAUTION]
>
使用hybris服务器需要单独的hybris许可证。

>[!NOTE]
>
对于开发人员， [API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可供下载。

### 下载并构建hybris服务器 {#download-and-build-your-hybris-server}

此过程中的步骤下载并构建hybris服务器。 它还创建了hybris和cq之间的连接所需的初始配置。 随后，该扩展将可与默认设置一起使用。

>[!CAUTION]
>
不支持5.5.1之前的Hybris版本。

>[!NOTE]
>
要完成此操作，您需要 [Groovy](https://groovy-lang.org/) 安装在系统上。

1. 下载 **hybris Commerce Suite** 从hybris下载站点分发。

   >[!CAUTION]
   >
   您需要一个帐户（来自hybris）才能访问此。

1. 将分发文件解压缩到所需的位置(称为 &lt;hybris-root-directory>)。
1. 在命令行中，执行以下命令：

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   运行时：
   >
   `ant clean all`
   >
   按 `Return` 需要时。

1. 将以下文件下载到解压缩的hybris分发的根文件夹，

   ```
       <hybris-root-directory>
   ```


[获取文件](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   对于hybris 5.6.0及更高版本，请使用以下setup.groovy。

   5.6.0及更高版本

[获取文件](/help/sites-deploying/assets/setup-1.groovy)

1. 从命令行中，执行以下命令到：

   * 更新hybris服务器的配置（根据扩展的要求）
   * 使用修改后的配置重新生成hybris服务器
   * 启动服务器

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   根据您的系统，完成其中的几个步骤可能需要花费几分钟时间。

1. 在浏览器中，导航到 **hybris管理控制台** 在：

   [http://localhost:9002](http://localhost:9002)

1. 单击 **初始化** 然后确认初始化操作（因为它删除现有数据）。

   进度显示在控制台上，带有 `FINISHED` 指示完成。

   >[!NOTE]
   >
   根据您的系统，这可能需要几分钟才能完成。

### 设置Geometrixx Outdoors商店 {#setup-the-geometrixx-outdoors-store}

此过程上载并配置演示商店 — 联机Geometrixx。

1. 启动您的hybris实例。 在命令行中，执行以下命令：

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. 在浏览器中，导航到 **hybris管理控制台** 在：

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   使用这些凭据：
   * 用户名：管理员
   * 密码：nimda

1. 在侧栏导航中，展开 **系统** 和 **工具**. 然后选择 **导入** 以打开 **向导：CSV导入** 窗口。
1. 在 **配置** 选项卡， **上传** 以下内容 **导入文件**：

[获取文件](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 设置 **区域设置** 至：

   `en_US - English (United States)`

1. 打开 **资源** 选项卡。
1. **上传** 以下内容 **Media-Zip**：

[获取文件](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 单击 **开始** 以导入指定的文件。 此 **结果** 选项卡显示任何日志条目。

1. 单击 **完成** 以关闭导入窗口。

1. 在侧栏中，选择 **系统**，则 **工具**，则 **导入**.

1. **上传** 以下内容 **导入文件**：

[获取文件](/help/sites-deploying/assets/base-store.csv)

   对于hybris 5.7，请使用以下代码：

[获取文件](/help/sites-deploying/assets/base-store-5_7.csv)

1. 设置 **区域设置** 至：

   `en_US - English (United States)`

1. 单击 **开始** 以导入指定的文件。 此 **结果** 选项卡显示任何日志条目。

1. 单击 **完成** 以关闭导入窗口。

1. 您现在可以使用产品驾驶舱查看导入的目录和产品：

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
