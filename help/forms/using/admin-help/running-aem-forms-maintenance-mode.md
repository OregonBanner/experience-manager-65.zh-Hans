---
title: 在维护模式下运行AEM表单
description: 在执行诸如为DSC打补丁、升级AEM表单或应用Service Pack等任务时，维护模式很有用。 了解有关在维护模式下运行AEM表单的更多信息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 在维护模式下运行AEM表单 {#running-aem-forms-in-maintenance-mode}

在执行诸如为DSC打补丁、升级AEM表单或应用Service Pack等任务时，维护模式很有用。

避免在服务器处于维护模式时调用任何进程。 如果在服务器处于维护模式时调用进程，则会发生以下情况：

* 如果进程是长期的，则会将其添加到作业数据库，但不会启动。 当您退出维护模式时，AEM Forms会处理其队列中的长期作业，即使服务器在维护模式下重新启动也是如此。
* 如果处理的时间较短，则会立即进行处理。

**将AEM表单置于维护模式**

1. 在Web浏览器中，输入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   浏览器窗口中将显示“现已暂停”消息。

   >[!NOTE]
   >
   >如果在服务器处于维护模式时将其关闭，则在重新启动时它仍处于维护模式。 完成维护任务后关闭维护模式。

**检查AEM表单是否正在维护模式下运行**

1. 在Web浏览器中，输入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   状态将显示在浏览器窗口中。 状态“true”表示服务器正在维护模式下运行，“false”表示服务器不在维护模式下。

**关闭维护模式**

1. 在Web浏览器中，输入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   浏览器窗口中将显示“正在运行”消息。
