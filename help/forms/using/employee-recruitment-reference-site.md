---
title: 员工招聘参考站点演练
seo-title: 员工招聘
description: AEM Forms参考网站展示了组织如何使用AEM Forms功能来实施员工招聘工作流。
seo-description: AEM Forms参考网站展示了组织如何使用AEM Forms功能来实施员工招聘工作流。
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
exl-id: bdfc0a20-1e98-47f9-a1d1-5af5b3ef15db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---

# 员工招聘参考站点演练{#employee-recruitment-reference-site-walkthrough}

## 概述 {#overview}

We.Finance是允许候选人通过参考网站门户申请就业的组织。 该组织还使用门户来管理候选人的面试安排、短名单和内部沟通。 网站可管理以下内容：

* 搜索和申请工作的候选人
* 候选人的筛选和短名单
* 面试过程
* 候选详细信息的收集
* 候选背景检查
* 向选定候选人推出优惠

>[!NOTE]
>
>员工招聘用例在We.Finance和We.Gov参考网站中均可用。 演练中使用的示例、图像和描述使用We.Finance参考网站。 但是，您也可以使用We.Gov运行这些用例和查看工件。 为此，请在上述URL中将&#x200B;**we-finance**&#x200B;替换为&#x200B;**we-gov**。

### 涉及的工作流模型{#workflow-models-involved}

员工招聘用例涉及两个工作流：

* 在面试之前 — 我们为员工招聘工作流提供资金
* 面试后 — 我们为员工招聘招聘后面试工作流提供资金

这些工作流在AEM中创建，可在以下位置找到：

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### 我们为员工招聘工作流{#we-finance-employee-recruiting-workflow}提供资金

以下是本文档中遵循的We Finance员工招聘工作流模型。

