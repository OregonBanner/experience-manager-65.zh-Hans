---
title: We.Finance汽车保险续订参考网站演练
description: 通过演练了解We.Finance汽车保险续订参考网站。
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# We.Finance汽车保险续订参考网站演练{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance引用站点方案  {#we-finance-reference-site-scenario}

We.Finance站点是一个金融服务站点，旨在帮助您学习AEM Forms的交互式通信功能。

阅读We.Finance汽车保险使用案例的详细演练，该用例展示AEM表单及其与Microsoft® Dynamics的集成如何帮助个性化金融服务公司的客户体验。 交互式演练旨在简化在金融公司中复杂数字交易和客户通信的实施。

**历程从用例开始：**

Sarah Rose是We.Finance的现有客户，并购买了汽车保险单。 现在正是莎拉续保的时候。 格洛丽亚·里奥斯是她的保险代理人。 We.Finance向Sarah发送有关政策更新的提醒。 Sarah按照电子邮件中的说明进行操作，并成功完成此过程。

## 自动保险申请演练 {#auto-insurance-application-walkthrough}

We.Finance汽车保险申请方案是一个面向用户的视觉叙述，基于两个角色：

* We.Finance客户Sarah Rose
* Gloria Rios，保险代理，We.Finance

### Gloria发送来自We.Finance的保单续约通讯 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria登录到AEM实例，单击 **汽车保险续约，** 然后单击 **打开代理UI**. 单击会使用Sarah Rose的保单详细信息预填充保险文档。 Gloria点击次数 **提交** ，并在“Submission Initiated”屏幕上显示消息，然后在几秒钟后显示“Submission Successful”。

Sarah收到一封电子邮件，主题为“您的汽车保险续订”。

![代理 UI](assets/agent_ui_email_new.png)

#### 亲眼看看 {#see-it-yourself}

转到 **Adobe Experience Manager** > **Forms** > **Forms和文档** > **We.Finance** > **汽车保险**. 选择车险续订 **交互式通信** 并单击 **打开代理UI**. 交互式通信在Agent UI中打开。 输入有效的电子邮件地址，以便他们可以接收带有附加策略文档的电子邮件，然后单击“提交”。

您可以直接从访问和查看“汽车保险续订”交互式通信 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah收到We.Finance的保单续订通信并决定续订 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封包含We.Finance附件的电子邮件，提醒Sarah她的汽车保险单即将过期。 附件是Sarah汽车保险信的打印版。

Sarah点击量 **立即续订** 并定向至其汽车保险信件的网络版本。 在此信的顶部，Sarah将查找保单过期前剩余的时间。 此页面为Sarah提供其保单详情的基本概览（如保单编号、应付金额）以及其他信息（如折扣优惠和忠诚度奖励）。 Sarah再次单击 **立即续订** 在政策的底部。

![ref1](assets/ref1.png)

#### 工作原理 {#how-it-works}

使用交互式通信的多渠道功能创建汽车保险单的Web和打印输出。

电子邮件中的“立即续订”按钮链接到自动保险续订应用程序，该应用程序是发布实例上的交互式通信。

#### 亲眼看看 {#see-it-yourself-1}

您必须已收到一封包含附加PDF的电子邮件。 该PDF是汽车保险单的打印版本。 单击 **立即续订** 以访问策略的Web版本。 检查您的个人信息和策略详细信息，然后单击 **立即续订** 它会带您进入另一个交互式通信。

此 **立即续订** 电子邮件中的按钮引导Sarah访问Web上的策略。 您可以访问以下URL：

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以查看汽车保险续订的详细摘要，然后单击 **立即续订** 在页面底部。

### Sarah到达付款页面 {#sarah-reaches-the-payment-page}

We.Finance会将Sarah转到“付款”页面。 Sarah用她的记录重新检查她的保险单号码和到期日期。 在页面的右侧，Sarah检查续订的付款摘要，总金额享受10%的溢价折扣。

#### 工作原理 {#how-it-works-1}

“立即续订”按钮会将Sarah引导至付款页面。 支付页面是自适应表单。

#### 亲眼看看 {#see-it-yourself-2}

单击 **立即续订** 以访问支付页面。 填写您的信用卡信息，然后单击 **进行付款**.

您可以在创作实例中访问付款页面：

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah进行支付并完成流程 {#sarah-makes-the-payment-and-completes-the-process}

Sarah填写她的信用卡详细信息并按一下 **进行付款**.

#### 工作原理 {#how-it-works-2}

当Sarah填写信用卡详细信息并单击提交时，将处理其信用卡付款，并且屏幕上将显示一条在自适应表单中配置的感谢消息。

#### 亲眼看看 {#see-it-yourself-3}

单击付款后，您可以查看确认消息，网址为

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
