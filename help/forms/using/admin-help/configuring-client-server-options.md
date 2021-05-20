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
feature: 文档安全
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '10275'
ht-degree: 0%

---

# 配置文档安全服务器{#configure-the-document-security-server}

1. 在管理控制台中，单击服务>文档安全>配置>服务器配置。
1. 配置设置，然后单击确定。

## 服务器配置设置{#server-configuration-settings}

**基本URL:** 基本文档安全URL，包含服务器名称和端口。附加到基础的信息会创建连接URL。 例如，附加了/edc/Main.do以访问网页。 用户还通过此URL响应外部用户注册邀请。

如果您使用的是IPv6，请输入基本URL作为计算机名或DNS名称。 如果您使用数字IP地址，则Acrobat将无法打开受策略保护的文件。 此外，还应对您的服务器使用HTTP安全(HTTPS)URL。

>[!NOTE]
>
>基本URL嵌入到受策略保护的文件中。 客户端应用程序使用基本URL连接回服务器。 安全文件将继续包含基本URL，即使以后发生更改也是如此。 如果更改基本URL，则需要为所有连接的客户端更新配置信息。

**默认脱机租用期：** 用户脱机使用受保护文档的默认时间长度。此设置确定在创建策略时自动离线租用期设置的初始值。 （请参阅创建和编辑策略。） 在租赁期到期时，收件人必须再次同步文档以继续使用它。

有关脱机租用和同步工作方式的讨论，请参阅[关于配置脱机租用和同步的入门指南](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html)。

**默认脱机同步时段：** 在文档最初受到保护时，任何文档在脱机状态下可使用的最长时间。

**客户端会话超时：** 如果通过客户端应用程序登录的用户没有与文档安全进行交互，则在该时间后，文档安全将断开连接，以分钟为单位。

**允许匿名用户访问：** 选择此选项可启用创建共享和个人策略的功能，以允许匿名用户打开受策略保护的文档。（没有帐户的用户可以访问文档，但无法登录到文档安全或使用其他受策略保护的文档。）

**禁用对版本7客户端的访问：** 指定用户是可以使用Acrobat还是Reader7.0连接到服务器。选择此选项后，用户必须使用Acrobat或Reader8.0及更高版本来完成PDF文档的文档安全操作。 如果策略要求在打开受策略保护的文档时，Acrobat或Reader8.0及更高版本必须以认证模式运行，则应禁用对Acrobat或Reader7的访问。 （请参阅指定用户和群组的文档权限。）

**允许对每个文档进行离** 线访问选择此选项可指定对每个文档进行脱机访问。如果启用了此设置，则用户将只能脱机访问用户至少联机打开过一次的文档。

**允许用户名密码验证：** 选择此选项可使客户端应用程序在连接到服务器时能够使用用户名/密码验证。

**允许Kerberos身份验证：** 选择此选项可使客户端应用程序在连接到服务器时能够使用Kerberos身份验证。

**允许客户端证书身份验证：** 选择此选项可使客户端应用程序在连接到服务器时能够使用证书身份验证。

**允许扩展** 身份验证选择以启用扩展身份验证，然后输入扩展身份验证登陆URL。

选择此选项将使客户端应用程序能够使用扩展身份验证。 扩展身份验证提供了在AEM Forms服务器上配置的自定义身份验证过程和不同的身份验证选项。 例如，用户现在可以从Acrobat和Reader客户端体验基于SAML的身份验证，而不是AEM表单用户名/密码。 默认情况下，登陆URL包含&#x200B;*localhost*&#x200B;作为服务器名称。 将服务器名称替换为完全限定的主机名。 如果未启用扩展身份验证，则登陆URL中的主机名将自动从基本URL填充。 请参阅[添加扩展身份验证提供程序](configuring-client-server-options.md#add-the-extended-authentication-provider)。

***注意&#x200B;**:在Adobe Acrobat 11.0.6及更高版本的Apple Mac OS X中，支持扩展身份验证。*

**扩展身份验证的首选HTML控制宽** 度指定在Acrobat中打开以输入用户凭据的扩展身份验证对话框的宽度。

**扩展身份验证的首选HTML控** 制高度指定在Acrobat中打开以输入用户凭据的扩展身份验证对话框的高度。

***注意&#x200B;**:此对话框的宽度和高度的限制如下：*
宽度：最小= 400，最大= 900

高度：最低= 450;最大= 800

**启用客户端凭据缓存：** 选择此选项可允许用户缓存其凭据（用户名和密码）。缓存用户的凭据时，无需在每次打开文档或单击Adobe Acrobat中“管理安全策略”页面上的“刷新”按钮时输入其凭据。 您可以指定用户必须再次提供其凭据的间隔天数。 将天数设置为0可无限期地缓存凭据。

## 配置文档安全用户和管理员{#configuring-document-security-users-and-administrators}

### 为管理员分配文档安全角色{#assigning-document-security-roles-to-administrators}

您的AEM表单环境包含一个或多个具有创建用户和组相应权限的管理员用户。 如果贵组织使用文档安全，则还必须至少分配一位管理员，以管理受邀用户和本地用户。

