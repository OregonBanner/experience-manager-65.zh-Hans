---
title: 使用表单
description: 在AEM Forms应用程序中查看和更新与任务或起点关联的表单
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 使用表单 {#working-with-a-form}

如果启用了表单应用程序中的表单同步功能，则会下载该表单，并且您可以直接使用它。

这些表单将在您的应用程序中下载，并可供离线使用。 例如，您正在运行一家银行公司，客户在您的网站上填写申请。 应用程序是一个自适应表单，它接受来自客户的信息并将其存储以供审查。 管理员查看表单，并在AEM创作实例中创建验证表单。 管理员可以启用表单与AEM Forms应用程序的同步功能。 如果AEM Forms应用程序中提供了验证表单，则您的字段代理可以使用移动设备来验证客户的详细信息。 移动设备将与服务器同步，并且验证表单会加载到应用程序中。 您的现场代理可以访问您的客户、验证详细信息、将数据另存为草稿或提交验证表单。 每次应用程序联机时，表单都会与服务器同步。

要在AEM Forms应用程序中同步表单，请执行以下操作：

1. 在创作实例中，选择一个表单，然后单击 **查看属性**.
1. 在属性页面中，单击 **高级。**
1. 在“高级”下，启用选项： **与AEM Forms应用程序同步**，并选择 **保存**.

要同步多个表单，请在创作实例中选择表单管理器中的多个表单，然后选择 **与AEM Forms应用程序同步**. 发布表单后，AEM Forms应用程序可以连接到发布服务器并获取表单。

如果您的AFA(AEM Form Application) Android应用程序无法同步，请执行以下步骤，以解决同步问题：

1. 转到 **https://[服务器]：[端口]/system/console/configMgr**.
1. 搜索 **[!UICONTROL Granite令牌身份验证处理程序Adobe]** 并单击 **[!UICONTROL 编辑]**.
1. 选择 **[!UICONTROL 无]** 下拉菜单中的选项 **[!UICONTROL 登录令牌Cookie的SameSite属性]** 属性。
1. 单击&#x200B;**[!UICONTROL 保存]**。

![将图像与AFA Android应用程序同步](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>支持的表单：
>
>* 自适应表单（无延迟加载）
>* 移动设备表单
>
>在与AEM Forms OSGi服务器同步的AEM Forms应用程序中获取的自适应表单不支持表单级附件。 如果在创作表单时作者启用了字段级附件，则用户可以在字段中附加文件。


**打开和更新表单**

1. 要打开表单，请选择 **[!UICONTROL 表单]** 在主屏幕中。
1. 您可以更新表单的字段、添加附件、另存为草稿并提交表单。
