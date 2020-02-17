---
title: 员工招聘参考站点演练
seo-title: 员工招聘
description: AEM Forms参考站点展示组织如何使用AEM Forms功能来实施员工招聘工作流。
seo-description: AEM Forms参考站点展示组织如何使用AEM Forms功能来实施员工招聘工作流。
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 员工招聘参考站点演练 {#employee-recruitment-reference-site-walkthrough}

## 入门项目 {#prerequisite}

按照设置和配置AEM Forms引用站 [点中的说明设置引用站点](/help/forms/using/setup-reference-sites.md)。

## 概述 {#overview}

We.Finance是一个组织，允许候选人通过参考站点门户申请就业。 该组织还使用门户管理候选人的面试安排、入围和内部沟通。 该站点管理以下内容：

* 搜索和申请工作的候选人
* 筛选和候选人入围
* 面试流程
* 候选详细信息的集合
* 候选背景检查
* 向选定候选人推出选件

>[!NOTE]
>
>We.Finance和We.Gov参考站点均提供员工招聘用例。 演练中使用的示例、图像和说明使用We.Finance参考站点。 但是，您也可以使用We.Gov运行这些使用案例和检查对象。 为此，请在 **上述URL中将****we-finance替换为we-gov** 。

### 涉及的工作流模型 {#workflow-models-involved}

员工招聘用例涉及两个工作流：

* 面谈前——我们为员工招聘提供财务服务工作流
* 面试后——我们为员工招聘提供财务资助面试后工作流程

这些工作流是在AEM中创建的，可在以下位置找到：

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### We Finance员工招聘工作流 {#we-finance-employee-recruiting-workflow}

以下是本文档中遵循的“We Finance员工招聘”工作流的模型。

![we-finance-employee-recluiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### We Finance Employee Recluation Post Accession工作流 {#we-finance-employee-recruiting-post-interview-workflow}

以下是本文档中遵循的“我们财务员工面试后招聘”工作流程的模型。

![我们的财务——员工——招聘——面试——后工作流程](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 角色 {#personas}

此方案涉及以下角色：

* 莎拉·罗丝，该组织的求职者
* 招聘人员约翰·雅各布斯
* 招聘经理格洛丽亚·里奥斯
* John Doe，人力资源部

## 莎拉申请工作 {#sarah-applies-for-a-job}

莎拉·罗丝正在组织里寻找工作机会。 她访问他们的网站，并探索“职业”页面上列出的职位空缺。 她找到一份匹配的工作清单并申请。

![主页](assets/home-page.png)

We.Finance主页

![职业页面](assets/career-page.png)

We.Finance职业页面

Sarah单击“在工作发布时应用”。 作业申请表将打开。 她填写应用程序中的所有详细信息并提交它。

![作业——应用程序——表单](assets/job-application-form.png)

### 工作原理 {#how-it-works}

We.Finance主页和职业页面是AEM Sites页面。 职业页面嵌入了自适应表单，该表单使用可重复的面板来使用服务获取职位空缺并在页面上列出这些空缺。 您可以在上查看自适应表单 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`。

### 亲身体验 {#see-it-yourself}

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` 单击“ **[!UICONTROL 职业”]**。 单击 **[!UICONTROL 搜索]** ，以填充作业列表，然后单 **[!UICONTROL 击应用]** 作业。 在表单中填写详细信息并提交申请。

请确保在应用程序中指定有效的电子邮件ID，因为通过此演练进行的任何通信都将发送到指定的电子邮件ID。

## 约翰·雅各布斯将莎拉·罗丝的招聘经理简介列入名单 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

组织收到Sarah提交的工作申请。 招聘人员约翰·雅各布斯被指派负责审查莎拉的个人资料。 他在AEM收件箱中查看任务，找到与作业要求匹配的配置文件，然后单击入选名单。 莎拉的个人资料被转发给招聘经理格洛丽亚·里奥斯，供她审批。

![jacobs-inbox-1](assets/jjacobs-inbox-1.png)

John的AEM收件箱

![候选人名单](assets/candidate-shortlist.png)

约翰·雅各布斯将莎拉·罗丝的招聘经理简介列入名单

**工作原理**

作业申请表中的提交操作会触发一个工作流，该工作流在John Jacob的收件箱中创建一个任务以筛选申请。 当John审核并入围应用程序时，该工作流会在招聘经理Gloria的收件箱中创建一个任务。

### 亲身体验 {#see-it-yourself-1}

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`使用jacobs/password作为John Jacobs的用户名／密码登录。 打开“候选人配置文件复查”任务并列出申请人。

## Gloria审阅申请并批准申请人进行面试 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

招聘经理Gloria在其AEM收件箱中接收入围的配置文件作为任务。 她审核了这个问题，并批准了候选人莎拉·罗丝的采访。

![glorialinbox](assets/gloriainbox.png)

Gloria的AEM收件箱

![荣耀的日程安排采访](assets/gloriaschedulesinterview.png)

格洛丽亚批准莎拉·罗丝接受采访

**工作原理**

当Gloria批准候选人进行面试时，该工作流会在John Doe的AEM收件箱中创建一个任务，John Doe是We.Finance的招聘人员。

### 亲身体验 {#see-it-yourself-2}

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用jacobs/password作为John Jacobs的用户名／密码登录。 打开“候选人配置文件复查”任务并列出申请人。

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用grios/password作为Gloria Rios的用户名／密码登录。 打开“候选人配置文件审核”任务，然后单击“计划访谈”。

## John Doe安排了一次面试 {#john-doe-schedules-an-interview}

John Doe在其收件箱中接收安排面试的任务。 John Doe选择并打开该任务，并将面试日期、时间、地点以及负责面试的HR人员定为John Jacob。 John Doe单击“发送邀请电子邮件”。 向萨拉发送了一封电子邮件，并指派了招聘经理Gloria负责面试莎拉。

![johnjacosaeminbox](assets/johnjacobsaeminbox.png)

John Doe的AEM收件箱

![约翰斯切杜威采访](assets/johndoescheduleinterview.png)

无名氏安排面试时间，并将细节发给莎拉·罗斯

## 莎拉·罗丝收到电子邮件，询问时间表 {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose收到电子邮件，其中包含面试日程、地点和其他详细信息。 她单击“接受”表示她对面试日程和地点不满意。 在准确信息的指引下，Sarah参加了采访。

![萨拉赫罗斯受访者邮件](assets/sarahroseinterviewemail.png)

莎拉·罗丝收到面试日程

## 面试结束后，招聘经理将莎拉·罗丝列入候选名单 {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

在Sarah rose完成面试并清除面试后，招聘经理Gloria Rios从其收件箱中打开“候选人选择”任务，然后单击“选择”。 Gloria Rios的决定将传达给人力资源部门负责人John Doe，以便进一步处理。

![gloriasinboxoffer](assets/gloriariosinboxoffer.png)

Gloria的AEM收件箱

![gloriasselectandiate](assets/gloriariosselectcandidate.png)

格洛丽亚·里奥斯在采访后选择了莎拉·罗斯

## John Doe请求更多信息 {#john-doe-requests-more-information}

在要求候选人加入组织之前，需要检查她的背景。 John Doe打开并审阅选定申请人的详细信息，并发现她的某些工作和教育详细信息尚未填写。 John Doe单击“需要更多信息”。

![johndoeinbox](assets/johndoeinbox.png) johndoeneed更多 ![信息](assets/johndoeneedmoreinformation.png)

John Doe向Sarah rose索取有关她的教育和工作经验的更多信息

## Sarah Rose收到一封电子邮件，请求进一步的信息 {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose收到一封电子邮件，通知她需要进一步的信息才能处理她的就业申请。 电子邮件中包含一个指向表单的链接，用于填写所需信息。

![sarahroseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose收到一封电子邮件，通知需要进一步的信息才能处理她的就业申请

Sarah单击电子邮件中的“提供详细信息”链接。 此时会显示一个表单。 Sarah会按John Doe的要求填写所需的教育和就业详细信息，然后单击“提交”。

![additionalinformation1](assets/additionalinformation1.png)

Sarah通过单击电子邮件中的链接打开其他信息表单

![additionalinformation2](assets/additionalinformation2.png)

Sarah会根据John Doe的请求填充其他信息，然后单击“提交”

## John Doe会查看选定的候选人配置文件，以获取所提供的其他信息 {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe选择候选审阅请求并打开它。 John Doe发现Sarah根据需要填写了所有信息。 审核应用程序后，John Doe单击“批准”。 经John Doe批准，对Sarah rose进行背景调查的请求将转发给John Jacobs。

![johndoeadditioninformationinbox](assets/johndoeadditionainformationinbox.png)

John Doe的AEM收件箱

![johndoeadditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe审阅Sarah提供的其他信息并批准该信息

## 约翰·雅各布斯收到背景检查请求 {#john-jacobs-receives-a-background-check-request}

约翰·雅各布斯在收件箱中看到了背景支票申请。 约翰·雅各布斯开启了这项任务，并审阅了莎拉·罗丝提供的信息。 在执行背景检查后，John Jacobs单击“继续”以表示背景检查已成功。

![johjacobsbackgroundcheckbox](assets/johnjacobsbackgroundcheckinbox.png)

John Jacobs的AEM收件箱

![johnjacobsbackgroundcheckhead](assets/johnjacobsbackgroundcheckgoahead.png)

在执行背景检查后，John Jacobs单击“继续”

## 无名氏把加入信寄给莎拉·罗丝 {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe在其AEM收件箱中收到发送加入信函的请求。 John打开请求并查看详细信息。 John Doe附加了加入函PDF，然后单击“附加并发送加入函”。

![johndojoiningletterinbox](assets/johndoejoiningletterinbox.png)

John Doe的AEM收件箱

![johndojoiningletteratachandsend](assets/johndoejoiningletterattachandsend.png)

John Doe发出加入函，请签署

## 莎拉·罗斯收到并签署了联系信 {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose收到签署的加入信。 Sarah单击此处查看并签署加入信。 将打开加入字母PDF，其中包含一个用于签署文档的字段。

![sarahrosejoingletteremail](assets/sarahrosejoiningletteremail.png)

Sarah Rose收到签署的加入信

Sarah可以选择输入、使用绘图进行手写、插入签名图像，或使用手机的触摸屏绘制她的签名。 Sarah键入她的姓名，单击“单击以签名”，然后下载加入信函的签名副本。

![纱拉罗丝连接信笺](assets/sarahrosejoininglettersign.png)

Sarah在她的姓名中输入，在联系信上签字

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah单击“单击以签名”以完成对加入信函的签名

