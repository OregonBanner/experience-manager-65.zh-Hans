---
title: 一般AEM Forms设置
seo-title: 一般AEM Forms设置
description: 了解如何在管理控制台中配置“核心配置”页面设置，以帮助提高系统性能。
seo-description: 了解如何在管理控制台中配置“核心配置”页面设置，以帮助提高系统性能。
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 1%

---


# 一般AEM Forms设置{#general-aem-forms-settings}

管理控制台中的“核心配置”页提供的设置可以帮助您提高系统性能。 配置或更新这些设置后，请重新启动应用程序服务器。

有关启用安全备份模式的信息，请参阅[启用和禁用安全备份模式](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode)。


>[!NOTE]
>
>临时目录中的文件和全局文档存储(GDS)根目录中的长寿命文档可能包含敏感用户信息，如使用API或用户界面访问时需要特殊凭据的信息。 因此，必须使用操作系统可用的任何方法来正确保护此目录。 建议只有用于运行应用程序服务器的操作系统帐户才具有此目录的读写权限。


1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>核心系统设置>配置]**。
1. 在“核心配置”页面上，根据需要更改选项，然后单击&#x200B;**[!UICONTROL 确定]**。 有关这些选项的详细信息，请参阅[核心配置选项](configure-general-aem-forms-settings.md#core-configurations-options)。


## 核心配置选项{#core-configurations-options}

**临时目录的** 位置AEM表单将创建产品临时文件的目录路径。如果此设置的值为空，则位置默认为系统临时目录。 确保临时目录是可写文件夹。

>[!NOTE]
>
>确保临时目录位于本地文件系统上。 AEM表单不支持远程位置的临时目录。

**全局文档** 存储根目录全局文档存储(GDS)根目录用于以下用途：

* 储存长寿文档。 长寿命文档没有过期时间，直到删除它们（例如，在工作流程中使用的PDF文件）后才会持续存在。 长期文档是整个系统状态的关键部分。 如果这些文档中的某些或全部丢失或损坏，表单服务器可能会变得不稳定。 因此，此目录存储在RAID设备上很重要。
* 存储处理过程中需要的临时文档。

>[!NOTE]
>
>还可以在AEM表单存储库中启用文档。 但是，使用GDS时，系统性能会更好。

* 在群集中的节点之间传输文档。 如果您在群集环境中运行AEM表单，则必须可从群集中的所有节点访问此目录。
* 从远程API调用接收传入参数。

如果未指定GDS根目录，则该目录默认为应用程序服务器目录：

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>更改GDS根目录设置的值应特别小心。 GDS目录用于存储在流程中使用的长寿命文件以及重要的AEM表单产品组件。 更改GDS目录的位置是一个主要的系统更改。 错误地配置GDS目录的位置将导致AEM表单无法运行，并且可能需要完整的AEM表单重新安装。 如果为GDS目录指定新位置，则需要关闭应用程序服务器并迁移数据，然后才能重新启动服务器。 系统管理员必须将所有文件从旧位置移动到新位置，但保留内部目录结构。

>[!NOTE]
>
>请勿为临时目录和GDS目录指定同一目录。

