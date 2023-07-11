---
title: 员工招聘参考网站演练
description: AEM Forms参考网站展示了组织如何使用AEM Forms功能实施员工招聘工作流程。
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bdfc0a20-1e98-47f9-a1d1-5af5b3ef15db
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 0%

---

# 员工招聘参考网站演练 {#employee-recruitment-reference-site-walkthrough}

## 概述 {#overview}

We.Finance是一个允许候选人通过参考网站门户申请就业的组织。 该组织还使用该门户来管理候选人的面试安排、入围名单和内部沟通。 站点管理以下内容：

* 搜索和申请工作的候选人
* 筛选和甄选候选人
* 面试过程
* 候选人详细信息集合
* 候选背景检查
* 将优惠转出到选定的候选人

>[!NOTE]
>
>雇员招聘用例可在We.Finance和We.Gov参考站点中找到。 演练中使用的示例、图像和描述使用We.Finance引用站点。 但是，您也可以运行这些用例并使用We.Gov查看工件。 要执行此操作，请替换 **we-finance** 替换为 **we-gov** 在提及的URL中。

### 涉及的工作流模型 {#workflow-models-involved}

员工招聘用例涉及两个工作流：

* 面试前 — 我们财务员工招聘工作流程
* 面试之后 — 我们为员工招聘职位面试工作流提供资金

这些工作流是在AEM中创建的，可在以下位置找到：

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### 我们财务员工招聘工作流程 {#we-finance-employee-recruiting-workflow}

以下是本文档中遵循的We Finance员工招聘工作流模型。

