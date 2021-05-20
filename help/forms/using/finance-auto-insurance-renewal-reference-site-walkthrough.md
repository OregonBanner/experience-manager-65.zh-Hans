---
title: We.金融汽车保险续订参考站点演练
seo-title: We.金融汽车保险续订参考站点演练
description: We.金融汽车保险续订参考站点演练
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# We.Finance汽车保险续订参考站点演练{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance参考站点方案{#we-finance-reference-site-scenario}

We.Finance网站是一个金融服务网站，旨在帮助您学习AEM Forms的交互式通信功能。

阅读We.Finance Auto Insurance用例的详细演练，其中显示了AEM表单及其与Microsoft Dynamics的集成如何帮助个性化金融服务公司的客户体验。 交互式演练旨在简化金融公司复杂的数字交易和客户沟通的实施。

**历程从用例开始：**

莎拉·罗斯是We.Finance的现有客户，并购买了汽车保险单。 现在是她的保险单续保的时候了。 We.Finance保险代理Gloria Rios向Sarah发送关于她续保的提醒。 Sarah按照电子邮件中提供的说明操作，并成功完成了该过程。

## 自动保险申请演练{#auto-insurance-application-walkthrough}

We.Finance自动保险应用程序方案是用户的直观叙述，其基于两个角色：

* Sarah Rose，We.Finance客户
* 格洛丽亚·里奥斯，We.Finance保险代理

### Gloria从We.Finance {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}发送保单续订通信

Gloria登录AEM实例，单击&#x200B;**自动保险续订，**，然后单击&#x200B;**打开代理UI。**&#x200B;点击后，保险单上会填上莎拉·罗斯的保单细节。Gloria单击&#x200B;**提交**，屏幕上会显示一条消息“已启动提交”，然后在几秒内显示“已成功提交”。

Sarah收到一封电子邮件，主题为“您的汽车保险续订”。

![代理 UI](assets/agent_ui_email_new.png)

#### 自己看{#see-it-yourself}

转到&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和文档** > **We.Finance** > **汽车保险**。 选择自动保险续订&#x200B;**交互式通信**&#x200B;并单击&#x200B;**打开代理UI**。 交互式通信在代理UI中打开。 输入有效的电子邮件地址以接收附加的策略文档的电子邮件，然后单击“提交”。

您可以直接从`https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`访问和查看汽车保险续订交互式通信

### Sarah收到We.Finance发来的保单续订通信，并决定续订{#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封邮件，邮件中附有We.Finance的附件，提醒她，她的汽车保险政策即将到期。 附件是她的汽车保险函的印刷版。

Sarah单击&#x200B;**立即续订**，并被定向到她的汽车保险信函的Web版本。 除了这封信，Sarah还能找到她的政策到期的天数。 本页为Sarah提供了她的保险单详细信息（如保单编号、到期金额）的基本概述，以及折扣优惠和忠诚奖励等其他信息。 Sarah再次单击位于策略底部的&#x200B;**Renew Now**。

![ref1](assets/ref1.png)

#### 工作原理{#how-it-works}

您的汽车保险信函的Web和打印输出是使用Interactive Communications的多渠道功能创建的。

电子邮件中的立即续订按钮已链接到自动保险续订应用程序，该应用程序是发布实例上的交互式通信。

#### 自己看{#see-it-yourself-1}

您必须收到附有PDF的电子邮件。 PDF是您的汽车保险信函的打印版本。 单击&#x200B;**立即续订**&#x200B;以访问策略的Web版本。 检查您的个人信息和策略详细信息，然后单击&#x200B;**立即续订**，以转到另一个交互式通信。

电子邮件中的&#x200B;**Renew Now**&#x200B;按钮会将Sarah引导至策略的Web版本。 您可以访问以下URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以查看汽车保险续订的详细摘要，然后单击页面底部的&#x200B;**立即续订**。

### Sarah到达付款页面{#sarah-reaches-the-payment-page}

We.Finance将Sarah带到付款页面。 Sarah会使用她的记录重新检查她的政策编号和过期日期。 在页面右侧，她检查续订的“付款摘要”，其总金额有10%的溢价折扣。

#### 工作原理{#how-it-works-1}

立即续订按钮将Sarah引导至付款页面。 付款页面是自适应表单。

#### 自己看{#see-it-yourself-2}

单击&#x200B;**Renew Now**&#x200B;以访问“付款”页面。 填写您的信用卡信息，然后单击&#x200B;**付款**。

您可以在创作实例中访问付款页面(位于

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah付款并完成{#sarah-makes-the-payment-and-completes-the-process}流程

Sarah会填写她的信用卡详细信息并单击&#x200B;**付款**。

#### 工作原理{#how-it-works-2}

当Sarah填写信用卡详细信息并单击“提交”时，将处理她的信用卡付款，屏幕上会显示在自适应表单中配置的感谢消息。

#### 自己看{#see-it-yourself-3}

单击以下位置的付款后，您可以查看确认消息

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