有关GDS目录的其他信息，请参见[准备安装AEM表单（单台服务器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

**Adobe服务器字体目录的** 位置键入包含Adobe服务器字体的目录的路径。这些字体随AEM表单一起安装。 这些字体的默认位置是[aem-forms root]/fonts目录。 如果此目录不可访问，则可以将字体复制到其他位置，然后使用此设置指定新位置。

**客户字体目录的** 位置键入包含您要使用的其他字体的目录的路径。

***注&#x200B;**:从Windows系统字体缓存中选取字体，并需要重新启动系统才能更新缓存。指定客户字体目录后，请确保重新启动安装了AEM表单的系统。*

**系统字体目录的** 位置键入操作系统提供的字体目录的路径。可以添加多个目录，以分号&#x200B;**;**&#x200B;分隔。

**数据服务配置文** 件的位置指定services-config.xml文件的位置。默认情况下，此文件嵌入adobe-core-appserver.ear文件中，用户无法访问。 默认services-config.xml文件的副本位于[aem-forms root]\sdk\misc\DataServices\Server-Configuration中。 如果更改了此文件并移动了它，请在此字段中键入新位置。

Data Services配置文件允许自定义Data Services设置，如身份验证类型和调试输出。

此设置默认为空。

**默认文档最大内联大小(字** 节)在各种AEM表单组件之间传递文档时内存中保留的最大字节数。使用此设置进行性能调整。 小于此数的文档存储在内存中并保留在数据库中。 超过此最大值的文档存储在硬盘上。

此设置为必填。 默认值为65536字节。

**默认文档处理超时(秒** )文档在各个AEM表单组件之间传递的最大时间，以秒为单位。此时间过后，用于存储此文档的文件将被删除。 使用此设置可控制磁盘空间的使用。

此设置为必填。 默认值为600秒。

**文档扫描间隔(** 秒)删除不再需要且用于在服务之间传递文档数据的文件尝试之间的时间（以秒为单位）。

此设置为必填。 默认值为30秒。

**启** 用FIPS选择此选项以启用FIPS模式。联邦信息处理标准(FIPS)140-2是美国政府定义的密码学标准。 在FIPS模式下运行时，AEM表单使用RSA BSAFE Crypto-C 2.1加密模块将数据保护限制为FIPS 140-2认可的算法。

FIPS模式不支持在7.0之前的Adobe Acrobat®版本中使用的加密算法。如果启用了FIPS模式，并且您使用将兼容性级别设置为Acrobat 5的口令来加密PDF，则加密尝试将失败并出错。

通常，启用FIPS后，Assembler服务将不会对任何文档应用密码加密。 如果尝试这样做，将引发FIPSModeException，指示“FIPS模式中不允许密码加密”。 此外，当基本文档被密码加密时，FIPS模式不支持文档描述XML(DDX)PDFsFromBookmarks元素。

>[!NOTE]
>
>AEM forms软件不验证代码以确保FIPS兼容性。 它提供FIPS操作模式，以便FIPS认可的算法用于FIPS认可的库(RSA)的加密服务。

**启** 用WSDLS选择此选项可为AEM表单的所有服务启用Web服务定义语言(WSDL)生成。

在开发环境中启用此选项，开发人员在开发环境中使用WSDL生成来构建其客户端应用程序。 您可以选择在生产环境中禁用WSDL生成，以避免暴露服务的内部详细信息。

**在文档库中启用** 存储选择此选项可在AEM表单数据库中存储长寿命文档。启用此选项不会消除对GDS目录的需求。 但是，选择此选项可简化AEM表单备份。 如果仅使用GDS，则备份涉及将AEM formsAEM表单系统置于备份模式，然后完成数据库和GDS的备份。 如果选择数据库选项，则备份涉及完成新安装的数据库备份或完成数据库备份和GDS一次性备份以进行升级。 与仅GDS配置相比，清除作业和数据可能需要对数据库进行额外管理。 (请参阅将文档库用于存储时的备份选项。)

**启用DSC调** 用统计信息选择此选项后，AEM将跟踪调用统计信息，如调用次数、调用时间和调用错误数。此信息存储在JMX Bean中，以便您可以使用Java™ JConsole或第三方软件查看统计信息。 如果不想看到这些统计信息，请取消选择此选项以提高AEM表单的性能。

**启** 用RDSS选择此选项可在AEM表单中启用远程开发服务(RDS)servlet。启用此选项后，客户端工具可以与数据服务交互，执行部署或取消部署模型等操作，以创建目标和端点，或查找已部署到端点的模型。 默认情况下，此选项处于未选中状态。

**允许非安全** 的RDS请求选择此选项时，RDS请求无需使用https。默认情况下，此选项未被选中，与Data Services的所有通信都必须是https请求。

**允许从Flex应用程序上传非安** 全文档：用于从AdobeFlex®应用程序将文档上载到AEM的文件上传servlet要求用户先经过身份验证，然后才能上传文档。必须为用户分配“文档上传应用程序用户”角色或包含“文档上传”权限的其他角色。 这有助于防止未经授权的用户将文档上传到AEM forms服务器。 如果要在开发环境中禁用此安全功能，或要与AEM表单的先前版本向后兼容，请选择此选项。 默认情况下，此选项处于未选中状态。有关详细信息，请参阅使用AEM表单进行编程中的“使用AEM表单调用AEM表单远程处理”。

**允许从Java SDK应用程序进行非安全文档上** 传：必须保护HTTP DocumentManager上传。默认情况下，HTTP上传要求用户经过身份验证并获得授权，然后才能上传文档。 必须为用户分配服务用户角色或包含服务调用权限的其他角色。 这有助于防止未经授权的用户将文档上传到表单服务器。 如果要在开发环境中禁用此安全功能，以向后兼容先前版本的AEM表单，或根据防火墙设置，请选择此选项。 默认情况下，此选项处于未选中状态。有关详细信息，请参阅使用AEM表单进行编程中的“使用Java API调用AEM表单”。
