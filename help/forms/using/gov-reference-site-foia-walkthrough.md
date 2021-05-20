---
title: We.Gov引用站点FOIA演练
seo-title: We.Gov引用站点FOIA演练
description: 请参阅We.Gov参考网站演练，了解AEM Forms如何帮助政府接收和传递个人根据《信息自由法》要求提供的信息。
seo-description: 请参阅We.Gov参考网站演练，了解AEM Forms如何帮助政府接收和传递个人根据《信息自由法》要求提供的信息。
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# We.Gov引用站点FOIA演练{#we-gov-reference-site-foia-walkthrough}

## 参考站点信息自由法案方案{#reference-site-freedom-of-information-act-scenario}

We.Gov是一个国有组织，允许养父母在收养孩子时报养子女。 We.Gov还允许家长根据《信息自由法》向下列政府部门索取信息：

* 国防后勤局
* 国防部监察主任办公室
* 司法部 — 信息政策厅
* 海军部
* 环境保护署

有关《信息自由法》的更多信息，请参阅[www.foia.gov](https://www.foia.gov)。

方案涉及以下角色：

* 莎拉·罗斯，那位在
* 约翰·雅各布斯，负责处理请求的人，将请求转发给相应的部门
* 政府雇员格洛丽亚·里奥斯，根据要求提供信息

## Sarah在FOIA {#sarah-initiates-request-for-information-under-foia}下发起信息请求

根据《信息自由法》，Sarah要求复制2013-2016年期间儿童和家庭管理局案件日志。 Sarah向司法部 — 信息政策办公室提交了这一请求，并表示她愿意支付最多100美元的印刷和邮资费用。

### 工作原理{#how-it-works}

### 自己看{#see-it-yourself}

在浏览器中，打开`https://<hostname>:<PublishPort>/wegov`。 在We.Gov网站中，点按应用程序>所有应用程序。 在“所有应用程序”页面中，点按“FOIA请求的应用程序”下的“应用”。

## Sarah启动FOIA {#sarah-starts-her-application-for-information-under-foia}下的信息申请

Sarah单击&#x200B;**Apply**，并在“信息自由法案请求表”页面中，Sarah输入以下信息：

* **机构：** Sarah指定了司法部 — 信息政策办公室 — 处理请求的机构。

* **最多将支付**:Sarah说她愿意支付多达100美元的印刷和邮资费。
* **详细描述请求**:Sarah指明了&quot;请求2013-2016财政年度儿童和家庭管理局案例日志的副本&quot;。

![请求复制2013-2016财政年度儿童和家庭管理局案件日志](assets/sarahfiosform.png)

请求复制2013-2016财政年度儿童和家庭管理局案件日志

Sarah可以随时点按保存以保存表单的草稿，稍后再回来填写表单并提交它。 莎拉提交了表格。

>[!NOTE]
>
>从电子邮件继续工作流仅适用于已登录的用户。 在参考站点方案中，确保添加了用户Sarah Rose。 Sarah的登录凭据为`srose/password`。

## John Jacobs收到并批准该申请{#john-jacobs-receives-and-approves-the-application}

约翰·雅各布斯收到请求并将其路由到正确的人。 AEM收件箱可让她在一个位置查看所有提交的应用程序。

### 工作原理{#how-it-works-1}

当Sarah填写并提交FOIA应用程序时，该应用程序的记录会发送到John Jacobs的收件箱。 John Jacobs可以查看提交的申请，并接受或拒绝。

### 自己看{#see-it-yourself-1}

您可以访问位于https://***hostname***>的AEM收件箱：***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html。 登录AEM收件箱，使用jacobs/password作为John Jacobs的用户名/密码，并查看FOIA应用程序。 有关使用AEM收件箱执行以表单为中心的工作流任务的信息，请参阅[在AEM收件箱中管理Forms应用程序和任务](/help/forms/using/manage-applications-inbox.md)。

![约翰雅各布斯](assets/johnjacobs.png)

John Jacobs可以在申请仪表板中查看、批准或拒绝该申请。 John Jacobs选择并打开请求详细信息，并在审核请求后批准该请求。

![johnjacobustskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah收到确认电子邮件</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

在John Jacobs批准该申请后，Sarah会收到We.Gov网站的确认电子邮件。 Sarah被告知处理她的申请所需的费用和时间。 这封电子邮件还包括电子邮件和电话详情，莎拉可以联系，以获取她的应用程序的最新信息。

![sarahseemail](assets/sarahroseemail.png)

## Gloria收到FOIA请求二级批准{#gloria-receives-the-foia-request-for-second-level-approval}

约翰·雅各布斯填写了所需信息，并批准了莎拉的请求后，这些请求将转给格洛丽亚·里奥斯，由他最终批准。 格洛丽亚审查所附记录文件并批准该请求。

![格洛里亚辛布克](assets/gloriariosinbox.png)

### 工作原理{#how-it-works-2}

当John Jacobs批准FOIA请求时，将创建应用程序的PDF或记录文档，并将其发送到Gloria Rios的收件箱。 Gloria可以查看提交的请求，并批准或拒绝该请求。

### 自己看{#see-for-yourself}

您可以访问位于https://***hostname***>的AEM收件箱：***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html。 使用grios/password作为Gloria Rios的用户名/密码登录到AEM收件箱，并查看FOIS请求。

Gloria打开请求并检查FOIA请求的详细信息。 在审查了请求详情并检查提供所需文件的可行性后，Gloria批准了该请求。

![格洛里阿里](assets/gloriariosapproves.png)

## Sarah收到批准其请求的通知{#sarah-receives-notification-that-her-request-is-approved}

Gloria批准FOIA请求后，Sarah收到一封电子邮件，通知她她的请求已获得批准。 该电子邮件还包括关于提供文件的暂定时间表的信息，以及跟踪请求的联系详情。

![sarahseemailapproval](assets/sarahroseemailapproval.png)
