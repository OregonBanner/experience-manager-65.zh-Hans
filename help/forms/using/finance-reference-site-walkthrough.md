---
title: We.Finance参考站点演练
seo-title: We.Finance参考站点演练
description: 浏览We.Finance参考站点并了解其实施方式。 We.Finance是展示AEM Forms的主要特性和功能的示例实施。
seo-description: 浏览We.Finance参考站点并了解其实施方式。 We.Finance是展示AEM Forms的主要特性和功能的示例实施。
uuid: 3cc0dd85-63f6-4772-8c00-373bb85b1713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: b4fdbf86-d8f3-4da5-9e4e-4d5492ae1632
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# We.Finance参考站点演练{#we-finance-reference-site-walkthrough}

## Pre-requisites {#pre-requisites}

按照设置和配置AEM Forms引用站 [点中的说明设置引用站点](../../forms/using/setup-reference-sites.md)。

## We.Finance Reference站点方案 {#we-finance-reference-site-scenarios}

We.Finance是金融服务领域的领先组织，它优惠全面和个性化的财务解决方案以满足不同客户用户档案的需求。 他们优惠信用卡、住房抵押和住房保险服务。

他们的目标是通过自己喜欢的设备与现有和潜在客户联系，解释其服务的益处，并帮助他们登记其服务。 此外，他们还在寻求更多金融产品，如客户可能会觉得有趣的附加卡。

阅读We.Finance使用案例的详细演练，了解AEM Forms如何帮助金融组织实现其目标。 下面介绍了以下演练：