![we-finance-employee-recruitment-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### 我们财务部员工招聘面试流程 {#we-finance-employee-recruiting-post-interview-workflow}

以下是本文档中遵循的We Finance员工面试后招聘工作流的模型。

![we-finance-employee-recruitment-post-interview-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 角色 {#personas}

此方案涉及以下角色：

* Sarah Rose，申请组织工作的候选人
* 约翰·雅各布斯，招聘人员
* 招聘经理格洛丽亚·里奥斯
* John Doe，人力资源部的人

## Sarah申请工作 {#sarah-applies-for-a-job}

Sarah Rose正在组织中寻找工作机会。 她访问他们的门户网站，探索“职业生涯”页面上列出的空缺职位。 她找到一份相符的职位列表并申请。

![主页](assets/home-page.png)

We.Finance主页

![career-page](assets/career-page.png)

We.Finance职业生涯页面

Sarah在求职帖子上单击“申请”。 此时将打开作业申请表单。 她填写申请书中的所有细节并提交它。

![job-application-form](assets/job-application-form.png)

### 工作原理 {#how-it-works}

We.Finance主页和职业主页都是AEM Sites页面。 职业页面包含一个自适应表单，该表单使用可重复的面板获取使用服务的职位空缺并将其列在页面上。 您可以在以下位置查看自适应表单： `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`.

### 亲眼看看 {#see-it-yourself}

转到 `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` 并单击 **[!UICONTROL 职业]**. 单击 **[!UICONTROL 搜索]** 以便填充作业列表，然后单击 **[!UICONTROL 应用]** 找一份工作。 在表格中填写详情并提交申请。

请确保在应用程序中指定有效的电子邮件ID，因为通过此演练进行的任何通信都会发送到指定的电子邮件ID。

## 约翰·雅各布斯将莎拉·罗斯入围该招聘经理的名单 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

该组织将接收Sarah提交的工作申请。 招聘人员John Jacobs被指派检查Sarah的资料。 John查看其AEM收件箱中的任务，找到与工作要求匹配的配置文件，然后单击“短列表”。 莎拉的资料被转发给招聘经理格洛丽亚·里奥斯，等待她批准。

![jjacobs-inbox-1](assets/jjacobs-inbox-1.png)

John的AEM收件箱

![候选短列表](assets/candidate-shortlist.png)

约翰·雅各布斯将莎拉·罗斯入围该招聘经理的名单

**工作原理**

“职务申请”表单中的提交操作会触发一个工作流，该工作流会在John Jacob的收件箱中创建用于筛选申请的任务。 当John审核并甄选申请时，工作流程会在聘用经理Gloria的收件箱中创建一个任务。

### 亲眼看看 {#see-it-yourself-1}

转到 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`和使用jjacobs/密码作为John Jacobs的用户名/密码登录。 打开“候选人配置文件复查”任务并将申请人列入候选清单。

## Gloria审查申请并批准申请人进行面试 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

招聘经理Gloria在AEM收件箱中收到入围用户档案作为任务。 她审核并批准候选人萨拉·罗斯接受采访。

![gloriainbox](assets/gloriainbox.png)

Gloria的AEM收件箱

![gloriaschedulesinterview](assets/gloriaschedulesinterview.png)

格洛丽亚批准莎拉·罗斯接受采访

**工作原理**

当Gloria批准面试候选人时，工作流会在We.Finance的招聘人员John Doe的AEM收件箱中创建任务。

### 亲眼看看 {#see-it-yourself-2}

转到 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 和使用jjacobs/密码作为John Jacobs的用户名/密码登录。 打开“候选人配置文件复查”任务并将申请人列入候选清单。

转到 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 并使用grios/密码作为Gloria Rios的用户名/密码登录。 打开“候选人配置文件复查”任务，然后单击计划面试。

## John Doe安排了一次面试 {#john-doe-schedules-an-interview}

John Doe的收件箱中会安排面试。 John Doe选择并打开任务，并以John Jacob的身份确定面试日期和时间、地点以及负责面试的人力资源人员。 John Doe单击“发送邀请电子邮件”。 系统会向Sarah发送一封电子邮件，并指派一名负责面试Sarah的招聘经理Gloria。

![johnjacobsaeminbox](assets/johnjacobsaeminbox.png)

John Doe的AEM收件箱

![johndoescheduleinterview](assets/johndoescheduleinterview.png)

John Doe安排了面试，并向Sarah Rose发送了详细信息

## Sarah Rose收到包含面试安排的电子邮件 {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose收到一封电子邮件，其中包含面试时间表、地点和其他详细信息。 Sarah点击“接受”表示她同意面试的时间表和地点。 在精确信息的指引下，莎拉接受了采访。

![萨拉赫罗塞维耶韦韦韦邮件](assets/sarahroseinterviewemail.png)

Sarah Rose收到面试表

## 面试结束后，招聘经理将萨拉·罗斯列入候选名单 {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

在莎拉·罗斯接受面试并完成面试后，招聘经理格洛丽亚·里奥斯从收件箱中打开“候选人选择”任务，然后点击“选择”。 Gloria Rios的决定传达给人力资源部人员John Doe以便进一步处理。

![gloriariosinboxoffer](assets/gloriariosinboxoffer.png)

Gloria的AEM收件箱

![荣耀选择候选](assets/gloriariosselectcandidate.png)

格洛丽亚·里奥斯在面试后挑选莎拉·罗斯

## John Doe请求更多信息 {#john-doe-requests-more-information}

在邀请候选人加入该组织之前，必须核实莎拉的背景。 John Doe打开并查看选定申请人的详细信息，发现她的一些雇佣和教育详细信息尚未填写。 John Doe点击需要更多信息。

![Johndoeinbox](assets/johndoeinbox.png) ![johndoeneedmoreinformation](assets/johndoeneedmoreinformation.png)

John Doe向Sarah Rose索取更多关于她的教育和工作经验的信息

## Sarah Rose收到一封请求进一步信息的电子邮件 {#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose收到一封电子邮件，通知她需要更多信息，才能处理她的就业申请。 该电子邮件包含一个指向表单的链接，用于填写所需信息。

![sarahroseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose收到一封电子邮件，通知她需要更多信息，才能处理她的就业申请

Sarah单击电子邮件中的“提供详细信息”链接。 此时将显示一个表单。 Sarah填写John Doe要求的教育和就业详细信息，然后单击Submit。

![additionalinformation1](assets/additionalinformation1.png)

Sarah通过单击电子邮件中的链接打开其他信息表单

![additionalinformation2](assets/additionalinformation2.png)

Sarah填写John Doe请求的其他信息，然后单击“提交”

## John Doe会复查选定的候选人配置文件以获取提供的附加信息 {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe选择候选审阅请求并打开它。 John Doe发现Sarah已根据需要填写了所有信息。 审核应用程序后，John Doe单击“批准”。 经John Doe批准，向John Jacobs转发对Sarah Rose进行背景调查的请求。

![johndoeditionainformationinbox](assets/johndoeadditionainformationinbox.png)

John Doe的AEM收件箱

![johndoeditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe将审阅Sarah提供的其他信息并批准该信息

## John Jacobs收到后台检查请求 {#john-jacobs-receives-a-background-check-request}

John Jacobs在其收件箱中看到背景检查请求。 John Jacobs打开任务并回顾Sarah Rose提供的信息。 在执行背景检查后，John Jacobs单击“继续”以表示背景检查已成功。

![johnjacobsbackgroundcheckinbox](assets/johnjacobsbackgroundcheckinbox.png)

John Jacobs的AEM收件箱

![johnjacobsbackgroundcheckgoahead](assets/johnjacobsbackgroundcheckgoahead.png)

执行背景检查后，John Jacobs单击“Go Ahead（继续）”

## John，Doe给莎拉，Rose {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe在其AEM收件箱中收到发送加入信件的请求。 John打开请求并查看详细信息。 John Doe附加加入信件PDF，然后单击“附加并发送加入信件”。

![johndoejoiningletterinbox](assets/johndoejoiningletterinbox.png)

John Doe的AEM收件箱

![johndoejoiningletterattachandsend](assets/johndoejoiningletterattachandsend.png)

John，Doe寄了加入信供签名

## Sarah Rose收到并签署加入信 {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose收到签字信。 Sarah点击此处查看并签署加入信。 加入书信PDF打开，其中包含一个用于签署文档的字段。

![sarahrosejoiningletteremail](assets/sarahrosejoiningletteremail.png)

Sarah Rose收到加入信要求签名

Sarah可以选择键入、使用draw手写、插入签名图像或使用她的手机触摸屏绘制签名。 Sarah键入她的名字，单击Click To Sign，然后下载加入信的签名副本。

![sarahrosejoininglettersign](assets/sarahrosejoininglettersign.png)

Sarah键入她的名字在加入书信上签名

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah单击Click To Sign以完成签署加入信