管理员还必须具有管理控制台用户角色才能访问管理控制台。 （请参阅[创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。）

### 配置可见用户和组{#configuring-visible-users-and-groups}

要在策略用户搜索期间查看选定域中的用户和组，超级管理员或策略集管理员必须选择域并将其添加到每个策略集的可见用户和组列表（在用户管理中创建）。

可见的用户和组列表对策略集协调器可见，用于限制最终用户在选择要添加到策略的用户或组时可以浏览的域。 如果未执行此任务，则策略集协调器将找不到要添加到策略的任何用户或组。 任何给定策略集都可以有多个策略集协调器。

1. 在使用文档安全性安装和配置AEM表单环境后，请在“用户管理”中设置所有相应的域。<!-- Fix broken link (See Setting up and managing domains) -->

   ***注意&#x200B;**:必须先创建域，然后才能创建任何策略。*

1. 在管理控制台中，单击“服务”>“文档管理”>“策略”，然后单击“策略集”选项卡。
1. 选择全局策略集，然后单击可见的用户和组选项卡。
1. 单击添加域，然后根据需要添加现有域。
1. 导航至服务>文档安全>配置>我的策略，然后单击可见的用户和组选项卡。
1. 单击添加域，然后根据需要添加现有域。

## 添加扩展身份验证提供程序{#add-the-extended-authentication-provider}

AEM Forms提供了一个可针对您的环境进行自定义的示例配置。 执行以下步骤：

>[!NOTE]
>
>在Adobe Acrobat 11.0.6及更高版本的Apple Mac OS X中，支持扩展身份验证。

1. 获取部署该文件的WAR文件示例。 请参阅适用于您的应用程序服务器的安装指南。
1. 请确保Forms服务器具有完全限定的名称，而不是IP地址作为基本URL，并且它是HTTPS URL。 请参阅[服务器配置设置](configuring-client-server-options.md#server-configuration-settings)。
1. 从“服务器配置”页启用扩展身份验证。 请参阅[服务器配置设置](configuring-client-server-options.md#server-configuration-settings)。
1. 在用户管理配置文件中添加所需的SSO重定向URL。 请参阅[为扩展身份验证添加SSO重定向URL](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication)。

### 为扩展身份验证{#add-sso-redirect-urls-for-extended-authentication}添加SSO重定向URL

启用扩展身份验证后，在Acrobat XI或ReaderXI中打开策略保护文档的用户将获得用于身份验证的对话框。 此对话框加载您在文档安全服务器设置中指定为扩展身份验证登陆URL的HTML页面。 请参阅[服务器配置设置](configuring-client-server-options.md#server-configuration-settings)。

>[!NOTE]
>
>在Adobe Acrobat 11.0.6及更高版本的Apple Mac OS X中，支持扩展身份验证。

1. 在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。
1. 单击导出，然后将配置文件保存到磁盘。
1. 在编辑器中打开文件，并找到AllowedUrls节点。
1. 在`AllowedUrls`节点中，添加以下行：`<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. 保存文件，然后从“手动配置”页面导入更新的文件：在管理控制台中，单击设置>用户管理>配置>导入和导出配置文件。

## 配置脱机安全性{#configuring-offline-security}

文档安全提供了在没有Internet或网络连接的情况下脱机使用受策略保护的文档的功能。 此功能要求策略允许脱机访问，如[指定用户和组的文档权限](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups)中所述。 在脱机使用具有此策略的文档之前，收件人必须在联机时打开该文档，并在出现提示时单击“是”启用脱机访问。 也可请求收件人验证其身份。 然后，收件人可以在策略中指定的脱机租用期内脱机使用文档。

脱机租用期结束时，收件人必须再次与文档安全同步，方法是联机打开文档，或使用Acrobat或Acrobat Reader DC扩展菜单命令进行同步。 (请参阅&#x200B;*Acrobat Help*&#x200B;或相应的&#x200B;*Acrobat Reader DC扩展Help*。)

由于允许脱机访问的文档需要在脱机存储文件的计算机上缓存关键材料，因此，如果未经授权的用户能够获取关键材料，则文件可能会受到损害。 为了弥补这种可能性，提供了计划和手动密钥滚动选项，您可以对其进行配置以防止未经授权的人使用密钥访问文档。

### 设置默认的脱机租用期{#set-a-default-offline-lease-period}

受策略保护文档的收件人可以将文档脱机处理，时间为策略中指定的天数。 在最初将文档与文档安全性同步之后，收件人可以脱机使用它，直到脱机租用期到期。 当租赁期到期时，收件人必须联机并登录以与文档安全同步，以继续使用文档。

您可以配置默认的脱机租用期。 在任何人创建或编辑策略时，可以从默认状态更改租用期。

1. 在文档安全页面上，单击配置>服务器配置。
1. 在“默认离线租赁期”框中，键入离线租赁期的天数。
1. 单击确定。

### 管理密钥转换{#manage-key-rollovers}

文档安全使用加密算法和许可证来保护文档。 当对文档进行加密时，文档安全会生成并管理一个名为&#x200B;*DocKey*&#x200B;的解密密钥，该密钥将传递给客户端应用程序。 如果保护文档的策略允许脱机访问，则还会为每个对文档具有脱机访问权限的用户生成名为&#x200B;*主密钥*&#x200B;的脱机密钥。

>[!NOTE]
>
>如果主密钥不存在，则文档安全性会生成一个用于保护文档的安全密钥。

要脱机打开受策略保护的文档，用户的计算机必须具有相应的主密钥。 当用户与文档安全同步（联机打开受保护的文档）时，计算机获取主密钥。 如果此主密钥被泄露，则用户具有脱机访问权限的任何文档也可能被泄露。

减少脱机文档威胁的一种方法是避免允许脱机访问特别敏感的文档。 另一种方法是周期性地滚动主键。 当文档安全性将密钥转换到其上时，任何现有密钥都无法再访问受策略保护的文档。 例如，如果犯罪者从失窃的笔记本电脑中获取主密钥，则该密钥不能用于访问在发生翻车后受保护的文档。 如果您怀疑某个特定主密钥已被泄露，则可以手动滚动该密钥。

但是，您还需要注意，关键滚动更新会影响所有主键，而不仅仅影响一个主键。 它还降低了系统的可扩展性，因为客户端必须存储更多密钥才能进行离线访问。 默认的键值滚动更新频率为20天。 建议不要将此值设置为低于14天，因为可能会阻止用户查看离线文档，并且系统性能可能会受到影响。

在以下示例中，Key1是两个主键中较旧的键，Key2是较新的键。 当您首次单击Rollover Keys Now按钮时， Key1将变为无效，并且会生成一个较新的有效主密钥(Key3)。 用户在与文档安全同步时将获得密钥3，这通常是通过联机打开受保护的文档。 但是，用户在达到策略中指定的最大脱机租用期之前，不会强制与文档安全同步。 在第一个密钥滚动后，保持脱机状态的用户仍可以打开脱机文档，包括受Key3保护的文档，直到他们达到最大脱机租用期为止。 再次单击Rollover Keys Now按钮时， Key2将变为无效，并且Key4将被创建。 在两个密钥滚动过程中保持脱机状态的用户在与文档安全性同步之前无法打开受密钥3或密钥4保护的文档。

**更改关键滚动频率**

出于保密目的，当您使用离线文档时，文档安全会提供默认频率为20天的自动密钥滚动选项。 您可以更改滚动更新频率；但是，请避免将值设置为小于14天，因为可能会阻止用户查看离线文档，并且系统性能可能会受到影响。

1. 在文档安全页面上，单击配置>密钥管理。
1. 在“密钥滚动频率”框中，键入滚动周期的天数。
1. 单击确定。

**手动滚动主键**

为了保持离线文档的机密性，您可以手动滚动主键。 您可能发现有必要手动滚动某个键（例如，如果某个从缓存该键的计算机获取该键以允许脱机访问文档的某个人侵入了该键）。

>[!NOTE]
>
>避免经常使用手动滚动，因为它会导致所有主键（而不只是一个）滚动，并且可能会暂时阻止用户离线查看新文档。

主密钥必须被滚动两次，之后客户端计算机上以前存在的密钥才会失效。 使主密钥失效的客户端计算机必须与文档安全服务重新同步，以获取新的主密钥。

1. 在文档安全页面上，单击配置>密钥管理。
1. 单击“立即滚动”键，然后单击“确定”。
1. 等待大约10分钟。 服务器日志中显示以下日志消息：`Done RightsManagement key rollover for`*N* `principals`。 其中， *N*&#x200B;是文档安全系统中的用户数。
1. 单击“立即滚动”键，然后单击“确定”。
1. 等待大约10分钟。

## 配置事件审核和隐私设置{#configuring-event-auditing-and-privacy-settings}

文档安全可以审核和记录与与受策略保护的文档、策略、管理员和服务器的交互相关的事件的信息。 您可以配置事件审核，还可以指定要审核的事件类型。 要审核特定文档的事件，还必须启用策略上的审核选项。

启用审核后，您可以在“事件”页面上查看审核事件的详细信息。 文档安全用户还可以查看与他们使用或创建的受策略保护的文档专门相关的事件。

您可以选择以下类型的事件进行审核：

* 受策略保护的文档事件，例如授权用户或未授权用户尝试打开文档
* 策略事件，如创建、更改、删除、启用和禁用策略
* 用户事件，如外部用户邀请和注册、激活和停用的用户帐户、用户密码的更改以及配置文件更新
* AEM表单事件，如版本不匹配、目录服务器和授权提供程序不可用以及服务器配置更改

### 启用或禁用事件审核{#enable-or-disable-event-auditing}

您可以启用和禁用对与服务器、受策略保护的文档、策略、策略集和用户相关的事件的审核。 启用事件审核后，您可以选择审核所有可能的事件，也可以选择要审核的特定事件。

启用服务器审核后，您可以在“事件”页面上查看审核事件。

1. 在管理控制台中，单击服务>文档安全>配置>审核和隐私设置。
1. 要配置服务器审核，请在“启用服务器审核”下，选择“是”或“否”。
1. 如果您选择“是”，则在每个事件类别下，执行以下任一操作以选择要审核的选项：

   * 要审核类别中的所有事件，请选择“全部”。
   * 要仅审核某些事件，请取消选中“全部”，然后选中要审核的事件旁边的复选框。

      （请参阅[事件审核选项](configuring-client-server-options.md#event-auditing-options)。）

1. 单击确定。

>[!NOTE]
>
>使用网页时，请避免使用浏览器按钮，如“返回”按钮、“刷新”按钮以及“返回”或“向前”箭头，因为此操作可能会导致不需要的数据捕获和数据显示问题。

### 启用或禁用隐私通知{#enable-or-disable-privacy-notification}

您可以启用和禁用隐私通知消息。 启用隐私通知时，当收件人尝试打开受策略保护的文档时，会显示一条消息。 通知用户文档使用情况正在审核中。 您还可以指定一个URL，用户可以使用该URL查看隐私政策页面（如果有）。

1. 在管理控制台中，单击服务>文档安全>配置>审核和隐私设置。
1. 要配置隐私通知，请在启用隐私通知下，选择是或否。

   如果附加到文档的策略允许匿名用户访问，并且将“启用隐私声明”设置为“否”，则不会提示用户登录，并且不会显示隐私通知消息。

   如果附加到文档的策略不允许匿名用户访问，用户将看到隐私通知消息。

1. 如果适用，在隐私URL框中，键入隐私政策页面的URL。 如果隐私URL框留空，则会显示adobe.com的隐私页面。
1. 单击确定。

>[!NOTE]
>
>禁用隐私声明不会禁用文档使用情况审核。 通过扩展使用情况跟踪支持的开箱即用审核操作和自定义操作仍然可以收集用户行为信息。

### 导入自定义审核事件类型{#import-a-custom-audit-event-type}

如果您使用支持审核其他事件（如特定于特定文件类型的事件）的文档安全启用应用程序，则Adobe合作伙伴可以为您提供自定义审核事件，您可以将这些事件导入到文档安全中。 仅当Adobe合作伙伴向您提供了自定义事件类型时，才使用此功能。

1. 在管理控制台中，单击服务>文档安全>配置>事件管理。
1. 单击浏览以转到要导入的XML文件，然后单击导入。
1. 如果找到相同的事件代码和命名空间组合，则导入会覆盖服务器上的现有自定义审核事件类型。
1. 单击确定。

### 删除自定义审核事件类型{#delete-a-custom-audit-event-type}

1. 在管理控制台中，单击服务>文档安全>配置>事件管理。
1. 选中要删除的自定义审核事件类型旁边的复选框，然后单击删除。
1. 单击确定。

### 导出审核事件{#export-audit-events}

您可以将审核事件导出到文件以进行存档。

1. 在管理控制台中，单击服务>文档安全>配置>事件管理。
1. 根据需要编辑导出审核事件下的设置。 您可以指定：

   * 要导出的审核事件的最低年龄
   * 单个文件中要包含的最大审核事件数。 服务器会根据此值生成一个或多个文件。
   * 将在其中创建文件的文件夹。 此文件夹位于Forms服务器上。 如果文件夹路径是相对的，则它是相对于应用程序服务器根目录的。
   * 用于审核事件文件的文件前缀
   * 文件的格式，即与Microsoft Excel兼容的逗号分隔值(CSV)文件或XML文件。

1. 单击导出。 如果要取消导出，请单击“取消导出”。 如果其他用户计划了导出，则在导出完成之前，“取消导出”按钮将不可用。 如果其他用户计划了导出，则“取消导出”按钮将不可用。 要检查计划的“导出”或“删除”是否已启动或已完成，请单击“刷新”。

### 删除审核事件{#delete-audit-events}

您可以删除超过指定天数的审核事件。

1. 在管理控制台中，单击服务>文档安全>配置>事件管理。
1. 在“删除审核事件”下，在“删除审核事件早于”框中指定天数。
1. 单击删除。单击导出。 如果要取消删除，请单击“取消删除”。 如果其他用户计划了删除，则取消删除按钮在导出完成之前不可用。 如果其他用户计划了导出，则“取消删除”按钮将不可用。 要检查计划的删除是否已启动或已完成，请单击刷新。

### 事件审核选项{#event-auditing-options}

您可以启用和禁用事件审核，并指定要审核的事件类型。

**文档事件**

**查看文档：** 收件人查看受策略保护的文档。

**关闭文档：** 收件人关闭受策略保护的文档。

**打印低** 分辨率收件人打印具有指定低分辨率选项的受策略保护的文档。

**打印高分辨率：** 收件人打印指定了高分辨率选项的受策略保护的文档。

**将批注添加到文档：** 收件人将批注添加到PDF文档。

**撤销文档：** 用户或管理员撤销对受策略保护的文档的访问权限。

**取消撤销文档：** 用户或管理员重新授予对受策略保护文档的访问权限。

**表单填写：** 收件人在可填写表单的PDF文档中输入信息。

**删除策略：** 发布者从文档中删除策略以撤消安全保护。

**更改文档撤销URL:** 来自API级别的调用会更改为访问替换已吊销文档的新文档而指定的吊销URL。

**修改文档：** 收件人更改受策略保护的文档的内容。

**签名文档：** 收件人对文档进行签名。

**保护新文档：** 用户应用策略来保护文档。

**在文档上切换策略：** 用户或管理员切换附加到文档的策略。

**将文档发布为：** 在服务器上注册一个新文档，其documentName和许可证与现有文档相同，并且这些文档没有父子关系。此事件可使用AEM Forms SDK触发。

**迭代文档：** 在服务器上注册一个新文档，其documentName和许可证与现有文档相同，并且这些文档具有父子关系。此事件可使用AEM Forms SDK触发。

**策略事件**

**创建策略：** 用户或管理员创建策略。

**启用策略：** 管理员使策略可用。

**更改了策略：** 用户或管理员更改了策略。

**禁用的策略：** 管理员使策略不可用。

**已删除策略：** 用户或管理员删除策略。

**更改策略所有者：** API级别的调用会更改策略所有者。

**用户事件**

**已删除用户：** 管理员删除用户帐户。

**注册受邀用户：** 外部用户使用文档安全性进行注册。

**成功登录：** 管理员或用户成功登录尝试。

**受邀用户：** 文档安全性邀请用户进行注册。

**激活的用户：** 外部用户使用激活电子邮件中的URL激活其帐户，或者管理员启用帐户。

**更改密码：** 受邀用户更改其密码或管理员为本地用户重置密码。

**登录失败：** 管理员或用户登录尝试失败。

**已停用的用户：** 管理员会禁用本地用户帐户。

**配置文件更新：** 受邀用户更改其名称、组织名称和密码。

**帐户锁定：** 管理员锁定帐户。

**策略集事件**

**创建策略集：** 管理员或策略集协调员创建策略集。

**已删除策略集：** 管理员或策略集协调员删除策略集。

**修改的策略集：** 管理员或策略集协调员更改策略集。

**系统事件**

**目录同步完成：** 此信息在“事件”页面中不可用。当前目录同步信息（包括上次同步的当前同步状态和时间）将显示在“域管理”页上。 要在管理控制台中访问“域管理”页面，请单击设置>用户管理>域管理。

**客户端启用脱机访问：** 用户启用了对文档的脱机访问，这些文档是针对用户计算机上的服务器进行的。

**已同** 步的ClientClient应用程序必须与服务器同步信息以允许脱机访问。

**版本不匹配：** 与服务器不兼容的AEM Forms SDK版本尝试连接到服务器。

**目录同步信息：** 此信息在“事件”页面中不可用。当前目录同步信息（包括上次同步的当前同步状态和时间）将显示在“域管理”页上。 要在管理控制台中访问“域管理”页面，请单击设置>用户管理>域管理。

**服务器配置更改：** 对通过网页或通过导入config.xml文件手动完成的服务器配置进行的更改。这包括对基本URL、会话超时、登录锁定、目录设置、密钥转换、用于外部注册的SMTP服务器设置、水印配置、显示选项等的更改。

## 配置扩展的使用情况跟踪{#configuring-extended-usage-tracking}

文档安全可以跟踪对受保护文档可能执行的各种自定义事件。 您可以在全局级别或策略级别启用对文档安全服务器中事件的跟踪。 然后，您可以设置一个JavaScript来捕获在受保护的PDF文档中执行的特定操作，例如单击按钮或保存文档。 此使用情况数据将作为键值对中的XML文件发送，您可以使用该文件进行进一步分析。 访问受保护文档的最终用户可以允许或拒绝从客户端应用程序进行此类跟踪。

如果在全局级别启用了跟踪，则可以在策略级别覆盖此设置，并为特定策略禁用该设置。 如果在全局级别禁用跟踪，则无法执行策略级别的覆盖。 当事件计数达到25或文档关闭时，跟踪事件的列表会自动推送到服务器。 您还可以配置脚本，以根据您的要求显式推送事件列表。 您可以通过访问文档安全对象属性和方法来自定义事件跟踪。

启用跟踪后，所有随后创建的策略都将默认启用跟踪。 在服务器上启用跟踪之前创建的策略将需要手动更新。

### 启用或禁用扩展的使用情况跟踪{#enable-or-disable-extended-usage-tracking}

在开始之前，请确保已启用“服务器审核”。 有关审核的更多信息，请参阅[配置事件审核和隐私设置](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings)。

1. 在管理控制台中，单击服务>文档安全>配置>审核和隐私设置。
1. 要配置扩展的使用情况跟踪，请在启用跟踪下，选择是或否。
1. 要在登录页面上设置允许收集详细使用情况数据复选框的选项，请在“启用跟踪”默认值下，选择“是”或“否”。

要查看跟踪的事件，您可以使用“事件”页面上的“文档事件”过滤器。 使用JavaScript跟踪的事件将标记为详细使用情况跟踪。 有关事件的更多信息，请参阅[监视事件](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) 。

## 配置文档安全显示设置{#configure-document-security-display-settings}

1. 在管理控制台中，单击服务>文档安全>配置>显示选项。
1. 配置设置，然后单击确定。

### 显示设置{#display-settings}

**要显示搜索结果的行：** 执行搜索时在页面上显示的行数。

**客户端登录对话框的自定义**

这些设置控制用户通过客户端应用程序登录文档安全时登录提示中显示的文本。

**欢迎文本：** 欢迎消息文本，如“请使用您的用户名和密码登录”。欢迎消息文本应包含有关如何登录文档安全以及如何联系管理员或组织中其他指定支持人员以寻求帮助的信息。 例如，如果外部用户忘记了密码或需要注册或登录过程方面的帮助，则可能需要联系管理员。 欢迎文本的最大长度为512个字符。

**用户名文本：** 用户名框的文本标签。

**密码文本：** 密码框的文本标签。

**客户端证书身份验证对话框的自定义**

这些设置控制证书身份验证对话框中显示的文本。

**选择身份验证类型文本：** 显示用于指示用户选择身份验证类型的文本。

**选择证书文本：** 显示用于指示用户选择证书类型的文本。

**证书不可用错误文本：** 在选定的证书不可用时，最多显示512个字符的消息。

**客户端证书显示的自定义**

**仅显示受信任的凭据发行者：** 如果选择此选项，则客户端应用程序仅向用户显示AEM表单配置为信任的凭据发行者的证书（请参阅管理证书和凭据）。如果未选择此选项，则会向用户显示用户系统上所有证书的列表。

## 配置动态水印{#configure-dynamic-watermarks}

使用文档安全性，您可以为动态水印选项配置默认设置，在创建策略时可以应用该设置。 *水印*&#x200B;是文档中文本叠加的图像。 它有助于跟踪文档的内容，并有助于识别内容的非法使用。

动态水印可以由由定义的变量（如用户ID和日期及自定义文本）组成的文本或PDF中的富内容组成。 您可以使用多个元素配置水印，每个元素都具有自己的定位和格式。

水印不可编辑，因此它们是确保文档内容机密性的更安全方法。 动态水印还确保水印显示足够的用户特定信息以作为进一步分发文档的威慑。

当收件人查看或打印文档时，策略指定的水印将显示在受策略保护的文档中。 与永久水印不同，动态水印永远不会保存在文档中，这为在内联网环境中部署文档以确保查看应用程序显示特定用户的身份提供了必要的灵活性。 此外，如果文档有多个用户，使用动态水印意味着您可以使用一个文档而不是多个版本，每个版本具有不同的水印。 显示的水印反映当前用户的身份。

请注意，动态水印与用户可直接添加到Acrobat中文档的水印不同。 结果，在受策略保护的文档中可以有两个水印。

### 创建水印{#considerations-when-creating-watermarks}时的注意事项

您可以创建具有多个水印元素的动态水印，每个元素都指定为文本或PDF。 在水印中最多可以包含五个元素。

如果选择基于文本的水印，则可以在水印中指定多个元素，并包含多个文本条目，并指定每个元素的位置。 为这些元素指定有意义的名称，如页眉、页脚等。

例如，如果要在页眉、页脚、页边和文档中指定不同的文本作为水印，则可以创建多个水印元素并指定其位置。 如果希望用户的用户ID和文档访问的当前日期显示在标题中、策略名称在右边距中以及自定义文本“机密”在文档中以对角线显示，则可以定义单独的水印元素，并将文本作为类型，并指定其格式和位置。 当水印被应用到文档时，水印中的所有元素会同时被应用到文档中，按它们添加到水印的顺序排列。

通常，使用基于PDF的水印来包含图形内容（如徽标）或特殊符号（如版权或注册商标）。

您可以通过修改文档安全配置文件来更改对水印元素数量和PDF文件大小的限制。 请参阅[更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters)。

在配置水印时，请记住以下事项：

* 不能将受密码保护的PDF文档用作水印元素。 但是，如果您创建的水印包含其他未受密码保护的元素，则这些元素将作为水印的一部分应用。
* 您可以更改要用作水印元素的PDF文件最大大小。 但是，用作水印的大PDF文档在脱机同步应用了此类水印的文档期间会降低性能。 请参阅[更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters)。
* 只有所选PDF的第一页用作水印。 确保要显示为水印的信息在第一个页面上可用。
* 即使您可以指定PDF文档的缩放比例，如果您计划将PDF用作页眉、页脚或边距中的水印，请考虑其页面大小和布局。
* 指定字体名称时，请正确输入名称。 如果打开文档的客户端计算机中不存在您指定的字体，则AEM Forms会替换该字体。
* 如果选择文本作为水印内容，则将缩放选项指定为适合页面时，对于宽度不相同的页面，将不起作用。
* 在指定水印元素的位置时，请确保最多一个元素具有相同的位置。 如果两个水印元素具有相同的位置，如中心，则它们会在文档上出现重叠，并按顺序添加到水印中。
* 指定字体大小和类型时，请确保文本的长度在页面中完全可见。 文本内容会滚动到新行中，因此您希望在边距中显示的水印内容可能会与页面上的内容区域重叠。 但是，如果文档在Acrobat 9中打开，则超出单行的文本会被截断。

### 动态水印的限制{#limitations-of-dynamic-watermarks}

某些客户端应用程序可能不支持动态水印。 请参阅相应的Acrobat Reader DC扩展帮助。 此外，请记住以下支持动态水印的Acrobat版本：

* 不能将受密码保护的PDF文档用作水印元素。
* Acrobat和Adobe Reader 10之前的版本不支持以下水印功能：

   * PDF水印
   * 水印中的多个元素（文本/PDF）
   * 高级选项，如页面范围或显示选项
   * 文本格式选项，如指定字体、字体名称和颜色。 但是，早期版本的Acrobat和Reader将以默认字体和颜色显示文本内容。

* Acrobat 9.0及更早版本Acrobat 9.0及更早版本不支持动态水印中的策略名称。 如果Acrobat 9.0打开一个受策略保护的文档，其中包含策略名称和其他动态数据的动态水印，则该水印将显示为不包含策略名称。 如果动态水印仅包含策略名称，则Acrobat会显示错误消息

### 添加动态水印模板{#add-a-dynamic-watermark-template}

您可以创建动态水印模板。 这些模板仍可用作管理员或用户创建的策略的配置选项。

>[!NOTE]
>
>在导出配置文件时，动态水印配置信息不会与其他配置信息一起捕获。

1. 在管理控制台中，单击服务>文档安全>配置>水印。
1. 单击新建.
1. 在“名称”框中，键入新水印的名称。

   ***注意&#x200B;**:不能在水印或水印元素的名称或描述中使用某些特殊字符。请参阅[编辑策略的注意事项](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies)中列出的限制。*

1. 在“名称”下加号旁边，为水印元素（如“标题”）输入有意义的名称，并添加描述，然后展开加号以显示选项。
1. 在“源”下，选择“文本”或“PDF”形式的水印类型。
1. 如果选择了“文本”，请执行以下操作：

   * 选择要包含的水印类型。 如果选择“自定义文本”，请在相邻的框中键入要为水印显示的文本。 请记住将显示为水印的文本长度。
   * 为水印文本的文本内容指定文本格式属性，如字体名称、字体大小、前景颜色和背景颜色。 将前景和背景颜色指定为十六进制值。

      ***注意&#x200B;**:如果选择“适合页面”缩放选项，则无法编辑字体大小属性。*

1. 如果您为富水印选项选择了PDF，请单击“选择水印PDF”旁边的&#x200B;**浏览**&#x200B;以选择要用作水印的PDF文档。

   ***注意&#x200B;**:请勿使用受密码保护的PDF文档。如果指定受密码保护的PDF作为水印元素，则不会应用水印。*

1. 在“用作背景”下，选择“是”或“否”。

   **注意**:当前，无论此设置如何，水印都会显示在前景中。

1. 要控制水印在文档中的显示位置，请配置“垂直对齐”和“水平对齐”选项。
1. 选择适合页面大小，或选择%并在框中键入百分比。 值必须是整数，而不是小数。 要配置水印大小，您可以使用页面百分比值或设置水印以适合页面大小。
1. 在“旋转”(Rotation)框中，键入水印旋转的度。 范围是–180到180。 使用负值逆时针旋转水印。 值必须是整数，而不是小数。
1. 在“不透明度”框中，键入百分比。 使用整数，而不是小数。
1. 在高级选项下，设置以下内容：

   **页面范围选项**

   设置应显示水印的页面范围。 将起始页输入为1，将结束页输入为–1，以使所有页面都标有水印。

   **显示选项**

   选择要显示水印的位置。 默认情况下，水印同时显示在软拷贝（联机）和硬拷贝（打印）上。

1. 单击水印元素下的&#x200B;**New**&#x200B;以根据需要添加更多水印元素。
1. 单击确定。

### 编辑动态水印模板{#edit-a-dynamic-watermark-template}

1. 在管理控制台中，单击服务>文档安全>配置>水印。
1. 在列表中单击相应的水印。
1. 在“编辑水印”页面上，根据需要更改设置。
1. 单击确定。

### 删除动态水印模板{#delete-a-dynamic-watermark-template}

删除动态水印时，该动态水印不再可添加到新策略中。 但是，水印会保留在当前使用该水印的现有策略上，并且当前受保护策略的文档会继续显示动态水印，直到您或用户编辑包含已删除水印的策略为止。 编辑策略后，将不再应用水印。 出现一条消息，指示策略上的现有水印已被删除，用户可以选择另一个水印来替换它。

1. 在管理控制台中，单击服务>文档安全>配置>水印。
1. 选中相应水印旁边的复选框，然后单击删除。
1. 单击确定。

## 配置受邀用户注册{#configuring-invited-user-registration}

您组织外部的用户可以使用文档安全进行注册。 注册并激活其帐户的受邀用户可以使用其电子邮件地址和注册时创建的密码登录以记录安全性。 已注册的受邀用户可以使用他们有权使用的受策略保护的文档。

被邀请的用户在激活后会成为本地用户。 可以使用“已邀请”和“本地用户”区域配置和管理本地用户。 （请参阅[管理受邀和本地用户帐户](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)。）

根据您为受邀用户启用的功能，他们还可以使用以下文档安全功能：

* 将策略应用于文档
* 创建策略
* 将受邀用户添加到策略

当发生以下事件时，文档安全会自动生成注册邀请电子邮件，除非用户已在源LDAP目录中或先前已被邀请注册：

* 现有用户将受邀用户添加到策略
* 管理员在“受邀用户注册”页面上添加一个受邀用户帐户

注册电子邮件包含指向注册页面的链接以及有关如何注册的信息。 在受邀用户进行注册后，文档安全会发出一封激活电子邮件，其中包含指向激活页面的链接。 激活后，该帐户将一直有效，直到您将其停用或删除为止。

如果启用内置注册，则只需指定一次SMTP服务器、注册电子邮件详细信息、访问功能和重置密码电子邮件信息。 在启用内置注册之前，请确保您已在“用户管理”中创建了一个本地域，该域已将“文档安全邀请用户”角色分配给贵组织中的相应用户和组。 （请参阅[添加本地域](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain)和[创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。） 如果您不使用内置注册，则必须使用AEM Forms SDK创建自己的用户注册系统。 请参阅[使用AEM表单编程](https://www.adobe.com/go/learn-aemforms-programming-63)中有关“为AEM表单开发SPI”的帮助。 如果不使用内置注册选项，建议您在激活电子邮件和客户端登录屏幕上配置消息，以通知用户如何与管理员联系以获取新密码或其他信息。

**启用并配置邀请的用户注册**

默认情况下，已邀请的用户注册流程处于禁用状态。 您可以根据需要启用和禁用邀请用户的注册，以确保文档安全。

1. 在管理控制台中，单击服务>文档安全>配置>受邀用户注册。
1. 选择“启用受邀用户注册”。
1. （可选）根据需要更新受邀用户的注册设置：

   * [排除或包含外部用户或群组](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [服务器和注册帐户参数](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [注册邀请电子邮件设置](configuring-client-server-options.md#registration-invitation-email-settings)
   * [激活电子邮件设置](configuring-client-server-options.md#activation-email-settings)
   * [配置密码重置电子邮件](configuring-client-server-options.md#configure-a-password-reset-email)

1. （可选）在“内置注册”下，选择“是”以启用此选项。 如果不启用内置注册，则必须设置自己的用户注册系统。
1. 单击确定。

### 排除或包含外部用户或组{#exclude-or-include-an-external-user-or-group}

您可以限制某些外部用户或用户组使用文档安全性进行注册。 例如，此选项对于允许访问特定用户组但排除属于该组的特定个人非常有用。

以下设置位于“受邀用户注册”页面的“电子邮件限制过滤器”区域。

**排除项：** 键入要排除的用户或组的电子邮件地址。要排除多个用户或组，请在新行上键入每个电子邮件地址。 要排除属于某个特定域的所有用户，请输入通配符和域名。 例如，要排除example.com域中的所有用户，请输入&amp;ast;.example.com。

**包含：** 键入要包含的用户或组的电子邮件地址。要包含多个用户或组，请在新行上键入每个电子邮件地址。 要包含属于某个特定域的所有用户，请输入通配符和域名。 例如，要在example.com域中包含所有用户，请输入&amp;ast;.example.com。

### 服务器和注册帐户参数{#server-and-registration-account-parameters}

以下设置位于“受邀用户注册”页面的“常规设置”区域。

**SMTP主机：** SMTP服务器的主机名。SMTP服务器管理传出电子邮件通知以注册和激活受邀用户帐户。

如果SMTP主机需要，请在SMTP服务器帐户名称和SMTP服务器帐户密码框中键入连接到SMTP服务器的所需信息。 某些组织不执行此要求。 如果您需要信息，请咨询系统管理员。

**SMTP服务器套接字类名：** SMTP服务器的套接字类名。例如， javax.net.ssl.SSLSocketFactory。

**电子邮件内容类型：** 接受的MIME类型，如text/plain或text/html。

**电子邮件编码：** 发送电子邮件时使用的编码格式。您可以指定任何编码，例如，UTF-8(Unicode)或ISO-8859-1（拉丁语）。 默认为UTF-8。

**重定向电子邮件地址：** 当您为此设置指定电子邮件地址时，任何新邀请都会发送到提供的地址。此设置可用于测试目的。

**使用本地域：** 选择相应的域。在新安装中，确保您使用“用户管理”创建了域。 如果这是升级，则在升级期间创建了外部用户域，该域可供使用。

**对SMTP服务器使用SSL:** 选择此选项可为SMTP服务器启用SSL。

**在注册页面上显示登录链接：** 在注册页面上显示为受邀用户显示的登录链接。

**为SMTP服务器启用传输层安全性(TLS)**

1. 打开管理控制台。

   管理控制台的默认位置为`https://<server>:<port>/adminui`。

1. 导航至主页>服务>文档安全>配置>受邀用户注册。
1. 在“受邀用户注册”中，指定所有配置设置，然后单击“确定”。

   >[!NOTE]
   >
   >如果您使用Microsoft Office 365作为SMTP服务器来发送用户注册邀请，请使用以下设置：
   >
   >**SMTP主机：** smtp.office365.com
   >**端口：** 587

1. 接下来，您需要更新config.xml。 请参阅[为传输层安全(TLS)启用SMTP的配置](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>如果您对“受邀用户注册”选项进行了任何更改，则config.xml文件将被覆盖，并且TLS将被停用。 如果覆盖更改，您需要执行上述步骤以重新激活对“已邀请用户注册”的TLS支持。

### 注册邀请电子邮件设置{#registration-invitation-email-settings}

当您创建新的受邀用户帐户或现有用户添加之前未注册或受邀注册到策略的外部收件人时，文档安全会自动发出注册邀请电子邮件。 该电子邮件包含一个链接，收件人可使用该链接访问注册页面并输入个人帐户信息，包括用户名和密码。 密码可以是八个字符的任意组合。

当收件人激活帐户时，用户将变为本地用户。

以下设置位于“已邀请的用户注册”页面的“邀请电子邮件配置”区域。

**发件人：** 发送邀请电子邮件的电子邮件地址。“发件人”电子邮件地址的默认格式为postmaster@[your_installation_domain].com。

**主题：** 邀请电子邮件的默认主题。

**超时：** 如果外部用户未注册，则注册邀请在此后过期的天数。默认值为30天。

**消息：** 在消息正文中显示的邀请用户注册的文本。

### 激活电子邮件设置{#activation-email-settings}

在受邀用户注册后，文档安全会发送一封激活电子邮件。 激活电子邮件包含指向帐户激活页面的链接，用户可在该页面激活其帐户。 激活帐户后，用户可以使用其电子邮件地址和注册时创建的密码登录以记录安全性。

当收件人激活用户帐户时，用户将变为本地用户。

以下设置位于“受邀用户注册”页面的“激活电子邮件配置”区域。

>[!NOTE]
>
>还建议您在登录屏幕上配置消息，以建议外部用户如何联系其管理员以获取新密码或其他信息。

**发件人：** 发送激活电子邮件的电子邮件地址。此电子邮件地址接收来自注册人的电子邮件主机的失败投放通知，以及收件人回复注册电子邮件时发送的任何消息。 “发件人”电子邮件地址的默认格式为postmaster@[your_installation_domain].com。

**主题：** 激活电子邮件消息的默认主题。

**超时：** 如果用户未激活帐户，则激活邀请在此后过期的天数。默认值为30天。

**消息：** 消息正文中显示的用于指示需要激活收件人用户帐户的消息文本。您可能还希望包含诸如如何联系管理员以获取新密码等信息。

### 配置密码重置电子邮件{#configure-a-password-reset-email}

如果必须重置受邀用户的密码，则会生成一封确认电子邮件，邀请用户选择新密码。 无法确定用户的密码；如果用户忘记了该设置，则必须重置该设置。

以下设置位于“受邀用户注册”页面的“重置密码电子邮件”区域。

**发件人：** 发送密码重置电子邮件的电子邮件地址。“发件人”电子邮件地址的默认格式为postmaster@[your_installation_domain].com。

**主题：** 重置电子邮件的默认主题。

**消息：** 消息正文中显示的用于指示已重置收件人外部用户密码的消息文本。

## 允许用户和组创建策略{#enable-users-and-groups-to-create-policies}

“配置”页面包含指向“我的策略”页面的链接，在该页面中，您可以指定哪些最终用户可以创建我的策略，以及哪些用户和组在搜索结果中可见。 “我的策略”页面包含两个选项卡：

**“创建策略”选项卡：** 用于配置用户权限以创建自定义策略。

**可见的用户和群组选项卡：** 用于控制哪些用户和群组在用户搜索结果中可见。超级用户或策略集管理员需要选择在“用户管理”中创建的域并将其添加到每个策略集的可见用户和组。 此列表对策略集协调器可见，用于限制策略集协调器在选择要添加到策略的用户时可以浏览的域。

在授予用户创建自定义策略的权限之前，请考虑您希望各个用户拥有的访问权限或控制权限。 此外，还请考虑在使用户和组对搜索可见时，您希望其显示的情况。

### 指定可以创建策略的用户和组{#specify-users-and-groups-who-can-create-policies}

以管理员身份指定哪些用户和组可以创建自定义策略。 此权限可以在用户和群组级别设置。 搜索功能可在用户管理数据库中搜索用户和组。

1. 在管理控制台中，单击服务>文档安全>配置>我的策略。
1. 在“我的策略”页面上，单击创建策略选项卡，然后单击添加用户和群组。
1. 在“查找”框中，键入您要搜索的用户或群组的用户名或电子邮件地址。 如果您没有此信息，请将框留空。 您还可以键入部分名称或电子邮件地址，例如，当您只知道用户名的前两个字母时。
1. 在使用列表中，选择搜索参数名称或电子邮件。
1. 在类型列表中，选择组或用户以缩小搜索范围。
1. 在“在”列表中，选择要搜索的域。 如果您不知道用户或群组的域，请选择“所有域”。
1. 在显示列表中，指定每页要显示的搜索结果数，然后单击查找。
1. 要添加“我的策略”用户和群组，请选中要添加的每个用户和群组对应的复选框。
1. 单击“添加”，然后单击“确定”。

您选定的用户和组现在具有创建自定义策略的权限。

### 从用户或组{#remove-the-create-custom-policies-permission-from-a-user-or-group}中删除创建自定义策略权限

1. 在文档安全页面上，单击配置>我的策略。
1. 在“我的策略”页面上，单击创建策略选项卡。 将显示有权创建自定义策略的用户和组。
1. 选中要从此权限中删除的用户和组旁边的复选框。
1. 单击删除，然后单击确定。

### 指定在搜索中可见的用户和组{#specify-users-and-groups-that-are-visible-in-searches}

当用户管理其自定义策略时，他们可以搜索要添加到其策略中的用户和组。 您必须指定在这些搜索中显示用户和组的域。

1. 在文档安全页面上，单击配置>我的策略。
1. 在“我的策略”页面上，单击可见的用户和群组选项卡。
1. 要使域中的用户和组可见，请单击添加域，选择域，然后单击添加。 要删除域，请选中域名旁边的复选框，然后单击删除。

## 手动编辑文档安全配置文件{#manually-editing-the-document-security-configuration-file}

您可以导入和导出存储在文档安全数据库中的配置信息。 例如，当您从暂存环境移动到生产环境时，您可能希望创建配置信息的备份副本，或者您可能希望编辑只能配置为编辑此文件的高级选项。

您可以使用配置文件进行以下更改：

[在创建和编辑策略时显示CATIA权限](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[指定离线同步的超时时间段](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[拒绝特定应用程序的文档安全服务](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[更改水印配置参数](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[禁用外部链接](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>导入配置文件会根据文件中的信息重新配置系统。 动态水印配置和自定义事件信息是例外，这些信息不会与导出的配置文件一起保存。 您必须在新系统中手动配置此信息。 只有系统管理员或熟悉文档安全和XML的专业服务顾问才应修改配置文件的内容，如重新配置损坏的设置或调整特定企业部署方案的参数。

**导出配置文件**

1. 在管理控制台中，单击服务>文档安全11 >配置>手动配置。
1. 单击导出，然后将配置文件保存到其他位置。 默认文件名为config.xml。
1. 单击确定。
1. 在更改配置文件之前，请创建一个备份副本，以备您需要还原。

**导入配置文件**

1. 在管理控制台中，单击服务>文档安全11 >配置>手动配置。
1. 单击浏览以转到配置文件，然后单击导入。 不能直接在“文件名”(File Name)框中键入路径。
1. 单击确定。

### 指定离线同步的超时时间段{#specify-a-timeout-period-for-offline-synchronization}

文档安全允许用户在未连接到文档安全服务器时打开并使用受保护的文档。 用户的客户端应用程序必须定期与服务器同步，以保留离线使用的有效文档。 当用户首次打开受保护的文档时，系统会询问他们的计算机是否应被授权执行定期客户端同步。

默认情况下，当用户连接到文档安全服务器时，每四小时自动进行一次同步，并根据需要进行同步。 如果文档的脱机时段在用户脱机时过期，则用户必须重新连接到服务器，以使客户端应用程序能够与服务器同步。

在文档安全配置文件中，可以指定自动后台同步的默认频率。 此设置用作默认超时时段客户端应用程序，除非客户端明确设置其自身的超时值。

1. 导出文档安全配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）
1. 在编辑器中打开配置文件并找到`PolicyServer`节点。 在该节点下，找到`ServerSettings`节点。
1. 在`ServerSettings`节点中，添加以下条目，然后保存文件：

   `<entry key="BackgroundSyncFrequency" value="`*时间* `"/>`

   其中， *time*&#x200B;是自动后台同步之间的秒数。 如果将此值发送到`0`，则始终会进行同步。 默认值为`14400`秒（每四小时）。

1. 导入配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）

### 拒绝特定应用程序的文档安全服务{#denying-document-security-services-for-specific-applications}

您可以配置文档安全性，以拒绝对满足特定条件的应用程序提供服务。 标准可以指定单个属性（如平台名称），也可以指定多组属性。 此功能可帮助您控制必须处理的请求文档安全性。 以下是此功能的一些应用程序：

* **收入保护：** 您可能希望拒绝访问任何不支持收入惯例的客户端应用程序。
* **应用程序兼容性：** 某些应用程序可能与文档安全服务器的策略或行为不兼容。

当客户端应用程序尝试建立与文档安全性相关的链接时，它们会提供应用程序、版本和平台信息。 文档安全性将此信息与从文档安全配置文件获取的拒绝设置进行比较。

拒绝设置可以包含多组拒绝条件。 如果任何一个集的所有属性都匹配，则拒绝请求应用程序访问文档安全服务。

拒绝服务功能要求客户端应用程序使用文档安全C++客户端SDK版本8.2或更高版本。 以下Adobe产品在请求文档安全服务时提供产品信息：

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard及更高版本
* Adobe Reader 9.0及更高版本
* 适用于Microsoft Office 8.2及更高版本的Acrobat Reader DC扩展

客户端应用程序使用文档安全C++客户端SDK中的客户端API来请求文档安全服务。 客户端API请求包括平台和SDK版本信息（预编译为客户端API）以及从客户端应用程序获取的产品信息。

客户端应用程序或插件在其回调函数的实现中提供产品信息。 应用程序提供以下信息：

* 集成商名称
* Integrator版本
* 应用程序系列
* 应用程序名称
* 应用程序版本

如果有任何信息不适用，客户端应用程序会将相应的字段留空。

一些Adobe应用程序在请求文档安全服务时包括产品信息，包括Acrobat、Adobe Reader和Acrobat Reader DC的Microsoft Office扩展。

**Acrobat和Adobe Reader**

当Acrobat或Adobe Reader从文档安全请求服务时，它会提供以下产品信息：

* **集成商：** Adobe Systems, Inc.
* **Integrator版本：** 1.0
* **应用程序系列：** Acrobat
* **应用程序名称：** Acrobat
* **应用程序版本：** 9.0.0

**Acrobat Reader DC Extensions for Microsoft Office**

Acrobat Reader DC Extensions for Microsoft Office是与Microsoft Word、Microsoft Excel和Microsoft PowerPoint等Microsoft Office产品一起使用的插件。 在请求服务时，它会提供以下信息：

* **集成商：** Adobe Systems Incorporated
* **Integrator版本：** 8.2
* **应用程序系列：** Acrobat Reader DC Extensions for Microsoft Office
* **应用程序名称：** Microsoft Word、Microsoft Excel或Microsoft PowerPoint
* **应用程序版本：** 2003或2007

**配置文档安全性以拒绝特定应用程序的服务**

1. 导出文档安全配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）
1. 在编辑器中打开配置文件并找到`PolicyServer`节点。 添加`ClientVersionRules`节点作为`PolicyServer`节点的直接子节点（如果不存在）：

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

   `SDKPlatforms` 指定托管客户端应用程序的平台。可能的值包括：

   * Microsoft Windows
   * Apple OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` 指定客户端应用程序使用的文档安全C++客户端API的版本。例如，`"8.2"`。

   `APPFamilies` 由客户端API定义。

   `AppName`指定客户端应用程序的名称。逗号用作名称分隔符。 要在名称中包含逗号，请使用反斜线(\)字符对其进行转义。 例如，*&quot;Adobe Systems\, Inc.&quot;*。

   `AppVersions` 指定客户端应用程序的版本。

   `Integrators` 指定开发插件或集成应用程序的公司或组的名称。

   `IntegratorVersions` 是插件或集成应用程序的版本。

1. 对于每组附加的拒绝数据，添加另一个&#x200B;*MyEntryName*&#x200B;元素。
1. 保存配置文件。
1. 导入配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）

**示例**

在本例中，所有Windows客户端都被拒绝访问。

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

在此示例中，My Application版本3.0和My Other Application版本2.0被拒绝访问。 无论拒绝的原因如何，都会使用相同的拒绝信息URL。

```xml
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

在此示例中，来自Microsoft PowerPoint 2007或Microsoft PowerPoint 2010安装的Acrobat Reader DC Extensions for Microsoft Office的所有请求都将被拒绝。

```xml
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

### 更改水印配置参数{#change-the-watermark-configuration-parameters}

默认情况下，您最多可以在水印中指定五个元素。 此外，要用作水印的PDF文档的最大文件大小限制为100KB。 您可以在config.xml文件中更改这些参数。

***注意&#x200B;**:您应该谨慎更改这些参数。*

1. 导出文档安全配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）
1. 在编辑器中打开配置文件并找到`ServerSettings`节点。
1. 在`ServerSettings`节点中，添加以下条目，然后保存文件：`<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   第一个条目&#x200B;*max file size*&#x200B;是PDF水印元素允许的最大文件大小（以KB为单位）。 默认值为100KB。

   第二个条目&#x200B;*max elements*&#x200B;是水印中允许的元素的最大数量。 默认值为5。

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. 导入配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）

### 禁用外部链接{#disabling-external-links}

许多文档安全用户在使用Right Management用户界面时，无法访问外部链接，如&#x200B;**www.adobe.com**:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`。

对config.xml的以下更改将禁用“权限管理”用户界面中的所有外部链接。

1. 导出文档安全配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）
1. 在编辑器中打开配置文件并找到`DisplaySettings`节点。
1. 要禁用所有外部链接，请在`DisplaySettings`节点中添加以下条目，然后保存文件：`<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. 导入配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）

### 为传输层安全(TLS){#configuration-to-enable-smtp-for-transport-layer-security-tls}启用SMTP的配置

对config.xml所做的以下更改为“受邀用户注册”功能启用了TLS支持。

1. 导出文档安全配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）
1. 在编辑器中打开配置文件并找到`DisplaySettings`节点。
1. 找到以下节点：`<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. 将`ExternalUser`节点中`SmtpUseTls`键的值设置为&#x200B;**true**。
1. 将`ExternalUser`节点中`SmtpUseSsl`键的值设置为&#x200B;**false**。
1. 保存`config.xml`。
1. 导入配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）

### 禁用文档安全文档{#disable-soap-endpoints-for-document-security-documents}的SOAP端点

对config.xml进行了以下更改，以禁用文档安全文档的SOAP端点。

1. 导出文档安全配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）
1. 在编辑器中打开配置文件，并找到以下节点：`<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. 在DRM节点中，找到`entry`节点：

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. 要禁用文档安全文档的SOAP端点，请将值属性设置为&#x200B;**false**。

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. 保存`config.xml`。
1. 导入配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）

### 提高文档安全服务器的可扩展性 {#increasingscalability}

默认情况下，在同步文档以供离线使用时，文档安全客户端将获取用户有权访问的所有其他文档的策略、水印、许可证和撤销更新信息。 如果这些更新和信息未与客户端同步，则在脱机模式下打开的文档仍可能会打开旧的策略、水印和撤销信息。

您可以通过限制发送到客户端的信息来提高文档安全服务器的可扩展性。 发送给客户端的信息量减少，从而提高了可扩展性、缩短了响应时间，并改善了服务器的性能。 执行以下步骤以提高可扩展性：

1. 导出文档安全配置文件。 （请参阅[手动编辑文档安全配置文件](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）
1. 在编辑器中打开配置文件，然后找到ServerSettings节点。
1. 在ServerSettings节点中，将`DisableGlobalOfflineSynchronizationData`属性的值设置为`true`。

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   当设置为true时，文档安全服务器仅发送当前文档的信息，而其余文档（用户有权访问的其他文档）的信息不会发送到客户端。

   >[!NOTE]
   >
   >默认情况下，`DisableGlobalOfflineSynchronizationData`键的值设置为`false`。

1. 保存并导入配置文件。 （请参阅[手动编辑文档安全配置文件](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。）