* [信用卡申请演练](#credit-card-application-walkthrough)
* [住房抵押申请演练](#home-mortgage-application-walkthrough)
* [Microsoft Dynamics的家庭抵押应用程序演练](#home-mortgage-application-walkthrough-with-microsoft-dynamics)
* [家庭保险申请演练](#home-insurance-application-walkthrough)
* [财富管理演练](#wealthmanagementwalkthrough)
* [汽车保险申请演练](#autoinsuranceapplicationwalkthrough)

## 信用卡申请演练 {#credit-card-application-walkthrough}

We.Finance信用卡应用方案涉及以下角色：

* Sarah Rose,We.Finance客户
* Gloria Rios,We.Finance信用卡和抵押主管

以下信息图描述了信用卡应用程序的分步工作流。

![workflow_aem](assets/workflow_aem.png)

让我们详细查看参考站点方案，了解AEM Forms如何帮助We.Finance实现其目标。

### Sarah从We.Finance收到新闻稿并申请信用卡 {#sarah-receives-a-newsletter-from-we-finance-and-applies-for-a-credit-card}

莎拉·罗丝是We.Finance的现有客户。 她从We.Finance收到一份关于优惠上新信用卡的新闻快讯。 她觉得优惠很兴奋，决定申请信用卡。 她单击新闻稿中的“立即应用”按钮，然后转到We.Finance门户上的信用卡应用程序。

![营销——电子邮件](assets/marketing-email.png)

#### 工作原理 {#how-it-works}

发送到Sarah的Newsletter是一个自定义实施，它会触发到指定电子邮件ID的电子邮件。 电子邮件中的“立即应用”按钮链接到信用卡应用程序，该应用程序是发布实例上的自适应表单。

#### 亲身体验 {#see-it-yourself}

在发布实例上打开以下URL以触发新闻稿电子邮件。 确保替换为有 `[emailID]` 效的电子邮件帐户以接收新闻稿。 打开新闻稿，然后单 **[!UICONTROL 击立即应用]** ，以转到信用卡应用程序。

`https://[publishServer]:[publsihPort]/content/campaigns/we-finance/start.html?app=cc&email=[emailID]&givenName=Sarah&familyName=Rose`

### 莎拉觉得这优惠很有趣，并选择 {#sarah-finds-the-offer-interesting-and-chooses-to-apply}

Sarah决定申请信用卡，然后点按电 **子邮件上的** “立即申请”按钮。 Sarah会转到We.Finance门户上的信用卡应用程序。 应用程序表单使用卡布局按部分组织。

Sarah从可用选项中选择信用卡，然后单击“继 **[!UICONTROL 续”]**。

![cc-application-form-desktop](assets/cc-application-form-desktop.png)

在“个人信息”页面上，当Sarah提供其社会安全号时，她会收到一个提示，提示她使用自己的凭据登录。

![login-ssn](assets/login-ssn.png)

Sarah是We.Finance的现有客户。 她使用自己的We.Finance帐户凭据登录，并且表单中会自动填充她的个人详细信息。 Sarah继续填写申请表，此时会弹出提醒，要求她参加会议。 她单击“ **[!UICONTROL 保存我在应用程序表单上的进度]** ”。 它保存了Sarah迄今填写的所有信息，并弹出一个对话框，确认她是否希望收到一封电子邮件，其中包含一个链接，指向她的草稿申请，以备日后完成。

Sarah单击“ **[!UICONTROL 发送邮件”]**。 她会收到一封电子邮件，其中包含恢复其信用卡申请的链接。

![恢复](assets/resume.png)

**Sarah通过移动设备访问信用卡应用程序**

如果Sarah正从其移动设备访问信用卡应用程序，则响应式应用程序将在针对移动设备优化的视图中打开。 在此视图中，应用程序表单一次呈现为一个部分。 它允许Sarah在导航应用程序时逐步视图和提供信息。

![在移动设备上填写信用卡申请](assets/form-on-mobile.png)

**工作原理**

“立 **即应用** ”按钮将Sarah定向到信用卡应用程序。 应用程序是自适应表单，您可以在的创作实例中查看该表单 `https://[host]:'port'/editor.html/content/forms/af/we-finance/cc-app.html`。

您可以在自适应表单中查看的一些主要功能包括：

* 它基于XSD模式。
* 它使用We Finance主题A构建，用于样式设计，使用We.Finance模板构建布局。 此外，它还使用在表单标题布局中没有面板标题的布局进行移动导航。 当从移动设备打开时，它显示渐进式移动布局。 您可以在上查看模 `https://[host]:'port'/libs/wcm/core/content/sites/templates.html/conf/we-finance` 板，也可以在上查看主题 `https://[host]:'port'/editor.html/content/dam/formsanddocuments-themes/we-finance/we-finance-theme-a/jcr:content`。
* 它包括自适应表单规则，用于调用表单数据模型服务以预填已登录用户的用户详细信息。 它还调用服务，按社会保险号或表单中提供的电子邮件地址预填信息。 您可以在查看表单数据模型及其服务 `https://[host]:'port'/aem/forms.html/content/dam/formsanddocuments-fdm`。
* 它使用各种自适应表单组件来捕获输入并适应用户响应。 它还使用支持HTML5输入类型的电子邮件等组件。
* 它使用签名步骤组件显示完成的表单并允许在表单上进行电子签名。
* “保存我的进度”按钮为用户生成唯一的ID，并将部分填充的应用程序另存为AEM存储库中的某个节点中的草稿。 此外，它还显示一个对话框，请求获得发送电子邮件的权限，该电子邮件包含指向包含草稿应用程序的节点的链接。 确认对话框上的“发送邮件”按钮会触发一封电子邮件，其中包含指向包含草稿的节点的链接。
* 它使用调用AEM工作流提交操作来触发信用卡批准工作流。 您可以在以下位置查看此表单中使用的工作流： `https://[host]:'port'/editor.html/conf/global/settings/workflow/models/we-finance-credit-card-workflow.html`

建议查看表单以了解用于构建表单的模式、组件、规则、表单数据模型、表单工作流和提交操作。

另外，请参阅以下文档以了解有关信用卡应用程序自适应表单中使用的功能的更多信息：

* [自适应表单创作简介](../../forms/using/introduction-forms-authoring.md)
* [使用XML模式创建自适应表单](../../forms/using/adaptive-form-xml-schema-form-model.md)
* [规则编辑器](../../forms/using/rule-editor.md)
* [主题](../../forms/using/themes.md)
* [数据集成](../../forms/using/data-integration.md)
* [在自适应表单中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [OSGi上以表单为中心的工作流程](../../forms/using/aem-forms-workflow.md)

**亲身体验**

以Sarah Rose身份登录时，单击信用 **卡应用程序上** “立即申请”按钮。 填写一些详细信息，浏览各种自适应表单组件，然后单击 **Save my progress** ，以便收到一封电子邮件，其中包含链接到草稿应用程序的“继续 **** ”按钮。 请确保在应用程序表单中指定电子邮件ID以接收电子邮件。

查看We.Finance主题：

`https://<host>:<AuthorPort>/editor.html/content/dam/formsanddocuments-themes/we-Finance/we-Finance-Theme-A/jcr:content`

您可以在以下位置查看We.Finance模板：

`https://<host>:<AuthorPort>/editor.html/conf/we-finance/settings/wcm/templates/we-finance-template/structure.html`

### Sarah恢复并提交申请 {#sarah-resumes-and-submits-the-application}

Sarah稍后回来，找到We.Finance发来的一封电子邮件。 她单击电 **子邮件中** “继续”按钮，转到信用卡申请草稿。 她之前填写的信息会预先填充。 她填写剩余的申请表，对申请进行签名，然后提交。

![resume-1](assets/resume-1.png)

或者，她也可以访问We.Finance主页上 **的“我的表单** ”下的申请草稿。

![门户草稿](assets/portal-drafts.png)

#### 工作原理 {#how-it-works-1}

电子邮件中的“继续”按钮将Sarah重定向到包含其草稿应用程序的节点。

#### 亲身体验 {#see-it-yourself-1}

您必须已收到一封电子邮件，其中包含您在填写申请表时指定的电子邮件ID上指向该申请草稿的链接。 继续，填写申请中的其余部分，然后提交。

### We.Finance接收并批准该应用程序 {#approving-the-application}

We.Finance收到Sarah提交的信用卡申请。 任务分配给Gloria Rios。 她会在自己的AEM收件箱中审阅任务并批准它。

![收件箱](assets/inbox.png)

#### 工作原理 {#how-it-works-2}

当Sarah填写并提交信用卡应用程序时，将触发一个Forms Workflow，并在Gloria的AEM收件箱中创建一个任务。

OSGi上的AEM Forms提供以表单为中心的工作流，使您能够构建基于表单的自适应工作流。 这些工作流可用于审阅和批准、业务流程流、开始文档服务、与Adobe Sign签名工作流程集成等。 有关详细信息，请参 [阅OSGi上以表单为中心的工作流程](../../forms/using/aem-forms-workflow.md)。

下图描述了处理信用卡应用程序并生成应用程序PDF输出的AEM工作流。

![workflow](assets/workflow.png)

#### 亲身体验 {#see-it-yourself-2}

您可以访问位于https://&lt;*hostname*>:&lt;*PublishPort*>/content/we-finance/global/en.html的we.finance站点的AEM收件箱。 在页面中，点按 **登录**，选中以代表身份登录复选框 **，使用Gloria Rios的用户名／密码登录AEM收件箱**`grios/password` ，然后批准信用卡应用程序。 有关将AEM收件箱用于以表单为中心的工作流任务的信息，请参阅 [管理AEM收件箱中的表单应用程序和任务](../../forms/using/manage-applications-inbox.md)。

![收件箱-1](assets/inbox-1.png)

当您批准该应用程序时，Sarah会收到一封包含欢迎工具包的电子邮件。

### Sarah收到欢迎工具包并申请附加卡 {#sarah-receives-the-welcome-kit-and-applies-for-an-add-on-card}

当Sarah的信用卡申请获得批准时，她会收到一封电子邮件，其中附有欢迎工具包的链接。 她打开了欢迎包，其中包含她的信用卡帐户详细信息。 欢迎工具包还展示了为Sarah个性化的促销优惠。 当她向下滚动时，欢迎工具包包含一个嵌入式表单，用于申请附加卡。 Sarah从欢迎工具包中快速填写了所需的详细信息并申请了附加卡。 此时会显示加载项卡应用程序的确认对话框。

![welcome-kit-for-sara](assets/welcome-kit-for-sara.png)

欢迎工具包是为Sarah提供的，并显示与她相关的信息。 它为她提供了下载PDF版欢迎工具包的选项。

![白金卡的优势](assets/benefits-of-platinum-card.png)

欢迎工具包中还包含另一个申请表，Sarah可以填写并提交该表单，以便从欢迎工具包中申请附加卡，而无需访问We.Finance门户。

![apply-addon-card](assets/apply-addon-card.png)

#### 工作原理 {#how-it-works-3}

欢迎工具包是包中包含的交互式通 `cq-we-finance-content-pkg.zip` 信。 桌面版本中用于展示欢迎工具包中信用卡优势的交互式卡是使用文档片段的默认卡布局创建的自定义布局。

附加卡应用程序是欢迎工具包交互通信中的嵌入式自适应表单。

#### 亲身体验 {#see-it-yourself-3}

单击您在上一步中收到的电子邮件中的“继续”按钮。 它打开草稿应用程序。 填写所有详细信息并提交申请。 然后您将收到一个欢迎工具包。 查看欢迎工具包。

您还可以在以下URL视图欢迎工具包：

https://&lt;*host*>:&lt;*port*>/content/aemforms-refsite/doclink.html?文档=/content/forms/af/we-finance/credit-card/creditwelcomkit&amp;customerId=197&amp;渠道

您可以在创作和发布实例上访问它。

### Sarah收到一张信用卡对帐单 {#sarah-receives-a-credit-card-statement}

当Sarah开始使用信用卡时，她会收到We.Finance发来的另一封电子邮件，其中包含她的信用卡对账单。 以下图像显示了电子邮件，其中包含指向移动设备上信用卡对帐单的链接。

![语句电子邮件](assets/statement-email.png)

Sarah在电子邮件中单击“视图对帐单”以视图信用卡对帐单。 该声明是一种交互式通信。 它同时具有Web和打印(PDF)版本。 该语句与Forms Data Model集成，从数据库检索特定于客户的数据。 该交互式声明包含各种元素：

* 语句摘要
* 详细费用报告
* 图形费用分析
* 可选择在报表内支付到期款项
* 下载付款收据

![信用卡对帐单的不同部分](assets/sara-rose-statement.png)

Sarah无需访问门户或通过电子邮件搜索信用卡对帐单的PDF版本以便脱机存档。 她只需单击“下载语句”即可下载该语句的PDF版本。

详细的语句列在响应式表中。 该声明还提供了从声明中支付部分或全部到期款项的选项。

![详细说明](assets/statement-details.png)

Sarah计划在报表里付款。 Sarah还可以使用Flexi Pay选项将付款分为等额部分。

#### 工作原理 {#how-it-works-4}

信用卡对帐单是一种交互式通信。 语句中的详细费用表是响应式表。 费用分析的图形是图表组件，它读取费用表并生成饼图。

#### 亲身体验 {#see-it-yourself-4}

您可以通过以下URL查看交互式信用卡对帐单：

https://&lt;*hostname*>:&lt;*port*>/content/aemforms-refsite/doclink.html?文档=/content/forms/af/we-finance/credit-card/credit-card-statement&amp;customerId=197&amp;渠道=web

您可以在创作和发布实例上访问它。

信用卡对帐单在对帐单结尾处显示促销优惠。 您可以将Adobe目标与AEM Forms Interactive Communication集成，以根据特定客户细分提供促销目标优惠。 要将您的交互式通信配置为使用Adobe目标进行自定义和目标优惠，请参阅 [创建目标体验](/help/forms/using/experience-targeting-forms.md)。

![](do-not-localize/offers.png)

### We.Finance分析信用卡申请的绩效 {#we-finance-analyzes-the-performance-of-the-credit-card-application}

We.Finance会不时检查其信用卡应用程序的性能，以检查客户可能遇到的任何问题。 他们利用此分析对信用卡申请中的更改做出知情决定，以增强用户体验，降低表单的放弃率，从而提高转化率。 他们利用AEM Forms与Adobe Analytics的集成来进行分析。 以下图像描绘了其分析仪表板。

有关如何解释分析仪表板的更多信息，请参阅查 [看和了解AEM Forms分析报告](../../forms/using/view-understand-aem-forms-analytics-reports.md)。

![cc-analytics](assets/cc-analytics.png)

#### 工作原理 {#how-it-works-5}

使用Adobe Analytics跟踪信用卡申请表的性能指标。 有关配置Adobe Analytics和查看报告的详细信息，请参 [阅配置表单和文档分析](../../forms/using/configure-analytics-forms-documents.md)。

#### 亲身体验 {#see-it-yourself-br}

为便于您视图和浏览分析报告，我们将在参考站点中为信用卡应用程序提供种子数据。 在使用种子数据之前，请参阅 [配置分析](../../forms/using/setup-reference-sites.md#configureanalytics)。 在创作实例中执行以下步骤以将报表与种子数据视图:

1. 转到表 **单和文档** UI，网址为https://&lt;*hostname*>:&lt;*AuthorPort*>/aem/forms.html/content/dam/formsanddocuments。

1. 单击以打开 **We.Finance文件夹** 。
1. 选择“ **信用卡应用程序** ”自适应表单，然后在工具栏中单击“启 **[!UICONTROL 用分析”]**。

1. 再次选择自适应表单，然后单 **[!UICONTROL 击工具栏中的]** “分析报告”以生成报告。 您最初将看到一个空白报告。

要生成包含种子数据的分析报告，请执行以下操作：

1. 在CRXDE lite的地址浏览器中，键入： `/apps/we-finance/demo-artifacts/analyticsTestData/Credit card Analytics Test Data`
1. 测试数据在左侧目录结构中被选中。
1. 多次单击所选文件以在右侧面板中打开其内容。
1. 复制种子数据文件中的所有内容。
1. 在CRXDE中，导航到： `/content/dam/formsanddocuments/we-finance/cc-app/jcr:content/analyticsdatanode/lastsevendays`
1. 在“属 **[!UICONTROL 性]** ”(Properties **[!UICONTROL )下的“分析数]**&#x200B;据”(Analyticsdata)字段中，粘贴种子数据文件的复制内容。

1. 选择 **信用卡自适应表单的应用程序** ，然后单击工具栏中的 **[!UICONTROL 分析报表]** ，以生成包含种子数据的报表。

**信用卡申请的A/B测试**

除了分析信用卡应用程序的性能并不断改进之外，We.Finance还利用AEM Forms与目标的集成来创建A/B测试。 它允许他们为信用卡申请表提供不同的体验，并确定在表单填写和提交方面可带来更好转化率的体验。

要在AEM Forms服务器中配置目标，请参 [阅在AEM Forms中设置和集成目标](../../forms/using/ab-testing-adaptive-forms.md#set%20up%20and%20integrate%20target%20in%20aem%20forms)。

执行以下步骤以体验为We.Finance信用卡申请表创建A/B测试：

1. 转到表 **单和文档** ，网址为https://&lt;*hostname*>:&lt;*AuthorPort*>/aem/forms.html/content/dam/formsanddocuments。

1. 单击以打开 **We.Finance文件夹** 。
1. 选择“ **申请信用卡自适应表** ”。
1. 单击 **工具栏** 中的“更多” **，然后选择“**&#x200B;配置A/B测试”。 此时将打开“配置A/B测试”页。

1. 指定 **活动名**。
1. 从“受众”下拉列表中，选择要向其提供表单不同体验的受众。 例如， **访客使用Chrome**。
1. 在体验 **A和** B的“体验分发”字段中，按百分比指定分发，以确定体验在总受众中的分发。 例如，如果您为体验A和体验B分别指定40、60，则体验A将提供给40%的受众，其余60%将看到体验B。
1. 单击 **配置**。 将显示一个对话框，确认A/B测试的创建。
1. 单击&#x200B;**完成**。
1. 选择“信 **用卡申请”表单** ，然后单击“ **编辑”**。 它提供了打开其中一个体验的选项。 单击 **体验B**。 表单将在编辑模式下打开。

1. 根据需要修改表单，以创建不同于默认体验A的其他体验。
1. 转到表单和文档UI，选择表单，单击“更 **多**”，然后选择 **开始A/B测试**。
1. 现在，使用以下URL在Chrome浏览器中多次打开表单：

   `https://[hostname]:[port]/content/dam/formsanddocuments/we-finance/cc-app/jcr:content?wcmmode=disabled`

   >[!NOTE] 在下次打开表单之前，从浏 **览器的** cookie持久性中删除名为mbox的cookie。 您将随机看到表单的体验A和B。

1. 选择表单，单击“ **更多**”，然后单 **击“A/B测试报告”**。 由于您刚刚开始测试，因此报告中找不到太多数据。 现在，让我们提供一些种子数据，了解A/B测试报告的外观。
1. 打开CRXDE Lite并备份以下文件：/libs/fd/fmaddon/gui/components/admin/targetreport/clientlibs/targetreport/js/targetreport.js
1. 将上述文件中 `onReportLoadSuccess` 的函数定义替换为以下文件中的函数定义：/apps/we-finance/demo-artifacts/targetreport.js

   >[!NOTE]
   >
   >这些更改仅用于演示目的。 确保完成此过程后恢复文件内容。

1. 刷新您生成的报表，您将看到如下内容。 查看报告仪表板。

![ab测试报告](assets/ab-test-report.png)

要结束A/B测试，请单击报告 **仪表板上的“End A/B test** ”按钮。 此时，会显示一个对话框，提示您声明体验。 选择入选方并确认结束A/B测试。

如果您选择体验A作为获胜者，A/B测试将结束，并且今后，只有体验A将提供给所有受众，包括Chrome上的体验A。

## 住房抵押申请演练 {#home-mortgage-application-walkthrough}

We.Finance住房抵押方案涉及以下角色：

* Sarah Rose,We.Finance客户
* Gloria Rios,We.Finance信用卡和抵押主管
* John Doe,We.Finance客户关怀代表

以下信息图描述了家庭按揭贷款应用程序的分步工作流程。

![home_mortgage_application_alkthrough](assets/home_mortgage_application_walkthrough.png)

现在，让我们详细了解参考站点方案中的步骤，以了解AEM Forms如何帮助We.Finance实现其目标。

### Sarah访问We.Finance网站并申请住房抵押 {#sarah-visits-we-finance-website-and-applies-for-home-mortgage}

莎拉·罗丝计划买一套房子，并寻找住房抵押计划。 她是We.Finance客户，因此访问We.Finance门户来探索家庭抵押优惠。 她转到“贷款”部分，在门户上查找按揭贷款计算器。 她填写详细信息，然后点击“计算我的抵押贷款”，这会返回抵押计划。

![贷款1](assets/loans1.png)![贷款2](assets/loans2.png)

抵押计算器

![loans3](assets/loans3.png)

按揭贷款计算器结果

#### 工作原理 {#how-it-works-6}

“贷款”页面上的住房抵押计算器是AEM站点页面中嵌入的自适应表单。 您可以在编辑模式下查看“贷款”页面 `https://[authorHost]:[authorPort]/editor.html/content/we-finance/global/en/loan-landing-page.html`。

嵌入式抵押计算器是自适应表单，它使用规则根据计算器字段中提供的贷款详细信息计算EMI金额。 您可以在上查看自适应表单 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/hm-calc.html`。

#### 亲身体验 {#see-it-yourself-5}

转到We.Finance门户，单 `https://<publishHost>:<publishPort>/content/we-finance/global/en.html` 击贷 **[!UICONTROL 款]**。 在按揭贷款计算器中提供详细信息并查看结果。

### 莎拉觉得这优惠很有趣，并选择 {#sarah-finds-the-offer-interesting-and-chooses-to-apply-1}

Sarah选择申请住房抵押，然后单击“立即 **[!UICONTROL 应用”]** （在住房抵押计算器结果上）。 它打开了住房抵押申请。

如果Sarah正从其移动设备访问家庭按揭贷款应用程序，则应用程序表单将在为在移动设备上查看而优化的视图中打开。 在此视图中，应用程序表单一次呈现一个部分。 它允许Sarah在浏览应用程序表单时逐步视图和提供信息。

以下图像显示了Sarah在其移动设备上浏览家庭按揭贷款应用程序时的工作流。

![在移动设备上填写抵押申请](assets/mortgage-form-on-mobile.png)

如果Sarah从桌 **面单击** “立即应用”，则按揭申请表会打开，如下所示。 按揭贷款计算器中Sarah提供的信息预填在申请表中。 Sarah将填充其余的详细信息并单击“继 **续”**。

![按揭申请](assets/mortgage-application.png)

根据Sarah在抵押计算器中填写的信息，她会得到几个抵押计划。 她选择符合自己要求的计划并继续填写申请。 她终于签了字，提交了申请。

提交的申请将交给We.Finance批准。

![保存草稿应用程序](assets/mortgage-plans.png)

#### 工作原理 {#how-it-works-7}

“立 **即应用** ”按钮将Sarah定向到家庭抵押申请。 应用程序是自适应表单，您可以在的创作实例中查看该表单 `https://[host]:'port'/editor.html/content/forms/af/we-finance/hm-app.html`。

您可以在自适应表单中查看的一些主要功能包括：

* 它基于XSD模式 `homeMortgageApplication.xsd`。
* 它使用We Finance Theme B构建，用于样式设计，使用We.Finance模板构建布局。 此外，它还使用在表单标题布局中没有面板标题的布局进行移动导航。 当从移动设备打开时，它显示渐进式移动布局。 您可以在AEM作者实例的以下位置查看自适应表单中使用的模板和主题：

   * `https://[host]:'port'/libs/wcm/core/content/sites/templates.html/conf/we-finance`
   * `https://[host]:'port'/editor.html/content/dam/formsanddocuments-themes/we-finance/we-finance-theme-b/jcr:content`

* 应用程序中的第一个选项卡“入门”是动态按揭贷款计算器，它根据用户选择显示选项。 例如，“购买”和“再融资”选项的字段和值不同。 此功能是使用show-hide规则实现的。 此外，当您单击“继续”并且“计划”选项卡已初始化时，它会调用在表单数据模型中配置的Web服务，以获取和显示抵押计划。 您可以在上查看表单数据模型和配置的服务 `https://[host]:'port'/aem/forms.html/content/dam/formsanddocuments-fdm`。
* 它使用各种自适应表单组件来捕获输入并适应用户响应。 它还使用支持HTML5输入类型的电子邮件等组件。
* 它使用签名步骤组件显示完成的表单并允许在表单上进行电子签名。
* 它使用调用AEM工作流提交操作来触发We Finance Home Mortgage AEM工作流。 您可以在以下位置查看此表单中使用的工作流： `https://[host]:'port'/editor.html/conf/global/settings/workflow/models/we-finance-home-mortgage-workflow.html`

建议查看表单以了解用于构建表单的模式、组件、规则、表单数据模型、表单工作流和提交操作。

另外，请参阅以下文档以了解有关家庭抵押应用程序自适应表单中使用的功能的更多信息：

* [自适应表单创作简介](../../forms/using/introduction-forms-authoring.md)
* [使用XML模式创建自适应表单](../../forms/using/adaptive-form-xml-schema-form-model.md)
* [规则编辑器](../../forms/using/rule-editor.md)
* [主题](../../forms/using/themes.md)
* [数据集成](../../forms/using/data-integration.md)
* [在自适应表单中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [OSGi上以表单为中心的工作流程](../../forms/using/aem-forms-workflow.md)

#### 亲身体验 {#see-it-yourself-6}

转到并 `https://'[server]:[port]'/content/we-finance/global/en/all-forms.html` 单击“Home Mortgage Application” **上的** “立即应用”按钮。 在“入门”选项卡中填写详细信息，尝试不同的选项，然后提交应用程序。

请确保在应用程序中指定有效的电子邮件ID，以便在您的收件箱中接收确认邮件。

### We.Finance接收此应用程序 {#approving_the_application-1}

We.Finance收到Sarah提交的抵押申请。 批准或拒绝应用程序的任务分配给Gloria Rios。 她查看申请，发现Sarah的政府ID缺失。

![grios收件箱](assets/grios-inbox.png)

Gloria打开任务，单击“需要更多信息”，并对缺少的政府ID添加评论。

![need-more-info](assets/need-more-info.png)

任务现已分配给We.Finance的客户关怀代表John Doe。 他打开任务，评论歌洛莉亚的评论。 他联系了莎拉，要求她寄一份身份证。 在收到Sarah身份证的副本后，他将其附加到任务，并提交重新评估的申请。

![再评价](assets/reevaluation.png)

任务被重新分配给歌洛莉亚。 她查看附加的ID并批准该应用程序。

#### 工作原理 {#how-it-works-8}

当Sarah填写并提交家庭抵押申请时，将触发一个Forms Workflow，并在Gloria的AEM收件箱中创建一个任务。 当Gloria查看应用程序并请求获取更多信息时，任务将分配给John Doe。 当John Doe附加ID并重新提交应用程序时，它将分配给Gloria。 这在与抵押贷款应用程序关联的AEM工作流中定义。

OSGi上的AEM Forms提供以表单为中心的工作流，使您能够构建基于表单的自适应工作流。 这些工作流可用于审阅和批准、业务流程流、开始文档服务、与Adobe Sign签名工作流程集成等。 有关详细信息，请参 [阅OSGi上以表单为中心的工作流程](../../forms/using/aem-forms-workflow.md)。

下图描述了与抵押贷款应用程序关联的AEM工作流。

![mortgage-workflow-model](assets/mortgage-workflow-model.png)

#### 亲身体验 {#see-it-yourself-7}

您可以访问位于的AEM收件箱 `https://<hostname>:<AuthorPort>/content/we-finance/global/en/login.html?resource=/aem/inbox.html`。 使用Gloria Rios和John Doe的用户名/ `grios/password` 口令登录到AEM收件箱，并浏览家庭按揭 `jdoe/jdoe` 申请工作流程。

有关将AEM收件箱用于以表单为中心的工作流任务的信息，请参阅 [管理AEM收件箱中的表单应用程序和任务](../../forms/using/manage-applications-inbox.md)。

### Sarah收到欢迎工具包 {#sarah-receives-the-welcome-kit}

当Sarah的抵押申请获得批准时，她会收到一封电子邮件，其中附有欢迎工具包的链接。 她打开了欢迎包，包括一个轮盘，展示为莎拉定制的促销优惠。

![mortgage-welcome-kit](assets/mortgage-welcome-kit.png)

欢迎工具包是为Sarah提供的，并显示与她相关的信息。 它为她提供了下载PDF版欢迎工具包的选项。 底部的箭头按钮允许Sarah向下滚动并浏览欢迎工具包中的其他部分。

#### 工作原理 {#how-it-works-9}

欢迎工具包是包中包含的交互式通 `cq-we-finance-content-pkg.zip` 信。 欢迎包中的促销优惠由Adobe目标服务器提供。 优惠是针对特定客户细分定制和定位的。 欢迎工具包可从预配置的Adobe目标服务器为女性客户的受众部分获取优惠。

欢迎工具包的桌面版本中的交互式卡使用使用文档片段的默认卡布局创建的自定义布局。

#### 亲身体验 {#see-it-yourself-8}

如果您在填写抵押申请时提供了电子邮件ID，则您应该已收到一封电子邮件，其中包含指向欢迎工具包的链接。 检查您的收件箱并查看欢迎工具包。

您可以在AEM发布实例中视图它，其URL为：

`https://[host]:'port'/content/forms/af/we-finance/mortgage-loan-welcome-kit.html`

### Sarah收到一个帐户语句 {#sarah-receives-an-account-statement}

当Sarah获得贷款和开始支付分期付款时，她会收到We.Finance发来的另一封电子邮件，其中包含她的月度账户报表。

![mortgage-statement-email](assets/mortgage-statement-email.png)

Sarah在电子邮件中单击“视图声明”以视图抵押帐户声明。 该交互式声明包含各种元素：

* 语句摘要
* 声明详细信息

下图显示了Desktop上帐户语句的不同部分。

![抵押贷款帐户报表](assets/mortgage-statement.png)

详细的报表列在响应式表格中，并提供了从报表中支付部分或全部到期金额的选项。

#### 工作原理 {#how-it-works-10}

抵押声明是一种交互式通信。 它使用JSON批量处理过程生成。 语句中的详细费用表是响应式表。

#### 亲身体验 {#see-it-yourself-9}

您可以通过以下URL查看交互式按揭贷款帐户声明：

https://&lt;*hostname*>:&lt;*port*>/content/forms/af/we-finance/mortgage-account-statement.html?wcmmode=disabled

您可以在创作和发布实例上访问它。

### We.Finance分析抵押申请的表现 {#we-finance-analyzes-the-performance-of-the-mortgage-application}

We.Finance会不时检查其抵押申请的表现，以检查客户可能面临的任何问题。 他们使用本分析对抵押申请中的更改做出明智决策，以增强用户体验、降低表单放弃率，从而提高转化率。 他们利用AEM Forms与Adobe Analytics的集成来进行分析。 以下图像描绘了其分析仪表板。

有关如何解释分析仪表板的更多信息，请参阅查 [看和了解AEM Forms分析报告](../../forms/using/view-understand-aem-forms-analytics-reports.md)。

![mortgage-analytics](assets/mortgage-analytics.png)

#### 工作原理 {#how-it-works-11}

使用Adobe Analytics跟踪抵押申请表的绩效指标。 有关配置Adobe Analytics和查看报告的详细信息，请参 [阅配置表单和文档分析](../../forms/using/configure-analytics-forms-documents.md)。

#### 亲身体验 {#see-it-yourself-br-1}

为便于您视图和浏览分析报告，我们将在参考站点中为按揭贷款应用程序提供种子数据。 在使用种子数据之前，请参阅 [配置分析](../../forms/using/setup-reference-sites.md#configureanalytics)。 在创作实例中执行以下步骤以将报表与种子数据视图:

1. 转到表 **单和文档** UI，网址为https://&lt;*hostname*>:&lt;*AuthorPort*>/aem/forms.html/content/dam/formsanddocuments。

1. 单击以打开 **we-finance文件夹** 。
1. 选择“ **[!UICONTROL 应用程序用于家庭抵押]** ”自适应表单，然后在工具栏中单击“启 **[!UICONTROL 用分析”]**。

1. 再次选择表单，然后单击工 **[!UICONTROL 具栏中的]** “分析报表”以生成报表。 您最初将看到一个空白报告。

要生成包含种子数据的分析报告，请执行以下操作：

1. 在CRXDE lite的地址浏览器中，键入以下内容： `/apps/we-finance/demo-artifacts/analyticsTestData/HomeMortgageAnalyticsTestData`
1. 测试数据在左侧目录结构中被选中。
1. 多次-单击选定文件以在右侧面板中打开其内容。
1. 复制种子数据文件中的所有内容。
1. 在CRXDE中，导航到： `/content/dam/formsanddocuments/we-finance/hm-app/jcr:content/analyticsdatanode/lastsevendays`
1. 在“属性”(Properties)下的“分析数据”(Analyticsdata)字段中，粘贴种子数据文件的复制内容。
1. 现在，为“家庭抵押贷款申请表”再次生成分析报告。 您将看到包含种子数据的报告。

**抵押申请的A/B测试**

除了分析按揭贷款应用程序的性能并不断改进之外，We.Finance还利用AEM Forms与目标的集成来创建A/B测试。 它允许他们提供不同的申请表体验，并确定在表单填写和提交方面可带来更好转化率的体验。

要在AEM Forms服务器中配置目标，请参 [阅在AEM Forms中设置和集成目标](../../forms/using/ab-testing-adaptive-forms.md#set%20up%20and%20integrate%20target%20in%20aem%20forms)。

在创作实例中执行以下步骤，体验为We.Finance抵押申请表创建A/B测试：

1. 转到表 **单和文档** ，网址为https://&lt;*hostname*>:&lt;*AuthorPort*>/aem/forms.html/content/dam/formsanddocuments。

1. 单击以打开 **We.Finance文件夹** 。
1. 选择“ **应用程序”作为“家庭抵押** ”自适应表单。
1. 单击 **工具栏** 中的“更多” **，然后选择“**&#x200B;配置A/B测试”。 此时将打开“配置A/B测试”页。

1. 指定 **活动名**。
1. 从“受众”下拉列表中，选择要向其提供表单不同体验的受众。 例如， **访客使用Chrome**。
1. 在体验 **A和** B的“体验分发”字段中，按百分比指定分发，以确定体验在总受众中的分发。 例如，如果您为体验A和体验B分别指定40、60，则体验A将提供给40%的受众，其余60%将看到体验B。
1. 单击 **配置**。 将显示一个对话框，确认A/B测试的创建。
1. 单击&#x200B;**完成**。
1. 选择“ **Application for Home Mortgage** （家庭抵押申请）”自适应表单，然后单 **击“Edit（编辑）**”。 它提供了打开其中一个体验的选项。 单击 **体验B**。 表单将在编辑模式下打开。
1. 根据需要修改表单，以创建不同于默认体验A的其他体验。
1. 转到表单和文档UI，选择表单，单击“更 **多**”，然后选择 **开始A/B测试**。
1. 现在，使用以下URL在Chrome浏览器中多次打开表单：
   `https://[hostname]:[port]/content/dam/formsanddocuments/we-finance/hm-app/jcr:content?wcmmode=disabled`

   >[!NOTE]
   > 在下次打开表单之前，从浏 **览器的** cookie持久性中删除名为mbox的cookie。 您将随机看到表单的体验A和B。

1. 选择表单，单击“ **更多**”，然后单 **击“A/B测试报告”**。 由于您刚刚开始测试，因此报告中找不到太多数据。 现在，让我们提供一些种子数据，了解A/B测试报告的外观。
1. 打开CRXDE Lite并备份以下文件：/libs/fd/fmaddon/gui/components/admin/targetreport/clientlibs/targetreport/js/targetreport.js
1. 将上述文件中 `onReportLoadSuccess` 的函数定义替换为以下文件中的函数定义：/apps/we-finance/demo-artifacts/targetreport.js

   >[!NOTE]
   >
   >这些更改仅用于演示目的。 确保完成此过程后恢复文件内容。

1. 刷新您生成的报表，您将看到如下内容。 查看报告仪表板。

![ab-test-report-1](assets/ab-test-report-1.png)

要结束A/B测试，请单击报告 **仪表板上的“End A/B test** ”按钮。 此时，会显示一个对话框，提示您声明体验。 选择入选方并确认结束A/B测试。

如果您选择体验A作为获胜者，A/B测试将结束，并且今后，只有体验A将提供给所有受众，包括Chrome上的体验A。

## Microsoft Dynamics的家庭抵押应用程序演练 {#home-mortgage-application-walkthrough-with-microsoft-dynamics}

We.Finance住房抵押与Microsoft Dynamics方案涉及以下角色：

* Sarah Rose,We.Finance客户
* We.Finance Microsoft Dynamics实例的管理员

Microsoft Dynamics的家庭抵押应用程序演练演示了当参考站点使用Microsoft Dynamics进行数据集成时，We.Finance客户如何使用该站点申请家庭抵押。 该演练以Microsoft Dynamics接收的用户填写的数据结束。 在继续执行此方案之前，您需要完成We.Finance参考站点的 [Microsoft Dynamics 365家庭抵押工作流程配置](/help/forms/using/ms-dynamics-configuration-home-mortgage.md)。

### Sarah访问We.Finance网站并申请住房抵押 {#sarah-visits-we-finance-website-and-applies-for-home-mortgage-1}

莎拉·罗丝计划买一套房子，并寻找住房抵押计划。 她是We.Finance客户，因此访问We.Finance门户来探索家庭抵押优惠。 她转到“贷款”部分，在门户上查找按揭贷款计算器。 她填写详细信息，然后点击“计算我的抵押贷款”，这会返回抵押计划。

![贷款1](assets/loans1.png)![贷款2](assets/loans2.png)

抵押计算器

![loans3](assets/loans3.png)

按揭贷款计算器结果

#### 工作原理 {#how-it-works-12}

“贷款”页面上的住房抵押计算器是AEM站点页面中嵌入的自适应表单。 您可以在编辑模式下查看“贷款”页面 `https://[authorHost]:[authorPort]/editor.html/content/we-finance/global/en/loan-landing-page.html`。

嵌入式抵押计算器是自适应表单，它使用规则根据计算器字段中提供的贷款详细信息计算EMI金额。 您可以在上查看自适应表单 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/ms-dynamics/home-mortgage-calculator.html`。

#### 亲身体验 {#see-it-yourself-10}

转到We.Finance门户，单 `https://<publishHost>:<publishPort>/content/we-finance/global/en.html` 击贷 **[!UICONTROL 款]**。 在按揭贷款计算器中提供详细信息并查看结果。

### 莎拉觉得这优惠很有趣，并选择 {#sarah-finds-the-offer-interesting-and-chooses-to-apply-2}

Sarah选择申请住房抵押，然后单击“立即 **[!UICONTROL 应用”]** （在住房抵押计算器结果上）。 它打开了住房抵押申请。

如果Sarah正从其移动设备访问家庭按揭贷款应用程序，则应用程序表单将在为在移动设备上查看而优化的视图中打开。 在此视图中，应用程序表单一次呈现一个部分。 它允许Sarah在浏览应用程序表单时逐步视图和提供信息。

以下图像显示了Sarah在其移动设备上浏览家庭按揭贷款应用程序时的工作流。

![在移动设备上填写抵押申请](assets/mortgage-form-on-mobile.png)

如果Sarah从桌 **面单击** “立即应用”，则按揭申请表会打开，如下所示。 按揭贷款计算器中Sarah提供的信息预填在申请表中。 Sarah将填充其余的详细信息并单击“继 **续”**。

![按揭申请](assets/mortgage-application.png)

根据Sarah在抵押计算器中填写的信息，她会得到几个抵押计划。 她选择符合自己要求的计划并继续填写申请。 她终于签了字，提交了申请。

提交的申请将交给We.Finance批准。

![保存草稿应用程序](assets/mortgage-plans.png)

#### 工作原理 {#how-it-works-13}

“立 **即应用** ”按钮将Sarah定向到家庭抵押申请。 应用程序是自适应表单，您可以在的创作实例中查看该表单 `https://[host]:'port'/editor.html/content/forms/af/we-finance/ms-dynamics/application-for-home-mortgage.html`。

您可以在自适应表单中查看的一些主要功能包括：

* 它基于XSD模式 `homeMortgageApplication.xsd`。
* 它使用We Finance Theme B构建，用于样式设计，使用We.Finance模板构建布局。 此外，它还使用在表单标题布局中没有面板标题的布局进行移动导航。 当从移动设备打开时，它显示渐进式移动布局。 您可以在AEM作者实例的以下位置查看自适应表单中使用的模板和主题：

   * `https://[host]:'port'/libs/wcm/core/content/sites/templates.html/conf/we-finance`
   * `https://[host]:'port'/editor.html/content/dam/formsanddocuments-themes/we-finance/we-finance-theme-b/jcr:content`

* 应用程序中的第一个选项卡“入门”是动态按揭贷款计算器，它根据用户选择显示选项。 例如，“购买”和“再融资”选项的字段和值不同。 此功能是使用show-hide规则实现的。 此外，当您单击“继续”并且“计划”选项卡已初始化时，它会调用在表单数据模型中配置的Web服务，以获取和显示抵押计划。 您可以在上查看表单数据模型和配置的服务 `https://[host]:'port'/aem/forms.html/content/dam/formsanddocuments-fdm`。
* 它使用各种自适应表单组件来捕获输入并适应用户响应。 它还使用支持HTML5输入类型的电子邮件等组件。
* 它使用签名步骤组件显示完成的表单并允许在表单上进行电子签名。

建议查看表单以了解用于构建表单的模式、组件、规则、表单数据模型、表单工作流和提交操作。

### 管理员视图Microsoft Dynamics实例中提交的数据 {#the-administrator-views-the-submitted-data-in-the-microsoft-dynamics-instance}

We.Finance接收Sarah在Microsoft Dynamics实例上提交的抵押申请。 管理员点击潜在客户列中的条目以转到为Sarah Rose创建的潜在客户记录。

![msdynamicsrecord](assets/msdynamicsrecord.png)

## 家庭保险申请演练 {#home-insurance-application-walkthrough}

We.Finance家庭保险方案涉及以下人员：

* Sarah Rose,We.Finance客户
* Gloria Rios,We.Finance信用卡和抵押主管
* Frank De Costa,We.Finance保险代理

以下信息图描述了家庭保险应用程序场景的分步工作流。

![workflow_insurance](assets/workflow_insurance.png)

现在，让我们详细了解参考站点方案中的步骤，以了解AEM Forms如何帮助We.Finance实现其目标。

### Sarah从We.Finance收到新闻快讯并申请家庭保险 {#sarah-receives-a-newsletter-from-we-finance-and-applies-for-home-insurance}

莎拉·罗斯是We.Finance的住房抵押客户，希望在住房保险方面达成一笔好交易。 她访问We.Finance门户网站并探索家庭保险计划。 We.Finance将她确定为现有客户，并向她发送有针对性的电子邮件新闻稿。 Newsletter包含家庭保险优惠。

![保险时事通讯](assets/insurance-newsletter.png)

#### 工作原理 {#how-it-works-14}

发送到Sarah的Newsletter是一个自定义实施，它会触发到指定电子邮件ID的电子邮件。 新闻稿中的“立即应用”按钮链接到主页保险应用程序，该应用程序是发布实例上的自适应表单。

#### 亲身体验 {#see-it-yourself-11}

打开以下URL以触发新闻稿电子邮件。 确保替换为有 `[emailID]` 效的电子邮件帐户以接收新闻稿。 打开新闻稿，然后单 **[!UICONTROL 击立即应用]** ，以转到主页保险应用程序。

`https://[authorServer]:[authorPort]/content/campaigns/we-finance/start.html?app=ins&email=[emailID]&givenName=Sarah&familyName=Rose`

### 莎拉觉得家庭保险优惠很有趣，并选择申请 {#sarah-finds-the-home-insurance-offer-interesting-and-chooses-to-apply}

Sarah喜欢新闻快讯中的家庭保险计划，并决定申请该计划。 她单击新闻稿上的“立即申请”，该新闻稿将在We.Finance门户上打开主页保险应用程序。 应用程序表单使用卡布局按部分组织。

在“个人信息”页面上，当Sarah提供其社会安全号时，她会收到一个提示，提示她使用自己的凭据登录。

![保险SSN](assets/insurance-ssn.png)

Sarah是We.Finance的现有客户。 她使用自己的We.Finance帐户凭据登录，并且表单中会自动填充她的个人详细信息。 她继续填写并提交申请。

如果Sarah在移动设备上提交应用程序，她将浏览以下屏幕。

![移动保险形式](assets/insurance-form-on-mobile.png)

#### 工作原理 {#how-it-works-15}

新闻 **稿中的“立即申请** ”按钮将Sarah定向到We.Finance门户上的主页保险应用程序。 该应用程序是自适应表单，您可以在的创作实例中查看该表单 `https://[host]:'port'/editor.html/content/forms/af/we-finance/insurance/application-for-insurance.html`。

您可以在自适应表单中查看的一些主要功能包括：

* 它基于XSD模式 `insurance.xsd`。
* 它使用Insurance主题构建，用于样式设计，并在表单标题布局中使用没有面板标题的布局进行移动导航。 当从移动设备打开时，它显示渐进式移动布局。 您可以在上查看模 `https://[host]:'port'/libs/wcm/core/content/sites/templates.html/conf/we-finance` 板，也可以在上查看主题 `https://[host]:'port'/editor.html/content/dam/formsanddocuments-themes/we-finance/insurance/jcr:content`。

* 它包括自适应表单规则，用于调用表单数据模型服务以预填已登录用户的用户详细信息。 它还调用服务，按社会保险号或表单中提供的电子邮件地址预填信息。 您可以在查看表单数据模型及其服务 `https://[host]:'port'/aem/forms.html/content/dam/formsanddocuments-fdm`。
* 它使用各种自适应表单组件来捕获输入并适应用户响应。 它还使用支持HTML5输入类型的电子邮件等组件。
* “保存我的进度”按钮为用户生成唯一的ID，并将部分填充的应用程序另存为AEM存储库中的某个节点中的草稿。 此外，它还显示一个对话框，请求获得发送电子邮件的权限，该电子邮件包含指向包含草稿应用程序的节点的链接。 确认对话框上的“发送邮件”按钮会触发一封电子邮件，其中包含指向包含草稿的节点的链接。
* 它使用调用AEM工作流提交操作来触发主保险批准工作流。 您可以在以下位置查看此表单中使用的工作流： `https://[host]:'port'/editor.html/conf/global/settings/workflow/models/we-finance-insurance-workflow.html`

建议查看表单以了解用于构建表单的模式、组件、规则、表单数据模型、表单工作流和提交操作。

另外，请参阅以下文档，了解有关家庭保险应用程序自适应表单中使用的功能的更多信息：

* [自适应表单创作简介](../../forms/using/introduction-forms-authoring.md)
* [使用XML模式创建自适应表单](../../forms/using/adaptive-form-xml-schema-form-model.md)
* [规则编辑器](../../forms/using/rule-editor.md)
* [主题](../../forms/using/themes.md)
* [数据集成](../../forms/using/data-integration.md)
* [在自适应表单中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [OSGi上以表单为中心的工作流程](../../forms/using/aem-forms-workflow.md)

#### 亲身体验 {#see-it-yourself-12}

单击 **您在电子邮件中收到的Newsletter上的“立即应用** ”按钮。 或者，也可以转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/all-forms.html` 单击保险 **[!UICONTROL 申请]** (Apply)。 在“社 `123456789` 会保险编号”字段中指定。 出现提示时，请使用 `srose/srose` 用户名／密码登录。

填写详细信息，浏览各种自适应表单组件，并提交应用程序。 您可以在上查看自适应表单 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/insurance/application-for-insurance.html`。

### We.Finance批准申请并签署合同 {#we-finance-approves-the-application-and-a-contract-is-signed}

We.Finance收到Sarah提交的家庭保险申请。 任务分配给Gloria Rios。 她会在自己的AEM收件箱中审阅应用程序并批准它。

![insurance inbox-grios](assets/insurance-inbox-grios.png)

当Gloria批准Sarah的家庭保险申请时，Frank De Costa的AEM收件箱中会创建一个任务。 Frank评论任务。 他为莎拉准备了一份家庭保险单合同，将合同附在她的申请上，并寄给莎拉签订合同。 下面在代理UI中显示的合同是交互式通信的打印版本。

![保险联系信](assets/insurance-contact-letter.png)

Sarah会收到一封电子邮件，其中包含用于签署家庭保险单合同的链接。 Sarah审查并签署合同。

![保险合同电子邮件](assets/insurance-contract-email.png)

#### 工作原理 {#how-it-works-16}

当Sarah提交主页保险申请时，将触发一个Forms Workflow，并在Gloria的AEM收件箱中创建一个任务。 当Gloria审阅并批准该应用程序时，任务将分配给Frank De Costa。 从一个人物到另一个人物的任务流在与保险应用程序关联的AEM工作流中定义。 有关工作流的更多信息，请参 [阅OSGi上以表单为中心的工作流](../../forms/using/aem-forms-workflow.md)。

下图描述了与保险应用程序关联的AEM工作流。

![we-finance-insurance-workflow-model](assets/we-finance-insurance-workflow-model.png)

Frank用信函管理来准备一份家庭保险单合同。 他下载合同PDF并将其附加到Sarah的应用程序，然后单击“发送合同”。 该工作流会触发一封邮件，发送给Sarah，邮件中附有家庭保险单合同供签署。

#### 亲身体验 {#see-it-yourself-13}

执行以下操作：

1. 转到AEM收件箱， `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`然后以Gloria角色的用 `grios/grios` 户名口令身份登录。 批准Sarah的家庭保险申请任务。

1. 然后，以Frank角色的用户 `fdcosta/password` 名密码身份登录AEM收件箱。 视图任务。
1. 现在，转到并 `https://[authorHost]:[authorPort]/aem/forms.html/content/dam/formsanddocuments/we-finance/insurance` 预览HomeInsuranceWelcomeKit的字母模板。
1. 在“数据”面板中指定信息。 单击 **[!UICONTROL 预览]** ，然后将PDF下载到本地文件系统。 确保PDF文件以contract.pdf文件名保存。
1. 转到Frank的AEM收件箱，打开任务，附加下载的合同PDF，然后单击“发送合 **[!UICONTROL 同”]**。
1. 打开包含合同的电子邮件并签署文档。

### Sarah收到一个欢迎工具包 {#sarah-receives-a-welcome-kit}

当莎拉签署家庭保险合同时，她收到一封包含保单详情的电子邮件。

![保险单详细信息](assets/insurance-policy-details.png)

不久，她又收到了来自We.Finance的一封电子邮件，其中附有她的保险单的欢迎信件。 从欢迎工具包中，莎拉可以查阅她的政策文档和视图声明。

![保险欢迎包](assets/insurance-welcome-kit.png)

#### 亲身体验 {#see-it-yourself-14}

如果您在应用程序中指定了电子邮件ID，您会收到一封电子邮件，其中包含指向欢迎工具包的链接。 单击“ **[!UICONTROL 我的欢迎工具包]** ”以打开欢迎工具包。

![保险——欢迎——包——电子邮件](assets/insurance-welcome-kit-email.png)

## 理财说明书演练 {#wealth-management-prospectus-walkthrough}

We.Finance Wealth Management情景包含以下角色：

* Sarah Rose,We.Finance客户

财富管理演练展示了We.Finance客户如何利用这个网站来了解共同基金——蓝筹增长基金。 该参考站点使用交互式通信来显示有关该基金的信息。 该信息可以同时以Web和PDF格式提供。 演练的最后，客户将PDF版本的信息通过电子邮件发送给她的兄弟。

下图显示了财富管理演练的工作流：

![财富管理——招股说明书漫游](assets/wealth-management-prospectus-walkthrough.png)

### 莎拉访问We.Finance网站并打开Blue Chip Growth Fund招股说明书 {#sarah-visits-we-finance-website-and-opens-the-blue-chip-growth-fund-prospectus}

莎拉·罗丝正计划投资一只共同基金。 她是We.Finance的现有客户，因此访问We.Finance门户以探索可用的共同基金。 她进入财富管理部，打开We.Finance Blue Chip Growth Fund的页面。 本页包含有关招股说明书的链接，其中包含有关当前和历史价格、月度业绩、按行业分类的多样化、费用、费用、税金的详细信息，以及更多有关这些基金的信息。

![slide1](assets/slide1.png)

#### 工作原理 {#how-it-works-17}

蓝筹增长基金的招股说明书是一种互动沟通。 它使用文本、图像、图表和表组件(文档片段)来显示产品摘要、股票风格、基金业绩、基金详细信息和其他相关信息。 您可以在以下位置在编辑模式下查看交互式通信： `https://[authorHost]:[ authorPort]/editor.html/content/forms/af/we-finance/wealth-management/wealth-management/channels/web.html`

图表和表从表单数据模型检索数据。 表单数据模型连接到配置的数据源，即本演练中的数据库，以检索特定于基金的信息。 您可以在 `https://[authorHost]:[authorPort]/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/we-finance/wealth-management`

#### 亲身体验 {#see-it-yourself-15}

访问We.Finance门户，点击Wealth Management, `https://[publishHost]:[publishPort]/wefinance`按资产类别展开Funds，然后点击We.Finance Blue Chip Growth Fund。 We.Finance Blue Chip Growth Fund招股说明书开始。

### Sarah探索Blue Chip Growth Fund招股说明书，了解该基金 {#sarah-explores-the-blue-chip-growth-fund-prospectus-to-learn-about-the-fund}

Sarah探索了招股说明书的“概述”、“价格和绩效”、“组合管理”、“费用和最低限额”和“税金和付款”标签，以了解当前和历史价格、历史增长、与标普500指数的比较、按行业分散、基金管理人以及与基金相关的开支。 相关信息被分隔到不同的标签中。 招股说明书是一种互动沟通。 交互式通信具有响应式设计。 她可以在任何屏幕尺寸的设备上打开交互式通信，而交互式通信会重排设计以适合底层设备。

![slide1-1](assets/slide1-1.png)

#### 工作原理 {#how-it-works-18}

蓝筹成长基金互动通讯使用母板和子面板将相关信息分成不同部分。 父面板将所有子面板组织到选项卡中。

将父选项卡的布局设置为顶部的选项卡，以将所有子面板转换为选项卡。 您可以在的编辑模式下查看交互式通信的面板 `https://[authorHost]:[ authorPort]/editor.html/content/forms/af/we-finance/wealth-management/wealth-management/channels/web.html`。

#### 亲身体验 {#see-it-yourself-16}

访问Blue Chip Growth Fund的交互式通信 `https://[publishHost]:[ publishPort]/content/forms/af/we-finance/wealth-management/wealth-management/channels/web.html?wcmmode=disabled`。 浏览所有选项卡。

### Sarah视图和电子邮件：PDF版蓝筹基金页面 {#sarah-views-and-emails-the-pdf-version-of-the-blue-chip-growth-fund-page}

萨拉周末要去乡下。 她计划与哥哥讨论蓝筹基金。 她的哥哥在一家银行工作，并帮助她做出与金融相关的决策。 Sarah在笔记本电脑上下载了PDF版蓝筹基金页面，供脱机阅读。 她还通过电子邮件将PDF版本副本发送给哥哥。

![blue-chip-pdf](assets/blue-chip-pdf.gif)

#### 工作原理 {#how-it-works-19}

蓝筹增长基金的招股说明书是一种互动沟通。 它具有Web和PDF渠道。 交互式通信与AEM工作流集成，通过电子邮件发送PDF版本。 您可以在上查看工作流模型 `https://[authorHost]:[ authorPort]/editor.html/conf/global/settings/workflow/models/wealthmanagement.html`。

![财富管理](assets/wealth-management.png)

#### 亲身体验 {#see-it-yourself-17}

要下载PDF版本，请转到Blue Chip Growth Fund交互通信，点 `https://[publishHost]:[ publishPort]/content/forms/af/we-finance/wealth-management/wealth-management/channels/web.html`按下载PDF。

要通过电子邮件发送PDF，请转到Blue Chip Growth Fund交互式通信，点 `https://[publishHost]:[ publishPort]/content/forms/af/we-finance/wealth-management/wealth-management/channels/web.html`按EMAIL PDF。 指定 **全名** 和电 **子邮件地址**。 单击“ **发送电子邮件**”。

## 汽车保险申请演练 {#auto-insurance-application-walkthrough}

We.Finance汽车保险应用方案涉及以下角色：

* Sarah Rose,We.Finance客户
* Conrad Simms,We.Finance保险代理

Sarah Rose是We.Finance的现有客户，已购买汽车保险单。 现在是每年续订她的保险单的时候。 We.Finance保险代理的康拉德·西姆斯向莎拉发送了她的保单续签通知。 提醒电子邮件包含一个PDF，其中包含策略续订详细信息以及指向交互式通信的Web版本的链接。 交互式通信具有适合移动设备的响应式设计。 她可以在任何设备上打开交互式通信，并且交互通信会重排以适合底层设备的屏幕大小。 附加到电子邮件的PDF版本的交互式通信对脱机阅读很有帮助。

Sarah按照电子邮件中提供的说明操作，并成功地重新发布了该过程。 下图显示了自动保险应用程序演练的工作流： 自 ![动保险申请演练](assets/auto-insurance-application-walkthrough.png)

### 康拉德向We.Finance发送了保险单续订通讯 {#conrad-sends-an-insurance-policy-renewal-communication-from-we-finance}

Conrad登录AEM实例，打开“自动保险仪表板”，指定Sarah的 **客户ID**，然后单击“ **续订策略”**。 此时 **将打开代理UI** ，其中显示Sarah Rose已填写的策略详细信息。 Conrad指定了Sarah的电子邮件地址，并单击“提 **交”**。 Sarah会收到一封电子邮件，其中包含“您 **的汽车保险续订”主题**。

![cc-仪表板](assets/cc-dashboard.png)

#### 工作原理 {#how-it-works-20}

保险单续签通信是一种交互通信。 Conrad Simms使用代理UI将保险单续订通信发送给Sarah。 通信包括打印(PDF)和指向交互通信的Web渠道的链接。 交互式通信使用AEM Workflow发送电子邮件。 您可以在 `https://[authorHost]:[ authorPort]/editor.html/conf/global/settings/workflow/models/we-finance-auto-insurance-renewal.html`

![自动保险工作流](assets/auto-insurance-workflow.png)

#### 亲身体验 {#see-it-yourself-18}

以Conrad Simms(csimms/ **password)的身份登录We.Finance Auto Insurance仪表板** 。 URL为 `https://[publishhost]:[publishport]/content/we-finance/global/en/login.html?resource=/content/we-finance/ccdashboard.html`。 指定客 **户ID**。 Sarah Rose的客户ID为900001。 单击“ **续订策略**”。 交互式通信在代理UI中打开。 在代理UI中，输入有效的电子邮件地址以发送附加了策略文档的电子邮件，然后单击“提 **交”**。 屏幕上会显示一条消息“已启动提交”，然后在几秒内会显示另一条消息“已成功提交”。 一封电子邮件，主题为“ **您的自动保险续订** ”，并会在指定的电子邮件地址发送。 萨拉·罗斯的政策是优惠政策。

汽车保险演练中还包含另一位客户艾莉森·琼斯。 Alison Jones的客户ID为900002。 当您将交互式通信发送给Alison Jones时，会发送标准策略。 标准和高级策略的区别在于：

* 高级策略有横幅图像，标准策略只有地址块下方的文本。
* 标准政策的成本低于高级政策。
* 优惠政策有防盗奖励，标准政策有明智的骑乘奖励

这两个策略都使用相同的交互式通信。 策略中的部分会根据策略类型条件进行更改或隐藏。 您可以直接从 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal`

**将Microsoft Dynamics用作数据源**

该参考站点还提供交互式通信，该通信使用Microsoft Dynamics作为表单数据模型的数据源。 请执行以下步骤以配置用于自动保险演练的交互式通信：

1. 登录到 `https://[author]:'port'/crx/de as an administrator`。
1. Open the `/apps/we-finance/components/ccrui/ccrui.jsp`file.
1. Set the value of `FormFieldRequestParameter`to `/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal-dynamics`
1. 点按 **全部保存**。 该参考站点被配置为使用使用MS Dynamics作为数据源的交互通信。

现在，以Conrad Simms(csimms/ **password)的身份登录We.Finance汽车保险仪表板** 。 URL为 `https://[publishhost]:[publishport]/content/we-finance/global/en/login.html?resource=/content/we-finance/ccdashboard.html`。 指定客 **户ID**。 Sarah Rose的客户ID为900001。 单击“ **续订策略**”。 交互式通信在代理UI中打开。 在代理UI中，输入有效的电子邮件地址以发送附加了策略文档的电子邮件，然后单击“提 **交”**。 屏幕上会显示一条消息“已启动提交”，然后在几秒内会显示另一条消息“已成功提交”。 以您的自动保险续 **订为主题的电子邮件** ，将在指定的电子邮件地址发送。

>[!NOTE]
>
>当您使用使用Microsoft Dynamics作为数据源的交互式通信时，发送到Sarah的电子邮件中的链接指向不使用Microsoft Dynamics的交互式通信。 要修复此问题，请手动更改电子邮件模板中的链接。

![agent_ui_email](assets/agent_ui_email.png)

### Sarah收到We.Finance发来的保险单续订通信，并决定续订 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封来自We.Finance的附件电子邮件，提醒她，她的汽车保险政策即将到期。 附件是其汽车保险单续订详细信息的打印版本。

Sarah单击 **“立即续签** ”，并转到Web版的汽车保险信。 在这封信的上面，莎拉找到了她的政策到期的剩余天数。 该页为Sarah提供了有关其保险单详细信息（如保单编号、到期金额）的概述，以及折扣优惠和忠诚度奖励等其他信息。 Sarah再次单 **击策略底部的** “立即续订”。

![自动保险续签电子邮件](assets/auto-insurance-renewal-email.png)

#### 工作原理 {#how-it-works-21}

您的自动保险信的Web和打印输出是使用Interactive Communications的多渠道功能创建的。 电&#x200B;**子邮件中的“立即续订** ”按钮链接到自动保险续订应用程序，该应用程序是发布实例上的交互式通信。

![ic-web版本](assets/ic-web-version.png)

#### 亲身体验 {#see-it-yourself-19}

您必须已收到附有PDF的电子邮件。 PDF是您的汽车保险书的印刷版。 单击 **立即续订** ，以访问Web版本的策略。 查看您的个人信息和策略详细信息，然后单击“ **立即续订**”。 您需要使用自适应表单进行付款。

电 **子邮件中的** “立即续订”按钮将Sarah定向到策略的Web版本。 您可以访问以下URL:

`https://[publishServer]:[publishPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=900001`

您可以查看汽车保险续订的详细摘要，然后单击页 **面底部的** “立即续订”。

### Sarah打开付款页面并进行付款并完成此流程 {#sarah-opens-the-payment-page-and-makes-the-payment-and-completes-the-process}

当Sarah在交 **互式通信的Web版本上单击** “立即续订”时，将打开付款页面。 Sarah会重新检查其政策编号和到期日期，并保留其记录。 在页面右侧，她以总金额的10%溢价折扣检查续订的“付款摘要”。 Sarah填写她的信用卡详细信息并单击“ **付款”**。

![支付自适应表单](assets/payment-adaptive-form.png)

#### 工作原理 {#how-it-works-22}

“立即续签”按钮将Sarah引导到付款页面。 付款页面是自适应表单。 Sarah会填写信用卡详细信息并单击“提 **交”**。 系统将处理她的信用卡付款，并在屏幕上显示自适应表单中配置的感谢信。

#### 亲身体验 {#see-it-yourself-20}

单击 **立即续订** ，以访问付款页面。 填写您的信用卡信息，然后单击“ **付款”**。 您可以通过以下网址访问创作实例中的付款页面：

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=900001`

单击“付款”按钮后，将显示感谢信。
