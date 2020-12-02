---
title: We.Gov参考站点FOIA演练
seo-title: We.Gov参考站点FOIA演练
description: 请浏览We.Gov参考网站，了解AEM Forms如何帮助政府接收和传递个人根据《信息自由法》要求提供的信息。
seo-description: 请浏览We.Gov参考网站，了解AEM Forms如何帮助政府接收和传递个人根据《信息自由法》要求提供的信息。
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# We.Gov参考站点FOIA演练{#we-gov-reference-site-foia-walkthrough}

## 参考站点信息自由法案方案{#reference-site-freedom-of-information-act-scenario}

We.Gov是一个州立组织，允许养父母在收养孩子时报到抚养孩子。 We.Gov还允许家长根据信息自由法案向下列政府部门申请信息：

* 国防后勤局
* 总督国防部
* 司法部——信息政策厅
* 海军部
* 环境保护署

有关《信息自由法》的详细信息，请参阅[www.foia.gov](https://www.foia.gov)。

此方案涉及以下角色：

* 莎拉·罗丝，那个在
* 约翰·雅各布斯，负责处理请求的人，将请求转发给相应的部门
* Gloria Rios，根据要求提供信息的政府雇员

## Sarah发起FOIA {#sarah-initiates-request-for-information-under-foia}下的信息请求

根据《信息自由法》,Sarah要求复制2013至2016年儿童和家庭管理局案件日志。 Sarah向司法部——信息办公室政策提交了这一请求，并表示她愿意支付最多100美元的印刷和邮资费用。

### 工作原理{#how-it-works}

### 亲自查看{#see-it-yourself}

在浏览器中，打开`https://<hostname>:<PublishPort>/wegov`。 在We.Gov站点中，点按应用程序>所有应用程序。 在“所有应用程序”页面中，点按“FOIA请求的应用程序”下的“应用”。

## Sarah开始她的FOIA {#sarah-starts-her-application-for-information-under-foia}下的信息申请

Sarah单击&#x200B;**Apply**，在“信息自由法案请求表”页面中，Sarah输入以下信息：

* **代理：** Sarah指定将请求提交到的机构为司法部——信息政策办公室。

* **最多可支付**:Sarah说，她愿意支付最高达100美元的印刷和邮资费用。
* **详细描述请求**:Sarah指定“请求2013至2016财政年度儿童和家庭管理局案例日志的副本”。

![请求复制2013至2016财政年度儿童和家庭管理局案件日志](assets/sarahfiosform.png)

请求复制2013至2016财政年度儿童和家庭管理局案件日志

随时，Sarah可以点击“保存”以保存表单的草稿，稍后再回来填写表单并提交。 Sarah提交表格。

>[!NOTE]
>
>“从电子邮件继续”工作流仅适用于已登录的用户。 在参考站点场景中，确保添加了用户Sarah Rose。 Sarah的登录凭据为`srose/password`。

## John Jacobs接收并批准该应用程序{#john-jacobs-receives-and-approves-the-application}

约翰·雅各布会收到请求，并将其路由到合适的人。 AEM Inbox使她能够在一个位置查看所有提交的应用程序。

### 工作原理{#how-it-works-1}

当Sarah填写并提交FOIA应用程序时，会将该应用程序的记录发送到John Jacobs的收件箱。 John Jacobs可以视图提交的申请并接受或拒绝。

### 亲自查看{#see-it-yourself-1}

您可以访问位于https://&lt;***hostname***>的AEM收件箱：&lt;***PublishPort***/content/we-finance/global/en/login.html?resource=/aem/inbox.html。 登录AEM收件箱，使用jjacobs/password作为John Jacobs的用户名／密码，查看FOIA应用程序。 有关使用AEM收件箱管理以表单为中心的工作流任务的信息，请参阅[在AEM收件箱中管理Forms应用程序和任务](/help/forms/using/manage-applications-inbox.md)。

![约翰雅各布](assets/johnjacobs.png)

John Jacobs可以从申请仪表板查看、批准或拒绝申请。 约翰·雅各布斯选择并打开请求的详细信息，审阅请求后批准请求。

![约翰·哈布斯特斯克德特-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah收到确认电子邮件</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

在John Jacobs批准该申请后，Sarah会从We.Gov网站收到一封确认电子邮件。 Sarah获悉处理申请所需的费用和时间。 该电子邮件还包含电子邮件和电话详细信息，莎拉可以联系以获取有关其应用程序的更新。

![萨拉赫罗塞马](assets/sarahroseemail.png)

## Gloria收到FOIA请求二级批准{#gloria-receives-the-foia-request-for-second-level-approval}

约翰·雅各布斯填写了所需信息并批准了莎拉的请求后，这些请求将交给格洛丽亚·里奥斯进行最终批准。 Gloria审阅随附的记录文档并批准该请求。

![美丽银箱](assets/gloriariosinbox.png)

### 工作原理{#how-it-works-2}

当John Jacobs批准FOIA请求时，将创建PDF或应用程序记录文档并将其发送到Gloria Rios的收件箱。 Gloria可以视图提交的请求，批准或拒绝它。

### 亲自查看{#see-for-yourself}

您可以访问位于https://&lt;***hostname***>的AEM收件箱：&lt;***PublishPort***/content/we-finance/global/en/login.html?resource=/aem/inbox.html。 使用grios/password作为Gloria Rios的用户名／密码登录AEM收件箱，并查看FOIS请求。

Gloria打开请求并检查FOIA请求的详细信息。 在审查请求的详细情况并检查提供所需文档的可行性后，Gloria批准了该请求。

![歌颂](assets/gloriariosapproves.png)

## Sarah收到通知，其请求已获得批准{#sarah-receives-notification-that-her-request-is-approved}

Gloria批准FOIA请求后，Sarah会收到一封电子邮件，通知她其请求已获得批准。 该电子邮件还包含关于提供文档的暂定时间表的信息，以及联系人详细信息，以便跟进该请求。

![sarahroseemailapproval](assets/sarahroseemailapproval.png)

