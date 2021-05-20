---
title: 常规AEM Forms设置
seo-title: 常规AEM Forms设置
description: 了解如何在管理控制台中配置核心配置页面设置，以帮助提高系统性能。
seo-description: 了解如何在管理控制台中配置核心配置页面设置，以帮助提高系统性能。
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 1%

---

# 常规AEM Forms设置{#general-aem-forms-settings}

管理控制台中的“核心配置”页面提供了有助于提高系统性能的设置。 配置或更新这些设置后，请重新启动应用程序服务器。

有关启用安全备份模式的信息，请参阅[启用和禁用安全备份模式](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode)。


>[!NOTE]
>
>临时目录中的文件和全局文档存储(GDS)根目录中的长期文档可能包含敏感用户信息，例如在使用API或用户界面访问时需要特殊凭据的信息。 因此，必须使用操作系统可用的任何方法来正确保护此目录。 建议只有用于运行应用程序服务器的操作系统帐户才具有此目录的读写权限。


1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>核心系统设置>配置]**。
1. 在核心配置页面中，根据需要更改选项，然后单击&#x200B;**[!UICONTROL 确定]**。 有关这些选项的详细信息，请参阅[核心配置选项](configure-general-aem-forms-settings.md#core-configurations-options)。


## 核心配置选项{#core-configurations-options}

**临时目录的** 位置AEM表单将创建产品临时文件的目录路径。如果此设置的值为空，则位置默认为系统临时目录。 确保临时目录是可写文件夹。

>[!NOTE]
>
>确保临时目录位于本地文件系统上。 AEM表单不支持远程位置的临时目录。

**全局文档存储根** 目录全局文档存储(GDS)根目录用于以下目的：

* 存储长期的文件。 长期文档没有过期时间，并且会一直保留，直到它们被删除（例如，工作流程中使用的PDF文件）。 长期文件是整个系统状态的关键部分。 如果这些文档中的部分或全部丢失或损坏，则表单服务器可能会变得不稳定。 因此，此目录存储在RAID设备上很重要。
* 存储处理过程中需要的临时文档。

>[!NOTE]
>
>您还可以在AEM Forms数据库中启用文档存储。 但是，使用GDS时，系统性能会更好。

* 在群集中的节点之间传输文档。 如果您在群集环境中运行AEM表单，则必须从群集中的所有节点访问此目录。
* 接收来自远程API调用的传入参数。

如果未指定GDS根目录，则该目录将默认为应用程序服务器目录：

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>更改GDS根目录设置的值时应特别注意。 GDS目录用于存储流程中使用的长生命周期文件，以及关键的AEM表单产品组件。 更改GDS目录的位置是一项主要的系统更改。 如果未正确配置GDS目录的位置，则AEM表单将无法正常运行，并可能需要完全重新安装AEM表单。 如果为GDS目录指定了新位置，则需要关闭应用程序服务器并迁移数据，然后才能重新启动服务器。 系统管理员必须将所有文件从旧位置移动到新位置，但保留内部目录结构。

>[!NOTE]
>
>请勿为临时目录和GDS目录指定相同的目录。

