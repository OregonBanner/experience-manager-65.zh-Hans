---
title: 配置客户端和服务器选项
seo-title: 配置客户端和服务器选项
description: 了解如何配置各种客户端和服务器选项，如服务器配置设置、文档安全角色和事件审核。
seo-description: 了解如何配置各种客户端和服务器选项，如服务器配置设置、文档安全角色和事件审核。
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 配置文档安全服务器 {#configure-the-document-security-server}

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“服务器配置”。
1. 配置设置，然后单击确定。

## 服务器配置设置 {#server-configuration-settings}

**基本URL:** 基本文档安全URL，包含服务器名和端口。 附加到基础的信息会创建连接URL。 例如，在访问网页时会附加/edc/Main.do。 用户还通过此URL响应外部用户注册邀请。

如果您使用IPv6，请输入基本URL作为计算机名或DNS名称。 如果您使用数字IP地址，Acrobat将无法打开受策略保护的文件。 此外，请为服务器使用HTTP安全(HTTPS)URL。

>[!NOTE]
>
>基本URL嵌入到受策略保护的文件中。 客户端应用程序使用基本URL连接回服务器。 受保护的文件将继续包含基本URL，即使以后更改了它。 如果更改基本URL，则需要更新所有连接客户端的配置信息。

**默认脱机租用期：** 用户脱机使用受保护文档的默认时长。 此设置决定了在创建策略时“自动脱机租用期”设置的初始值。 （请参阅创建和编辑策略。）当租赁期到期时，收件人必须再次同步文档才能继续使用。

有关脱机租用和同步工作方式的讨论，请参阅 [Primer on configuring offline lease and synchronization](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html)。

**默认脱机同步期：** 任何文档在最初受保护后可脱机使用的最大时间。

**客户端会话超时：** 通过客户端应用程序登录的用户不与文档安全交互时，文档安全断开连接的时长（以分钟为单位）。

**允许匿名用户访问：** 选择此选项可启用创建共享策略和个人策略的功能，这些策略允许匿名用户打开受策略保护的文档。 (没有帐户的用户可以访问文档，但无法登录文档安全或使用其他受策略保护的文档。)

**禁用对版本7客户端的访问：** 指定用户是否可以使用Acrobat或Reader 7.0连接到服务器。 选择此选项后，用户必须使用Acrobat或Reader 8.0及更高版本以完成PDF文档的文档安全操作。 如果策略要求在打开受策略保护的文档时，Acrobat或Reader 8.0及更高版本必须以认证模式运行，则应禁用对Acrobat或Reader 7的访问。 (请参阅指定用户和用户组的文档权限。)

**允许每文档脱机访问** 。选择此选项可指定每文档的脱机访问。 如果启用此设置，则用户将只能脱机访问用户至少联机打开过一次的文档。

**允许用户名密码身份验证：** 选择此选项可使客户端应用程序在连接到服务器时使用用户名／口令身份验证。

**允许Kerberos身份验证：** 选择此选项可使客户端应用程序在连接到服务器时使用Kerberos身份验证。

**允许客户端证书身份验证：** 选择此选项可使客户端应用程序在连接到服务器时使用证书身份验证。

**允许扩展身份验证** “选择”以启用扩展身份验证，然后输入扩展身份验证登录URL。

选择此选项可使客户端应用程序使用扩展身份验证。 扩展身份验证为自定义身份验证过程和在AEM Forms服务器上配置的不同身份验证选项提供了支持。 例如，用户现在可以从Acrobat和Reader客户端体验基于SAML的身份验证，而不是AEM表单用户名／密码。 默认情况下，登陆URL包含 *localhost* 作为服务器名。 用完全限定的主机名替换服务器名。 如果尚未启用扩展身份验证，则登陆URL中的主机名将自动从基本URL填充。 请参 [阅添加扩展身份验证提供者](configuring-client-server-options.md#add-the-extended-authentication-provider)。

***注意&#x200B;**:Apple Mac OS X上支持Adobe Acrobat 11.0.6及更高版本的扩展身份验证。*

**扩展身份验证的首选HTML控制宽度** 指定扩展身份验证对话框的宽度，该对话框在Acrobat中打开以输入用户凭据。

**扩展身份验证的首选HTML控制高度** 指定扩展身份验证对话框的高度，该对话框在Acrobat中打开以输入用户凭据。

***注意&#x200B;**:此对话框的宽度和高度限制如下：*宽度：最小= 400，最大= 900

高度：最少= 450;最大= 800

**启用客户端凭据缓存：** 选择此选项可允许用户缓存其凭据（用户名和密码）。 缓存用户的凭据后，他们不必在每次打开文档时或在Adobe Acrobat的“管理安全策略”页面上单击“刷新”按钮时输入凭据。 您可以指定用户必须再次提供凭据的天数。 将天数设置为0可无限期地缓存凭据。

## 配置文档安全用户和管理员 {#configuring-document-security-users-and-administrators}

### 为管理员分配文档安全角色 {#assigning-document-security-roles-to-administrators}

您的AEM表单环境包含一个或多个具有创建用户和用户组的相应权限的用户。 如果您的组织使用文档安全，则至少还必须向一个管理员分配管理受邀用户和本地用户的权限。

管理员还必须具有管理控制台用户角色才能访问管理控制台。 (请参阅 [创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。)

### 配置可见的用户和用户组 {#configuring-visible-users-and-groups}

要在策略用户搜索期间视图选定域中的用户和用户组，超级管理员或策略集管理员必须选择域并将其添加到每个策略集的可见用户和用户组列表中（在用户管理中创建）。

可见的用户和用户组列表对策略集协调器可见，用于限制最终用户在选择要添加到策略的用户或用户组时可以浏览的域。 如果未执行此任务，则策略集协调员将找不到要添加到策略的任何用户或用户组。 任何给定策略集都可以有多个策略集协调员。

1. 在安装和配置AEM表单环境及文档安全性后，请在“用户管理”中设置所有适当的域。 <!-- Fix broken link (See Setting up and managing domains) -->

   ***注意&#x200B;**:必须先创建域，然后才能创建任何策略。*

1. 在管理控制台中，单击“服务”>“文档管理”>“策略”，然后单击“策略集”选项卡。
1. 选择“全局策略集”，然后单击“可见的用户和用户组”选项卡。
1. 单击“添加域”，然后根据需要添加现有域。
1. 导航到服务>文档安全性>配置>我的策略，然后单击可见的用户和用户组选项卡。
1. 单击“添加域”，然后根据需要添加现有域。

## 添加扩展身份验证提供者 {#add-the-extended-authentication-provider}

AEM表单提供了一个示例配置，您可以为环境自定义该配置。 执行以下步骤：

>[!NOTE]
>
>Apple Mac OS X上支持Adobe Acrobat 11.0.6及更高版本的扩展身份验证。

1. 获取部署WAR文件的示例。 请参阅适用于应用程序服务器的安装指南。
1. 确保表单服务器具有完全限定的名称而不是作为基本URL的IP地址，并且它是HTTPS URL。 请参阅 [服务器配置设置](configuring-client-server-options.md#server-configuration-settings)。
1. 从“服务器配置”页启用扩展身份验证。 请参阅 [服务器配置设置](configuring-client-server-options.md#server-configuration-settings)。
1. 在用户管理配置文件中添加所需的SSO重定向URL。 请参 [阅添加SSO重定向URL以进行扩展身份验证](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication)。

### 添加SSO重定向URL以进行扩展身份验证 {#add-sso-redirect-urls-for-extended-authentication}

启用扩展身份验证后，在Acrobat XI或Reader XI中打开受策略保护的文档的用户将看到一个用于身份验证的对话框。 此对话框加载您在文档安全服务器设置上指定为扩展身份验证登录URL的HTML页。 请参阅 [服务器配置设置](configuring-client-server-options.md#server-configuration-settings)。

>[!NOTE]
>
>Apple Mac OS X上支持Adobe Acrobat 11.0.6及更高版本的扩展身份验证。

1. 在管理控制台中，单击“设置”>“用户管理”>“配置”>“导入和导出配置文件”。
1. 单击“导出”，然后将配置文件保存到磁盘。
1. 在编辑器中打开文件，然后找到AllowedUrls节点。
1. 在节 `AllowedUrls` 点中，添加以下行： `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```as3
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. 保存文件，然后从“手动配置”页面导入更新的文件：在管理控制台中，单击“设置”>“用户管理”>“配置”>“导入和导出配置文件”。

## 配置脱机安全性 {#configuring-offline-security}

文档安全性允许脱机使用受策略保护的文档，而无需Internet或网络连接。 此功能要求策略允许脱机访问，如指定用户 [和用户组的文档权限中所述](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups)。 在脱机使用具有此策略的文档之前，收件人必须在联机时打开文档，并在出现提示时单击“是”启用脱机访问。 还可以请求收件人验证其身份。 然后，收件人可以在策略中指定的脱机租用期内脱机使用文档。

脱机租用期结束时，收件人必须通过联机打开文档或使用Acrobat或Acrobat Reader DC扩展菜单命令进行同步，从而与文档安全性再次同步。 (请参 *阅“Acrobat帮助* ”或相应的 *Acrobat Reader DC扩展帮助*。)

由于允许脱机访问的文档需要在脱机存储文件的计算机上缓存关键材料，因此，如果未经授权的用户能够获得关键材料，则文件可能会受到潜在的破坏。 为弥补这种可能性，提供了计划和手动的密钥翻转选项，您可以配置这些选项以防止未经授权的人使用密钥访问文档。

### 设置默认脱机租用期 {#set-a-default-offline-lease-period}

受策略保护的收件人可以使文档在策略中指定的天数内脱机。 在最初将文档与文档安全性同步后，收件人可以脱机使用它，直到脱机租用期到期为止。 当租赁期到期时，收件人必须联机文档并登录以与文档安全同步以继续使用文档。

您可以配置默认的脱机租用期。 当任何人创建或编辑策略时，可以从默认的租用期更改。

1. 在文档安全页面上，单击配置>服务器配置。
1. 在“默认脱机租用期”框中，键入脱机租用期的天数。
1. 单击“确定”。

### 管理密钥翻转 {#manage-key-rollovers}

文档安全性使用加密算法和许可证来保护文档。 当对文档加密时，文档安全会生成并管理一个称为 *DocKey* 的解密密钥，该密钥传递给客户端应用程序。 如果保护文档的策略允许脱机访问，则还会为具有脱机访问文档的每个用户生成一个称为主密钥的脱机密钥 ** 。

>[!NOTE]
>
>如果主密钥不存在，文档安全将生成一个密钥以保护文档。

要脱机打开受策略保护的文档，用户的计算机必须具有相应的主键。 当用户与文档安全同步时，计算机获取主密钥(联机打开受保护的文档)。 如果此主密钥泄露，则用户可脱机访问的任何文档也可能泄露。

减少线下文档威胁的一种方法是避免允许线下访问特别敏感的文档。 另一种方法是周期性地滚动到主键上。 当文档安全性将密钥翻过时，任何现有密钥都无法再访问受策略保护的文档。 例如，如果犯罪者从被盗笔记本电脑中获得主密钥，则该密钥无法用于访问在翻车后受保护的文档。 如果您怀疑某个特定的主密钥已泄露，则可以手动将其滚动到该密钥上。

但是，您还需要注意到，键的翻转会影响所有主键，而不仅仅影响一个主键。 由于客户端必须存储更多密钥才能进行脱机访问，因此它还降低了系统的可伸缩性。 默认的键翻转频率为20天。 建议不要将此值设置为低于14天，因为可能会阻止用户查看脱机文档，并且系统性能可能会受到影响。

在以下示例中，Key1是两个主键中较旧的键，Key2是较新的键。 当您第一次单击“立即翻转键”按钮时，Key1将变为无效，并生成一个较新的有效主键(Key3)。 当用户与文档安全同步时，用户将获得Key3，这通常是通过在线打开受保护的文档。 但是，在用户达到策略中指定的最大脱机租用期之前，不会强制用户与文档安全同步。 在第一个密钥展期后，保持脱机状态的用户仍可打开脱机文档，包括受Key3保护的脱机，直到他们达到最大脱机租用期。 再次单击“立即翻转键”按钮时，Key2将变为无效，Key4将创建。 在两个密钥滚动过程中保持脱机的用户无法打开使用Key3或Key4保护的文档，直到他们与文档安全同步。

**更改关键翻转频率**

为保密起见，当您使用脱机文档时，文档安全性会提供一个默认频率为20天的自动密钥展期选项。 您可以更改翻转频率；但是，请避免将值设置为低于14天，因为可能会阻止用户查看脱机文档，并且系统性能可能会受到影响。

1. 在文档安全页面上，单击配置>密钥管理。
1. 在“关键翻转频率”框中，键入翻转期间的天数。
1. 单击“确定”。

**手动滚动到主键上**

为了保持脱机文档的机密性，您可以手动滚动主键。 您可能会发现必须手动滚动某个键(例如，如果某人从缓存该键以允许脱机访问文档的计算机获取该键)。

>[!NOTE]
>
>避免经常使用手动翻转，因为这会导致所有主键翻转，而不仅仅是滚动一个，并且可能会暂时阻止用户脱机查看新文档。

主密钥必须滚动两次，之后客户端计算机上先前存在的密钥才会失效。 使主密钥失效的客户端计算机必须与文档安全服务重新同步以获取新的主密钥。

1. 在文档安全页面上，单击配置>密钥管理。
1. 单击“立即翻转键”，然后单击“确定”。
1. 等待大约10分钟。 服务器日志中显示以下日志消息： `Done RightsManagement key rollover for`*N *`principals`. 其*&#x200B;中&#x200B;*N是文档安全系统中的用户数。
1. 单击“立即翻转键”，然后单击“确定”。
1. 等待大约10分钟。

## 配置事件审核和隐私设置 {#configuring-event-auditing-and-privacy-settings}

文档安全性可以审计和记录与受策略保护的文档、策略、管理员和服务器交互相关的事件信息。 您可以配置事件审核，并指定要审核的事件类型。 要审核特定文档的事件，还必须启用策略上的审核选项。

启用视图后，您可以在事件页面上对已审核的事件的详细信息进行审核。 文档安全用户还可以视图与他们使用或创建的受策略保护的文档特别相关的事件。

您可以选择以下类型的事件进行审核：

* 受策略保护的文档事件，如授权或未授权用户尝试打开文档
* 策略事件，如创建、更改、删除、启用和禁用策略
* 用户事件，如外部用户邀请和注册、激活和取消激活的用户帐户、对用户密码的更改以及用户档案更新
* AEM表单事件，如版本不匹配、目录服务器和授权提供者不可用以及服务器配置更改

### 启用或禁用事件审核 {#enable-or-disable-event-auditing}

您可以启用和禁用与服务器、受策略保护的事件、策略、策略集和用户相关的文档审计。 启用事件审核后，您可以选择审核所有可能的事件，也可以选择要审核的特定事件。

启用服务器审核后，您可以在视图页面上事件已审核的事件。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“审核和隐私设置”。
1. 要配置服务器审核，请在“启用服务器审核”下，选择“是”或“否”。
1. 如果您选择了“是”，则在每个事件类别下，执行下列操作之一以选择要审核的选项：

   * 要审核类别中的所有事件，请选择全部。
   * 要仅审核某些事件，请取消选择“全部”，然后选中要审核的事件旁边的复选框。

      (请参阅 [事件审计选项](configuring-client-server-options.md#event-auditing-options)。)

1. 单击“确定”。

>[!NOTE]
>
>处理网页时，请避免使用浏览器按钮，如后退按钮、刷新按钮和后退或前进箭头，因为此操作可能会导致不需要的数据捕获和数据显示问题。

### 启用或禁用隐私通知 {#enable-or-disable-privacy-notification}

您可以启用和禁用隐私通知消息。 启用隐私通知后，当收件人尝试打开受策略保护的文档时，将显示一条消息。 通知用户正在审核文档使用情况。 您还可以指定用户可用来视图隐私策略页面的URL（如果有）。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“审核和隐私设置”。
1. 要配置隐私通知，请在“启用隐私声明”下，选择“是”或“否”。

   如果附加到文档的策略允许匿名用户访问，并且“启用隐私声明”设置为“否”，则不会提示用户登录，并且不显示隐私通知消息。

   如果附加到文档的策略不允许匿名用户访问，则用户将看到隐私通知消息。

1. 如果适用，在“隐私URL”框中，键入您的隐私政策页面的URL。 如果“隐私URL”框留空，则显示adobe.com的隐私页面。
1. 单击“确定”。

>[!NOTE]
>
>禁用隐私声明不会禁用文档使用审计。 开箱即用审计操作和通过扩展使用情况跟踪支持的自定义操作仍可收集用户行为信息。

### 导入自定义审核事件类型 {#import-a-custom-audit-event-type}

如果您使用支持对其他文档(如特定于某个文件类型的事件)进行审计的支持事件安全的应用程序，则Adobe合作伙伴可以为您提供可导入文档安全的自定义审计事件。 仅当Adobe合作伙伴向您提供自定义事件类型时，才使用此功能。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“事件管理”。
1. 单击“浏览”以转到要导入的XML文件，然后单击“导入”。
1. 如果发现相同的事件代码和命名空间组合，导入将覆盖服务器上的现有自定义审计事件类型。
1. 单击“确定”。

### 删除自定义审核事件类型 {#delete-a-custom-audit-event-type}

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“事件管理”。
1. 选中要删除的自定义审计事件类型旁边的复选框，然后单击“删除”。
1. 单击“确定”。

### 导出审核事件 {#export-audit-events}

您可以将审核事件导出到文件，以便进行存档。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“事件管理”。
1. 根据需要编辑“导出审核”事件下的设置。 您可以指定：

   * 导出审计事件的最低年龄
   * 单个文件中要包含的最大审计事件数。 服务器根据此值生成一个或多个文件。
   * 将在其中创建文件的文件夹。 此文件夹位于表单服务器上。 如果文件夹路径是相对的，则它是相对于应用程序服务器根目录的。
   * 用于审计事件文件的文件前缀
   * 文件的格式，即与Microsoft Excel兼容的以逗号分隔的值(CSV)文件或XML文件。

1. 单击“导出”。 如果要取消导出，请单击“取消导出”。 如果其他用户已计划导出，则在导出完成之前“取消导出”按钮不可用。 如果其他用户已计划导出，则“取消导出”按钮将不可用。 要检查计划的“导出”或“删除”是否已开始或完成，请单击“刷新”。

### 删除审计事件 {#delete-audit-events}

您可以删除早于指定天数的审计事件。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“事件管理”。
1. 在“删除审核事件”下，在“删除审核事件早于”框中指定天数。
1. 单击删除。单击“导出”。 如果要取消删除，请单击“取消删除”。 如果其他用户已计划删除，则在导出完成之前，“取消删除”按钮不可用。 如果其他用户已计划导出，则“取消删除”按钮将不可用。 要检查计划的删除是否已开始或完成，请单击刷新。

### 事件审计选项 {#event-auditing-options}

您可以启用和禁用事件审核，并指定要审核的事件的类型。

**文档事件**

**视图文档:** 收件人视图受策略保护的文档。

**关闭文档:** 收件人关闭受策略保护的文档。

**打印低分辨率** “收件人”打印受策略保护的文档并指定低分辨率选项。

**高分辨率打印：** 收件人打印受策略保护的文档，并指定高分辨率选项。

**将注释添加到文档:** 收件人会向PDF文档添加注释。

**撤销文档:** 用户或管理员撤销对受策略保护的文档的访问权限。

**取消撤销文档:** 用户或管理员重新启用对受策略保护的文档的访问权限。

**表单填写：** 收件人在PDF文档中输入可填写的表单信息。

**删除的策略：** 发布者从文档删除策略以撤销安全保护。

**更改文档撤销URL:** 来自API级别的调用会更改指定的撤销URL，以访问取代已撤销文档的新文档。

**修改文档:** 收件人会更改受策略保护的文档的内容。

**签名文档:** 收件人签了文档。

**确保新文档:** 用户应用策略以保护文档。

**切换文档策略：** 用户或管理员切换附加到文档的策略。

**发布文档为：** 将在服务器上注册一个documentName和许可证与现有文档相同的新文档，该文档没有父子关系。 此事件可使用AEM表单SDK触发。

**迭代文档:** 在服务器上注册一个documentName和许可证与现有文档相同的新文档，该文档具有父子关系。 此事件可使用AEM表单SDK触发。

**政策事件**

**创建策略：** 用户或管理员创建策略。

**启用策略：** 管理员使策略可用。

**更改的策略：** 用户或管理员更改策略。

**禁用策略：** 管理员使策略不可用。

**已删除的策略：** 用户或管理员将删除策略。

**更改策略所有者：** 来自API级别的调用会更改策略所有者。

**用户事件**

**已删除的用户：** 管理员将删除用户帐户。

**注册受邀用户：** 外部用户注册文档安全。

**成功登录：** 管理员或用户成功登录。

**受邀用户：** 文档安全性邀请用户进行注册。

**激活的用户：** 外部用户可使用激活电子邮件中的URL激活其帐户，或由管理员启用帐户。

**更改密码：** 受邀用户更改其口令，或管理员为本地用户重置口令。

**登录失败：** 管理员或用户登录尝试失败。

**已停用的用户：** 管理员禁用本地用户帐户。

**用户档案更新：** 受邀用户可更改其姓名、组织名称和密码。

**帐户已锁定：** 管理员锁定帐户。

**策略集事件**

**CreatedPolicy Set:** 管理员或策略集协调员创建策略集。

**已删除的策略集：** 管理员或策略集协调员将删除策略集。

**修改后的策略集：** 管理员或策略集协调员更改策略集。

**系统事件**

**目录同步完成：** 此信息不可从“事件”页面获取。 “域管理”页上显示当前目录同步信息，包括上次同步的当前同步状态和时间。 要访问管理控制台中的“域管理”页面，请单击“设置”>“用户管理”>“域管理”。

**客户端启用脱机访问：** 用户启用了对针对用户计算机上服务器的安全文档的脱机访问。

**Synchronized Client** Client应用程序必须与服务器同步信息才允许脱机访问。

**版本不匹配：** 与服务器不兼容的AEM表单SDK版本尝试连接到服务器。

**目录同步信息：** 此信息不可从“事件”页面获取。 “域管理”页上显示当前目录同步信息，包括上次同步的当前同步状态和时间。 要访问管理控制台中的“域管理”页面，请单击“设置”>“用户管理”>“域管理”。

**服务器配置更改：** 对通过网页或通过导入config.xml文件手动完成的服务器配置所做的更改。 这包括对基本URL、会话超时、登录锁定、目录设置、密钥滚动、外部注册的SMTP服务器设置、水印配置、显示选项等的更改。

## 配置扩展的使用情况跟踪 {#configuring-extended-usage-tracking}

文档安全性可以跟踪可在受保护的文档上执行的各种自定义事件。 您可以在全局级别或策略级别启用来自文档安全服务器的事件跟踪。 然后，您可以设置JavaScript来捕获在受保护的PDF文档中执行的特定操作，如单击按钮或保存文档。 此使用数据以键值对形式作为XML文件发送，您可以使用它进一步分析。 访问受保护文档的最终用户可以允许或拒绝从客户端应用程序进行此类跟踪。

如果在全局级别启用跟踪，则可以在策略级别覆盖此设置，并针对特定策略禁用它。 如果在全局级别禁用了跟踪，则无法覆盖策略级别。 当列表计数达到25或文档关闭时，跟踪的事件的事件会自动推送到服务器。 您还可以配置脚本以根据您的要求显式推送事件列表。 您可以通过访问事件安全对象属性和方法来自定义文档跟踪。

启用跟踪后，随后创建的所有策略都将默认打开跟踪。 在服务器上启用跟踪之前创建的策略需要手动更新。

### 启用或禁用扩展使用跟踪 {#enable-or-disable-extended-usage-tracking}

在开始之前，请确保已启用“服务器审核”。 有关审 [核的更多信息，请参阅配置事件审核和隐私设置](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) 。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“审核和隐私设置”。
1. 要配置扩展的使用情况跟踪，请在“启用跟踪”下，选择“是”或“否”。
1. 要在登录页面上设置“允许收集详细的使用数据”复选框，请在“启用跟踪默认值”下，选择“是”或“否”。

要视图跟踪的事件，您可以在事件页面上使用文档事件过滤器。 使用JavaScript跟踪的事件标记为“详细使用情况跟踪”。 有关事件 [的更多信息](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) ，请参阅监视事件。

## 配置文档安全显示设置 {#configure-document-security-display-settings}

1. 在管理控制台中，单击“服务”>“文档安全性”>“配置”>“显示选项”。
1. 配置设置，然后单击确定。

### Display settings {#display-settings}

**要显示搜索结果的行：** 执行搜索时在页面上显示的行数。

**自定义客户端登录对话框**

这些设置控制在用户通过客户端应用程序登录文档安全性时显示的登录提示中显示的文本。

**欢迎文本：** 欢迎消息文本，如“请使用您的用户名和密码登录”。 欢迎消息文本应包含有关如何登录到文档安全性以及如何联系您的组织中的管理员或其他指定支持人员寻求帮助的信息。 例如，如果外部用户忘记了密码或需要注册或登录过程的帮助，则可能需要与管理员联系。 欢迎文本的最大长度为512个字符。

**用户名文本：** 用户名框的文本标签。

**密码文本：** 密码框的文本标签。

**自定义客户端证书身份验证对话框**

这些设置控制证书身份验证对话框中显示的文本。

**选择身份验证类型文本：** 显示用于指示用户选择身份验证类型的文本。

**选择证书文本：** 显示用于指示用户选择证书类型的文本。

**证书不可用错误文本：** 在所选证书不可用时最多显示512个字符的消息。

**客户端证书显示的自定义**

**仅显示受信任的凭证发行方：** 选择此选项后，客户端应用程序仅向用户显示AEM表单配置为信任的凭证发行方的证书（请参阅管理证书和凭据）。如果未选择此选项，则用户系统上将显示所有证书的列表。

## 配置动态水印 {#configure-dynamic-watermarks}

使用文档安全性，您可以配置动态水印选项的默认设置，在创建策略时可以应用该设置。 水 *印* ，是叠加在文档中文本上的图像。 它可用于跟踪文档的内容，并有助于识别内容的非法使用。

动态水印可以由由定义的变量（如用户ID和日期以及自定义文本）组成的文本或PDF中的丰富内容组成。 可以使用多个元素配置水印，每个元素都具有自己的位置和格式。

水印不可编辑，因此它们是确保文档内容机密性的更安全方法。 动态水印还确保水印显示足够的用户特定信息，以阻止进一步分发文档。

当收件人视图或打印文档时，策略指定的水印显示在受策略保护的文档中。 与永久水印不同，动态水印从不保存在文档中，这提供了在内部网环境中部署文档时所需的灵活性，以确保查看应用程序显示特定用户的身份。 此外，如果一个文档有多个用户，则使用动态水印意味着您可以使用一个文档而不是多个版本，每个版本具有不同的水印。 显示的水印反映了当前用户的身份。

请注意，动态水印与用户可以直接添加到Acrobat文档的水印不同。 结果是，在受策略保护的文档中可以有两个水印。

### 创建水印时的注意事项 {#considerations-when-creating-watermarks}

您可以创建包含多个水印元素的动态水印，其中每个元素都指定为文本或PDF。 在水印中最多可包含五个元素。

如果选择基于文本的水印，则可以在水印中指定多个元素并包含多个文本条目，并指定每个元素的位置。 为这些元素指定有意义的名称，如页眉、页脚等。

例如，如果要在页眉、页脚、边距上和跨文档中指定不同的文本作为水印，可创建多个水印元素并指定其位置。 如果希望用户的用户ID和访问文档的当前日期显示在标题中，右边距中的策略名称，以及自定义文本“机密”在文档中对角线显示，则应以文本作为类型定义单独的水印元素，并指定其格式和位置。 当水印应用到文档时，水印中的所有元素将同时应用到文档，其顺序与添加到水印的顺序相同。

通常，您使用基于PDF的水印来包含图形内容（如徽标）或特殊符号（如版权或注册商标）。

您可以通过修改文档安全配置文件来更改水印元素数量和PDF文件大小的限制。 请参 [阅更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters)。

配置水印时，请牢记以下几点：

* 不能使用受口令保护的PDF文档作为水印元素。 但是，如果您创建的水印包含其他未受密码保护的元素，则这些元素将作为水印的一部分应用。
* 您可以更改要用作水印元素的PDF文件最大大小。 但是，在脱机同步应用了此类水印的文档时，用作水印的大型PDF文档会降低性能。 请参 [阅更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters)。
* 只有选定PDF的第一页用作水印。 确保要作为水印显示的信息在第一页本身上可用。
* 即使可以指定PDF文档的缩放比例，如果您计划将PDF用作页眉、页脚或边距中的水印，请考虑其页面大小和布局。
* 指定字体名称时，请正确输入名称。 如果打开文档的客户端计算机中不存在AEM表单，则会替换您指定的字体。
* 如果选择文本作为水印内容，则对于宽度不同的页面，将缩放选项指定为“适合页面”不起作用。
* 在指定水印元素的位置时，请确保不超过一个元素具有相同的位置。 如果两个水印元素具有相同的位置（如中心），则它们会在文档上显示重叠，并按它们添加到水印的顺序显示。
* 指定字体大小和类型时，请确保文本的长度在页面中完全可见。 文本内容会滚动到新行中，因此您希望出现在页边距中的水印内容可能会重叠到页面上的内容区域。 但是，如果在Acrobat 9中打开文档，则超出单行的文本将被截断。

### 动态水印的限制 {#limitations-of-dynamic-watermarks}

某些客户端应用程序可能不支持动态水印。 请参阅相应的Acrobat Reader DC扩展帮助。 此外，请记住以下关于支持动态水印的Acrobat版本的信息：

* 不能使用受口令保护的PDF文档作为水印元素。
* Acrobat和Adobe Reader版本早于10，不支持以下水印功能：

   * PDF水印
   * 水印中的多个元素(Text/PDF)
   * 高级选项，如页面范围或显示选项
   * 文本格式选项，如指定的字体、字体名称和颜色。 但是，Acrobat和Reader的早期版本将以默认字体和颜色显示文本内容。

* Acrobat 9.0及更早版本：Acrobat 9.0及早期版本不支持动态水印中的策略名称。 如果Acrobat 9.0打开了受策略保护的文档，其中包含策略名称和其他动态数据的动态水印，则显示水印时不带策略名称。 如果动态水印仅包含策略名称，则Acrobat会显示一条错误消息

### 添加动态水印模板 {#add-a-dynamic-watermark-template}

您可以创建动态水印模板。 这些模板仍可用作管理员或用户创建的策略的配置选项。

>[!NOTE]
>
>在导出配置文件时，动态水印配置信息不会与其他配置信息一起捕获。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“水印”。
1. 单击新建.
1. 在“名称”框中，键入新水印的名称。

   ***注意&#x200B;**:水印或水印元素的名称或说明中不能使用某些特殊字符。 请参阅编辑策略的注[意事项中列出的限制](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies)。*

1. 在“名称”下加号旁，为水印元素（如“标题”）输入有意义的名称，然后添加描述，并展开加号以显示选项。
1. 在“源”下，选择“文本”或“PDF”作为水印的类型。
1. 如果选择了“文本”，请执行以下操作：

   * 选择要包括的水印类型。 如果选择“自定义文本”，请在相邻的框中键入要显示的水印文本。 记住将显示为水印的文本长度。
   * 为水印文本的文本内容指定文本格式属性，如字体名称、字体大小、前景颜色和背景颜色。 将前景色和背景色指定为十六进制值。

      ***注意&#x200B;**:如果选择“适合页面大小”缩放选项，则无法编辑字体大小属性。*

1. 如果您为富水印选项选择了PDF，则单击“ **Select Watermark** PDF”（选择水印PDF）旁边的“浏览”(Browse)，以选择要用作水印的PDF文档。

   ***注意&#x200B;**:请勿使用受口令保护的PDF文档。 如果指定受口令保护的PDF作为水印元素，则不会应用水印。*

1. 在“用作背景”下，选择“是”或“否”。

   **注意**:当前，无论此设置如何，水印都显示在前景中。

1. 要控制水印在文档上的显示位置，请配置“垂直对齐”和“水平对齐”选项。
1. 选择“适合页面大小”或选择%并在框中键入百分比。 该值必须是整数，而不是分数。 要配置水印大小，您可以使用页面百分比值或设置水印以适合页面大小。
1. 在“旋转”框中，键入水印旋转的度数。 范围是-180到180。 使用负值逆时针旋转水印。 该值必须是整数，而不是分数。
1. 在“不透明度”框中，键入百分比。 使用整数，而不是分数。
1. 在“高级选项”下，设置以下各项：

   **页面范围选项**

   设置应显示水印的页面范围。 将开始页输入为1，将结束页输入为-1，以使所有页面都标有水印。

   **显示选项**

   选择要显示水印的位置。 默认情况下，水印同时显示在软拷贝（联机）和硬拷贝（打印）上。

1. 如果 **需要** ，单击“水印元素”下的“新建”以添加更多水印元素。
1. 单击“确定”。

### 编辑动态水印模板 {#edit-a-dynamic-watermark-template}

1. 在管理控制台中，单击“服务”>“文档安全性”>“配置”>“水印”。
1. 在列表中单击相应的水印。
1. 在“编辑水印”页面上，根据需要更改设置。
1. 单击“确定”。

### 删除动态水印模板 {#delete-a-dynamic-watermark-template}

删除动态水印时，不再可添加到新策略。 但是，水印会保留在当前使用水印的现有策略上，并且策略当前保护的文档会继续显示动态水印，直到您或用户编辑包含已删除水印的策略。 编辑策略后，不再应用水印。 将显示一条消息，指示策略上的现有水印已被删除，用户可以选择另一个水印来替换它。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“水印”。
1. 选中相应水印旁边的复选框，然后单击“删除”。
1. 单击“确定”。

## 配置受邀用户注册 {#configuring-invited-user-registration}

您组织外部的用户可以使用文档安全性进行注册。 注册并激活其帐户的受邀用户可以使用其电子邮件地址和注册时创建的密码登录文档安全性。 已注册的受邀用户可以使用其具有权限的受策略保护的文档。

当被邀请的用户被激活时，他们将成为本地用户。 可以使用“已邀请”和“本地用户”区域配置和管理本地用户。 (请参阅 [管理已邀请和本地用户帐户](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)。)

根据您为受邀用户启用的功能，他们还可以使用以下文档安全功能：

* 将策略应用于文档
* 创建策略
* 将受邀用户添加到策略

文档安全性会在发生以下事件时自动生成注册邀请电子邮件，除非用户已位于源LDAP目录中或以前受邀注册：

* 现有用户将受邀用户添加到策略
* 管理员在“已邀请的用户注册”页面上添加已邀请的用户帐户

注册电子邮件包含指向注册页面的链接以及有关如何注册的信息。 在被邀请的用户注册后，文档安全会发出激活电子邮件，其中包含指向激活页面的链接。 激活后，帐户将保持有效，直到您取消激活或删除它。

如果启用内置注册，则只需指定一次SMTP服务器、注册电子邮件详细信息、访问功能和重置密码电子邮件信息。 在启用内置注册之前，请确保您已在“用户管理”中创建了本地域，并将“文档安全邀请用户”角色分配给组织中的相应用户和用户组。 (请参 [阅添加本地域](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain)[和创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。)如果您不使用内置注册，则必须使用AEM表单SDK创建自己的用户注册系统。 请参阅使用AEM表单进行编程中的“为AEM表单开发SPI” [帮助](https://www.adobe.com/go/learn-aemforms-programming-63)。 如果不使用“内置注册”选项，建议您在激活电子邮件和客户端登录屏幕中配置一条消息，以通知用户如何联系管理员获取新密码或其他信息。

**启用和配置受邀用户注册**

默认情况下，已邀请的用户注册进程处于禁用状态。 您可以根据需要启用和禁用已邀请用户的注册以实现文档安全。

1. 在管理控制台中，单击“服务”>“文档安全性”>“配置”>“受邀用户注册”。
1. 选择“启用受邀用户注册”。
1. （可选）根据需要更新受邀用户的注册设置：

   * [排除或包括外部用户或用户组](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [服务器和注册帐户参数](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [注册邀请电子邮件设置](configuring-client-server-options.md#registration-invitation-email-settings)
   * [激活电子邮件设置](configuring-client-server-options.md#activation-email-settings)
   * [配置密码重置电子邮件](configuring-client-server-options.md#configure-a-password-reset-email)

1. （可选）在“内置注册”下，选择“是”以启用此选项。 如果不启用内置注册，则必须设置自己的用户注册系统。
1. 单击“确定”。

### 排除或包括外部用户或用户组 {#exclude-or-include-an-external-user-or-group}

您可以限制某些外部用户或用户组的文档安全注册。 此选项非常有用，例如，允许访问特定用户组，但排除属于该用户组的特定个人。

以下设置位于“已邀请的用户注册”页面的“电子邮件限制过滤器”区域。

**排除：** 键入要排除的用户或用户组的电子邮件地址。 要排除多个用户或用户组，请在新行上键入每个电子邮件地址。 要排除属于特定域的所有用户，请输入通配符和域名。 例如，要排除example.com域中的所有用户，请输入&amp;ast;.example.com。

**包含：** 键入要包含的用户或用户组的电子邮件地址。 要包括多个用户或用户组，请在新行上键入每个电子邮件地址。 要包括属于特定域的所有用户，请输入通配符和域名。 例如，要在example.com域中包含所有用户，请输入&amp;ast;.example.com。

### 服务器和注册帐户参数 {#server-and-registration-account-parameters}

以下设置位于“已邀请的用户注册”页面的“常规设置”区域。

**SMTP主机：** SMTP服务器的主机名。 SMTP服务器管理发出的电子邮件通知以注册和激活受邀用户帐户。

如果SMTP主机需要，请在“SMTP服务器帐户名”和“SMTP服务器帐户密码”框中键入所需信息以连接到SMTP服务器。 有些组织不执行此要求。 如果需要信息，请咨询您的系统管理员。

**SMTP服务器套接字类名：** SMTP服务器的套接字类名。 例如，javax.net.ssl.SSLSocketFactory。

**电子邮件内容类型：** 接受的MIME类型，如text/plain或text/html。

**电子邮件编码：** 发送电子邮件时使用的编码格式。 您可以指定任何编码，例如，UTF-8(Unicode)或ISO-8859-1（拉丁语）。 默认为UTF-8。

**重定向电子邮件地址：** 当您为此设置指定电子邮件地址时，任何新邀请都将发送到提供的地址。 此设置可用于测试目的。

**使用本地域：** 选择相应的域。 在新安装中，请确保您使用“用户管理”创建了域。 如果这是升级，则在升级过程中会创建外部用户域，并且可以使用该域。

**对SMTP服务器使用SSL:** 选择此选项可为SMTP服务器启用SSL。

**在注册页面上显示登录链接：** 在为受邀用户显示的注册页面上显示登录链接。

**为SMTP服务器启用传输层安全性(TLS)**

1. 打开管理控制台。

   管理控制台的默认位置为 `https://<server>:<port>/adminui`。

1. 导航到“主页”>“服务”>“文档安全性”>“配置”>“受邀用户注册”。
1. 在“受邀用户注册”中，指定所有配置设置，然后单击“确定”。

   >[!NOTE]
   >
   >如果使用Microsoft Office 365作为SMTP服务器发送用户注册邀请，请使用以下设置：
   >
   >**SMTP主机：** smtp.office365.com
   >**端口：** 587

1. 接下来，您需要更新config.xml。 请参 [阅为传输层安全(TLS)启用SMTP的配置](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>如果对“受邀用户注册”选项进行了任何更改，则会覆盖config.xml文件并取消激活TLS。 如果覆盖更改，您需要执行上述步骤以重新激活对已邀请用户注册的TLS支持。

### 注册邀请电子邮件设置 {#registration-invitation-email-settings}

文档安全性在您创建新的受邀用户帐户或现有用户添加以前未注册或受邀注册到策略的外部收件人时自动发出注册邀请电子邮件。 电子邮件中包含一个链接，收件人可使用该链接访问注册页面并输入个人帐户信息，包括用户名和密码。 密码可以是八个字符的任意组合。

当收件人激活帐户时，用户将成为本地用户。

以下设置位于“已邀请的用户注册”页面的“邀请电子邮件配置”区域。

**发件人：** 发送邀请电子邮件的电子邮件地址。 发件人电子邮件地址的默认格式为postmaster@[your_installation_domain].com。

**主题：** 邀请电子邮件的默认主题。

**超时：** 如果外部用户未注册，则注册邀请的过期天数。 默认值为30天。

**消息：** 邀请用户注册的消息正文中显示的文本。

### 激活电子邮件设置 {#activation-email-settings}

在受邀用户注册后，文档安全性会发送激活电子邮件。 激活电子邮件中包含指向帐户激活页面的链接，用户可在该页面激活其帐户。 激活帐户后，用户可以使用其电子邮件地址和注册时创建的密码登录文档安全性。

当收件人激活用户帐户时，用户将成为本地用户。

以下设置位于“已邀请的用户注册”页面的“激活电子邮件配置”区域。

>[!NOTE]
>
>还建议您在登录屏幕上配置一条消息，建议外部用户如何联系其管理员获取新密码或其他信息。

**发件人：** 发送激活电子邮件的电子邮件地址。 此电子邮件地址会从注册者的电子邮件主持人接收失败的投放通知，并会收到收件人回复注册电子邮件时发送的任何消息。 发件人电子邮件地址的默认格式为postmaster@[your_installation_domain].com。

**主题：** 激活电子邮件的默认主题。

**超时：** 如果用户未激活帐户，激活邀请的过期天数。 默认值为30天。

**消息：** 消息正文中显示的文本会显示一条消息，指示需要激活收件人的用户帐户。 您可能还希望包含诸如如何联系管理员以获取新密码等信息。

### 配置密码重置电子邮件 {#configure-a-password-reset-email}

如果必须重置受邀用户的口令，则会生成一封确认电子邮件，邀请用户选择新口令。 无法确定用户的口令；如果用户忘记了它，则必须重置它。

以下设置位于“已邀请的用户注册”页面的“重置密码电子邮件”区域。

**发件人：** 发送密码重置电子邮件的电子邮件地址。 发件人电子邮件地址的默认格式为postmaster@[your_installation_domain].com。

**主题：** 重置电子邮件的默认主题。

**消息：** 消息正文中显示的文本会显示一条消息，指示收件人的外部用户密码已重置。

## 使用户和用户组能够创建策略 {#enable-users-and-groups-to-create-policies}

“配置”页面包含指向“我的策略”页的链接，您可以在该页中指定哪些最终用户可以创建我的策略，以及哪些用户和组在搜索结果中可见。 “我的策略”页面包含两个选项卡：

**创建策略选项卡：** 用于配置用户权限以创建自定义策略。

**可见的“用户和用户组”选项卡：** 用于控制哪些用户和用户组在用户搜索结果中可见。 超级用户或策略集管理员需要选择在用户管理中创建的域并将其添加到每个策略集的可见用户和组。 此列表对策略集协调员可见，用于设置策略集协调员在选择要添加到策略的用户时可以浏览哪些域的限制。

在授予用户创建自定义策略的权限之前，请考虑您希望各个用户拥有多少访问权限或控制权。 此外，请考虑您希望用户和用户组在搜索中可见时的暴露程度。

### 指定可以创建策略的用户和用户组 {#specify-users-and-groups-who-can-create-policies}

以管理员身份指定哪些用户和用户组可以创建自定义策略。 可以在用户和用户组级别设置此权限。 搜索功能可搜索用户和用户组的用户管理数据库。

1. 在管理控制台中，单击“服务”>“文档安全”>“配置”>“我的策略”。
1. 在“我的策略”页面上，单击“创建策略”选项卡，然后单击“添加用户和用户组”。
1. 在“查找”框中，键入要搜索的用户或用户组的用户名或电子邮件地址。 如果您没有此信息，请将该框留空。 您还可以键入部分名称或电子邮件地址，例如您只知道用户名的前两个字母时。
1. 在使用列表中，选择搜索参数名称或电子邮件。
1. 在“类型”列表中，选择“组”或“用户”以缩小搜索范围。
1. 在入列表中，选择要搜索的域。 如果您不知道用户或用户组的域，请选择“所有域”。
1. 在“显示”列表中，指定每页要显示的搜索结果数，然后单击“查找”。
1. 要添加“我的策略”用户和用户组，请选中要添加的每个用户和用户组对应的复选框。
1. 单击“添加”，然后单击“确定”。

您选定的用户和用户组现在具有创建自定义策略的权限。

### 从用户或用户组删除创建自定义策略权限 {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. 在文档安全页面上，单击配置>我的策略。
1. 在“我的策略”页面上，单击“创建策略”选项卡。 此时将显示具有创建自定义策略权限的用户和用户组。
1. 选中要从此权限中删除的用户和用户组旁边的复选框。
1. 单击“删除”，然后单击“确定”。

### 指定在搜索中可见的用户和用户组 {#specify-users-and-groups-that-are-visible-in-searches}

当用户管理其自定义策略时，他们可以搜索要添加到其策略中的用户和用户组。 您必须指定用户和用户组在这些搜索中可见的域。

1. 在文档安全页面上，单击配置>我的策略。
1. 在“我的策略”页面上，单击“可见的用户和用户组”选项卡。
1. 要使域中的用户和用户组可见，请单击“添加域”，选择域，然后单击“添加”。 要删除域，请选中该域名旁边的复选框，然后单击“删除”。

## 手动编辑文档安全配置文件 {#manually-editing-the-document-security-configuration-file}

您可以导入和导出存储在文档安全数据库中的配置信息。 例如，当您从分阶段移动到生产环境时，您可能希望制作配置信息的备份副本，或者您可能希望编辑只能配置在编辑此文件中的高级选项。

您可以使用配置文件进行以下更改：

[在创建和编辑策略时显示CATIA权限](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[指定脱机同步的超时时间](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[拒绝特定应用程序的文档安全服务](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[禁用外部链接](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>导入配置文件会根据文件中的信息重新配置系统。 动态水印配置和自定义事件信息是例外，这些信息不会与导出的配置文件一起保存。 必须在新系统中手动配置此信息。 只有熟悉文档安全性和XML的系统管理员或专业服务顾问才应修改配置文件的内容，例如重新配置损坏的设置或调整特定企业部署方案的参数。

**导出配置文件**

1. 在管理控制台中，单击“服务”>“文档安全性11”>“配置”>“手动配置”。
1. 单击“导出”，然后将配置文件保存到其他位置。 默认文件名为config.xml。
1. 单击“确定”。
1. 在更改配置文件之前，请制作备份副本，以备需要还原时需要。

**导入配置文件**

1. 在管理控制台中，单击“服务”>“文档安全性11”>“配置”>“手动配置”。
1. 单击“浏览”转到配置文件，然后单击“导入”。 不能直接在“文件名”(File Name)框中键入路径。
1. 单击“确定”。

### 指定脱机同步的超时时间 {#specify-a-timeout-period-for-offline-synchronization}

文档安全使用户能够在未连接到文档安全服务器时打开和使用受保护的文档。 用户的客户端应用程序必须定期与服务器同步，以保持有效的文档脱机使用。 当用户第一次打开受保护的文档时，系统会询问他们的计算机是否应获得执行定期客户端同步的授权。

默认情况下，当用户连接到文档安全服务器时，每四小时自动进行同步，并根据需要进行同步。 如果用户脱机时文档的脱机期间过期，则用户必须重新连接到服务器，以使客户端应用程序与服务器同步。

在文档安全配置文件中，可以指定自动后台同步的默认频率。 此设置用作默认超时期客户端应用程序，除非客户端明确设置自己的超时值。

1. 导出文档安全配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在编辑器中打开配置文件并找到该 `PolicyServer` 节点。 在该节点下，找到该 `ServerSettings` 节点。
1. 在节 `ServerSettings` 点中，添加以下条目，然后保存文件：

   `<entry key="BackgroundSyncFrequency" value="`*time *`"/>`

   其 *中* ，时间是自动后台同步之间的秒数。 如果将此值发送到，则始 `0`终进行同步。 默认值是秒 `14400` （每四小时）。

1. 导入配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 拒绝特定应用程序的文档安全服务 {#denying-document-security-services-for-specific-applications}

您可以配置文档安全性，以拒绝满足特定条件的应用程序的服务。 条件可以指定单个属性，如平台名称，也可以指定多组属性。 此功能可以帮助您控制文档安全性必须处理的请求。 以下是该功能的一些应用程序：

* **收入保护：** 您可能希望拒绝访问任何不支持您的收入惯例的客户端应用程序。
* **应用程序兼容性：** 某些应用程序可能与文档安全服务器的策略或行为不兼容。

当客户端应用程序尝试建立具有文档安全性的链接时，它们会提供应用程序、版本和平台信息。 文档安全性将此信息与从文档安全配置文件获得的拒绝设置进行比较。

“拒绝”设置可以包含多组拒绝条件。 如果任何一个集的所有属性都匹配，则拒绝请求应用程序访问文档安全服务。

拒绝服务功能要求客户端应用程序使用文档安全性C++客户端SDK版本8.2或更高版本。 以下Adobe产品在请求文档安全服务时提供产品信息：

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard及更高版本
* Adobe Reader 9.0及更高版本
* 适用于Microsoft Office 8.2和更高版本的Acrobat Reader DC扩展

客户端应用程序使用文档安全C++客户端SDK中的客户端API从文档安全中请求服务。 客户端API请求包括平台和SDK版本信息（预编译到客户端API中）以及从客户端应用程序获取的产品信息。

客户端应用程序或插件在实现回调函数时提供产品信息。 应用程序提供以下信息：

* 集成商名称
* 集成商版本
* 应用程序系列
* 应用程序名称
* 应用程序版本

如果任何信息不适用，客户端应用程序将相应字段留空。

当请求文档安全服务时，多个Adobe应用程序会包含产品信息，包括Acrobat、Adobe Reader和Acrobat Reader DC的Microsoft Office扩展。

**Acrobat和Adobe Reader**

当Acrobat或Adobe Reader从文档安全性请求服务时，它会提供以下产品信息：

* **集成商：** Adobe Systems, Inc.
* **集成商版本：** 1.0
* **应用程序系列：** Acrobat
* **应用程序名称：** Acrobat
* **应用程序版本：** 9.0.0

**适用于Microsoft Office的Acrobat Reader DC扩展**

适用于Microsoft Office的Acrobat Reader DC扩展是与Microsoft Word、Microsoft Excel和Microsoft PowerPoint一起使用的Microsoft Office产品的插件。 当它请求服务时，它提供以下信息：

* **集成商：** Adobe Systems Incorporated
* **集成商版本：** 8.2
* **应用程序系列：** 适用于Microsoft Office的Acrobat Reader DC扩展
* **应用程序名称：** Microsoft Word、Microsoft Excel或Microsoft PowerPoint
* **应用程序版本：** 2003年或2007年

**将文档安全性配置为拒绝特定应用程序的服务**

1. 导出文档安全配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在编辑器中打开配置文件并找到该 `PolicyServer` 节点。 添加一 `ClientVersionRules` 个节点作为该节点的直接子 `PolicyServer` 节点（如果不存在）:

   ```as3
    <node name="ClientVersionRules">
        <map>
            <entry key="infoURL" value="URL"/>
        </map>
        <node name="Denials">
            <map/>
            <node name="MyEntryName">
                <map>
                    <entry key="SDKPlatforms" value="platforms"/>
                    <entry key="SDKVersions" value="versions"/>
                    <entry key="AppFamilies" value="families"/>
                    <entry key="AppNames" value="names"/>
                    <entry key="AppVersions" value="versions"/>
                    <entry key="Integrators" value="integrators"/>
                    <entry key="IntegratorVersions" value="versions"/>
                </map>
            </node>
            <node name="MyOtherEntryName"
                <map>
                    [...]
                </map>
            </node>
            [...]
        </node>
    </node>
   ```

   其中：

   `SDKPlatforms` 指定承载客户端应用程序的平台。 可能的值包括：

   * Microsoft Windows
   * Apple OS X
   * Sun Solaris
   * HP-UX
   `SDKVersions` 指定客户端应用程序使用的文档安全C++客户端API的版本。 For example, `"8.2"`.

   `APPFamilies` 由客户端API定义。

   `AppName`指定客户端应用程序的名称。 逗号用作名称分隔符。 要在名称中包含逗号，请用反斜杠(\)字符对其进行转义。 例如， *“Adobe Systems\, Inc.”*。

   `AppVersions` 指定客户端应用程序的版本。

   `Integrators` 指定开发插件或集成应用程序的公司或组的名称。

   `IntegratorVersions` 是插件或集成应用程序的版本。

1. 对于每组额外的拒绝数据，添加另 *一个MyEntryName* 元素。
1. 保存配置文件。
1. 导入配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

**示例**

在此示例中，所有Windows客户端都被拒绝访问。

```as3
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://www.dont.use/windows.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="SDKPlatforms" value="Microsoft Windows"/>
             </map>
         </node>
     </node>
 </node>
```

在此示例中，拒绝访问“我的应用程序版本3.0”和“我的其他应用程序版本2.0”。 无论拒绝的原因如何，都会使用相同的拒绝信息URL。

```as3
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
     </map>
     <node name="Denials">
         <map/>
         <node name="FirstDenialSettings">
             <map>
                 <entry key="AppNames" value="My Application"/>
                 <entry key="AppVersions" value="3.0"/>
             </map>
         </node>
         <node name="SecondDenialSettings">
             <map>
                 <entry key="AppNames" value="My Other Application"/>
                 <entry key="AppVersions" value="2.0"/>
             </map>
         </node>
     </node>
 </node>
```

在此示例中，拒绝从Microsoft PowerPoint 2007或Microsoft PowerPoint 2010安装Microsoft Office的Acrobat Reader DC扩展的所有请求。

```as3
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="AppFamilies" value=
     "document security Extension for Microsoft Office"/>
                 <entry key="AppNames" value= "Microsoft PowerPoint"/>
                 <entry key="AppVersions" value="2007,2010"/>
             </map>
         </node>
     </node>
 </node
```

### 更改水印配置参数 {#change-the-watermark-configuration-parameters}

默认情况下，您可以在水印中指定最多五个元素。 此外，要用作水印的PDF文档的最大文件大小限制为100KB。 您可以在config.xml文件中更改这些参数。

***注意&#x200B;**:您应该谨慎更改这些参数。*

1. 导出文档安全配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在编辑器中打开配置文件并找到该 `ServerSettings` 节点。
1. 在节 `ServerSettings` 点中，添加以下条目，然后保存文件： `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   第一个条目， *最大文件大小* ，是PDF水印元素允许的最大文件大小（以KB为单位）。 默认为100KB。

   第二个条目 *,max elements* ，是水印中允许的最大元素数。 默认为5。

   ```as3
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. 导入配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 禁用外部链接 {#disabling-external-links}

许多文档安全用户在使用“正确的管理”用户界面时 **** ，无法访问外部链接，如www.adobe.com:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

对config.xml的以下更改将禁用“Right Management”用户界面中的所有外部链接。

1. 导出文档安全配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在编辑器中打开配置文件并找到该 `DisplaySettings` 节点。
1. 要禁用所有外部链接，请在节 `DisplaySettings` 点中添加以下条目，然后保存文件： `<entry key="ExternalLinksAllowed" value="false"/>`

   ```as3
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. 导入配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 用于为传输层安全(TLS)启用SMTP的配置 {#configuration-to-enable-smtp-for-transport-layer-security-tls}

对config.xml的以下更改启用了对“已邀请用户注册”功能的TLS支持。

1. 导出文档安全配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在编辑器中打开配置文件并找到该 `DisplaySettings` 节点。
1. 找到以下节点： `<node name="ExternalUser">`

   ```as3
   <node name="ExternalUser">
   ```

1. 将节点中键 `SmtpUseTls` 的值设 `ExternalUser` 置为 **true**。
1. 将节点中键 `SmtpUseSsl` 的值设 `ExternalUser` 置为 **false**。
1. 保存 `config.xml`。
1. 导入配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 禁用文档安全文档的SOAP端点 {#disable-soap-endpoints-for-document-security-documents}

对config.xml的以下更改可禁用文档安全文档的SOAP端点。

1. 导出文档安全配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在编辑器中打开配置文件并找到以下节点： `<node name="DRM">`

   ```as3
   <node name="DRM">
   ```

1. 在DRM节点中，找到该节 `entry` 点：

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. 要为文档安全文档禁用SOAP端点，请将value属性设置为 **false**。

   ```as3
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. 保存 `config.xml`。
1. 导入配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 提高文档安全服务器的可伸缩性 {#increasingscalability}

默认情况下，在同步脱机使用的文档以及当前文档的信息时，文档安全客户端会获取用户有权访问的所有其他文档的策略、水印、许可证和撤销更新信息。 如果这些更新和信息未与客户端同步，则在脱机模式下打开的文档可能仍会打开，并显示旧的策略、水印和撤销信息。

通过限制发送到客户端的信息，可以提高文档安全服务器的可伸缩性。 发送给客户端的信息量减少，从而提高了可伸缩性、缩短了响应时间并提高了服务器的性能。 执行以下步骤以提高可伸缩性：

1. 导出文档安全配置文件。 (请参 [阅手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在编辑器中打开配置文件并找到ServerSettings节点。
1. 在ServerSettings节点中，将属性的值 `DisableGlobalOfflineSynchronizationData`设置为 `true`。

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   当设置为true时，文档安全服务器仅发送当前文档的信息，而其余文档(用户有权访问的其他文档)的信息不发送给客户端。

   >[!NOTE]
   >
   >默认情况下，键的 `DisableGlobalOfflineSynchronizationData`值设置为 `false`。

1. 保存并导入配置文件。 (请参 [阅手动编辑文档安全配置文件](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

