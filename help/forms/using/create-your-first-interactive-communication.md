---
title: 教程——创建您的第一个交互式通信
seo-title: 创建您的第一个交互式通信
description: 了解如何创建您的第一个交互式通信。
seo-description: 了解如何创建您的第一个交互式通信。
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---


# 教程：创建您的第一个交互式通信{#tutorial-create-your-first-interactive-communication}

了解如何创建您的第一个交互式通信。

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

交互式通信集中化和管理安全、个性化和交互式通信(如业务通信、文档、声明、营销邮件、帐单和欢迎套件)的创建、组合和投放。 交互式通信可以使用两种渠道交付：印刷和Web。 打印渠道用于创建PDF和纸张通信，而Web渠道用于提供在线体验。

本教程提供了用于创建交互式通信的端到端框架。 本教程分为一个用例和多个指南。 每个指南都可以帮助您创建用作构件块的功能，以创建交互式通信。

下图说明了创建交互式通信所需的构件块。

![workflow](assets/workflow.gif)

在本教程的结尾，您将能够：

* 创建构建块(表单数据模型、文档片段和模板)
* 创建交互式通信
* 测试和发布交互式通信

## 用例{#use-case}

旅程开始了如何学习使用案例：

电信运营商通过电子邮件向客户发送月度账单。 帐单是交互式通信。 电子邮件包括：

* 受密码保护的PDF，在本教程中称为“打印渠道”。 它包括客户详细信息、帐单详细信息、费用汇总、支付帐单的便捷方式和使用详细信息。
* 指向Web版本的帐单的链接，在本教程中称为Web渠道。 除了PDF版中介绍的详细信息外，Web版还以图形形式呈现了使用细节和基于Adobe Target的个性化优惠。 Web版本还包含在线支付表单。 无需离开IC即可进行在线支付。
* 指向增值服务的链接，如在线存储、音乐订阅和点播视频订阅。

## 前提条件 {#prerequisites}

* 设置AEM作者实例。
* 在创作实例上安装[AEM Forms加载项](/help/forms/using/installing-configuring-aem-forms-osgi.md)
* 设置MYSQL数据库
* 从数据库提供程序获取JDBC数据库驱动程序（JAR文件）。 本教程中的示例基于MySQL数据库，并使用Oracle的[MySQL JDBC数据库驱动程序](https://dev.mysql.com/downloads/connector/j/5.1.html)。

## 第1步：规划交互式通信{#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

规划交互式通信的第一步是最终确定交互式通信的内容。 内容完成后，您必须对其进行分析，以确定创建交互式通信所需的各种资产类型。

**目标：**

使用以下数据输入模式为交互式通信创建解剖结构：

* 静态文本
* 表单数据模型
* 代理 UI
* 条件数据
* 图像

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/planning-interactive-communications.md)

## 第2步：创建表单数据模型{#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

表单数据模型允许您将交互式通信连接到不同的数据源。 例如，AEM用户用户档案、RESTful Web服务、基于SOAP的Web服务、OData服务和关系型数据库。 表单模式模型是业务实体和在连接数据源中可用服务的统一数据表示。 您可以将表单数据模型与交互式通信结合使用，从连接的数据源检索数据。 有关表单数据模型的详细信息，请参阅[AEM Forms数据集成](/help/forms/using/data-integration.md)。

**目标：**

* 将数据库实例（MySQL数据库）配置为数据源
* 使用MySQL数据库作为数据源创建表单数据模型
* 将数据模型对象添加到表单数据模型
* 为表单数据模型配置读写服务
* 在数据模型对象之间创建关联
* 视图自动生成的样本数据
* 编辑示例数据
* 测试表单数据模型和配置的服务以及测试数据

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-form-data-model0.md)

## 第3步：创建文档片段{#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

文档片段是用于组成交互通信的通信的可重用组件。 文档片段的类型有：文本、列表和条件。

**目标：**

* 创建文档片段
* 创建变量
* 创建和应用规则

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-document-fragments.md)

## 第4步：创建模板{#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

要创建交互式通信，必须在AEM服务器上提供用于打印和Web渠道的模板。

打印渠道的模板在AdobeForms设计器中创建并上传到AEM服务器。 然后，这些模板便可在创建交互式通信时使用。

Web渠道的模板是在AEM中创建的。 模板作者和管理员可以创建、编辑和启用Web模板。 创建并启用这些模板后，即可在创建交互式通信时使用。

**目标：**

* 使用AdobeForms设计器创建用于印刷渠道的XDP模板
* 将XDP模板上传到AEM Forms服务器
* 创建并启用Web渠道的模板

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-templates-print-web.md)

## 第5步：创建交互通信{#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

为Web版本创建表单数据模型、文档片段和模板等所有构建基块后，您就可以开始创建交互式通信。

交互式通信可通过两种渠道提供：印刷和Web。 您还可以创建交互式通信，将打印渠道作为主控。 Web渠道的打印为主控选项可确保Web渠道的内容、继承和数据绑定是从打印渠道派生的。

**目标：**

* 为打印渠道创建交互式通信
* 为Web渠道创建交互式通信
* 创建印刷和Web交互式通信，将印刷作为主控
* 在Web版交互通信中创建动态表
* 在Web版本的交互通信中创建图表
* 在Web版交互通信中创建超链接

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-interactive-communication0.md)

## 第6步：测试交互通信{#step-test-your-interactive-communication}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

创建交互式通信后，务必测试您在其中所做的每项更改。 测试交互式通信的每个字段非常繁琐。 AEM Forms公司提供一个SDK(Calvin SDK)，以在Web浏览器中自动测试交互式通信。

**目标：**

* 创建测试套件
* 创建测试用例
* 运行测试用例

## 第7步：发布您的交互式通信{#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

使用打印和Web渠道创建和测试交互式通信后，即可发布这些资源。 本教程中介绍的用例侧重于将这些资产与电子邮件客户端集成。 电子邮件客户端充当将交互式通信发送到多个电子邮件地址的桥梁。

**目标：**

* 将交互式通信与电子邮件客户端集成，以便能够向客户发送通信
* 将PDF文档作为附件包含(在打印渠道中创建的交互式通信)
* 包括指向Web版交互通信的链接

