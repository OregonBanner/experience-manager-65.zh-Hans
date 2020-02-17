---
title: 员工自助服务参考站点演练
seo-title: 员工自助服务
description: AEM Forms参考站点展示组织如何利用AEM Forms功能实施员工招聘和自助工作流。
seo-description: AEM Forms参考站点展示组织如何利用AEM Forms功能实施员工招聘和自助工作流。
uuid: 6710f7c4-352c-4b07-91d8-7ad97d448559
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d64189a4-c7c3-427e-9a60-8d063373465f
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 员工自助服务参考站点演练{#employee-self-service-reference-site-walkthrough}

## 入门项目 {#prerequisite}

按照设置和配置AEM Forms引用站 [点中的说明设置引用站点](../../forms/using/setup-reference-sites.md)。

## 概述 {#overview}

员工自助服务系统通常托管在公司的内部网上，它使员工能够访问从他们的办公桌上可以使用的大量信息和服务。 它允许并给予员工完全的控制权，以执行诸如访问他们的雇佣细节、申请休假和提交费用报告等操作。 另一方面，它帮助组织提高流程效率并削减成本，同时保持员工知情和参与。

员工自助服务参考站点展示了如何利用AEM Forms在您的组织中实施员工自助服务系统。

>[!NOTE]
>
>员工自助服务演练中使用的示例、图像和说明使用We.Finance参考站点。

## 利益冲突问卷演练 {#conflict-of-interest-questionnaire-walkthrough}

组织不时要求其员工提交利益冲突调查表，以识别可能与其组织发生冲突的员工的外部活动或个人关系。

Sarah组织的合规部门已要求员工提交利益冲突调查表。

### Sarah提交利益冲突调查表 {#sarah-submits-the-conflict-of-interest-questionnaire}

Sarah转到其组织的门户，登录并单击“员工”以访问员工仪表板。 她在员工仪表板上查找利益冲突调查表并单击“应 **[!UICONTROL 用”]**。

![we-finance-home](assets/we-finance-home.png)

组织门户

![employee-dashboard](assets/employee-dashboard.png)

员工控制板

Sarah使用“下一步”按钮导航表单并阅读“简介”和“定义”部分。 她回答“问题”部分中的问题。 最后，她签字并提交调查表。

组织门户和调查表是响应式的，并且适合移动设备。 以下工作流程显示了Sarah如何在其移动设备上导航并提交调查表。

![移动设备上的冲突形式](assets/conflict-form-on-mobile.png)

**工作原理**

组织门户和员工仪表板是AEM Sites页面。 仪表板列出了若干自助服务选项，如利益冲突调查表。 “应用”按钮链接到自适应表单。

自适应表单使用规则根据“问题”选项卡中提供的答案显示——隐藏信息。 此外，表单还使用Scribble组件在“声明”选项卡中进行签名。 请在上查看自适应表单 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/self-service/conflict-of-interest.html`。

**亲身体验**

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/self-service-forms.html` 使用Sarah的用 `srose/srose` 户名／密码登录。 单击 **[!UICONTROL Employee]** （员工）以访问控制板，然后单击 **[!UICONTROL Apply]** on Conflict of Interest调查表。 审查并提交调查表。

#### Gloria审查和批准了利益冲突问卷提交 {#gloria-reviews-and-approves-the-conflict-of-interest-questionnaire-submission}

Sarah提交的利益冲突调查表被分配给Gloria Rios审查。 Gloria在组织中担任合规官。 Gloria登录到其AEM收件箱，并查看分配给她的任务。 她批准了Sarah提交的调查表并完成了任务。

![冲突收件箱](assets/conflict-inbox.png)

Gloria的收件箱

![冲突批准](assets/conflict-approved.png)

打开任务

**工作原理**

Conflict of Interest调查表中的提交操作会触发一个工作流，该工作流会在Gloria的收件箱中创建一个任务以供批准。 在上查看表单工作流 `https://[authorHost]:[authorPort]/editor.html/conf/global/settings/workflow/models/we-finance/employee/self-service/we-finance-employee-conflict-of-interest.html`

![员工自助服务参考站点](assets/employee_self_service_reference_site_new.png)

**亲身体验**

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用Gloria Rios的 `grios/password` 用户名／密码登录。 打开为利益冲突调查表创建的任务并批准它。

## 公司卡应用程序演练 {#corporate-card-application-walkthrough}

莎拉出差很多，她需要一张公司信用卡来支付搬家时的账单。 她通过组织的员工门户申请公司卡。

### Sarah提交公司卡申请 {#sarah-submits-the-corporate-card-application}

Sarah进入其组织的门户，登录并单击“员工” **** ，访问员工仪表板。 她在员工控制面板上查找公司卡应用程序，然后单击“ **[!UICONTROL 应用”]**。

![we-finance-home-1](assets/we-finance-home-1.png)

组织门户

![employee-dashboard-1](assets/employee-dashboard-1.png)

员工控制板

她单击“ **[!UICONTROL 应用]** ”(Apply on the Corporate Card)应用程序。 将打开单页应用程序。 她会填写所有详细信息，并单击“ **[!UICONTROL 应用]** ”以提交应用程序。

![卡表单](assets/card-form.png)

**工作原理**

组织门户和员工仪表板是AEM Sites页面。 功能板列出了若干自助服务选项，如公司卡应用程序。 应用程序上的“应用”按钮链接到自适应表单。

公司卡应用程序的自适应表单是一个简单、一页、响应式自适应表单。 它使用基本的自适应表单组件，如文本、电话、数字框和数字步进器。 在以下位置查看自适应表单：\
`https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/self-service/corporate-card.html`.

**亲身体验**

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/self-service-forms.html` 使用Sarah的用 `srose/srose` 户名／密码登录。 单击 **[!UICONTROL Employee]** （员工）以访问控制板，然后单击Apply **[!UICONTROL on Corporate Card application(在公司卡]** 上应用)。 填写详细信息，然后提交申请。

### Gloria审阅并批准公司卡申请 {#gloria-reviews-and-approves-the-corporate-card-application}

Sarah提交的公司卡申请被分配给Gloria Rios审阅。 Gloria登录到其AEM收件箱，并查看分配给她的任务。 她批准了Sarah提交的申请并完成了任务。

![公司卡收件箱](assets/corporate-card-inbox.png)

Gloria的收件箱

![公司卡批准](assets/corporate-card-approved.png)

打开任务

**工作原理**

公司卡应用程序中的提交工作流会触发一个表单工作流，该工作流会在Gloria的收件箱中创建一个任务以供批准。 在上查看表单工作流 `https://[authorHost]:[authorPort]/editor.html/conf/global/settings/workflow/models/we-finance/employee/self-service/we-finance-employee-corporate-card.html`

![企业卡工作流模型](assets/corporate-card-workflow-model.png)

**亲身体验**

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用Gloria Rios的 `grios/password` 用户名／密码登录。 打开为公司卡应用程序创建的任务并进行批准。

## 费用报告提交演练 {#expense-report-submission-walkthrough}

在出差期间，莎拉需要提交费用报告以获得批准。 她所在组织的自助服务选项允许她在线提交费用报告。

### Sarah提交费用报告申请 {#sarah-submits-the-expense-report-application}

Sarah进入其组织的门户，登录并单击“员工” **** ，访问员工仪表板。 她在员工控制面板上查找“费用报表”应用程序，然后单击“ **[!UICONTROL 应用”]**。

![we-finance-home-2](assets/we-finance-home-2.png)

组织门户

![employee-dashboard-2](assets/employee-dashboard-2.png)

员工控制板

她单击“ **[!UICONTROL 应用]** ”(Apply on the Expense Report)应用程序。 此时将打开一个应用程序表单，该表单包含两个选项卡：“报告名称”和“报告详细信息”。 “报 **表详细信息** ”选项卡中的+图标允许她在一个报表中添加超过支出的项目。

组织门户和应用程序是响应式的，并且适合移动设备。 以下工作流程显示了Sarah如何在其移动设备上导航并提交费用报告。

![移动费用报告](assets/expense-report-on-mobile.png)

**工作原理**

组织门户和员工仪表板是AEM Sites页面。 功能板列出了多个自助服务选项，如“费用报告”应用程序。 “应用”按钮链接到自适应表单。

自适应表单中的“报告名称”和“报告详细信息”选项卡是面板组件。 “报告详细信息”面板包含“费用”面板。 它是一个可重复使用的面板，允许在报告中添加多项支出。 请在上查看自适应表单及其配置 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/expense-report.html`。

**亲身体验**

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/self-service-forms.html` 使用Sarah的用 `srose/srose` 户名／密码登录。 单击 **[!UICONTROL Employee]** （员工）以访问控制板，然后单击Apply **[!UICONTROL on Expense]** Report（在费用报表应用程序上应用）。 填写详细信息并提交申请。

### Gloria审阅并批准费用报告 {#gloria-reviews-and-approves-the-expense-report}

由Sarah提交的费用报告被分配给Gloria Rios审阅。 Gloria登录到其AEM收件箱，并查看分配给她的任务。 她批准了Sarah提交的申请并完成了任务。

![expense-report-inbox](assets/expense-report-inbox.png)

Gloria的收件箱

![expense-report-approved](assets/expense-report-approved.png)

打开任务

**工作原理**

费用报告应用程序中的提交工作流会触发一个表单工作流，该工作流会在Gloria的收件箱中创建一个任务以供批准。 在上查看表单工作流 `https://[authorHost]:[authorPort]/editor.html/conf/global/settings/workflow/models/we-finance/employee/self-service/we-finance-employee-expense-report-workflow.html`

![公司卡费用——报告——工作流——模型](assets/corporate-card-expense-report-workflow-model.png)

**亲身体验**

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用Gloria Rios的 `grios/password` 用户名／密码登录。 打开为“费用报表”应用程序创建的任务并进行批准。

## 离开应用程序演练 {#leave-application-walkthrough}

莎拉计划下月放假，并想申请一周的休假。

### Sarah提交了休假申请 {#sarah-submits-the-leave-application}

Sarah进入其组织的门户，登录并单击“员工” **** ，访问员工仪表板。 她在员工仪表板上找到离开应用程序，然后单击“ **[!UICONTROL 应用”]**。

![we-finance-home-3](assets/we-finance-home-3.png)

组织门户

![employee-dashboard-3](assets/employee-dashboard-3.png)

员工控制板

此时将打开休假应用程序，其中预填了Sarah的姓名和员工ID。 它还显示了她的休假平衡和历史。 她填写了请假详细信息，并提交申请以供批准。

组织门户和应用程序是响应式的，并且适合移动设备。 以下工作流程显示了Sarah如何在其移动设备上导航并提交应用程序。

![leave-form-on-mobile](assets/leave-form-on-mobile.png)

**工作原理**

组织门户和员工仪表板是AEM Sites页面。 功能板列出了若干自助服务选项，如leave应用程序。 “应用”按钮链接到自适应表单。

休假申请的自适应表单基于员工休假表单数据模型。 在Leave Balance部分中，将使用Form Data Model服务填充Leave `getLeavesOf` Balance表。 “开始日期”和“结束日期”字段使用规则验证日期值是否等于当前日期或之后。 使用函数计算休假持续 `calcBusinessDays` 时间。

您可以在以下位置查看自适应表单和表单数据模型：

`https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/self-service/leave-application.html`

`https://[authorHost]:[authorPort]/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/db`

**亲身体验**

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/self-service-forms.html` 使用Sarah的用 `srose/srose` 户名／密码登录。 单击 **[!UICONTROL Employee]** （员工）以访问控制板，然后单击Apply **** on Leave Application（在退出应用程序时应用）。 填写详细信息并提交申请。

#### Gloria审阅并批准休假申请 {#gloria-reviews-and-approves-the-leave-application}

Sarah提交的休假申请被分配给Gloria Rios进行审查。 Gloria登录到其AEM收件箱，并查看分配给她的任务。 她批准了Sarah提交的申请并完成了任务。

![leave-inbox](assets/leave-inbox.png)

Gloria的收件箱

![leave approved](assets/leave-approved.png)

打开任务

**工作原理**

leave应用程序中的提交工作流会触发一个表单工作流，该工作流会在Gloria的收件箱中创建一个任务以供批准。 在上查看表单工作流 `https://[authorHost]:[authorPort]/editor.html/conf/global/settings/workflow/models/we-finance/employee/self-service/we-finance-employee-leave-application.html`

![企业卡片休假应用工作流模型](assets/corporate-card-leave-application-workflow-model.png)

**亲身体验**

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用Gloria Rios的 `grios/password` 用户名／密码登录。 打开为离开应用程序创建的任务并进行批准。
