---
title: We.Gov参考站点FOIA演练
seo-title: We.Gov参考站点FOIA演练
description: 请参阅We.Gov参考网站演练，了解AEM Forms如何帮助政府接收和传递个人根据《信息自由法》要求提供的信息。
seo-description: 请参阅We.Gov参考网站演练，了解AEM Forms如何帮助政府接收和传递个人根据《信息自由法》要求提供的信息。
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# We.Gov参考站点FOIA演练 {#we-gov-reference-site-foia-walkthrough}

## 先决条件 {#pre-requisite}

按照设置和配置AEM Forms引用站点中的 [说明设置您的We.Gov引用站点](/help/forms/using/setup-reference-sites.md)。

## 参考站点信息自由法案情景 {#reference-site-freedom-of-information-act-scenario}

We.Gov是一个国营组织，允许养父母在收养孩子时报到抚养孩子。 We.Gov还允许父母根据信息自由法案向下列政府部门请求信息：

* 国防后勤局
* 国防部监察长办公室
* 司法部——信息厅政策
* 海军部
* 环保署

有关《信息自由法》的更多信息，请参 [阅www.foia.gov](https://www.foia.gov)。

此方案涉及以下角色：

* 莎拉·罗丝，那个在
* 约翰·雅各布斯，负责处理请求的人，将请求转发给相应的部门
* Gloria Rios，根据要求提供信息的政府雇员

## Sarah根据FOIA发起信息请求 {#sarah-initiates-request-for-information-under-foia}

根据《信息自由法》,Sarah要求复制2013至2016年度儿童和家庭管理局案件日志。 Sarah向司法部——信息办公室政策提交了这一请求，并表示她愿意支付最多100美元的印刷和邮资费用。

### 工作原理 {#how-it-works}

### 亲身体验 {#see-it-yourself}

In your browser, open `https://<hostname>:<PublishPort>/wegov`. 在We.Gov站点中，点按应用程序>所有应用程序。 在“所有应用程序”页面中，点按“FOIA请求的应用程序”下的“应用”。

## Sarah在FOIA下启动申请获取信息 {#sarah-starts-her-application-for-information-under-foia}

Sarah单击 **“应用** ”，在“信息自由法案请求表”页面中，Sarah输入以下信息：

* **** 代理：Sarah指定了将请求提交到的机构，即司法部——信息政策办公室。

* **最高可支付**:Sarah指出，她愿意支付多达100美元的印刷和邮资费用。
* **详细描述请求**:Sarah指出，“请求复制2013至2016财政年度儿童和家庭管理局案例日志”。

![请求复制2013至2016财政年度儿童和家庭管理局案件记录](assets/sarahfiosform.png)

请求复制2013至2016财政年度儿童和家庭管理局案件记录

Sarah可以随时点击“保存”以保存表单的草稿，稍后再回来填写并提交表单。 莎拉提交了表格。

>[!NOTE]
>
>从电子邮件继续工作流程仅适用于已登录的用户。 在参考站点场景中，确保添加了用户Sarah Rose。 Sarah的登录凭据为 `srose/password`。

## John Jacobs接收并批准该应用程序 {#john-jacobs-receives-and-approves-the-application}

约翰·雅可布收到请求，并将其发送给正确的人。 AEM收件箱可让她在一个位置查看所有提交的应用程序。

### 工作原理 {#how-it-works-1}

当Sarah填写并提交FOIA应用程序时，会向John Jacobs的收件箱发送申请记录。 John Jacobs可以查看提交的申请并接受或拒绝。

### 亲身体验 {#see-it-yourself-1}

您可以访问位于https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html的AEM收件箱。 登录AEM收件箱，使用jacobs/password作为John Jacobs的用户名／密码，并查看FOIA应用程序。 有关将AEM收件箱用于以表单为中心的工作流任务的信息，请参阅 [管理表单应用程序和AEM收件箱中的任务](/help/forms/using/manage-applications-inbox.md)。

![约翰雅各布](assets/johnjacobs.png)

John Jacobs可以从应用程序仪表板中查看、批准或拒绝应用程序。 约翰·雅各布斯选择并打开请求详细信息，在查看请求后批准请求。

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah收到确认电子邮件</strong>{#strong-sarah-receives-an-acknowledgement-email-strong}

在John Jacobs批准该申请后，Sarah会从We.Gov网站收到一封确认电子邮件。 Sarah会收到处理申请所需的费用和时间的通知。 该电子邮件还包含电子邮件和电话详细信息，萨拉可以联系以获取有关其应用程序的更新。

![sarahroseemail](assets/sarahroseemail.png)

## Gloria收到FOIA请求，请求二级批准 {#gloria-receives-the-foia-request-for-second-level-approval}

约翰·雅各布斯填写了所需信息并批准了莎拉的请求后，这些请求将交给格洛丽亚·里奥斯，由他最终批准。 Gloria审阅随附的记录文档并批准该请求。

![格洛里亚辛盒](assets/gloriariosinbox.png)

### 工作原理 {#how-it-works-2}

当John Jacobs批准FOIA请求时，将创建应用程序的PDF或记录文档，并将其发送到Gloria Rios的收件箱。 Gloria可以查看提交的请求，并批准或拒绝它。

### 亲自查看 {#see-for-yourself}

您可以访问位于https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html的AEM收件箱。 使用grios/password作为Gloria Rios的用户名／密码登录到AEM收件箱，并查看FOIS请求。

Gloria打开请求并检查FOIA请求的详细信息。 在审查了请求的详细信息并检查了提供所需文件的可行性后，Gloria批准了该请求。

![荣耀授权](assets/gloriariosapproves.png)

## Sarah收到通知，她的请求已获得批准 {#sarah-receives-notification-that-her-request-is-approved}

Gloria批准FOIA请求后，Sarah会收到一封电子邮件，通知她她的请求已获得批准。 该电子邮件还包含关于提供文档的暂定时间线的信息，以及联系人详细信息，以便对请求采取后续行动。

![sarahroseemailapproval](assets/sarahroseemailapproval.png)

