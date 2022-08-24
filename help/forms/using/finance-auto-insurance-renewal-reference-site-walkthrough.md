---
title: We.金融汽车保险续订参考站点演练
seo-title: We.Finance Auto Insurance Renewal reference site walkthrough
description: We.金融汽车保险续订参考站点演练
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# We.金融汽车保险续订参考站点演练{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance参考站点方案  {#we-finance-reference-site-scenario}

We.Finance网站是一个金融服务网站，旨在帮助您学习AEM Forms的交互式通信功能。

阅读We.Finance Auto Insurance用例的详细演练，其中显示了AEM表单及其与Microsoft Dynamics的集成如何帮助将客户在金融服务公司的体验个性化。 交互式演练旨在简化金融公司复杂的数字交易和客户沟通的实施。

**历程从用例开始：**

莎拉·罗斯是We.Finance的现有客户，并购买了汽车保险单。 现在是她的保险单续保的时候了。 We.Finance保险代理Gloria Rios向Sarah发送关于她续保的提醒。 Sarah按照电子邮件中提供的说明操作，并成功完成了该过程。

## 自动保险申请演练 {#auto-insurance-application-walkthrough}

We.Finance自动保险应用程序方案是用户的直观叙述，其基于两个角色：

* Sarah Rose，We.Finance客户
* 格洛丽亚·里奥斯，We.Finance保险代理

### 格洛丽亚向We.Finance发送保险单续订通信 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria登录AEM实例，单击 **汽车保险续期，** 然后点击 **打开代理UI。**&#x200B;点击后，保险单上会填上莎拉·罗斯的保单细节。 Gloria点击&#x200B;**提交** “已启动提交”屏幕上会显示一条消息，然后在几秒内显示“已成功提交”。

Sarah收到一封电子邮件，主题为“您的汽车保险续订”。

![代理 UI](assets/agent_ui_email_new.png)

#### 亲眼看看 {#see-it-yourself}

转到 **Adobe Experience Manager** > **Forms** > **Forms和文档** > **We.Finance** > **汽车保险**. 选择汽车保险续订 **交互式通信** 单击 **Open Agent UI**. 交互式通信在代理UI中打开。 输入有效的电子邮件地址以接收附加的策略文档的电子邮件，然后单击“提交”。

您可以直接从访问和查看“汽车保险续订”交互式通信 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah收到We.Finance发来的保单续订通信，并决定续订 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封邮件，邮件中附有We.Finance的附件，提醒她，她的汽车保险政策即将到期。 附件是她的汽车保险函的印刷版。

Sarah点击 **立即续订** 并指向她的汽车保险信函的网络版本。 除了这封信，Sarah还能找到她的政策到期的天数。 本页为Sarah提供了她的保险单详细信息（如保单编号、到期金额）的基本概述，以及折扣优惠和忠诚奖励等其他信息。 莎拉再次点击 **立即续订** 在政策的底部。

![ref1](assets/ref1.png)

#### 工作原理 {#how-it-works}

您的汽车保险信函的Web和打印输出是使用Interactive Communications的多渠道功能创建的。

电子邮件中的立即续订按钮已链接到自动保险续订应用程序，该应用程序是发布实例上的交互式通信。

#### 亲眼看看 {#see-it-yourself-1}

您必须已收到附有的PDF的电子邮件。 该PDF是您的汽车保险信函的打印版本。 单击 **立即续订** 以访问Web版本的策略。 检查您的个人信息和策略详细信息，然后单击 **立即续订** 这会将您转到另一个交互式通信。

的 **立即续订** 按钮，将Sarah引导至策略的Web版本。 您可以访问以下URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以查看“汽车保险续订”的详细摘要，然后单击 **立即续订** 页面底部。

### 莎拉到达付款页面 {#sarah-reaches-the-payment-page}

We.Finance将Sarah带到付款页面。 Sarah会使用她的记录重新检查她的政策编号和过期日期。 在页面右侧，她检查续订的“付款摘要”，其总金额有10%的溢价折扣。

#### 工作原理 {#how-it-works-1}

立即续订按钮将Sarah引导至付款页面。 付款页面是自适应表单。

#### 亲眼看看 {#see-it-yourself-2}

单击 **立即续订** 以访问“付款”页面。 填写您的信用卡信息，然后单击 **付款**.

您可以在创作实例中访问付款页面(位于

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### 莎拉付了钱，完成了这个过程 {#sarah-makes-the-payment-and-completes-the-process}

Sarah会填写她的信用卡详细信息和点击量 **付款**.

#### 工作原理 {#how-it-works-2}

当Sarah填写信用卡详细信息并单击“提交”时，将处理她的信用卡付款，屏幕上会显示在自适应表单中配置的感谢消息。

#### 亲眼看看 {#see-it-yourself-3}

单击以下位置的付款后，您可以查看确认消息

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
