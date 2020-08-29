---
title: We.Finance汽车保险续订参考站点演练
seo-title: We.Finance汽车保险续订参考站点演练
description: 'null'
seo-description: 'null'
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---


# We.Finance汽车保险续订参考站点演练{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance参考站点方案  {#we-finance-reference-site-scenario}

We.Finance站点是一个金融服务站点，旨在帮助您学习AEM Forms的交互式通信功能。

阅读详细的We.Finance汽车保险用例演练，其中展示AEM的表单及其与Microsoft Dynamics的集成如何帮助在金融服务公司中实现个性化的客户体验。 交互式演练旨在简化复杂数字交易和客户沟通在金融公司中的实施。

**旅程开始包含用例：**

Sarah Rose是We.Finance的现有客户，已购买汽车保险。 现在是她续签保险单的时候。 We.Finance保险代理Gloria Rios向Sarah发出提醒，提醒她续订保单。 Sarah按照电子邮件中提供的说明操作并成功完成该过程。

## 自动保险申请演练 {#auto-insurance-application-walkthrough}

We.Finance自动保险应用程序场景是用户的视觉解说，它基于两个角色：

* Sarah Rose,We.Finance客户
* Gloria Rios,We.Finance保险代理

### Gloria从We.Finance发送保险单续订通信 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria登录AEM实例，单击“ **自动保险续订”** ，然后单击“ **打开代理UI”。**&#x200B;点击一下鼠标，将用Sarah Rose的保单详情预填保险文档。 Gloria单击&#x200B;**“提交** ”，屏幕上将显示一条消息“已启动提交”，然后在几秒内显示“已成功提交”。

Sarah收到一封电子邮件，主题为“您的汽车保险续订”。

![代理 UI](assets/agent_ui_email_new.png)

#### 亲自查看 {#see-it-yourself}

转到Adobe Experience Manager **** > **Forms** > **Forms和文档** >我 **们财务>******&#x200B;汽车保险。 选择“自动保险续订” **交互通信** ，然后单击“ **打开代理UI”**。 交互式通信在代理UI中打开。 输入有效的电子邮件地址以接收附加了策略文档的电子邮件，然后单击“提交”。

您可以直接从 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah收到We.Finance发来的保险单续订通信，并决定续订 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封附有We.Finance附件的电子邮件，提醒她自己的汽车保险政策即将过期。 附件是她的汽车保险信件的印刷版。

Sarah单击 **“立即续订** ”并转到其汽车保险信件的Web版本。 Sarah在这封信上找到了她的政策到期的剩余天数。 本页为Sarah提供了她的保单详细信息（如保单编号、到期金额）的基本概述，以及折扣优惠和忠诚度奖励等其他信息。 Sarah再次单 **击策略** 底部的“立即续订”。

![ref1](assets/ref1.png)

#### 工作方式 {#how-it-works}

您的汽车保险信件的Web和打印输出是使用Interactive Communications的多渠道功能创建的。

电子邮件中的“立即续订”按钮链接到“自动保险续订”应用程序，该应用程序是发布实例上的交互式通信。

#### 亲自查看 {#see-it-yourself-1}

您必须已收到一封附有PDF的电子邮件。 PDF是您的汽车保险信件的印刷版。 单 **击“** Renew Now（立即续订）”以访问Web版本的策略。 检查您的个人信息和策略详细信息，然 **后单击** “立即续订”，以转到其他交互式通信。

电 **子邮件** 中的“立即续订”按钮将Sarah引导至策略的Web版本。 您可以访问以下URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以查看“自动保险续订”的详细摘要，然后 **单击页** 面底部的“立即续订”。

### Sarah进入付款页面 {#sarah-reaches-the-payment-page}

We.Finance将Sarah带到付款页面。 Sarah会重新检查其政策编号和到期日，并记录其记录。 在页面右侧，她以总金额的10%溢价折扣检查续订的“付款摘要”。

#### 工作方式 {#how-it-works-1}

Renew Now（立即续订）按钮将指示Sarah进入付款页面。 付款页面是自适应表单。

#### 亲自查看 {#see-it-yourself-2}

单击 **立即续** 订以访问付款页面。 填写您的信用卡信息，然后单击“ **付款”**。

您可以访问以下网址的创作实例中的付款页面：

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah付款并完成该流程 {#sarah-makes-the-payment-and-completes-the-process}

Sarah会填写她的信用卡详细信息并单击“ **付款”**。

#### 工作方式 {#how-it-works-2}

当Sarah填充信用卡详细信息并单击“提交”时，将处理她的信用卡付款，屏幕上将显示以自适应表单配置的感谢信。

#### 亲自查看 {#see-it-yourself-3}

您可以在单击付款后视图确认消息

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
