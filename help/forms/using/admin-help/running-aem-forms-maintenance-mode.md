---
title: 在维护模式下运行AEM表单
seo-title: 在维护模式下运行AEM表单
description: 维护模式在执行修补DSC、升级AEM表单或应用服务包等任务时很有用。 了解有关在维护模式下运行AEM表单的更多信息。
seo-description: 维护模式在执行修补DSC、升级AEM表单或应用服务包等任务时很有用。 了解有关在维护模式下运行AEM表单的更多信息。
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在维护模式下运行AEM表单 {#running-aem-forms-in-maintenance-mode}

维护模式在执行修补DSC、升级AEM表单或应用服务包等任务时很有用。

避免在服务器处于维护模式时调用任何进程。 这是当服务器处于维护模式时调用进程时发生的情况：

* 如果该过程是长期的，则会将其添加到作业数据库，但不会启动。 当您退出维护模式时，AEM表单会处理其队列中长期存在的作业，即使服务器在维护模式下重新启动也是如此。
* 如果该过程为短期过程，则立即进行处理。

**将AEM表单置于维护模式**

1. 在Web浏览器中，输入：

   `https://`*[hostname ]*端`:`*[口]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=`*[管理员用户名&#x200B;]*`&password=`*[密码]*

   浏览器窗口中会显示“现在已暂停”消息。

   >[!NOTE]
   >
   >如果在服务器处于维护模式时关闭服务器，则重新启动服务器后仍处于维护模式。 完成维护任务后，必须关闭维护模式。

**检查AEM表单是否在维护模式下运行**

1. 在Web浏览器中，输入：

   `https://`*[hostname]:[port ]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=`*[administrator用户名]*`&password=`*[密码&#x200B;]*

   状态显示在浏览器窗口中。 状态为“true”表示服务器正在维护模式下运行，而“false”表示服务器未处于维护模式。

**关闭维护模式**

1. 在Web浏览器中，输入：

   `https://`*[hostname]:[port ]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=`*[administrator用户名]*`&password=`*[密码&#x200B;]*

   浏览器窗口中会显示“现在正在运行”消息。

