---
title: “教程：创建您的第一个自适应表单”
seo-title: “教程：创建您的第一个自适应表单”
description: 了解如何创建业务类、交互式和响应式表单。
seo-description: 了解如何创建业务类、交互式和响应式表单。
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
translation-type: tm+mt
source-git-commit: 43c04a8b2f1e2e7f2067cec055d8737dfc7b3e84
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---


# 教程：创建您的第一个自适应表单 {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 简介 {#introduction}

您是否希望获得可简化注册、提高参 **与度并缩短周转时间的适合移** 动设备的表单 **** ，自适应表单是您的理想选择。 自适应表单提供移动、自动化和分析友好的表单体验。 您可以轻松构建具有响应性和交互性的表单，使用自动化流程减少管理和重复性任务，使用数据分析来改进和个性化客户对表单的体验。

本教程提供了用于创建自适应表单的端到端框架。 本教程分为一个用例和多个指南。 每个指南都可以帮助您学习并向在本教程中创建的自适应表单添加新功能。 您在每个指南后面都有一个有效的自适应表单。 有自适应表单创建指南。 随后的指南将很快推出。 在本教程的结尾，您将能够：

* 创建自适应表单和表单数据模型。
* 设置自适应表单的样式。
* 使用自适应表单规则编辑器构建业务规则。
* 测试和发布自适应表单。

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

旅程开始了如何学习使用案例：

网站为不同的客户优惠各种产品。 客户浏览门户、选择和订购产品。 每个客户都创建一个帐户并提供送货和帐单地址。 现有客户萨拉·罗斯希望将她的送货地址添加到网站。 该网站提供在线表单以添加和更新送货地址。

该网站在Adobe Experience Manager(AEM)上运行，并使用AEM [!DNL Forms] 进行数据捕获和处理。 地址添加和更新表单是一种自适应表单。 网站将客户详细信息存储在数据库中。 他们使用地址添加和更新表单来检索和显示可用地址。 他们还使用自适应表单接受更新的和新的地址。

### 先决条件 {#prerequisite}

* 设置AEM作者实例。
* 在 [创作实例上安装](../../forms/using/installing-configuring-aem-forms-osgi.md) AEM Forms加载项。
* 从数据库提供程序获取JDBC数据库驱动程序（JAR文件）。 本教程中的示例基于数 [!DNL MySQL] 据库，并使 [!DNL Oracle's] 用 [MySQL JDBC数据库驱动程序](https://dev.mysql.com/downloads/connector/j/5.1.html)。

* 使用下面显示的字段设置包含客户数据的数据库。 数据库不是创建自适应表单的必备工具。 本教程使用数据库来显示AEM的表单数据模型和持久性功 [!DNL Forms]能。

![自适应格式数据](assets/adaptiveformdata.png)

## 第1步：创建自适应表单 {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

自适应表单是新一代、引人入胜、响应迅速、动态且自适应的表单。 利用自适应表单，您可以提供个性化且有针对性的体验。 AEM [!DNL Forms] 提供拖放式WYSIWYG编辑器以创建自适应表单。 有关自适应表单的详细信息，请参 [阅创作自适应表单的简介](../../forms/using/introduction-forms-authoring.md)。

目标：

* 创建允许客户添加送货地址的自适应表单
* 自适应表单的布局字段，用于显示和接受客户的信息
* 创建提交操作以发送包含表单内容的电子邮件
* 预览并提交自适应表单

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Step 2: Create Form Data Model {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

表单数据模型允许将自适应表单连接到不同的数据源。 例如，AEM用户用户档案、RESTful Web服务、基于SOAP的Web服务、OData服务和关系型数据库。 表单数据模型是业务实体和服务在互联数据源中的统一数据表示模式。 您可以将表单数据模型与自适应表单一起使用，以检索、更新、删除数据并将数据添加到连接的数据源。

目标：

* 将网站的数据库实例(数[!DNL MySQL] 据库)配置为数据源
* 使用数据库作为数 [!DNL MySQL] 据源创建表单数据模型
* 将数据模型对象添加到表单数据模型
* 为表单数据模型配置读写服务
* 测试表单数据模型和配置的服务以及测试数据

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 第3步：将规则应用于自适应表单字段 {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

自适应表单为自适应表单对象提供了一个编写规则的编辑器。 这些规则根据预设条件、用户输入和用户对表单的操作定义对表单对象触发的操作。 它有助于确保准确性并加快表单填写体验。

目标：

* 创建规则并将其应用于自适应表单字段
* 使用规则触发表单数据模型服务以将数据更新到数据库

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 第4步：设置自适应表单的样式 {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

自适应表单提供主题 [和编辑](../../forms/using/themes.md) 器，用于为自适应表单创建主题。 主题包含组件和面板的样式详细信息，您可以以不同的形式重复使用主题。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。 将主题应用于表单时，指定的样式会反映在表单的相应组件上。 自适应表单还支持特定于表单的样式的串联样式。

目标：

* 将开箱即用主题应用于自适应表单
* 使用主题编辑器创建自适应表单的主题
* 在自定义主题中使用Web字体

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 第5步：测试自适应表单 {#step-test-your-adaptive-form}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

自适应表单是客户互动不可或缺的一部分。 测试自适应表单时，每次更改都很重要。 测试表单的每个字段很繁琐。 AEM [!DNL Forms] 提供SDK(Calvin SDK)以自动测试自适应表单。 Calvin允许您在Web浏览器中自动测试自适应表单。

目标：

* 为自适应表单创建测试套件
* 为自适应表单创建测试用例
* 运行测试用例

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](testing-your-adaptive-form.md)

## 第6步：发布自适应表单 {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

您可以将自适应表单发布为独立表单（单页应用程序），包括在AEM [Sites页面中](/help/forms/using/embed-adaptive-form-aem-sites.md)，或使用Forms门户 [!DNL Site] 在AEM上 [发布列表](../../forms/using/introduction-publishing-forms.md)。

目标：

* 将自适应表单发布为AEM页面
* 将自适应表单嵌入AEM页 [!DNL Sites] 面
* 将自适应表单嵌入到外部网页(AEM外部托管的非AEM网页)

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)