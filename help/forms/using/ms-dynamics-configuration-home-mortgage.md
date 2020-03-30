---
title: 为We.Finance参考站点的家庭抵押工作流程配置Microsoft Dynamics 365
seo-title: 为We.Finance参考站点的家庭抵押工作流程配置Microsoft Dynamics 365
description: 了解如何通过We.Finance Reference站点的家庭抵押工作流程的自适应表单来利用Microsoft® Dynamics 365服务
seo-description: 了解如何通过We.Finance Reference站点的家庭抵押工作流程的自适应表单来利用Microsoft® Dynamics 365服务
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# 为We.Finance参考站点的家庭抵押工作流程配置Microsoft Dynamics 365 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

了解如何通过We.Finance Reference站点的家庭抵押工作流程的自适应表单来利用Microsoft® Dynamics 365服务

## 概述 {#overview}

Microsoft® Dynamics 365是一款客户关系管理(CRM)和企业资源规划(ERP)软件，它为创建和管理客户帐户、联系人、潜在客户、机会和案例提供企业解决方案。

AEM Forms提供了一项云服务，可将Dynamics 365与 [Forms数据集成模块集成](/help/forms/using/data-integration.md) 。 Microsoft® Dynamics [](/help/forms/using/finance-reference-site-walkthrough.md#home-mortgage-application-walkthrough-with-microsoft-dynamics) （家庭抵押）应用程序演练演示了当客户使用Microsoft® Dynamics for Forms Data Integration时，如何使用We.Finance参考站点申请贷款。 在使用Microsoft® Dynamics场景的“家庭抵押”应用程序演练之前，您需要配置Microsoft® Dynamics 365以与We.Finance参考站点一起使用。

## 前提条件 {#prerequisites}

在开始设置和配置Dynamics 365之前，请确保您拥有：

* [设置和配置AEM Forms引用站点](/help/forms/using/setup-reference-sites.md)。

* AEM 6.3 Forms Service Pack 1和更高版本
* Microsoft® Dynamics 365帐户
* 使用Microsoft® Azure Active Directory注册Dynamics 365服务的应用程序
* 注册应用程序的客户端ID和客户端机密

## 将家庭抵押计算器与您的网站主页关联 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在创作实例中，转到以下页面：

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 向下滚动到“家庭抵押计算器”。
1. 高亮显示右列（计算器）面板，然后点按以显示弹出菜单。 在弹出菜单中，点按配置。 此时将显示“编辑AEM表单容器”对话框。

   ![计算器配置面板](assets/calculatorconfigurepanel.png)

1. 在“编辑AEM表单容器”对话框中，浏览资产路径，然后在以下路径中选择家庭抵押计算器，然后点按确 **认**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 点按&#x200B;**完成**。
1. 发布已编辑的页面。

   >[!NOTE]
   >
   >计算器字段与FDM的绑定是通过We.Finance参考站点包预配置的。 要视图绑定，您可以在创作模式下打开表单并查看字段绑定引用。

1. 要创建自定义实体以存储家庭抵押申请的申请者记录，请将AEMFormsFSIRefsite_1_0.zip解决方案包导入您的Microsoft® Dynamics实例：

   1. 从以下位置下载包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 将解决方案包导入Microsoft® Dynamics实例。 在Microsoft® Dynamics实例中，转到“设置 **”>“解决方** 案 **”** ，然后点 **按导入**。

1. 要设置刷新中使用的用户联系信息，请将Sarah Rose Contact.CSV包导入您的Microsoft® Dynamics实例：

   1. 从以下位置下载包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 将包导入Microsoft® Dynamics实例。 在Microsoft® Dynamics实例中，转到“ **Sales** > **Contacts** ”，然后点按“ **Import Data**”。

