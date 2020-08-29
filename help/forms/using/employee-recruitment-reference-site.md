---
title: 员工招聘参考站点演练
seo-title: 员工招聘
description: AEM Forms参考站点展示组织如何使用AEM Forms功能实施员工招聘工作流程。
seo-description: AEM Forms参考站点展示组织如何使用AEM Forms功能实施员工招聘工作流程。
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# 员工招聘参考站点演练 {#employee-recruitment-reference-site-walkthrough}

## 概述 {#overview}

We.Finance是一个组织，允许候选人通过参考网站申请就业。 该组织还使用门户管理候选人的面试安排、入围和内部沟通。 该站点管理以下内容：

* 搜索和申请工作的候选人
* 候选人的筛选和入围
* 面试流程
* 候选详细信息集合
* 候选背景检查
* 将优惠转出给选定候选人

>[!NOTE]
>
>We.Finance和We.Gov参考站点均提供员工招聘用例。 演练中使用的示例、图像和说明使用We.Finance参考站点。 但是，您也可以使用We.Gov运行这些用例和检查项目。 为此，请在 **上述URL中****将we-finance** 替换为we-gov。

### 涉及的工作流模型 {#workflow-models-involved}

员工招聘用例涉及两个工作流:

* 面试前——我们财务员工招聘工作流
* 面试后- We Finance Employee Recruiting Post面试工作流

这些工作流在AEM中创建，可在以下位置找到：

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### We Finance员工招聘工作流 {#we-finance-employee-recruiting-workflow}

以下是此文档中遵循的We Finance员工招聘工作流的模型。

