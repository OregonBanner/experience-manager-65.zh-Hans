---
title: 常规AEM Forms设置
seo-title: General AEM Forms settings
description: 了解如何在管理控制台中配置有助于提高系统性能的“核心配置”页面设置。
seo-description: Learn to configure the Core Configurations page settings in administration console that can help improve system performance.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# 常规AEM Forms设置 {#general-aem-forms-settings}

管理控制台中的“核心配置”页面提供了有助于提高系统性能的设置。 在配置或更新这些设置后，重新启动应用程序服务器。

有关启用安全备份模式的信息，请参见 [启用和禁用安全备份模式](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>临时目录中的文件和全局文档存储(GDS)根目录中的长期文档可能包含敏感的用户信息，例如使用API或用户界面访问时需要特殊凭据的信息。 因此，务必通过使用操作系统可用的任何方法来正确保护此目录。 建议只有用于运行应用服务器的操作系统帐户才具有此目录的读写访问权限。


1. 在管理控制台中，单击 **[!UICONTROL 设置>核心系统设置>配置]**.
1. 在Core Configurations页面上，根据需要更改选项并单击 **[!UICONTROL 确定]**. 有关选项的详细信息，请参阅 [核心配置选项](configure-general-aem-forms-settings.md#core-configurations-options).


## 核心配置选项 {#core-configurations-options}

**临时目录的位置** AEM表单将创建产品临时文件的目录路径。 如果此设置的值为空，则该位置将默认为系统临时目录。 确保临时目录是可写文件夹。

>[!NOTE]
>
>确保临时目录位于本地文件系统中。 AEM forms不支持远程位置的临时目录。

**全局文档存储根目录** 全局文档存储(GDS)根目录用于以下目的：

* 存储长期文档。 长效文档没有过期时间，并且会一直存在，直到被删除(例如，工作流进程中使用的PDF文件)。 长效文档是整个系统状态的关键部分。 如果某些或所有这些文档丢失或损坏，表单服务器可能会变得不稳定。 因此，此目录必须存储在RAID设备上。
* 存储处理过程中所需的临时文档。

>[!NOTE]
>
>您还可以在AEM表单数据库中启用文档存储。 但是，使用GDS可以提高系统性能。

* 在群集中的节点之间传输文档。 如果您在群集环境中运行AEM表单，则必须从群集中的所有节点访问此目录。
* 接收来自远程API调用的传入参数。

如果不指定GDS根目录，则该目录默认为应用程序服务器目录：

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>更改GDS根目录设置的值时应特别小心。 GDS目录用于存储进程中使用的长期文件以及关键AEM表单产品组件。 更改GDS目录的位置是一项重大的系统更改。 错误配置GDS目录的位置将导致AEM表单不起作用，并且可能需要完全重新安装AEM表单。 如果为GDS目录指定了新位置，则需要关闭应用程序服务器并迁移数据，然后才能重新启动服务器。 系统管理员必须将所有文件从旧位置移动到新位置，但保留内部目录结构。

>[!NOTE]
>
>不要为临时目录和GDS目录指定相同的目录。

有关GDS目录的其他信息，请参见 [准备安装AEM表单（单服务器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Adobe服务器字体目录的位置** 键入包含Adobe服务器字体的目录的路径。 这些字体随AEM表单一起安装。 这些字体的默认位置为 [aem-forms根]/fonts目录。 如果无法访问此目录，则可以将字体复制到其他位置，然后使用此设置指定新位置。

**Customer Fonts目录的位置** 键入包含要使用的其他字体的目录的路径。

***注释&#x200B;**：从Windows系统字体缓存中挑选字体，需要重新启动系统才能更新缓存。 指定Customer font目录后，请确保重新启动安装了AEM forms的系统。*

**System Fonts目录的位置** 键入操作系统提供的fonts目录的路径。 可以添加多个目录，以分号分隔 **；**.

**数据服务配置文件的位置** 指定services-config.xml文件的位置。 默认情况下，此文件嵌入在adobe-core-appserver.ear文件中，且用户无法访问。 默认services-config.xml文件的副本位于 [aem-forms根]\sdk\misc\DataServices\Server-Configuration. 如果更改了此文件并移动了它，请在此字段中键入新位置。

数据服务配置文件允许自定义数据服务设置，如身份验证类型和调试输出。

默认情况下，此设置为空。

**默认文档最大内联大小（字节）** 在各种AEM表单组件之间传递文档时内存中保留的最大字节数。 使用此设置进行性能调整。 小于此数字的文档存储在内存中并保留在数据库中。 超过此最大值的文档存储在硬盘上。

此设置是必需的。 默认值为65536字节。

**默认文档处理超时（秒）** 在各种AEM表单组件之间传递的文档被视为活动状态的最长时间（以秒为单位）。 在此时间过后，用于存储此文档的文件可能会被删除。 使用此设置可控制磁盘空间的使用。

此设置是必需的。 默认值为600秒。

**文档扫描间隔（秒）** 尝试删除不再需要的文件以及用于在服务之间传递文档数据的文件之间的间隔时间（以秒为单位）。

此设置是必需的。 默认值为30秒。

**启用FIPS** 选择此选项可启用FIPS模式。 联邦信息处理标准(FIPS) 140-2是美国政府定义的加密标准。 在FIPS模式下运行时，AEM Forms通过使用RSA BSAFE Crypto-C 2.1加密模块将数据保护限制为FIPS 140-2批准的算法。

FIPS模式不支持Adobe Acrobat® 7.0之前的版本中使用的加密算法。如果启用了FIPS模式，并且您使用加密服务使用兼容性级别设置为Acrobat 5的口令对PDF进行加密，则加密尝试将失败，并出现错误。

通常，启用FIPS时，汇编程序服务不会对任何文档应用密码加密。 如果尝试此操作，则会引发FIPSModeException，指示“在FIPS模式下不允许密码加密”。 此外，当基础文档进行了密码加密时，FIPS模式中不支持文档描述XML (DDX) PDFsFromBookmarks元素。

>[!NOTE]
>
>AEM forms软件不会验证代码以确保FIPS兼容性。 它提供了FIPS操作模式，以便将FIPS批准的算法用于来自FIPS批准的库(RSA)的加密服务。

**启用WSDL** 选择此选项可为AEM表单中的所有服务启用Web服务定义语言(WSDL)生成。

在开发人员使用WSDL生成来构建客户端应用程序的开发环境中启用此选项。 您可以选择在生产环境中禁用WSDL生成，以避免公开服务的内部详细信息。

**在数据库中启用文档存储** 选择此选项可在AEM表单数据库中存储长期文档。 启用此选项不会删除对GDS目录的需要。 但是，选择此选项可以简化AEM表单备份。 如果只使用GDS，则备份包括将AEM formsAEM forms系统置于备份模式，然后完成数据库和GDS的备份。 如果选择数据库选项，则备份包括完成数据库备份以进行新安装，或完成数据库备份和GDS的一次性备份以进行升级。 与仅GDS配置相比，清除作业和数据可能需要对数据库进行额外管理。 （请参阅将数据库用于文档存储时的备份选项。）

**启用DSC调用统计信息** 选择此选项后，AEM Forms将跟踪调用统计信息，例如调用次数、调用所用时间以及调用中的错误数。 此信息存储在JMX Bean中，以便您可以使用Java™ JConsole或第三方软件查看统计信息。 如果不想查看这些统计信息，请取消选择此选项以提高AEM表单性能。

**启用RDS** 选择此选项可在AEM表单中启用远程开发服务(RDS) servlet。 启用此选项后，客户端工具可以与数据服务进行交互，以执行部署或取消部署模型等操作，从而创建目标和端点，或找出哪些模型已部署到端点。 默认情况下，不选中此选项。

**允许不安全的RDS请求** 选择此选项时，RDS请求不需要使用https。 默认情况下，此选项未选中，所有与数据服务的通信都必须是https请求。

**允许从Flex应用程序上传不安全的文档：** 文件上传servlet用于将文档从AdobeFlex®应用程序上传到AEM表单，它要求用户在上传文档之前必须经过身份验证和授权。 必须为用户分配文档上载应用程序用户角色或包含文档上载权限的其他角色。 这有助于防止未经授权的用户将文档上传到AEM表单服务器。 如果要在开发环境中禁用此安全功能，或者要与以前版本的AEM Forms向后兼容，请选择此选项。 默认情况下，不选中此选项。 有关详细信息，请参阅使用AEM表单编程中的“使用AEM表单远程处理调用AEM表单”。

**允许从Java SDK应用程序上传不安全的文档：** HTTP DocumentManager上传必须是安全的。 默认情况下，HTTP上传要求用户在上传文档之前进行身份验证和授权。 必须为用户分配服务用户角色或包含服务调用权限的其他角色。 这有助于防止未经授权的用户将文档上传到表单服务器。 如果要在开发环境中禁用此安全功能、要与以前版本的AEM Forms向后兼容，或要基于防火墙设置，请选择此选项。 默认情况下，不选中此选项。 有关详细信息，请参阅使用AEM表单编程中的“使用Java API调用AEM表单”。