![we-finance-employee-recluiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### 我们为员工招聘后面试工作流{#we-finance-employee-recruiting-post-interview-workflow}提供资金

以下是本文档中遵循的We Finance员工职位面试招聘工作流模型。

![we-finance-employee-recluition-pusion-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 角色 {#personas}

方案涉及以下角色：

* 莎拉·罗斯，该组织的求职者
* 招聘人员约翰·雅各布斯
* 招聘经理格洛丽亚·里奥斯
* John Doe，人力资源部的人

## Sarah申请工作{#sarah-applies-for-a-job}

莎拉·罗斯在组织里寻找工作机会。 她访问了他们的网站，并浏览了“职业生涯”页面上列出的职位空缺。 她找到一份匹配的工作清单并申请。

![主页](assets/home-page.png)

We.Finance主页

![职业生涯页面](assets/career-page.png)

We.财务职业页

Sarah单击在职务发帖上应用。 将打开作业申请表单。 她填写了申请中的所有细节并提交了。

![作业 — 应用程序 — 表单](assets/job-application-form.png)

### 工作原理{#how-it-works}

We.Finance主页和职业页面是AEM Sites页。 职业生涯页面嵌入了自适应表单，该表单使用可重复面板通过服务获取职位空缺并在页面上列出这些空缺。 您可以在`https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`查看自适应表单。

### 自己看{#see-it-yourself}

转到`https://[publishHost]:[publishPort]/content/we-finance/global/en.html`并单击&#x200B;**[!UICONTROL Career]**。 单击&#x200B;**[!UICONTROL 搜索]**&#x200B;以填充作业列表，然后单击&#x200B;**[!UICONTROL 应用]**&#x200B;作业。 在表格中填写详细信息并提交申请。

请确保您在应用程序中指定了有效的电子邮件ID，因为通过此演练的任何通信都将发送到指定的电子邮件ID。

## 约翰·雅各布斯将莎拉·罗斯的招聘经理简介列入招聘经理的短片{#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

组织接收Sarah提交的求职申请。 招聘人员约翰·雅各布斯被指派负责审阅莎拉的个人资料。 他在AEM收件箱中查看任务，找到符合工作要求的用户档案，然后单击“入选”。 莎拉的资料被转发给招聘经理格洛丽亚·里奥斯，请她批准。

![jacobs-inbox-1](assets/jjacobs-inbox-1.png)

John的AEM收件箱

![候选人候选名单](assets/candidate-shortlist.png)

约翰·雅各布斯入围Sarah Rose招聘经理的简介

**工作原理**

“作业申请”表单中的提交操作会触发一个工作流，该工作流会在John Jacob的收件箱中创建一个任务以筛选应用程序。 当John审核并列出应用程序的短名单时，该工作流会在招聘经理Gloria的收件箱中创建一个任务。

### 自己看{#see-it-yourself-1}

转到`https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`，然后使用jacobs/password作为John Jacobs的用户名/密码登录。 打开“候选人资料复核”任务并填写申请人的短名单。

## 格洛丽亚审查了申请并批准了面试申请人{#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

招聘经理Gloria在其AEM收件箱中接收入围的用户档案，作为任务。 她审核了这份报告，并批准了候选人莎拉·罗斯的采访。

![gloriabox](assets/gloriainbox.png)

Gloria的AEM收件箱

![格洛里策划访谈](assets/gloriaschedulesinterview.png)

格洛丽亚批准莎拉·罗斯接受采访

**工作原理**

当Gloria批准面试的候选人时，该工作流会在John Doe的AEM收件箱中创建一个任务，John Doe是We.Finance的招聘人员。

### 自己看{#see-it-yourself-2}

转到`https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`并使用jacobs/password作为John Jacobs的用户名/密码登录。 打开“候选人资料复核”任务并填写申请人的短名单。

转到`https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` ，然后使用grios/password作为Gloria Rios的用户名/密码登录。 打开“候选用户档案审核”任务，然后单击“计划面试”。

## John Doe安排一次访谈{#john-doe-schedules-an-interview}

John Doe在其收件箱中接收安排面试的任务。 John Doe选择并打开该任务，并将面试日期、时间、地点以及负责面试的人力资源负责人作为John Jacob进行修复。 John Doe单击“发送邀请电子邮件”。 向莎拉发送一封电子邮件，并为招聘经理Gloria分配一项任务，以与莎拉进行面谈。

![johnjacbaseminbox](assets/johnjacobsaeminbox.png)

John Doe的AEM收件箱

![约翰·杜斯·切杜达访谈](assets/johndoescheduleinterview.png)

John Doe安排了面试，并将细节发给Sarah Rose

## 莎拉·罗丝收到了带面试时间表{#sarah-rose-receives-the-email-with-interview-schedule}的电子邮件

Sarah Rose收到包含面试时间表、地点和其他详细信息的电子邮件。 她点击“接受”，表示她对面试日程和地点没有问题。 在准确信息的指导下，莎拉得以参加面试。

![萨拉赫罗塞马梅](assets/sarahroseinterviewemail.png)

莎拉·罗丝收到面试日程

## 面试后，招聘经理的入围名单是莎拉·罗斯{#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

在莎拉·罗斯完成面试并清除面试后，招聘经理Gloria Rios从她的收件箱中打开“候选人选择”任务，并单击“选择”。 Gloria Rios的决定被传达给人力资源部人员John Doe，以供进一步处理。

![格洛里亚辛博舍](assets/gloriariosinboxoffer.png)

Gloria的AEM收件箱

![格洛里亚罗斯选择候选人](assets/gloriariosselectcandidate.png)

格洛丽亚·里奥斯在采访后选择莎拉·罗斯

## John Doe请求更多信息{#john-doe-requests-more-information}

在要求候选人加入组织之前，需要检查她的背景。 John Doe打开并审查所选申请人的详细情况，发现她的某些就业和教育细节尚未填写。 John Doe点击需要更多信息。

![](assets/johndoeinbox.png) ![johndoeinboxjohndoedmoreinformation](assets/johndoeneedmoreinformation.png)

John Doe向Sarah Rose请求有关她的教育和工作经历的更多信息

## Sarah Rose收到一封电子邮件，请求进一步的信息{#sarah-rose-receives-an-email-requesting-further-information}

Sarah Rose收到一封电子邮件，通知她需要进一步的信息才能处理她的就业申请。 该电子邮件包括指向表单的链接，用于填写所需信息。

![sarahseemailmoredetails](assets/sarahroseemailmoredetails.png)

Sarah Rose收到一封电子邮件，通知需要进一步的信息才能处理她的就业申请

Sarah单击电子邮件中的Provide Details（提供详细信息）链接。 将显示一个表单。 Sarah将按照John Doe的要求填写所需的教育和就业详细信息并点击“提交”。

![其他信息1](assets/additionalinformation1.png)

Sarah通过单击电子邮件中的链接打开其他信息表单

![其他信息2](assets/additionalinformation2.png)

Sarah会按照John Doe的要求填充其他信息，并单击“提交”

## John Doe查看所选候选用户档案，以获取{#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}提供的其他信息

John Doe选择候选审阅请求并将其打开。 John Doe发现Sarah已按要求填写了所有信息。 审核应用程序后，John Doe单击“批准”。 经John Doe批准，对Sarah Rose进行背景调查的请求将转发给John Jacobs。

![johndoadditionalinformationinbox](assets/johndoeadditionainformationinbox.png)

John Doe的AEM收件箱

![johndoeadditionalinformationreview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe审核Sarah提供的其他信息并予以批准

## 约翰·雅各布斯收到背景调查请求{#john-jacobs-receives-a-background-check-request}

约翰·雅各布斯在收件箱中看到了背景检查请求。 约翰·雅各布开启了这项任务，并回顾了莎拉·罗斯提供的信息。 执行背景检查后，John Jacobs点击“继续”以表示背景检查已成功。

![johnjacobsbackgroundcheckbox](assets/johnjacobsbackgroundcheckinbox.png)

John Jacobs的AEM收件箱

![johnjacobsbackgroundcheckaed](assets/johnjacobsbackgroundcheckgoahead.png)

在进行背景检查后，John Jacobs点击“Go Aek（继续）”

## 无名氏将加入信发给莎拉·罗斯{#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe在其AEM收件箱中收到发送加入信的请求。 John打开请求并查看详细信息。 John Doe附加连接信件PDF，然后单击“附加并发送连接信件”。

![johndojoiningletterinbox](assets/johndoejoiningletterinbox.png)

John Doe的AEM收件箱

![johndojoiningletterattachandsend](assets/johndoejoiningletterattachandsend.png)

John Doe发出加入书以供签署

## 莎拉·罗斯收到并签署加入函{#sarah-rose-receives-and-signs-the-joining-letter}

莎拉·罗斯收到加入签名的信。 Sarah单击此处查看并签署加入信。 将打开加入信PDF，其中包含一个用于签署文档的字段。

![sarahrosejoingletteremail](assets/sarahrosejoiningletteremail.png)

莎拉·罗斯收到加入签名的信

Sarah可以选择输入、使用绘图进行手写、插入签名图像，或者使用手机触摸屏来绘制她的签名。 Sarah在她的姓名中输入，单击“单击以签名”，然后下载加入信的签名副本。

![沙拉柔连字符](assets/sarahrosejoininglettersign.png)

莎拉在她的名字上签字，以签署加入信

![sarahrosejoinglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah单击Click To Sign ，以完成对加入信的签名
