---
title: We.Gov引用站点FOIA演练
seo-title: We.Gov reference site FOIA walkthrough
description: 请参阅We.Gov参考网站演练，了解AEM Forms如何帮助政府接收和传播个人根据《信息自由法》请求的信息。
seo-description: See the We.Gov reference site walkthrough to understand how AEM Forms helps governments receive and impart information requested by individuals under the Freedom of Information Act.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# We.Gov引用站点FOIA演练 {#we-gov-reference-site-foia-walkthrough}

## 参考站点《信息自由法》场景 {#reference-site-freedom-of-information-act-scenario}

We.Gov是一个国营组织，如果养父母收养了孩子，他们可登记子女抚养费。 We.Gov还允许家长根据《信息自由法》向以下政府部门索取信息：

* 国防后勤局
* 国防部监察长办公室
* 司法部 — 信息政策厅
* 海军部
* 环境保护局

有关《信息自由法》的更多信息，请参阅 [www.foia.gov](https://www.foia.gov).

此方案涉及以下角色：

* Sarah Rose，索取信息的人
* 处理请求的人员John Jacobs将请求转发给相应的部门
* Gloria Rios，政府雇员，根据请求提供信息

## Sarah根据FOIA提出信息请求 {#sarah-initiates-request-for-information-under-foia}

根据《信息自由法》，Sarah要求提供2013年至2016年儿童和家庭管理局案件记录副本。 Sarah将此请求提交给司法部 — 信息政策办公室，并表明她愿意支付高达100美元的印刷和邮资费用。

### 工作原理 {#how-it-works}

### 亲眼看看 {#see-it-yourself}

在浏览器中，打开 `https://<hostname>:<PublishPort>/wegov`. 在We.Gov站点中，点按应用程序>所有应用程序。 在所有应用程序页面中，点按FOIA请求的应用程序下的应用。

## Sarah根据FOIA开始她的信息申请 {#sarah-starts-her-application-for-information-under-foia}

Sarah点击量 **应用** 在《信息自由法》申请表页面中，Sarah输入的信息包括：

* **代理商：** Sarah指定处理该请求的机构为司法部 — 信息政策办公室。

* **将支付最高为**：Sarah指定她愿意支付高达100美元的印刷和邮资费用。
* **详细描述请求**：Sarah指定“请求2013至2016财年的儿童和家庭管理案例副本”。

![索取2013至2016财政年度儿童和家庭管理局案件记录副本](assets/sarahfiosform.png)

索取2013至2016财政年度儿童和家庭管理局案件记录副本

Sarah可随时点按保存以保存表单草稿，稍后再回来填写表单并提交它。 Sarah提交了表格

>[!NOTE]
>
>从电子邮件恢复工作流仅适用于登录用户。 在引用站点场景中，确保添加了用户Sarah Rose。 Sarah的登录凭据为 `srose/password`.

## John Jacobs接收并批准申请 {#john-jacobs-receives-and-approves-the-application}

John Jacobs会收到请求并将其路由到适当的人员。 通过AEM收件箱，她可以在一个位置查看所有提交的申请。

### 工作原理 {#how-it-works-1}

当Sarah填写并提交FOIA申请表时，申请表记录会发送到John Jacobs的收件箱中。 John Jacobs可以查看提交的申请，并接受或拒绝它。

### 亲眼看看 {#see-it-yourself-1}

您可以访问AEM收件箱，网址为https://&lt;***主机名***>：&lt;***发布端口***>/content/we-finance/global/en/login.html？resource=/aem/inbox.html. 使用jjacobs/password作为John Jacobs的用户名/密码登录到AEM收件箱，并查看FOIA应用程序。 有关使用AEM收件箱处理以表单为中心的工作流任务的信息，请参阅 [在AEM收件箱中管理Forms应用程序和任务](/help/forms/using/manage-applications-inbox.md).

![约翰雅各布](assets/johnjacobs.png)

John Jacobs可以从应用程序仪表板查看、批准或拒绝应用程序。 John Jacobs选择并打开请求详细信息，然后在查看请求后批准该请求。

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah收到一封确认电子邮件</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

在John Jacobs批准申请后， Sarah会收到来自We.Gov网站的确认电子邮件。 Sarah被告知处理她的申请所需的费用和时间。 该电子邮件还包括电子邮件和电话详细信息，sarah可以联系以获取有关其应用程序的更新。

![萨拉赫罗西邮件](assets/sarahroseemail.png)

## Gloria收到FOIA关于二级审批的请求 {#gloria-receives-the-foia-request-for-second-level-approval}

在John Jacobs填写必填信息并批准Sarah的请求后，该请求将转至Gloria Rios获得最终批准。 Gloria审阅附加的记录文档并批准请求。

![gloriariosinbox](assets/gloriariosinbox.png)

### 工作原理 {#how-it-works-2}

当John Jacobs批准FOIA的请求时，将创建一个应用程序的PDF或记录文档，并发送到Gloria Rios的收件箱。 Gloria可以查看提交的请求，并批准或拒绝该请求。

### 亲自查看 {#see-for-yourself}

您可以访问AEM收件箱，网址为https://&lt;***主机名***>：&lt;***发布端口***>/content/we-finance/global/en/login.html？resource=/aem/inbox.html. 使用grios/password作为Gloria Rios的用户名/密码登录到AEM收件箱，并查看FOIS请求。

Gloria打开请求并检查信息自由局请求的细节。 在查看了请求的详细信息并检查了提供所需文件的可行性之后，Gloria批准了该请求。

![gloriariosapproves](assets/gloriariosapproves.png)

## Sarah会收到通知，告知其请求已被批准 {#sarah-receives-notification-that-her-request-is-approved}

在Gloria批准FOIA的请求后，Sarah收到一封电子邮件，通知她她的请求已被批准。 该电子邮件还包括有关提供文档的暂定时间表和详细联系方式的信息，以便跟进请求。

![萨拉赫罗西电子邮件审批](assets/sarahroseemailapproval.png)
