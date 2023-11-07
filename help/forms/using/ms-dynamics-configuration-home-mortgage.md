---
title: 为We.Finance参考网站的住房抵押贷款工作流配置Microsoft Dynamics 365
description: 了解如何通过自适应表单为We.Finance参考网站的住房抵押贷款工作流使用Microsoft&reg； Dynamics 365服务。
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 为We.Finance参考网站的住房抵押贷款工作流配置Microsoft Dynamics 365 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

了解如何通过自适应表单为We.Finance参考网站的住房抵押贷款工作流使用Microsoft® Dynamics 365服务

## 概述 {#overview}

Microsoft® Dynamics 365是一款客户关系管理(CRM)和企业资源规划(ERP)软件，可提供用于创建和管理客户帐户、联系人、潜在客户、机会和案例的企业解决方案。

AEM Forms提供云服务以将Dynamics 365与 [Forms数据集成](/help/forms/using/data-integration.md) 模块。 在将“住房抵押贷款应用程序演练”与Microsoft® Dynamics结合使用之前，您需要配置Microsoft® Dynamics 365以与We.Finance参考网站一起使用。

## 前提条件 {#prerequisites}

在开始设置和配置Dynamics 365之前，请确保您具有：

* AEM 6.3 Forms Service Pack 1及更高版本
* Microsoft® Dynamics 365帐户
* 已向Microsoft® Azure Active Directory注册Dynamics 365服务应用程序
* 已注册应用程序的客户端ID和客户端密码

## 将住房抵押贷款计算器与您的网站主页链接 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在创作实例上，转到以下页面：

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 向下滚动到“住房抵押贷款计算器”。
1. 突出显示右列的（计算器）面板，然后点按以显示弹出菜单。 在弹出菜单中，点按配置。 此时会显示编辑AEM Forms容器对话框。

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. 在编辑AEM Forms容器对话框中，浏览资产路径并选择以下路径中的home-mortgage-calculator ，然后点击 **确认**：

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 点按 **完成**.
1. 发布已编辑的页面。

   >[!NOTE]
   >
   >计算器字段与FDM的绑定是通过We.Finance引用站点包预配置的。 要查看绑定，您可以在创作模式下打开表单并查看字段绑定引用。

1. 要创建用于存储房屋抵押贷款申请的申请人记录的自定义实体，请将AEMFormsFSIRefsite_1_0.zip解决方案包导入您的Microsoft® Dynamics实例：

   1. 从以下位置下载包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 将解决方案包导入Microsoft® Dynamics实例。 在Microsoft® Dynamics实例中，转到 **设置** > **解决方案** 然后点击 **导入**.

1. 要设置重新网站中使用的用户联系人详细信息，请将Sarah Rose Contact.CSV包导入您的Microsoft® Dynamics实例：

   1. 从以下位置下载包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 将程序包导入您的Microsoft® Dynamics实例。 在Microsoft® Dynamics实例中，转到 **销售** > **联系人** 然后点击 **导入数据**.
