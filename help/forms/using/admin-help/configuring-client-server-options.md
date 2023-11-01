---
title: 配置客户端和服务器选项
description: 了解如何配置各种客户端和服务器选项，如服务器配置设置、Document Security角色和事件审核。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '10239'
ht-degree: 0%

---

# 配置Document Security服务器 {#configure-the-document-security-server}

1. 在管理控制台中，单击服务> document security >配置>服务器配置。
1. 配置设置并单击“确定”。

## 服务器配置设置 {#server-configuration-settings}

**基本URL：** 基础Document Security URL，包含服务器名称和端口。 附加到基础的信息将创建连接URL。 例如，会追加/edc/Main.do以访问网页。 用户还可以通过此URL响应外部用户注册邀请。

如果您使用的是IPv6，请输入基本URL作为计算机名或DNS名。 如果您使用数字IP地址，Acrobat将无法打开受策略保护的文件。 此外，请为您的服务器使用HTTP安全(HTTPS) URL。

>[!NOTE]
>
>基础URL嵌入在受策略保护的文件中。 客户端应用程序使用基本URL连接回服务器。 安全文件将继续包含基本URL，即使稍后更改它。 如果更改基本URL，则需要更新所有连接客户端的配置信息。

**默认脱机租赁期：** 用户可以脱机使用受保护文档的默认时间长度。 此设置确定在创建策略时自动离线租赁期设置的初始值。 （请参阅创建和编辑策略。） 租赁期到期后，收件人必须再次同步文档才能继续使用它。