![we-finance-employee-recruiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### We Finance员工招聘后面试工作流 {#we-finance-employee-recruiting-post-interview-workflow}

以下是此文档中遵循的We Finance员工职位面试招聘工作流的模型。

![we-finance-employee-recuration-post-apt-assion-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 角色 {#personas}

此方案涉及以下角色：

* 莎拉·罗丝，该组织的求职者
* 招聘人员约翰·雅各布斯
* Gloria Rios，招聘经理
* John Doe,HR人员

## 莎拉申请工作 {#sarah-applies-for-a-job}

莎拉·罗斯正在组织里寻找工作机会。 她访问他们的门户网站，并探索“职业”页面上列出的职位空缺。 她找到一份匹配的工作清单并申请。

![主页](assets/home-page.png)

We.财务主页

![职业页面](assets/career-page.png)

We.Finance职业页面

Sarah单击“在工作发布时应用”。 作业申请表将打开。 她填写应用程序中的所有详细信息并提交它。

![作业——应用程序——表单](assets/job-application-form.png)

### 工作方式 {#how-it-works}

We.Finance主页和职业页面是AEM Sites页面。 职业页面嵌入一个自适应表单，该表单使用可重复的面板通过服务获取职位空缺并在页面上列表这些空缺。 您可以在查看自适应表单 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`。

### 亲自查看 {#see-it-yourself}

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` 单击“ **[!UICONTROL 职业]**”。 单击 **[!UICONTROL “搜索]** ”以填充作业列表，然后单 **[!UICONTROL 击]** “应用作业”。 在表单中填写详细信息并提交申请。

请确保在应用程序中指定有效的电子邮件ID，因为通过此演练的任何通信都将发送到指定的电子邮件ID。

## 约翰·雅各布入围了莎拉·罗丝的招聘经理用户档案 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

组织接收Sarah提交的工作申请。 招聘人员约翰·雅各布斯被指派负责审查莎拉的用户档案。 他在AEM收件箱中查看任务，找到与工作要求匹配的用户档案，然后单击“入围名单”。 莎拉的用户档案被转发给招聘经理格洛丽亚·里奥斯，请她批准。

![jacobs-inbox-1](assets/jjacobs-inbox-1.png)

John的AEM收件箱

![候选人名单](assets/candidate-shortlist.png)

约翰·雅各布入围了莎拉·罗丝的招聘经理用户档案

**工作方式**

作业申请表中的提交操作会触发一个工作流，该工作流会在John Jacob的收件箱中创建一个用于筛选申请的任务。 当John审核和入围应用程序时，该工作流会在招聘经理Gloria的收件箱中创建任务。

### 亲自查看 {#see-it-yourself-1}

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`使用jacobs/password作为John Jacobs的用户名／密码登录。 打开“候选用户档案复查”任务并列出申请人。

## 格洛丽亚审阅申请并批准申请人进行面试 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

招聘经理Gloria在其AEM收件箱中收到入围用户档案，作为任务。 她审核了这个问题，并批准了候选人莎拉·罗丝的采访。

![gloriabox](assets/gloriainbox.png)

Gloria的AEM收件箱

![格洛里斯·米歇尔访谈](assets/gloriaschedulesinterview.png)

格洛丽亚批准莎拉·罗丝接受采访

**工作方式**

当Gloria批准候选人进行面试时，该工作流会在John Doe的AEM收件箱中创建一个任务,John Doe是We.Finance的招聘人员。

### 亲自查看 {#see-it-yourself-2}

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用jacobs/password作为John Jacobs的用户名／密码登录。 打开“候选用户档案复查”任务并列出申请人。

转到并 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 使用grios/password作为Gloria Rios的用户名／密码登录。 打开“候选人用户档案审阅”任务并单击“计划面试”。

## 无名氏计划采访 {#john-doe-schedules-an-interview}

John Doe在其收件箱中收到安排面试的任务。 John Doe选择并打开任务，并将面试日期、时间、地点以及负责面试的HR人员定义为John Jacob。 John Doe单击“发送邀请电子邮件”。 向莎拉发送了一封电子邮件，还为招聘经理格洛丽亚分配了一名任务，负责采访莎拉。

![johnjacabsaeminbox](assets/johnjacobsaeminbox.png)

John Doe的AEM收件箱

![johndoescheduperience](assets/johndoescheduleinterview.png)

John Doe计划访谈，并将详细信息发送给Sarah Rose

## 莎拉·罗丝收到电子邮件，询问计划 {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose收到电子邮件，其中包含面试计划、地点和其他详细信息。 她单击“接受”，表示她可以接受面试计划和场所。 在准确信息的指引下，Sarah参加了采访。

![萨拉赫罗塞受访者邮件](assets/sarahroseinterviewemail.png)

莎拉·罗斯接受采访计划

## 面试结束后，招聘经理的入围者莎拉·罗丝 {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

在Sarah Rose完成访谈并清除这些访谈后，招聘经理Gloria Rios从收件箱中打开“候选人选择”任务，然后单击“选择”。 Gloria Rios的决定被传达给人力资源主管John Doe，供进一步处理。

![格洛里亚辛博克斯](assets/gloriariosinboxoffer.png)

Gloria的AEM收件箱

![美丽选择候选者](assets/gloriariosselectcandidate.png)

格洛丽亚·里奥斯在采访后选择莎拉·罗斯

## John Doe请求更多信息 {#john-doe-requests-more-information}

在要求候选人加入组织之前，需要检查她的背景。 John Doe打开并查看选定申请人的详细信息，发现她的一些工作和教育细节尚未填写。 John Doe单击“需要更多信息”。

![johndoeiboxjohndoened](assets/johndoeinbox.png)![更多信息](assets/johndoeneedmoreinformation.png)

John Doe向Sarah Rose索取有关她的教育和工作经验的更多信息

## Sarah Rose收到一封电子邮件，请求进一步的信息 {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose收到一封电子邮件，通知她需要进一步的信息才能处理她的就业申请。 该电子邮件包含一个指向表单的链接，用于填写所需的信息。

![sarhoeseemailmore详细信息](assets/sarahroseemailmoredetails.png)

Sarah Rose收到一封电子邮件，通知需要进一步的信息才能处理她的就业申请

Sarah单击电子邮件中的“提供详细信息”链接。 将显示一个表单。 Sarah会按照John Doe的要求填写所需的教育和就业详细信息，然后单击“提交”。

![additionalinformation1](assets/additionalinformation1.png)

Sarah通过单击电子邮件中的链接打开其他信息表单

![additionalinformation2](assets/additionalinformation2.png)

Sarah会根据John Doe的请求填充其他信息，然后单击“提交”

## John Doe会查看选定的候选用户档案，以了解所提供的附加信息 {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe选择候选审阅请求并打开它。 John Doe发现Sarah已根据需要填写所有信息。 审核应用程序后，John Doe单击“批准”。 经John Doe批准，对Sarah Rose进行背景调查的请求将转发给John Jacobs。

![johndoeadditioninformationinbox](assets/johndoeadditionainformationinbox.png)

John Doe的AEM收件箱

![johndoeadditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe审阅Sarah提供的其他信息并予以批准

## 约翰·雅各布收到背景支票请求 {#john-jacobs-receives-a-background-check-request}

约翰·雅各布斯在收件箱中看到了背景支票申请。 约翰·雅各布斯在任务上发表文章，评论莎拉·罗丝提供的信息。 执行背景检查后，John Jacobs点击Go Ahead以表示背景检查已成功。

![johnjacobsbackgroundcheckbox](assets/johnjacobsbackgroundcheckinbox.png)

约翰·雅各布的AEM收件箱

![johnjacobsbackgroundcheckhead](assets/johnjacobsbackgroundcheckgoahead.png)

执行背景检查后，John Jacobs点击“继续”

## 无名氏把加入信寄给莎拉·罗丝 {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe在其AEM收件箱中收到发送加入信的请求。 John打开请求并视图详细信息。 John Doe附加了加入信函PDF，然后单击“附加并发送加入信函”。

![johndojoiningletterinbox](assets/johndoejoiningletterinbox.png)

John Doe的AEM收件箱

![johndojoining信笺附件发送](assets/johndoejoiningletterattachandsend.png)

John Doe发出加入函以供签署

## 莎拉·罗斯收到并签署加入信 {#sarah-rose-receives-and-signs-the-joining-letter}

莎拉·罗斯收到签名的加入信。 Sarah单击此处查看并签署加入信。 加入字母PDF将打开一个用于签署文档的字段。

![沙拉氏菌属](assets/sarahrosejoiningletteremail.png)

莎拉·罗斯收到签名的加入信

Sarah可以选择输入、使用draw进行手写、插入签名图像，或使用手机的触摸屏来绘制签名。 Sarah键入姓名，单击“单击以签名”，然后下载加入信的签名副本。

![沙拉氏连字符](assets/sarahrosejoininglettersign.png)

Sarah在她的姓名上输入，在加入信上签名

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah单击“单击以签名”以完成对加入信函的签名

