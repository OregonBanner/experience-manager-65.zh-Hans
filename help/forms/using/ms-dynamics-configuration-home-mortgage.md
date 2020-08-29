---
title: 为We.Finance参考站点的家庭抵押工作流程配置Microsoft Dynamics 365
seo-title: 为We.Finance参考站点的家庭抵押工作流程配置Microsoft Dynamics 365
description: 了解如何通过自适应表单利用We.Finance Reference网站的家庭抵押工作流程的Microsoft® Dynamics 365服务
seo-description: 了解如何通过自适应表单利用We.Finance Reference网站的家庭抵押工作流程的Microsoft® Dynamics 365服务
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---


# 为We.Finance参考站点的家庭抵押工作流程配置Microsoft Dynamics 365 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

了解如何通过自适应表单利用We.Finance Reference网站的家庭抵押工作流程的Microsoft® Dynamics 365服务

## 概述 {#overview}

Microsoft® Dynamics 365是一款客户关系管理(CRM)和企业资源规划(ERP)软件，它为创建和管理客户帐户、联系人、潜在客户、机会和案例提供企业解决方案。

AEM Forms提供云服务，将Dynamics 365与 [Forms数据集成](/help/forms/using/data-integration.md) 模块集成 在使用Microsoft® Dynamics的“家庭抵押”应用程序演练之前，您需要配置Microsoft® Dynamics 365以与We.Finance参考站点一起使用。

## 前提条件 {#prerequisites}

在开始设置和配置Dynamics 365之前，请确保：

* AEM 6.3FormsService Pack 1及更高版本
* Microsoft® Dynamics 365帐户
* 已注册的Dynamics 365服务应用程序（使用Microsoft® Azure Active Directory）
* 已注册应用程序的客户端ID和客户端机密

## 将家庭抵押计算器与您的网站主页关联 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在创作实例中，转到以下页面：

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 向下滚动到“Home Mortgage Calculator（家庭抵押计算器）”。
1. 高亮显示右列（计算器）面板，然后点按以显示弹出菜单。 在弹出菜单中，点按配置。 出现“编辑AEM Forms容器”对话框。

   ![计算器配置面板](assets/calculatorconfigurepanel.png)

1. 在“编辑AEM Forms容器”对话框中，浏览资产路径，选择以下路径的住房抵押计算器，然后点按确 **认**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 点按&#x200B;**完成**。
1. 发布已编辑的页面。

   >[!NOTE]
   >
   >计算器字段与FDM的绑定是通过We.Finance参考站点包预配置的。 要视图绑定，您可以在创作模式下打开表单并查看字段绑定引用。

1. 要创建用于存储家庭抵押申请申请人记录的自定义实体，请将AEMFormsFSIRefsite_1_0.zip解决方案包导入您的Microsoft® Dynamics实例：

   1. 从以下位置下载包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 将解决方案包导入Microsoft® Dynamics实例。 在您的Microsoft® Dynamics实例中，转到“设 **置** ”>“ **解决方案** ”，然 **后点按**“导入”。

1. 要设置在refsite中使用的用户联系人详细信息，请将Sarah Rose Contact.CSV包导入您的Microsoft® Dynamics实例：

   1. 从以下位置下载包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 将包导入您的Microsoft® Dynamics实例。 在Microsoft® Dynamics实例中，转至“销 **售** ”>“ **联系人** ”，然 **后点按导入数据**。