有关离线租赁和同步的工作原理的讨论，请参见 [关于配置脱机租用和同步的入门指南](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**默认脱机同步时段：** 任何文档从最初受保护起可脱机使用的最长时间。

**客户端会话超时：** 如果通过客户端应用程序登录的用户不与Document Security交互，则Document Security断开连接的时长（以分钟为单位）。

**允许匿名用户访问：** 选择此选项可启用创建共享策略和个人策略的功能，以允许匿名用户打开受策略保护的文档。 （没有帐户的用户可以访问文档，但他们无法登录到Document Security或使用其他受策略保护的文档。）

**禁用对版本7客户端的访问：** 指定用户是否可以使用Acrobat或Reader7.0连接到服务器。 如果选择该选项，用户必须使用Acrobat或Reader 8.0及更高版本才能对PDF文档完成Document Security操作。 如果策略要求Acrobat或Reader 8.0及更高版本在打开受策略保护的文档时必须在认证模式下运行，则应禁用对Acrobat或Reader7的访问。 （请参阅指定用户和组的文档权限。）

**允许每个文档的脱机访问** 选择此选项可指定每个文档的脱机访问。 如果启用此设置，则用户将只能脱机访问至少在线打开过一次的文档。

**允许用户名密码身份验证：** 选择此选项可允许客户端应用程序在连接到服务器时使用用户名/密码验证。

**允许Kerberos身份验证：** 选择此选项可允许客户端应用程序在连接到服务器时使用Kerberos身份验证。

**允许客户端证书身份验证：** 选择此选项可允许客户端应用程序在连接到服务器时使用证书身份验证。

**允许扩展身份验证** 选择以启用扩展身份验证，然后输入扩展身份验证登录URL。

选择此选项可使客户端应用程序使用扩展身份验证。 扩展身份验证为AEM Forms服务器上配置的自定义身份验证流程和不同的身份验证选项提供了支持。 例如，用户现在可以从Acrobat和Reader客户端体验基于SAML的身份验证，而不是AEM表单用户名/密码。 默认情况下，登录URL包含 *localhost* 作为服务器名称。 将服务器名称替换为完全限定的主机名。 如果尚未启用扩展身份验证，则会从基本URL自动填充登陆URL中的主机名。 请参阅 [添加扩展身份验证提供程序](configuring-client-server-options.md#add-the-extended-authentication-provider).

***注意&#x200B;**：带有Adobe Acrobat 11.0.6版或更高版本的Apple Mac OS X支持扩展身份验证。*

**扩展身份验证的首选HTML控制宽度** 指定在Acrobat中打开用于输入用户凭据的扩展身份验证对话框的宽度。

**扩展身份验证的首选HTML控制高度** 指定在Acrobat中打开用于输入用户凭据的扩展身份验证对话框的高度。

***注意&#x200B;**：此对话框的宽度和高度限制如下：*
宽度：最小值= 400，最大值= 900

高度：最小值= 450；最大值= 800

**启用客户端凭据缓存：** 选择此选项可允许用户缓存其凭据（用户名和密码）。 缓存用户的凭据时，他们不必在每次打开文档时或在Adobe Acrobat的“管理安全策略”页面上单击“刷新”按钮时输入凭据。 您可以指定用户必须再次提供其凭据之前的天数。 将天数设置为0可无限期地缓存凭据。

## 配置Document Security用户和管理员 {#configuring-document-security-users-and-administrators}

### 将Document Security角色分配给管理员 {#assigning-document-security-roles-to-administrators}

您的AEM表单环境包含一个或多个具有创建用户和组的相应权限的管理员用户。 如果您的组织正在使用Document Security，则还必须至少向一位管理员分配管理受邀用户和本地用户的权限。

管理员还必须具有管理控制台用户角色才能访问管理控制台。 (请参阅 [创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### 配置可见的用户和组 {#configuring-visible-users-and-groups}

要在策略用户搜索期间查看所选域中的用户和组，超级管理员或策略集管理员必须选择域（在用户管理中创建）并将其添加到每个策略集的可见用户和组列表中。

可见的用户和组列表对策略集协调器可见，用于限制最终用户选择要添加到策略中的用户或组时可以浏览的域。 如果未执行此任务，则策略集协调员将找不到任何要添加到策略中的用户或组。 任何给定的策略集都可以有多个策略集协调器。

1. 使用Document Security安装和配置AEM Forms环境后，请在“用户管理”中设置所有相应的域。 <!-- Fix broken link (See Setting up and managing domains) -->

   ***注意&#x200B;**：必须先创建域，然后才能创建任何策略。*

1. 在管理控制台中，单击服务>文档管理>策略，然后单击策略集选项卡。
1. 选择“全局策略集”，然后单击“可见用户和组”选项卡。
1. 单击添加域，并根据需要添加现有域。
1. 导航到“服务”>“Document Security”>“配置”>“我的策略”，然后单击“可见的用户和组”选项卡。
1. 单击添加域，并根据需要添加现有域。

## 添加扩展身份验证提供程序 {#add-the-extended-authentication-provider}

AEM forms提供了一个示例配置，您可以为您的环境自定义该配置。 执行以下步骤：

>[!NOTE]
>
>Apple Mac OS X 11.0.6及更高版本中的Adobe Acrobat支持扩展身份验证。

1. 获取WAR文件的样例并部署它。 请参阅适用于您的应用程序服务器的安装指南。
1. 确保表单服务器具有完全限定的名称（而不是IP地址）作为基本URL，并且它是HTTPS URL。 请参阅 [服务器配置设置](configuring-client-server-options.md#server-configuration-settings).
1. 从“服务器配置”页启用“扩展验证”。 请参阅 [服务器配置设置](configuring-client-server-options.md#server-configuration-settings).
1. 在用户管理配置文件中添加所需的SSO重定向URL。 请参阅 [为扩展身份验证添加SSO重定向URL](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### 为扩展身份验证添加SSO重定向URL {#add-sso-redirect-urls-for-extended-authentication}

启用扩展身份验证后，用户在Acrobat XI或Reader XI中打开受策略保护的文档时，会看到身份验证对话框。 此对话框加载您在Document Security Server设置上指定为扩展身份验证登录URL的HTML页。 请参阅 [服务器配置设置](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>Apple Mac OS X 11.0.6及更高版本中的Adobe Acrobat支持扩展身份验证。

1. 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。
1. 单击导出并将配置文件保存到磁盘。
1. 在编辑器中打开文件，并找到AllowedUrls节点。
1. 在 `AllowedUrls` 节点，添加以下行： `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. 保存文件，然后从“手动配置”页面导入更新的文件：在管理控制台中，单击“设置”>“用户管理”>“配置”>“导入和导出配置文件”。

## 配置脱机安全 {#configuring-offline-security}

document security提供在没有Internet或网络连接的情况下离线使用受策略保护的文档的功能。 此功能要求策略允许离线访问，如中所述 [指定用户和组的文档权限](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). 在脱机使用具有此类策略的文档之前，收件人必须在联机时打开该文档，并在出现提示时单击“是”启用脱机访问。 还可以请求收件人验证其身份。 然后，收件人可以在策略中指定的离线租赁期的持续时间内离线使用文档。

离线租赁期结束时，收件人必须联机打开文档或使用Acrobat或Acrobat Reader DC extensions菜单命令再次与Document Security同步。 (请参阅 *Acrobat帮助* 或相应的 *Acrobat Reader DC扩展帮助*.)

由于允许脱机访问的文档需要在脱机存储文件的计算机上缓存关键资料，因此，如果未经授权的用户可以获得关键资料，则文件可能会受到危害。 为了弥补这种可能性，提供了计划和手动密钥变换选项，您可以配置这些选项，以防止未经授权的人使用密钥访问文档。

### 设置默认离线租赁期 {#set-a-default-offline-lease-period}

受策略保护文档的收件人可以在策略指定的天内使文档离线。 最初将文档与Document Security同步后，收件人可以脱机使用文档，直到脱机租赁期到期。 租赁期到期后，收件人必须联机并登录以与Document Security同步才能继续使用该文档。

您可以配置默认的脱机租赁期。 当任何人创建或编辑策略时，可以将租赁期更改为默认租赁期。

1. 在document security页面上，单击配置>服务器配置。
1. 在默认脱机租赁期框中，键入脱机租赁期的天数。
1. 单击确定。

### 管理密钥变换 {#manage-key-rollovers}

Document Security使用加密算法和许可证来保护文档。 当文档安全加密时，它生成和管理一个称为的解密密钥 *文档密钥* 它会传递给客户端应用程序。 如果保护文档的策略允许脱机访问，则称为的脱机密钥 *主体键* 此外，还会为每个对文档具有离线访问权限的用户生成。

>[!NOTE]
>
>如果不存在主体密钥，则Document Security会生成一个主体密钥来保护文档。

要脱机打开受策略保护的文档，用户的计算机必须具有相应的主体密钥。 当用户与Document Security同步（在线打开受保护的文档）时，计算机将获得主体密钥。 如果此主体密钥被泄漏，用户离线访问的任何文档也可能被泄漏。

减少离线文档威胁的一种方法是避免允许离线访问特别敏感文档。 另一种方法是周期性地滚过主键。 当Document Security滚动密钥时，任何现有密钥都不能再访问受策略保护的文档。 例如，如果犯罪者从被盗的膝上型计算机获得主密钥，则该密钥不能用于访问变换后发生保护后的文档。 如果您怀疑特定主体密钥已泄露，则可以手动滚动密钥。

但是，您还需要注意，密钥滚动更新会影响所有主密钥，而不仅仅影响一个主密钥。 它还降低了系统的可扩展性，因为客户端必须存储更多密钥才能进行离线访问。 默认密钥滚动更新频率为20天。 建议不要将此值设置为小于14天，因为可能会阻止用户查看离线文档，并且系统性能可能会受到影响。

在下面的示例中，Key1是两个主键中较旧的键，Key2是较新的键。 第一次单击“Rollover Keys Now（立即滚动更新密钥）”按钮时，Key1无效，并生成一个较新的有效主体密钥(Key3)。 当用户与Document Security同步时（通常通过在线打开受保护的文档），将获得密钥3。 但是，在达到策略中指定的最大离线租赁期之前，不会强制用户与Document Security同步。 在第一次密钥滚动更新后，保持离线状态的用户仍可以打开离线文档，包括那些受Key3保护的文档，直到他们达到最大离线租赁期为止。 再次单击“Rollover Keys Now（立即滚动更新键）”按钮时，Key2将变为无效，并创建Key4。 在两次密钥滚动更新期间保持离线状态的用户无法打开受密钥3或密钥4保护的文档，直到他们与Document Security同步为止。

**更改键变换频率**

为保密起见，当您使用离线文档时，Document Security提供了一个自动密钥滚动更新选项，默认频率期间为20天。 您可以更改变换频率；但是，请避免将该值设置为小于14天，因为可能会阻止用户查看脱机文档，并且系统性能可能会受到影响。

1. 在Document Security页面上，单击配置>密钥管理。
1. 在“键变换频率”框中，键入变换期间的天数。
1. 单击确定。

**手动滚动主键**

要维护脱机文档的机密性，您可以手动滚动主体键。 您可能会发现必须手动滚动密钥（例如，如果从缓存该密钥的计算机中获取该密钥以启用对文档的脱机访问的用户危及该密钥）。

>[!NOTE]
>
>避免频繁使用手动变换，因为它会导致所有主体键变换（而不仅仅是一个主体键），并可能会暂时阻止用户离线查看新文档。

在客户端计算机上先前存在的密钥失效之前，必须将主密钥翻转两次。 已失效主体密钥的客户端计算机必须与Document Security服务重新同步，以获取新的主体密钥。

1. 在Document Security页面上，单击配置>密钥管理。
1. 单击“Rollover Keys Now（立即变换密钥）” ，然后单击“OK（确定）”。
1. 等待大约10分钟。 服务器日志中显示以下日志消息： `Done RightsManagement key rollover for`*N* `principals`. 位置 *N* 是document security系统中的用户数。
1. 单击“Rollover Keys Now（立即变换密钥）” ，然后单击“OK（确定）”。
1. 等待大约10分钟。

## 配置事件审核和隐私设置 {#configuring-event-auditing-and-privacy-settings}

Document Security可以审核和记录与与与受策略保护的文档、策略、管理员和服务器的交互相关的事件信息。 您可以配置事件审计，并指定要审计的事件类型。 要审计特定文档的事件，还必须启用策略上的审计选项。

启用审核后，您可以在“事件”页面上查看已审核事件的详细信息。 document security用户还可以查看与他们使用或创建的受策略保护的文档具体相关的事件。

您可以选择以下类型的审计事件：

* 受策略保护的文档事件，例如授权用户或未经授权用户尝试打开文档
* 策略事件，例如创建、更改、删除、启用和禁用策略
* 用户事件，如外部用户邀请和注册、已激活和已停用用户帐户、用户密码更改以及配置文件更新
* AEM表单事件，如版本不匹配、不可用的目录服务器和授权提供程序以及服务器配置更改

### 启用或禁用事件审核 {#enable-or-disable-event-auditing}

您可以启用和禁用与服务器、受策略保护的文档、策略、策略集和用户相关的事件审核。 启用事件审计时，您可以选择审计所有可能的事件，也可以选择要审计的特定事件。

启用服务器审核后，可以在“事件”页面上查看已审核的事件。

1. 在管理控制台中，单击服务> Document Security >配置>审核和隐私设置。
1. 要配置服务器审计，请在“启用服务器审计”下，选择“是”或“否”。
1. 如果选择是，请在每个事件类别下，执行以下操作之一以选择要审核的选项：

   * 要审计类别中的所有事件，请选择全部。
   * 要仅审计某些事件，请取消选择全部，然后选中要审计的事件旁边的复选框。

     (请参阅 [事件审计选项](configuring-client-server-options.md#event-auditing-options).)

1. 单击确定。

>[!NOTE]
>
>处理网页时，请避免使用浏览器按钮（如“返回”按钮、“刷新”按钮以及“后退”或“前进”箭头），因为此操作可能会导致不必要的数据捕获和数据显示问题。

### 启用或禁用隐私通知 {#enable-or-disable-privacy-notification}

您可以启用和禁用隐私通知消息。 启用隐私通知后，当收件人尝试打开受策略保护的文档时，将会显示一条消息。 通知通知用户正在审核文档使用情况。 您还可以指定用户可用于查看隐私策略页面的URL（如果可用）。

1. 在管理控制台中，单击“服务”>“Document Security”>“配置”>“审核和隐私设置”。
1. 要配置隐私通知，请在启用隐私通知下，选择是或否。

   如果附加到文档的策略允许匿名用户访问，并且“启用隐私声明”设置为“否”，则不会提示用户登录，并且不会显示隐私通知消息。

   如果附加到文档的策略不允许匿名用户访问，则用户将看到隐私通知消息。

1. 如果适用，在隐私URL框中，键入隐私策略页面的URL。 如果将隐私URL框保留为空，则会显示adobe.com中的隐私页面。
1. 单击确定。

>[!NOTE]
>
>禁用隐私声明不会禁用文档使用情况审核。 通过扩展使用跟踪支持的开箱即用审核操作和自定义操作仍可以收集用户行为信息。

### 导入自定义审核事件类型 {#import-a-custom-audit-event-type}

如果您使用启用了Document Security的应用程序，该应用程序支持审核其他事件，例如特定文件类型的事件，则Adobe合作伙伴可以为您提供自定义审核事件，您可以将这些事件导入Document Security。 仅当Adobe合作伙伴为您提供了自定义事件类型时才使用此功能。

1. 在管理控制台中，单击服务> Document Security >配置>事件管理。
1. 单击“浏览”转到要导入的XML文件，然后单击“导入”。
1. 如果发现相同的事件代码和命名空间组合，导入将覆盖服务器上现有的自定义审核事件类型。
1. 单击确定。

### 删除自定义审核事件类型 {#delete-a-custom-audit-event-type}

1. 在管理控制台中，单击服务> document security >配置>事件管理。
1. 选中要删除的自定义审核事件类型旁边的复选框，然后单击删除。
1. 单击确定。

### 导出审核事件 {#export-audit-events}

您可以将审核事件导出到文件以进行存档。

1. 在管理控制台中，单击服务> Document Security >配置>事件管理。
1. 根据需要编辑Export Audit Events下的设置。 您可以指定：

   * 要导出的审核事件的最小年龄
   * 单个文件中包含的最大审核事件数。 服务器根据此值生成一个或多个文件。
   * 将在其中创建文件的文件夹。 此文件夹位于表单服务器上。 如果文件夹路径是相对路径，则它是相对于应用程序服务器根目录的相对路径。
   * 用于审核事件文件的文件前缀
   * 文件的格式，即与Microsoft Excel兼容的逗号分隔值(CSV)文件或XML文件。

1. 单击“导出”。 如果要取消导出，请单击“取消导出”。 如果其他用户已计划导出，则在该导出完成之前，“取消导出”按钮不可用。 如果其他用户已计划导出，则“取消导出”按钮不可用。 要检查计划的导出或删除是否已启动或完成，请单击“刷新”。

### 删除审核事件 {#delete-audit-events}

您可以删除早于指定天数的审核事件。

1. 在管理控制台中，单击服务> Document Security >配置>事件管理。
1. 在删除审计事件下，指定删除早于以下时间的审计事件框中的天数。
1. 单击删除。单击“导出”。 如果要取消删除，请单击“取消删除”。 如果其他用户已计划删除，则在该导出完成之前，“取消删除”按钮不可用。 如果其他用户已计划导出，则“取消删除”按钮不可用。 要检查计划的删除是否已启动或完成，请单击“刷新”。

### 事件审计选项 {#event-auditing-options}

您可以启用和禁用事件审核，并指定要审核的事件类型。

**文档事件**

**查看文档：** 收件人查看受策略保护的文档。

**关闭文档：** 收件人关闭受策略保护的文档。

**打印低分辨率** 收件人打印指定了低分辨率选项的受策略保护的文档。

**打印高分辨率：** 收件人打印指定了高分辨率选项的受策略保护的文档。

**将注释添加到文档：** 收件人将注释添加到PDF文档。

**撤销文档：** 用户或管理员撤销对受策略保护文档的访问权限。

**取消撤销文档：** 用户或管理员恢复对受策略保护文档的访问权限。

**表单填写：** 收件人将信息输入到可填写表单的PDF文档中。

**已删除策略：** 发布者从文档中删除策略以撤销安全保护。

**更改文档吊销URL：** 来自API级别的调用会更改为访问替换已撤销文档的新文档而指定的撤销URL。

**修改文档：** 收件人更改受策略保护文档的内容。

**签名文档：** 收件人签署文档。

**保护新文档：** 用户应用策略来保护文档。

**切换文档策略：** 用户或管理员切换附加到文档的策略。

**文档发布方式：** 将在服务器上注册一个documentName和许可证与现有文档相同的新文档，并且该文档没有父子关系。 此事件可以使用AEM Forms SDK触发。

**迭代文档：** 将在服务器上注册一个documentName和许可证与现有文档相同的新文档，这些文档具有父子关系。 此事件可以使用AEM Forms SDK触发。

**策略事件**

**已创建策略：** 用户或管理员创建策略。

**启用的策略：** 管理员使策略可用。

**已更改策略：** 用户或管理员更改策略。

**禁用的策略：** 管理员使策略不可用。

**已删除策略：** 用户或管理员删除策略。

**更改策略所有者：** 来自API级别的调用会更改策略所有者。

**用户事件**

**已删除的用户：** 管理员删除用户帐户。

**注册受邀用户：** 外部用户向Document Security注册。

**成功登录：** 管理员或用户成功登录的尝试。

**受邀用户：** Document Security邀请用户注册。

**已激活的用户：** 外部用户通过使用激活电子邮件中的URL激活其帐户，或者管理员启用帐户。

**更改密码：** 受邀用户更改其密码或管理员为本地用户重置密码。

**登录失败：** 管理员或用户登录尝试失败。

**已停用用户：** 管理员禁用本地用户帐户。

**配置文件更新：** 受邀用户更改其名称、组织名称和密码。

**帐户已锁定：** 管理员锁定帐户。

**策略集事件**

**已创建策略集：** 管理员或策略集协调员创建策略集。

**已删除策略集：** 管理员或策略集协调员删除策略集。

**已修改的策略集：** 管理员或策略集协调员更改策略集。

**系统事件**

**目录同步完成：** 无法从事件页面中获取此信息。 当前目录同步信息（包括当前同步状态和上次同步的时间）将显示在“域管理”页上。 要访问管理控制台中的“域管理”页面，请单击设置>用户管理>域管理。

**客户端启用脱机访问：** 用户允许对受用户计算机上服务器保护的文档进行脱机访问。

**已同步的客户端** 客户端应用程序必须与服务器同步信息以允许离线访问。

**版本不匹配：** 与尝试连接到服务器的服务器不兼容的AEM Forms SDK版本。

**目录同步信息：** 无法从事件页面中获取此信息。 当前目录同步信息（包括当前同步状态和上次同步的时间）将显示在“域管理”页上。 要访问管理控制台中的“域管理”页面，请单击设置>用户管理>域管理。

**服务器配置更改：** 通过网页或通过导入config.xml文件手动完成的服务器配置更改。 这包括更改基本URL、会话超时、登录锁定、目录设置、密钥变换、用于外部注册的SMTP服务器设置、水印配置、显示选项等。

## 配置扩展使用跟踪 {#configuring-extended-usage-tracking}

Document Security可以跟踪可能在受保护文档上执行的各种自定义事件。 您可以在全局级别或策略级别启用Document Security Server中的事件跟踪。 然后，您可以设置JavaScript来捕获在受保护的PDF文档中执行的特定操作，如单击按钮或保存文档。 此使用情况数据将作为XML文件以键值对的形式发送，您可以将其用于进一步分析。 访问受保护文档的最终用户可以允许或拒绝来自客户端应用程序的此类跟踪。

如果在全局级别启用跟踪，则可以在策略级别覆盖此设置，并为特定策略禁用此设置。 如果在全局级别禁用跟踪，则无法进行策略级别的覆盖。 当事件计数达到25或文档关闭时，跟踪事件的列表将自动推送到服务器。 您还可以配置脚本，以根据需要明确推送事件列表。 您可以通过访问Document Security对象的属性和方法来自定义事件跟踪。

启用跟踪后，所有随后创建的策略都将默认启用跟踪。 在服务器上启用跟踪之前创建的策略将需要手动更新。

### 启用或禁用扩展使用跟踪 {#enable-or-disable-extended-usage-tracking}

在开始之前，请确保已启用“服务器审核”。 请参阅 [配置事件审核和隐私设置](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) 以了解有关审核的更多信息。

1. 在管理控制台中，单击服务> Document Security >配置>审核和隐私设置。
1. 要配置扩展使用情况跟踪，请在“启用跟踪”下，选择“是”或“否”。
1. 要设置登录页上的允许收集详细的使用情况数据复选框，请在启用跟踪默认值下，选择是或否。

要查看跟踪的事件，您可以使用事件页面上的文档事件过滤器。 使用JavaScript跟踪的事件标记为详细使用情况跟踪。 请参阅 [监视事件](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) 以了解有关事件的更多信息。

## 配置Document Security显示设置 {#configure-document-security-display-settings}

1. 在管理控制台中，单击“服务”>“Document Security”>“配置”>“显示选项”。
1. 配置设置并单击“确定”。

### 显示设置 {#display-settings}

**为搜索结果显示的行：** 执行搜索时页面上显示的行数。

**自定义客户端登录对话框**

这些设置控制当用户通过客户端应用程序登录Document Security时显示的登录提示中的文本。

**欢迎文本：** 欢迎消息文本，如“请使用用户名和密码登录”。 欢迎消息文本应包含有关如何登录到Document Security以及如何联系管理员或组织中的其他指定支持人员寻求帮助的信息。 例如，如果外部用户忘记密码或在注册或登录过程中需要帮助，则可能需要联系管理员。 欢迎文本的最大长度为512个字符。

**用户名文本：** 用户名框的文本标签。

**密码文本：** 密码框的文本标签。

**自定义客户端证书身份验证对话框**

这些设置控制证书身份验证对话框中显示的文本。

**选择身份验证类型文本：** 显示的文本，用于指示用户选择身份验证类型。

**选择证书文本：** 显示的文本，用于指示用户选择证书类型。

**证书不可用错误文本：** 所选证书不可用时显示的消息最多为512个字符。

**自定义客户端证书显示**

**仅显示受信任的凭据颁发者：** 选择此选项时，客户端应用程序仅向用户提供AEM表单配置为信任的凭据颁发者提供的证书（请参阅管理证书和凭据）。 如果未选择此选项，则会向用户显示用户系统上所有证书的列表。

## 配置动态水印 {#configure-dynamic-watermarks}

使用Document Security，您可以配置在创建策略时应用的动态水印选项的默认设置。 A *水印* 是叠加在文档中文本上的图像。 此变量可用于跟踪文档的内容，并可帮助识别内容的非法使用。

动态水印可以是由已定义变量（如用户ID和日期以及自定义文本）组成的文本，也可以是PDF中的富文本。 您可以使用多个元素配置水印，每个元素都具有自己的位置和格式。

水印不可编辑，因此它们是确保文档内容机密性的更安全方法。 动态水印还可确保水印显示足够的用户特定信息，以起到阻止进一步分发文档的作用。

当收件人查看或打印文档时，策略指定的水印显示在受策略保护的文档中。 与永久水印不同，动态水印从不保存在文档中，这提供了在Intranet环境中部署文档时所需的灵活性，以确保查看应用程序显示特定用户的身份。 此外，如果文档有多个用户，则使用动态水印意味着您可以使用一个文档，而不是多个版本，每个版本具有不同的水印。 显示的水印反映当前用户的身份。

请注意，动态水印不同于用户可以直接添加到Acrobat中的文档的水印。 结果是，在受策略保护的文档中，可以有两个水印。

### 创建水印时的注意事项 {#considerations-when-creating-watermarks}

您可以使用多个水印元素创建动态水印，并将每个元素指定为文本或PDF。 一个水印中最多可以包含五个元素。

如果选择基于文本的水印，则可以在水印中指定具有多个文本条目的多个元素，并指定每个元素的位置。 为这些元素分配有意义的名称，如页眉、页脚等。

例如，如果要在页眉、页脚、边距和整个文档中指定不同的文本作为水印，则需要创建多个水印元素并指定其位置。 如果希望用户的用户ID和访问文档的当前日期显示在标题中，右边距中的策略名称以及自定义文本“CONFIDENTIAL”在文档中对角显示，则可以定义单独的以文本为类型的水印元素，并指定其格式和位置。 当将水印应用于文档时，水印中的所有元素按它们添加到水印的顺序同时应用于文档。

通常，使用基于PDF的水印来包括图形内容（如徽标或特殊符号，如版权或注册商标）。

您可以通过修改Document Security配置文件来更改对水印元素数量和PDF文件大小的限制。 请参阅 [更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

配置水印时，请牢记以下事项：

* 不能使用受密码保护的PDF文档作为水印元素。 但是，如果您创建的水印包含其他不受密码保护的元素，则这些元素将作为水印的一部分应用。
* 您可以更改要用作水印元素的最大PDF文件大小。 但是，用作水印的大型PDF文档在使用此类水印应用的文档的脱机同步过程中会降低性能。 请参阅 [更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* 仅将所选PDF的第一页用作水印。 确保要显示为水印的信息在第一页本身可用。
* 即使您可以指定PDF文档的缩放比例，但如果您计划在页眉、页脚或边距中将其用作水印，请考虑PDF的页面大小和布局。
* 指定字体名称时，请正确输入名称。 如果AEM forms在打开文档的客户端计算机上不存在您指定的字体，则替换该字体。
* 如果选择文本作为水印内容，则指定缩放选项为“适合页面”对宽度不同的页面不起作用。
* 指定水印元素的位置时，请确保只有一个元素具有相同的位置。 如果两个水印元素具有相同的位置（例如居中），则它们看起来重叠在文档上，并且按照它们添加到水印的顺序。
* 指定字体大小和类型时，请确保文本长度在页面中完全可见。 文本内容将滚动到新行中，因此您打算显示在边距中的水印内容可能会与页面上的内容区域重叠。 但是，如果文档在Acrobat 9中打开，则超出单行的文本将被截断。

### 动态水印的限制 {#limitations-of-dynamic-watermarks}

某些客户端应用程序可能不支持动态水印。 请参阅相应的Acrobat Reader DC扩展帮助。 此外，请牢记以下关于支持动态水印的Acrobat版本的说明：

* 不能使用受密码保护的PDF文档作为水印元素。
* Acrobat和Adobe Reader 10以前的版本不支持以下水印功能：

   * PDF水印
   * 水印中的多个元素(文本/PDF)
   * 高级选项，例如页面范围或显示选项
   * 文本格式选项，例如指定的字体、字体名称和颜色。 但是，早期版本的Acrobat和Reader将以默认字体和颜色显示文本内容。

* Acrobat 9.0及更早版本： Acrobat 9.0及更早版本不支持在动态水印中使用策略名称。 如果Acrobat 9.0打开受策略保护的文档，该文档包含动态水印，其中包括策略名称和其他动态数据，则水印显示时将不包含策略名称。 如果动态水印仅包含策略名称，则Acrobat会显示错误消息

### 添加动态水印模板 {#add-a-dynamic-watermark-template}

您可以创建动态水印模板。 这些模板仍作为管理员或用户创建的策略的配置选项提供。

>[!NOTE]
>
>导出配置文件时，动态水印配置信息不会与其他配置信息一起捕获。

1. 在管理控制台中，单击“服务”>“Document Security”>“配置”>“水印”。
1. 单击“新建”。
1. 在“名称”框中，键入新水印的名称。

   ***注意&#x200B;**：水印或水印元素的名称或描述中不能使用某些特殊字符。 请参阅中列出的限制 [编辑策略的注意事项](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. 在“名称”下，在加号旁边，为水印元素输入有意义的名称（如“标题”），然后添加说明，并展开加号以显示选项。
1. 在“源”下，选择水印类型“文本”或“PDF”。
1. 如果选择了文本，请执行以下操作：

   * 选择要包含的水印类型。 如果选择“自定文本”，请在相邻的框中键入水印要显示的文本。 请记住将显示为水印的文本长度。
   * 为水印文本的文本内容指定文本格式属性，如字体名称、字体大小、前景颜色和背景颜色。 将前景色和背景色指定为十六进制值。

     ***注意&#x200B;**：如果选择缩放选项为“适合页面”，则字体大小属性不可编辑。*

1. 如果您为富水印选项选择了PDF，请单击 **浏览** 在“选择水印PDF”旁边，选择要用作水印的PDF文档。

   ***注意&#x200B;**：请勿使用受密码保护的PDF文档。 如果将受密码保护的PDF指定为水印元素，则不会应用水印。*

1. 在“用作背景”下，选择“是”或“否”。

   **注意**：当前，无论此设置如何，水印都会显示在前景中。

1. 要控制水印在文档上的显示位置，请配置“垂直对齐”和“水平对齐”选项。
1. 选择“适合页面”或选择“%”，然后在框中键入百分比。 该值必须是整数，而不是小数。 要配置水印大小，您可以使用页面百分比值或设置水印以适合页面大小。
1. 在“旋转”框中，键入旋转水印的角度。 范围从–180到180。 使用负值将水印逆时针旋转。 该值必须是整数，而不是小数。
1. 在“不透明度”框中，键入百分比。 使用整数，而不是分数。
1. 在“高级选项”下，设置以下内容：

   **页面范围选项**

   设置应显示水印的页面范围。 输入起始页为1，结束页为–1，以使所有页面都标记有水印。

   **显示选项**

   选择要使水印显示的位置。 默认情况下，水印会同时出现在软拷贝（在线）和硬拷贝（打印）上。

1. 单击 **新建** 在水印元素下，可根据需要添加更多水印元素。
1. 单击确定。

### 编辑动态水印模板 {#edit-a-dynamic-watermark-template}

1. 在管理控制台中，单击“服务”>“Document Security”>“配置”>“水印”。
1. 单击列表中的相应水印。
1. 在“编辑水印”页面上，根据需要更改设置。
1. 单击确定。

### 删除动态水印模板 {#delete-a-dynamic-watermark-template}

删除动态水印时，无法再将其添加到新策略中。 但是，水印保留在当前使用它的现有策略上，并且策略当前保护的文档将继续显示动态水印，直到您或用户编辑包含已删除水印的策略为止。 编辑策略后，不再应用水印。 此时将显示一条消息，指示已在策略上删除现有水印，用户可以选择另一个水印来替换它。

1. 在管理控制台中，单击“服务”>“Document Security”>“配置”>“水印”。
1. 选中相应水印旁边的复选框，然后单击“删除”。
1. 单击确定。

## 配置受邀用户注册 {#configuring-invited-user-registration}

组织外部的用户可以注册Document Security。 注册并激活其帐户的受邀用户可以使用他们的电子邮件地址和注册时创建的密码登录到Document Security。 已注册的受邀用户可以使用他们有权访问的受策略保护文档。

激活受邀用户后，他们将成为本地用户。 可以使用“受邀用户”和“本地用户”区域配置和管理本地用户。 (请参阅 [管理受邀的用户帐户和本地用户帐户](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

根据您为受邀用户启用的功能，这些用户也可以使用以下Document Security功能：

* 将策略应用到文档
* 创建策略
* 将受邀用户添加到策略

发生以下事件时，Document Security会自动生成注册邀请电子邮件，除非该用户已在源LDAP目录中或之前已被邀请注册：

* 现有用户将受邀用户添加到策略
* 管理员在“受邀用户注册”页面上添加受邀用户帐户

注册电子邮件包含指向注册页面的链接以及有关如何注册的信息。 受邀用户注册后，Document Security会发出一封激活电子邮件，其中包含指向激活页面的链接。 激活后，帐户将保持有效，直至您停用或删除它。

如果启用内置注册，则只需指定SMTP服务器、注册电子邮件详细信息、访问功能以及重置密码电子邮件信息一次。 在启用内置注册之前，请确保已在“用户管理”中创建了本地域，并将“Document Security邀请用户”角色分配给组织中的相应用户和组。 (请参阅 [添加本地域](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) 和 [创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) 如果您不使用内置注册，则必须使用AEM Forms SDK创建自己的用户注册系统。 请参阅中的“为AEM表单开发SPI”帮助 [使用AEM表单编程](/help/forms/developing/introducing-java-api-soap-quick.md). 如果不使用“Built-in Registration（内置注册）”选项，建议在激活电子邮件和客户端登录屏幕上配置消息，以通知用户如何联系管理员以获取新密码或其他信息。

**启用并配置受邀用户注册**

默认情况下，邀请的用户注册过程处于禁用状态。 您可以根据需要启用和禁用Document Security的受邀请用户注册。

1. 在管理控制台中，单击“服务”>“Document Security”>“配置”>“受邀用户注册”。
1. 选择启用受邀用户注册。
1. （可选）根据需要更新邀请的用户注册设置：

   * [排除或包含外部用户或组](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [服务器和注册帐户参数](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [注册邀请电子邮件设置](configuring-client-server-options.md#registration-invitation-email-settings)
   * [激活电子邮件设置](configuring-client-server-options.md#activation-email-settings)
   * [配置密码重置电子邮件](configuring-client-server-options.md#configure-a-password-reset-email)

1. （可选）在“内置注册”下，选择“是”以启用此选项。 如果未启用内置注册，则必须设置自己的用户注册系统。
1. 单击确定。

### 排除或包含外部用户或组 {#exclude-or-include-an-external-user-or-group}

您可以限制某些外部用户或用户组使用Document Security进行注册。 例如，在允许访问特定用户组但排除属于该组的特定个人时，此选项非常有用。

以下设置位于“受邀用户注册”页面的“电子邮件限制过滤器”区域。

**排除：** 键入要排除的用户或组的电子邮件地址。 要排除多个用户或组，请在新行中输入每个电子邮件地址。 要排除属于特定域的所有用户，请输入通配符和域名。 例如，要排除example.com域中的所有用户，请输入&amp;ast；.example.com。

**包含：** 键入要包含的用户或组的电子邮件地址。 要包括多个用户或组，请在新行中输入每个电子邮件地址。 要包含属于特定域的所有用户，请输入通配符和域名。 例如，要在example.com域中包含所有用户，请输入&amp;ast；.example.com。

### 服务器和注册帐户参数 {#server-and-registration-account-parameters}

以下设置位于“受邀用户注册”页面的“常规设置”区域。

**SMTP主机：** SMTP服务器的主机名。 SMTP服务器管理传出电子邮件通知，以注册和激活受邀用户帐户。

如果SMTP主机需要，请在“SMTP服务器帐户名称”和“SMTP服务器帐户密码”框中键入所需信息以连接到SMTP服务器。 某些组织不强制执行此要求。 如果您需要信息，请咨询系统管理员。

**SMTP服务器套接字类名：** SMTP服务器的套接字类名称。 例如，javax.net.ssl.SSLSocketFactory。

**电子邮件内容类型：** 接受的MIME类型，如text/plain或text/html。

**电子邮件编码：** 发送电子邮件时使用的编码格式。 您可以指定任何编码，例如，UTF-8用于Unicode，ISO-8859-1用于Latin。 缺省值为UTF-8。

**重定向电子邮件地址：** 当您为此设置指定电子邮件地址时，任何新邀请都会发送到提供的地址。 此设置可用于测试目的。

**使用本地域：** 选择相应的域。 在新安装中，请确保使用“用户管理”创建了域。 如果是升级，则会在升级期间创建外部用户域，并且可以使用。

**对SMTP服务器使用SSL：** 选择此选项为SMTP服务器启用SSL。

**在注册页面上显示登录链接：** 在注册页面上显示受邀用户的登录链接。

**为SMTP服务器启用传输层安全性(TLS)**

1. 打开管理控制台。

   管理控制台的默认位置为 `https://<server>:<port>/adminui`.

1. 导航到主页>服务> Document Security >配置>受邀用户注册。
1. 在“受邀用户注册”中，指定所有配置设置，然后单击“确定”。

   >[!NOTE]
   >
   >如果您使用Microsoft Office 365作为SMTP服务器来发送用户注册邀请，请使用以下设置：
   >
   >**SMTP主机：** smtp.office365.com
   >**端口：** 587

1. 接下来，您需要更新config.xml。 请参阅 [用于启用传输层安全性(TLS)的SMTP的配置](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>如果您对“受邀用户注册”选项进行了任何更改，则会覆盖config.xml文件并停用TLS。 如果覆盖更改，则需要执行上述步骤以重新激活TLS对受邀用户注册的支持。

### 注册邀请电子邮件设置 {#registration-invitation-email-settings}

当您创建新的受邀用户帐户或现有用户添加之前未注册或受邀注册到策略的外部收件人时，Document Security会自动发出注册邀请电子邮件。 该电子邮件包含一个链接，收件人可以使用该链接访问注册页并输入个人帐户信息，包括用户名和密码。 密码可以是八个字符的任意组合。

当收件人激活帐户时，该用户即成为本地用户。

以下设置位于“受邀用户注册”页面的“邀请电子邮件配置”区域。

**从：** 发送邀请电子邮件的电子邮件地址。 发件人电子邮件地址的默认格式为postmaster@[your_installation_domain].com.

**主题：** 邀请电子邮件默认主题。

**超时：** 如果外部用户未注册，则为注册邀请过期的天数。 默认值为30天。

**消息：** 邀请用户注册的邮件正文中显示的文本。

### 激活电子邮件设置 {#activation-email-settings}

受邀用户注册后，Document Security会发送一封激活电子邮件。 激活电子邮件包含指向帐户激活页面的链接，用户可以在该页面激活其帐户。 激活帐户后，用户可以使用他们的电子邮件地址和注册时创建的密码登录到Document Security。

当收件人激活用户帐户时，该用户将成为本地用户。

以下设置位于“受邀用户注册”页面的“激活电子邮件配置”区域。

>[!NOTE]
>
>还建议您在登录屏幕上配置一条消息，以建议外部用户如何联系其管理员以获取新密码或其他信息。

**从：** 发送激活电子邮件的电子邮件地址。 此电子邮件地址会从注册人的电子邮件主机接收失败的投放通知，还会接收收件人为回复注册电子邮件而发送的任何消息。 发件人电子邮件地址的默认格式为postmaster@[your_installation_domain].com.

**主题：** 激活电子邮件的默认主题。

**超时：** 如果用户未激活帐户，则激活邀请将过期的天数。 默认值为30天。

**消息：** 消息正文中显示的文本，该消息指示需要激活收件人的用户帐户。 您可能还希望包括一些信息，如如何联系管理员以获取新密码。

### 配置密码重置电子邮件 {#configure-a-password-reset-email}

如果必须重置受邀用户的密码，则会生成一封确认电子邮件，邀请用户选择新密码。 无法确定用户的密码；如果用户忘记了密码，则必须重置密码。

以下设置位于“受邀用户注册”页面的“重置密码电子邮件”区域。

**从：** 发送密码重置电子邮件的电子邮件地址。 发件人电子邮件地址的默认格式为postmaster@[your_installation_domain].com.

**主题：** 重置电子邮件的默认主题。

**消息：** 消息正文中显示的文本，该消息指示收件人的外部用户密码已重置。

## 允许用户和组创建策略 {#enable-users-and-groups-to-create-policies}

“配置”页有一个指向“我的策略”页的链接，您可以在其中指定哪些最终用户可以创建我的策略，以及哪些用户和组在搜索结果中可见。 “我的策略”页有两个选项卡：

**创建策略选项卡：** 使用配置用户权限以创建自定义策略。

**可见的“用户和组”选项卡：** 用于控制哪些用户和组在用户搜索结果中可见。 超级用户或策略集管理员需要选择域，并将在“用户管理”中创建的域添加到每个策略集的可见用户和组。 此列表对策略集协调器可见，用于限制策略集协调器在选择要添加到策略的用户时可以浏览的域。

在授予用户创建自定义策略的权限之前，请考虑您希望各个用户拥有多少访问权限或控制。 此外，还要考虑希望用户和组在搜索中可见时的公开程度。

### 指定可以创建策略的用户和组 {#specify-users-and-groups-who-can-create-policies}

作为管理员，指定哪些用户和组可以创建自定义策略。 此权限可以在用户和组级别设置。 搜索功能在“用户管理”数据库中搜索用户和组。

1. 在管理控制台中，单击服务> Document Security >配置>我的策略。
1. 在“我的策略”页上，单击“创建策略”选项卡，然后单击“添加用户和组”。
1. 在“查找”框中，键入要搜索的用户或组的用户名或电子邮件地址。 如果您没有此信息，请将此框留空。 您还可以键入部分名称或电子邮件地址，例如，当您只知道用户名的前两个字母时。
1. 在使用列表中，选择搜索参数Name或Email。
1. 在“类型”列表中，选择“组”或“用户”以缩小搜索范围。
1. 在In列表中，选择要搜索的域。 如果您不知道用户或组的域，请选择“所有域”。
1. 在“显示”列表中，指定每页显示的搜索结果数，然后单击“查找”。
1. 要添加“我的策略”用户和组，请选中要添加的每个用户和组的复选框。
1. 单击“添加”，然后单击“确定”。

您选定的用户和组现在具有创建自定义策略的权限。

### 删除用户或组的创建自定义策略权限 {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. 在Document Security页面上，单击配置>我的策略。
1. 在“我的策略”页上，单击“创建策略”选项卡。 将显示具有创建自定义策略权限的用户和组。
1. 选中要从此权限中移除的用户和组旁边的复选框。
1. 单击“删除”，然后单击“确定”。

### 指定在搜索中可见的用户和组 {#specify-users-and-groups-that-are-visible-in-searches}

当用户管理其自定义策略时，可以搜索要添加到其策略中的用户和组。 您必须指定在这些搜索中显示用户和组的域。

1. 在Document Security页面上，单击配置>我的策略。
1. 在“我的策略”页上，单击“可见的用户和组”选项卡。
1. 要使域中的用户和组可见，请单击“添加域”，选择域，然后单击“添加”。 要删除域，请选中域名旁边的复选框，然后单击删除。

## 手动编辑Document Security配置文件 {#manually-editing-the-document-security-configuration-file}

您可以导入和导出存储在Document Security数据库中的配置信息。 例如，在从暂存环境移动到生产环境时，您可能希望制作配置信息的备份副本，或者您可能希望编辑只能配置用于编辑此文件的高级选项。

您可以使用配置文件进行以下更改：

[创建和编辑策略时显示CATIA权限](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[为脱机同步指定超时时间段](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[拒绝特定应用程序的Document Security服务](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[禁用外部链接](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>导入配置文件会根据文件中的信息重新配置系统。 动态水印配置和自定义事件信息除外，它们不与导出的配置文件一起保存。 您必须在新系统中手动配置此信息。 只有熟悉Document Security和XML的系统管理员或专业服务顾问才能修改配置文件的内容，如重新配置损坏的设置或调整特定企业部署方案的参数。

**导出配置文件**

1. 在管理控制台中，单击服务> document security 11 >配置>手动配置。
1. 单击“导出”，并将配置文件保存到其他位置。 默认文件名为config.xml。
1. 单击确定。
1. 在更改配置文件之前，请制作一个备份副本，以防您需要还原。

**导入配置文件**

1. 在管理控制台中，单击服务> document security 11 >配置>手动配置。
1. 单击“浏览”转到配置文件，然后单击“导入”。 不能直接在“文件名”框中键入路径。
1. 单击确定。

### 为脱机同步指定超时时间段 {#specify-a-timeout-period-for-offline-synchronization}

Document Security允许用户在未连接到Document Security服务器时打开和使用受保护的文档。 用户的客户端应用程序必须定期与服务器同步，以保持文档有效供脱机使用。 当用户首次打开受保护文档时，系统会询问他们是否应该授权计算机执行定期客户端同步。

默认情况下，当用户连接到Document Security服务器时，同步会根据需要每四小时自动进行一次。 如果文档的脱机期限在用户脱机时到期，则用户必须重新连接到服务器以使客户端应用程序能够与服务器同步。

在Document Security配置文件中，可以指定自动后台同步的默认频率。 除非客户端明确设置自己的超时值，否则此设置将用作客户端应用程序的默认超时时间段。

1. 导出document security配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在编辑器中打开配置文件并找到 `PolicyServer` 节点。 在该节点下，找到 `ServerSettings` 节点。
1. 在 `ServerSettings` 节点，添加以下条目，然后保存文件：

   `<entry key="BackgroundSyncFrequency" value="`*时间* `"/>`

   位置 *时间* 是自动后台同步之间的秒数。 如果您将此值发送至 `0`，始终进行同步。 默认值为 `14400` 秒（每四小时）。

1. 导入配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 拒绝特定应用程序的Document Security服务 {#denying-document-security-services-for-specific-applications}

您可以配置Document Security以拒绝对满足特定条件的应用程序的服务。 标准可以指定单个属性（如平台名称），也可以指定多组属性。 此功能可帮助您控制Document Security必须处理的请求。 以下是此功能的一些应用程序：

* **收入保护：** 您可能希望拒绝对不支持您的收入约定的任何客户端应用程序的访问。
* **应用程序兼容性：** 某些应用程序可能与您的Document Security Server的策略或行为不兼容。

当客户端应用程序尝试与Document Security建立链接时，它们会提供应用程序、版本和平台信息。 Document Security会将此信息与从Document Security配置文件中获取的“拒绝”设置进行比较。

拒绝设置可以包含多组拒绝条件。 如果任一组的所有属性匹配，则拒绝请求应用程序访问Document Security Services。

拒绝服务功能要求客户端应用程序使用Document Security C++客户端SDK版本8.2或更高版本。 以下Adobe产品在请求Document Security服务时提供产品信息：

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard及更高版本
* Adobe Reader 9.0及更高版本
* 适用于Microsoft Office 8.2及更高版本的Acrobat Reader DC扩展

客户端应用程序使用Document Security C++客户端SDK中的客户端API从Document Security请求服务。 客户端API请求包括平台和SDK版本信息（预编译到客户端API中）以及从客户端应用程序获取的产品信息。

客户端应用程序或插件在其实现回调函数时提供产品信息。 应用程序提供以下信息：

* 集成商名称
* Integrator版本
* 应用程序系列
* 应用程序名称
* 应用程序版本

如果有任何信息不适用，客户端应用程序会将相应的字段留空。

多个Adobe应用程序在请求Document Security服务时包括产品信息，其中包括Acrobat、Adobe Reader和Microsoft Office的Acrobat Reader DC扩展。

**Acrobat和Adobe Reader**

Acrobat或Adobe Reader从Document Security请求服务时，会提供以下产品信息：

* **集成商：** Adobe Systems公司
* **Integrator版本：** 1.0
* **应用程序系列：** Acrobat
* **应用程序名称：** Acrobat
* **应用程序版本：** 9.0.0

**适用于Microsoft Office的Acrobat Reader DC扩展**

Microsoft Office的Acrobat Reader DC扩展是一个与Microsoft Office产品Microsoft Word、Microsoft Excel和Microsoft PowerPoint一起使用的插件。 在请求服务时，它会提供以下信息：

* **集成商：** Adobe Systems Incorporated
* **Integrator版本：** 8.2
* **应用程序系列：** 适用于Microsoft Office的Acrobat Reader DC扩展
* **应用程序名称：** Microsoft Word、Microsoft Excel或Microsoft PowerPoint
* **应用程序版本：** 2003或2007

**配置Document Security以拒绝特定应用程序的服务**

1. 导出document security配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在编辑器中打开配置文件并找到 `PolicyServer` 节点。 添加 `ClientVersionRules` 节点作为 `PolicyServer` 节点（如果节点不存在）：

   ```xml
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

   `SDKPlatforms` 指定托管客户端应用程序的平台。 可能的值包括：

   * Microsoft Windows
   * APPLE OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` 指定客户端应用程序使用的Document Security C++客户端API的版本。 例如：`"8.2"`。

   `APPFamilies` 由客户端API定义。

   `AppName`指定客户端应用程序的名称。 使用逗号作为名称分隔符。 要在名称中包含逗号，请使用反斜杠(\)字符对其进行转义。 例如， *“Adobe Systems公司”*.

   `AppVersions` 指定客户端应用程序的版本。

   `Integrators` 指定开发插件或集成应用程序的公司或组的名称。

   `IntegratorVersions` 是插件或集成应用程序的版本。

1. 对于每个额外的拒绝数据集，添加另一个 *MyEntryName* 元素。
1. 保存配置文件。
1. 导入配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**示例**

在此示例中，所有Windows客户端都拒绝访问。

```xml
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

在此示例中，“我的应用程序”版本3.0和“我的其他应用程序”版本2.0被拒绝访问。 无论拒绝的原因如何，都会使用相同的拒绝信息URL。

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
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

在此示例中，来自Microsoft PowerPoint 2007或Microsoft PowerPoint 2010安装的Acrobat Reader DC Extensions for Microsoft Office的所有请求都将被拒绝。

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
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

默认情况下，您最多可以在水印中指定五个元素。 另外，要用作水印的PDF文档的最大文件大小限制为100KB。 您可以在config.xml文件中更改这些参数。

***注意&#x200B;**：您应谨慎更改这些参数。*

1. 导出document security配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在编辑器中打开配置文件并找到 `ServerSettings` 节点。
1. 在 `ServerSettings` 节点，添加以下条目，然后保存文件： `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   第一个条目， *最大文件大小* 是PDF水印元素允许的最大文件大小（以KB为单位）。 默认值为100KB。

   第二个条目， *最大元素* 是水印中允许的最大元素数。 默认值为5。

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. 导入配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 禁用外部链接 {#disabling-external-links}

许多Document Security用户无法访问外部链接，例如 **www.adobe.com** 当他们使用Right Management用户界面时：

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`。

对config.xml所做的以下更改将禁用Right Management用户界面中的所有外部链接。

1. 导出document security配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在编辑器中打开配置文件并找到 `DisplaySettings` 节点。
1. 要禁用所有外部链接，请在 `DisplaySettings` 节点，添加以下条目，然后保存文件： `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. 导入配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 用于启用传输层安全性(TLS)的SMTP的配置 {#configuration-to-enable-smtp-for-transport-layer-security-tls}

对config.xml的以下更改为“受邀用户注册”功能启用TLS支持。

1. 导出document security配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在编辑器中打开配置文件并找到 `DisplaySettings` 节点。
1. 找到以下节点： `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. 设置值 `SmtpUseTls` 键入 `ExternalUser` 节点至 **true**.
1. 设置值 `SmtpUseSsl` 键入 `ExternalUser` 节点至 **false**.
1. 保存 `config.xml`.
1. 导入配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 为Document Security文档禁用SOAP端点 {#disable-soap-endpoints-for-document-security-documents}

以下对config.xml进行了更改，以禁用Document Security文档的SOAP端点。

1. 导出document security配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在编辑器中打开配置文件，并找到以下节点： `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. 在DRM节点中，找到 `entry` 节点：

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. 要禁用Document Security文档的SOAP端点，请将值属性设置为 **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. 保存 `config.xml`.
1. 导入配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 提高文档安全服务器的可扩展性 {#increasingscalability}

默认情况下，在同步文档供脱机使用以及当前文档的信息时，Document Security客户端提取用户有权访问的所有其他文档的策略、水印、许可证和吊销更新信息。 如果这些更新和信息未与客户端同步，则以脱机模式打开的文档仍可能以旧策略、水印和吊销信息打开。

您可以通过限制发送到客户端的信息来提高Document Security Server的可伸缩性。 减少发送到客户端的信息量提高了可扩展性，缩短了响应时间，并改善了服务器的性能。 执行以下步骤以提高可扩展性：

1. 导出document security配置文件。 (请参阅 [手动编辑Document Security配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在编辑器中打开配置文件，并找到ServerSettings节点。
1. 在ServerSettings节点中，设置 `DisableGlobalOfflineSynchronizationData`属性至 `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   当设置为true时，document security服务器仅发送当前文档的信息，并且未向客户端发送其余文档（用户有权访问的其他文档）的信息。

   >[!NOTE]
   >
   >默认情况下， `DisableGlobalOfflineSynchronizationData`键设置为 `false`.

1. 保存并导入配置文件。 (请参阅 [手动编辑Document Security配置文件](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