有关GDS目录的其他信息，请参阅[准备安装AEM表单（单服务器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

**Adobe服务器字体目录的** 位置键入包含Adobe服务器字体的目录的路径。这些字体随AEM Forms一起安装。 这些字体的默认位置是[aem-forms根]/fonts目录。 如果此目录无法访问，则可以将字体复制到其他位置并使用此设置指定新位置。

**客户字体目录的位** 置键入包含要使用的其他字体的目录的路径。

***注意&#x200B;**:从Windows系统字体缓存中选取字体，并且需要系统重新启动才能更新缓存。指定客户字体目录后，请确保重新启动安装AEM表单的系统。*

**System Fonts目录的位** 置键入操作系统提供的字体目录的路径。可以添加多个目录，并以分号&#x200B;**;**&#x200B;分隔。

**数据服务配置文** 件的位置指定services-config.xml文件的位置。默认情况下，此文件将嵌入到adobe-core-appserver.ear文件中，且用户无法访问。 默认services-config.xml文件的副本位于[aem-forms根]\sdk\misc\DataServices\Server-Configuration中。 如果更改了此文件并将其移动，请在此字段中键入新位置。

Data Services配置文件允许自定义Data Services设置，如身份验证类型和调试输出。

默认情况下，此设置为空。

**默认文档最大内联大小（字节）** 在各种AEM表单组件之间传递文档时内存中保留的最大字节数。使用此设置进行性能调整。 小于此编号的文档将存储在内存中并保留在数据库中。 超过此最大值的文档存储在硬盘上。

此设置是强制性的。 默认值为65536字节。

**默认文档处理超时（秒）** 在不同AEM表单组件之间传递文档被视为活动的最大时间，以秒为单位。此时间过后，将删除用于存储此文档的文件。 使用此设置可控制磁盘空间的使用情况。

此设置是强制性的。 默认值为600秒。

**文档扫描间隔（秒）** 尝试删除不再需要且在服务之间用于传递文档数据的文件之间经过的时间，以秒为单位。

此设置是强制性的。 默认值为30秒。

**启用** FIPS选择此选项以启用FIPS模式。联邦信息处理标准(FIPS)140-2是美国政府定义的加密标准。 在FIPS模式下运行时，AEM Forms会使用RSA BSAFE Crypto-C 2.1加密模块，将数据保护限制为FIPS 140-2批准的算法。

FIPS模式不支持在低于7.0的Adobe Acrobat®版本中使用的加密算法。如果启用了FIPS模式，并且您使用加密服务通过使用将兼容性级别设置为Acrobat 5的密码来加密PDF，则加密尝试将失败，并出现错误。

通常，启用FIPS后，汇编程序服务不会对任何文档应用密码加密。 如果尝试这样做，将引发FIPSModeException，指示“在FIPS模式下不允许密码加密”。 此外，在对基本文档进行密码加密时，FIPS模式不支持文档描述XML(DDX)PDFsFromBookmarks元素。

>[!NOTE]
>
>AEM forms软件不验证代码以确保FIPS兼容性。 它提供FIPS操作模式，以便FIPS批准的算法用于FIPS批准的库(RSA)的加密服务。

**启** 用WSDLS选择此选项可为AEM表单中的所有服务启用Web服务定义语言(WSDL)生成。

在开发环境中启用此选项，在开发环境中，开发人员使用WSDL生成来构建其客户端应用程序。 可以选择在生产环境中禁用WSDL生成，以避免公开服务的内部详细信息。

**在数据库中启用文档存** 储选择此选项可在AEM表单数据库中存储长期存储的文档。启用此选项不会消除对GDS目录的需要。 但是，选择此选项可简化AEM表单备份。 如果您只使用GDS，则备份包括将AEM formsAEM Forms系统置于备份模式，然后完成数据库和GDS的备份。 如果选择数据库选项，则备份包括完成数据库备份以进行新安装或完成数据库备份和一次性备份GDS以进行升级。 与仅GDS配置相比，清除作业和数据可能需要对数据库进行其他管理。 （请参阅将数据库用于文档存储时的备份选项。）

**启用DSC调** 用统计信息选择此选项时，AEM将跟踪调用统计信息，如调用次数、调用所花费的时间以及调用中的错误数。此信息存储在JMX Bean中，以便您能够使用Java™ JConsole或第三方软件查看统计信息。 如果不想看到这些统计信息，请取消选择此选项以提高AEM表单性能。

**启用** RDSS选择此选项会启用AEM表单中的远程开发服务(RDS)Servlet。启用此选项后，客户端工具可以与数据服务交互，执行部署或取消部署模型以创建目标和端点之类的操作，或者查找哪些模型已部署到端点中。 默认情况下，此选项处于未选中状态。

**允许非安全** 的RDS请求选择此选项后，RDS请求不需要使用https。默认情况下，未选择此选项，与数据服务的所有通信都必须是https请求。

**允许从Flex应用程序上传非安全文档：** 用于从AdobeFlex®应用程序将文档上传到AEM表单的文件上传servlet要求用户先经过身份验证并获得授权，然后才能上传文档。必须为用户分配“文档上传应用程序用户”角色或包含“文档上传”权限的其他角色。 这有助于防止未授权用户将文档上传到AEM表单服务器。 如果要在开发环境中禁用此安全功能，或为了向后兼容AEM表单的先前版本，请选择此选项。 默认情况下，此选项处于未选中状态。有关详细信息，请参阅使用AEM表单编程中的“使用AEM表单远程调用AEM表单”。

**允许从Java SDK应用程序进行非安全文档上传：** HTTP DocumentManager上传必须是安全的。默认情况下，HTTP上传要求用户先经过身份验证并获得授权，然后才能上传文档。 必须为用户分配服务用户角色或包含服务调用权限的其他角色。 这有助于防止未经授权的用户将文档上载到表单服务器。 如果要在开发环境中禁用此安全功能，以向后兼容AEM表单的早期版本，或根据防火墙设置，请选择此选项。 默认情况下，此选项处于未选中状态。有关详细信息，请参阅使用AEM表单编程中的“使用Java API调用AEM表单”。
