---
title: 添加和配置用户
description: 通过管理控制台中的“用户管理”设置，您可以创建或删除用户并配置其他用户设置。
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---

# 添加和配置用户 {#adding-and-configuring-users}

用户和组信息保存在第三方存储系统中，如LDAP目录。 “用户管理”不会写入第三方存储系统。 相反，“用户管理”将用户和组信息与其自己的数据库同步

## 创建用户 {#create-a-user}

创建用户时，可以将用户添加到组并向其分配角色。

1. 在管理控制台中，单击 **[!UICONTROL 设置>用户管理>用户和群组]**，然后单击 **[!UICONTROL 新用户]**..
1. 下 **[!UICONTROL 常规设置]**，根据需要提供信息，然后单击 **[!UICONTROL 下一个]**. 有关设置的详细信息，请参阅 [用户设置](adding-configuring-users.md#user-settings).
1. （可选）要将用户添加到组，请单击 **[!UICONTROL 查找组]**，并执行以下任务：

   * 在 **[!UICONTROL 查找]** 框中，键入全部或部分组名。
   * 选择要搜索的域，选择要显示的项目数，然后单击 **[!UICONTROL 查找]**.
   * （可选）要查看组详细信息，请选择组名称，然后单击 **[!UICONTROL 确定]** 以返回到搜索结果页面。
   * 选中组的复选框，然后单击 **[!UICONTROL 确定]**.
   * 单击&#x200B;**[!UICONTROL 下一步]**。

1. （可选）要将角色分配给用户，请单击 **[!UICONTROL 查找角色]**，选中要分配的角色对应的复选框，然后单击 **[!UICONTROL 确定]**.
1. 单击 **[!UICONTROL 完成]**.

   >[!NOTE]
   >
   >如果您遇到用户的任何登录问题，请参阅 [JEE上的AEM Forms用户无法登录OSGi端的AEM Forms](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## 用户设置 {#user-settings}

在创建或编辑用户时指定以下设置。

**规范名称：** （必需）用户的唯一标识符。 域中的每个用户和组必须具有唯一的规范名称。 选中“系统生成”复选框以允许用户管理分配唯一值，或清除该复选框并指定“规范名称”的自定义值。

避免在规范名称中使用下划线字符(_)，例如， `sample_user`. 根据用户的规范名称搜索用户时，不会返回包含下划线字符的用户。

**名字：** （必需）用户的名字

**姓氏：** （必填）用户姓氏

**公用名：** 用户的全名或显示名称。 例如，如果名字= Gloria，姓氏= Rios，则普通名= Gloria Rios。

**电子邮件：** 用户的电子邮件地址

**电话：** 用户的电话号码

**描述：** 可选描述。 请根据贵组织的需求使用此字段。

**地址：** 用户的邮寄地址

**组织：** 用户所属的组织

**电子邮件别名：** 用户的电子邮件别名。 用逗号分隔电子邮件别名。

**域：** 用户所属的域

**区域设置：** 用户的ISO区域设置

**业务日历键：** 使您能够根据此设置的值将业务日历映射到用户。 业务日历定义业务日和非业务日。 在计算事件（如提醒、截止日期和呈报）的未来日期和时间时，AEM表单可以使用业务日历。 为用户分配业务日历键的方式取决于您使用的是企业域、本地域还是混合域。 (请参阅 [添加域](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

如果使用本地域或混合域，则有关用户的信息仅存储在User Management数据库中。 对于这些用户，将业务日历键设置为字符串。 然后，将业务日历键（字符串）映射到表单工作流中的业务日历。

如果您使用的是企业域，则有关用户的信息驻留在第三方存储系统中，如LDAP目录。 “用户管理”将目录中的用户信息与“用户管理”数据库同步。 此功能允许您将业务日历键映射到LDAP目录中的字段。 例如，假设目录中的每个用户记录都包含一个国家/地区字段，并且您要根据用户所在的国家/地区分配业务日历。 在这种情况下，您可以将“国家/地区”字段名称指定为“业务日历键”设置的值。 然后，您可以将业务日历键（为LDAP目录中的国家/地区字段定义的值）映射到表单工作流中的业务日历。

有关业务日历的其他信息，包括如何将业务日历键映射到业务日历，请参阅 [配置商业日历](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

将名称限制在53个字符以内。 较短的名称有助于防止在管理控制台的“流程管理”页面中显示业务日历键时出现问题。

**用户ID：** （必需）用户用于登录的用户ID。 用户ID不区分大小写，并且在整个域中必须是唯一的。

在企业域中，使用非DN属性作为用户ID，因为用户的DN在移动到组织的其他部分时可能会发生更改。 此设置取决于目录服务器。 值为 `objectGUID` 对于Active Directory 2003， `nsuniqueID` Sun™One和 `guid` 用于eDirectory。

确保用户ID是唯一的。 请勿使用分配给已删除用户的服务器。

AEM forms无法区分用户ID和密码相同但属于不同域的用户帐户。 为了避免此问题，请不要在多个域中创建具有相同用户ID的帐户。

将SQL Server用作数据库时，不能创建超过255个字符的用户ID。

使用MySQL时，用户ID可以包含扩展字符。 但是，在比较两个字符串（例如abcde和abcde）时，会将其视为相同字符串。 例如，在同步时，如果将新用户添加到数据库中，则会进行比较以检查数据库中是否存在具有相同用户ID的用户。 如果用户 *abcde* 当新用户存在数据库时 *abcde* 添加，比较无法区分这两个名称。 假定数据库中存在该用户，则忽略新用户而不添加该用户。

避免创建以数字符号(#)开头的用户名。 执行任务搜索不会返回有关这些用户名的结果。 (请参阅 [使用任务](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**密码和确认密码：** 用户用于登录的密码。 必须至少包含8个字符。 属于混合域的用户不需要密码。

## 查看有关用户的详细信息 {#view-details-about-a-user}

1. 在管理控制台中，单击设置>用户管理>用户和群组。
1. 指定信息以缩小搜索范围，并在“范围”列表中选择“用户”，然后单击“查找”。 搜索结果将列在页面底部。 您可以通过单击任意列标题对列表进行排序。
1. 单击用户的名称以显示有关的详细信息。 “编辑用户”页显示如下有关用户的详细信息：

   * 常规标识信息，如名称、电子邮件、地址、域和组织
   * 分配给用户的角色
   * 用户所属的组

## 更改本地用户的密码 {#change-the-password-for-a-local-user}

1. 在管理控制台中，单击 **[!UICONTROL 设置>用户管理>用户和群组]**.
1. 指定信息以缩小特定用户的搜索范围，然后单击 **[!UICONTROL 查找]**. 搜索结果将列在页面底部。 您可以通过单击任意列标题对列表进行排序。
1. 单击用户的名称，然后单击 **[!UICONTROL 更改密码]**.
1. 键入并确认新密码，然后单击 **[!UICONTROL 确定]**. 密码必须至少为八个字符。

## 编辑用户的属性 {#edit-a-user-s-properties}

1. 在管理控制台中，单击 **[!UICONTROL 设置>用户管理>用户和群组]**.
1. 要查找要编辑的用户，请执行以下任务：

   * 在 **[!UICONTROL 查找]** 框中，键入您的搜索条件。
   * 在 **[!UICONTROL 使用]** 列表，选择 **[!UICONTROL 名称]**， **[!UICONTROL 电子邮件]**，或 **[!UICONTROL 用户标识]**.
   * 在 **[!UICONTROL 在列表中]**，选择 **[!UICONTROL 用户]**.
   * 选择域，选择要显示的项目数，然后单击 **[!UICONTROL 查找]**.

1. 单击要编辑的用户。
1. 对于属于本地域或混合域的用户，在 **[!UICONTROL 详细信息]** 选项卡，编辑 **[!UICONTROL 常规设置]** 和 **[!UICONTROL 登录设置]**，然后单击 **[!UICONTROL 保存]**. 有关设置的详细信息，请参阅 [用户设置](adding-configuring-users.md#user-settings). 您无法编辑属于企业域的用户的常规设置和登录设置。
1. 要编辑用户的组设置，请单击 **[!UICONTROL 组成员资格]** 选项卡并执行以下任务：

   * 单击 **[!UICONTROL 查找组]** 并完成搜索信息。
   * 要将用户添加到新组，请选中该组的复选框，然后单击 **[!UICONTROL 确定]**，然后单击 **[!UICONTROL 保存]**.

   >[!NOTE]
   >
   >无法将本地用户添加到目录组。 但是，可以将目录用户添加到本地组。

   * 要从组中删除用户，请选中组的复选框，然后单击 **[!UICONTROL 删除]**，然后单击 **[!UICONTROL 保存]**.

1. 要编辑用户的角色，请单击 **[!UICONTROL 角色分配]** 选项卡并执行以下任务：

   * 要显示角色列表，请单击 **[!UICONTROL 查找角色]**.
   * 要添加角色，请选中该角色的复选框，然后单击 **[!UICONTROL 确定]**，然后单击 **[!UICONTROL 保存]**.
   * 要删除角色，请选中该角色的复选框，然后单击 **[!UICONTROL 取消分配]**，然后单击 **[!UICONTROL 保存]**.

## 删除用户 {#delete-a-user}

1. 在管理控制台中，单击 **[!UICONTROL 设置>用户管理>用户和群组]**.
1. 要查找要删除的用户，请执行以下任务：

   * 在 **[!UICONTROL 查找]** 框中，键入您的搜索条件。
   * 在 **[!UICONTROL 使用]** 列表，选择 **[!UICONTROL 名称]**， **[!UICONTROL 电子邮件]**，或 **[!UICONTROL 用户标识]**.
   * 在 **[!UICONTROL 在列表中]**，选择 **[!UICONTROL 用户]**.
   * 选择域，选择要显示的项目数，然后单击 **[!UICONTROL 查找]**.

1. 选中用户的复选框，然后单击 **[!UICONTROL 删除]**，然后单击 **[!UICONTROL 确定]**.

>[!NOTE]
>
>JEE上的AEM Forms还允许将在OSGi上运行的AEM forms加载项的用户识别为AEM用户。 在以下情形中，需要在JEE上的AEM Forms和在OSGi上运行的AEM Forms加载项之间进行单点登录(例如，HTML工作区)，则需要此项。 上述删除操作仅会从JEE上的AEM Forms中删除用户。 用户不会从在OSGi环境中运行的AEM Forms加载项中删除。 但是在删除用户后所做的任何登录尝试(登录AEM Forms附加组件JEE服务器或AEM Forms附加组件OSGi环境)都将被拒绝。

## 创建自定义登录错误处理程序 {#create-custom-login-error-handler}

如果用户没有所需的AEM表单和CQ权限，则尝试登录到CQ中嵌入的以下应用程序，则该用户将被重定向到包含错误跟踪的默认CQ 404页面：

* 通信管理解决方案
* AEM Forms工作区

  ***注意&#x200B;**：Flex工作区在AEM Forms版本中被弃用。*

* 表单管理器
* 进程报告

CQ提供了一种机制来覆盖默认的404处理程序jsp。

有关如何自定义错误处理页面的详细信息，请参阅 [自定义错误处理程序显示的页面](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) 请参阅Adobe Experience Manager文档。
