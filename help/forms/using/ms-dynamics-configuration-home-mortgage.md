---
title: 为We.Finance参考站点的住宅抵押工作流程配置Microsoft Dynamics 365
seo-title: Configure Microsoft Dynamics 365 for the home mortgage workflow of the We.Finance reference site
description: 了解如何通过We.Finance参考网站的住宅抵押工作流程的自适应表单来利用Microsoft® Dynamics 365服务
seo-description: Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# 为We.Finance参考站点的住宅抵押工作流程配置Microsoft Dynamics 365 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

了解如何通过We.Finance参考网站的住宅抵押工作流程的自适应表单来利用Microsoft® Dynamics 365服务

## 概述 {#overview}

Microsoft® Dynamics 365是一款客户关系管理(CRM)和企业资源规划(ERP)软件，为创建和管理客户帐户、联系人、商机、商机和案例提供企业解决方案。

AEM Forms提供了云服务以将Dynamics 365与 [Forms数据集成](/help/forms/using/data-integration.md) 模块。 在使用Microsoft® Dynamics方案的住房抵押贷款应用程序演练之前，您需要配置Microsoft® Dynamics 365以与We.Finance参考站点一起使用。

## 前提条件 {#prerequisites}

在开始设置和配置Dynamics 365之前，请确保：

* AEM 6.3 Forms Service Pack 1及更高版本
* Microsoft® Dynamics 365帐户
* 在Microsoft® Azure Active Directory中注册了Dynamics 365服务的应用程序
* 注册应用程序的客户端ID和客户端密钥

## 将家庭抵押贷款计算器与您的网站主页关联 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在创作实例中，转到以下页面：

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 向下滚动到住房抵押计算器。
1. 突出显示右列的（计算器）面板，然后点按以显示弹出菜单。 在弹出菜单中，点按配置。 此时会出现编辑AEM Forms容器对话框。

   ![计算器配置面板](assets/calculatorconfigurepanel.png)

1. 在编辑AEM Forms容器对话框中，浏览资产路径，然后在以下路径中选择家庭抵押贷款计算器，然后点按 **确认**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 点按&#x200B;**完成**。
1. 发布编辑的页面。

   >[!NOTE]
   >
   >计算器字段与FDM的绑定通过We.Finance参考站点包进行了预配置。 要查看绑定，您可以在创作模式下打开表单，并查看字段绑定引用。

1. 要创建自定义实体以存储住房抵押贷款申请的申请人记录，请将AEMFormsFSIRefsite_1_0.zip解决方案包导入您的Microsoft® Dynamics实例：

   1. 从以下位置下载包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 将解决方案包导入Microsoft® Dynamics实例。 在您的Microsoft® Dynamics实例中，转到 **设置** > **解决方案** 然后点按 **导入**.

1. 要设置在refsite中使用的用户联系详细信息，请将Sarah Rose Contact.CSV包导入您的Microsoft® Dynamics实例：

   1. 从以下位置下载包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 将包导入Microsoft® Dynamics实例。 在您的Microsoft® Dynamics实例中，转到 **销售** > **联系人** 然后点按 **导入数据**.
