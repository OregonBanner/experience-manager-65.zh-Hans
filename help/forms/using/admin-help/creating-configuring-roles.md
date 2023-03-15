---
title: 创建和配置角色
seo-title: Creating and configuring roles
description: 了解如何将用户和组与已成为“用户管理”数据库一部分的角色相关联。 您还可以创建、编辑和删除角色。
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---

# 创建和配置角色{#creating-and-configuring-roles}

使用“用户管理”网页，可以将用户和组与已成为“用户管理”数据库一部分的角色相关联。 您还可以创建、编辑和删除角色。

“用户管理”有两种类型的角色：

**可变角色：** 可以编辑和删除此类角色，也可以从这些角色类型中添加和删除角色权限。 您创建的任何角色都被视为可变角色。 您可以添加或删除分配给可变角色的用户和组。

**不可变角色：** “用户管理”中包含的默认角色是不可变角色。 无法编辑或删除这些角色。 但是，您可以添加或删除分配给不可变角色的用户和组。

可变和不可变角色也可以通过AEM Forms API创建。

## 默认角色 {#default-roles}

“用户管理”数据库中包含以下默认角色。

**管理控制台用户：** 可以访问管理控制台。

**应用程序管理员：** 可以使用所有Workbench功能。 可以使用Administration Console中的“应用程序和服务”页来配置服务运行时属性、端点和安全性。

**AEM Forms管理员：** 可以为所有已安装的服务执行所有任务。

**安全管理员：** 控制用户管理设置，并管理与任何User Manager域关联的用户和组

**服务用户：** 可以查看和调用任何服务

**超级管理员：** 有权访问系统中的所有管理功能，包括服务

**信任管理器：** 可以管理从管理控制台的“信任存储区管理”页管理的PKI信任设置和PKI凭据

### 其他默认角色 {#additional-default-roles}

可能包括以下其他默认角色，具体取决于您安装的AEM Forms组件

**文档上载应用程序用户：** 可以使用Flex Remoting上传文档。

**Forms管理员：** 可以在管理控制台的Forms页面中查看和修改设置

**AEM Forms Contentspace管理员：** 可以在管理控制台的Content Services（已弃用）页面中查看和修改设置

**AEM Forms Contentspace用户：** 可以登录Contentspace（已弃用）网页

**Documentum Connector管理员：** 可以在管理控制台的Connector for EMC Documentum页面中查看和修改设置

**AEM forms FileNet Connector管理员：** 可以在管理控制台的“IBM FileNet的连接器”页面中查看和修改设置

**AEM forms IBM CM连接器管理员：** 可以在管理控制台的“IBM Content Manager的连接器”页面中查看和修改设置

**Rights Management管理员：** 执行相关Rights Management页上所有服务器配置所需的所有任务

**Rights Management最终用户：** 可以访问Rights Management最终用户网页

**Rights Management邀请用户：** 可以邀请用户

**Rights Management管理受邀用户和本地用户：** 可以执行管理相关Rights Management页上的所有受邀用户和本地用户所需的任务

**Rights Management策略集管理员：** 执行相关Rights Management页上所有策略集所需的所有任务

**超级管理员Rights Management：** 执行“Rights Management”页所需的所有任务

**AEM Forms Workspace管理员：** 可以在管理控制台的Workspace页中查看和修改设置

***注释&#x200B;**：对于AEM Forms版本，已弃用Flex工作区。*

**工作区用户：** 可以登录到Workspace最终用户应用程序

**输出管理员：** 可以在Administration Console的“输出”页中查看和修改设置

**PDFG管理员：** 可以在管理控制台的“PDF生成器”页中查看和修改设置

**PDFG用户：** 可以访问PDF生成器的所有非管理功能

**Acrobat Reader DC扩展Web应用程序：** 可以使用Acrobat Reader DC扩展Web应用程序

>[!NOTE]
>
>出于安全原因，具有特定类型管理员权限的用户无法访问Workspace最终用户网页。 由于这些页面可以存在于防火墙之外，因此允许管理级别的任务可能会带来安全风险。 只有具有AEM Forms Workspace管理员或AEM Forms Workspace用户权限的用户才能访问Workspace最终用户网页。

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

## 创建角色 {#create-a-role}

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击新建角色。
1. 在“角色名称”框中，键入角色的名称，也可以键入角色的说明，然后单击下一步。

   >[!NOTE]
   >
   >使用MySQL时，不能创建名称相同但扩展字符使用不同的两个角色。 例如，当名为abcde的角色已存在时，尝试创建名为abcde的角色会导致错误。

1. 单击查找权限，选择要添加到角色的权限。
1. 单击“OK（确定）” ，然后单击“Next（下一步）”。
1. 将此角色分配给用户和组：

   * 单击“查找用户/组”。
   * 在“查找”框中，键入搜索条件。
   * 选择名称、电子邮件或用户ID ，然后选择用户、组或用户和组。
   * 选择域，选择要显示的结果数，然后单击“查找”。
   * 选中要为其分配此角色的用户和组的复选框，然后单击“确定”。

1. 要查看用户和组详细信息，请选择实体。
1. 单击“确定”，然后单击“完成”。

## 编辑角色 {#edit-a-role}

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击角色名称。

   默认情况下，“角色管理”页显示用户管理数据库中的所有角色。 如果角色列表很大，请使用页面顶部的查找区域来搜索特定的角色名称。

1. 单击要编辑的角色，编辑常规设置，然后单击保存。
1. 要编辑角色权限，请单击“权限”选项卡，然后执行以下任务：

   * 要添加新权限，请单击“查找权限”，选中要添加的权限对应的复选框，单击“确定”，然后单击“保存”。
   * 要从角色中删除权限，请选中该权限对应的复选框，单击“删除”，然后单击“保存”。

1. 要管理将角色分配给谁，请单击“角色用户”选项卡，然后执行以下任务：

   * 要将角色分配给新用户和组，请单击“查找用户/组”，然后填写搜索信息。 选中要为其分配此角色的每个用户和组的复选框，单击“确定”，然后单击“保存”。
   * 要删除角色，请选中用户或组的复选框，单击“取消分配”，然后单击“保存”。

## 删除角色 {#delete-a-role}

您可以删除已创建的任何角色，但无法删除产品中包含的默认AEM表单角色。

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击角色名称。

   默认情况下，“角色管理”页显示用户管理数据库中的所有角色。 如果角色列表很大，请使用页面顶部的查找区域来搜索特定的角色名称。

1. 选中要删除的角色对应的复选框，单击删除，然后单击确定。

## 为用户和组分配角色 {#assign-a-role-to-users-and-groups}

1. 在管理控制台中，单击设置>用户管理>用户和群组。
1. 指定信息以缩小搜索范围，然后单击“查找”。 搜索结果将列在页面底部。 您可以通过单击任意列标题对列表进行排序。
1. 选中要与角色关联的用户和组旁边的复选框，然后单击指定角色。
1. 选择要分配给用户或组的角色，然后单击确定。

您还可以使用“角色管理”页分配角色。

## 确定分配给角色的人员 {#determine-who-is-assigned-to-a-role}

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击角色名称。

   默认情况下，“角色管理”页显示用户管理数据库中的所有角色。 如果角色列表很大，请使用页面顶部的查找区域来搜索特定的角色名称。

1. 在“角色详细信息”页面上，单击“角色用户”选项卡。 将显示与该角色直接关联的用户和组的列表。

## 更改角色权限 {#change-role-permissions}

您可以更改所创建的任何角色的权限。 您无法更改产品中包含的默认AEM表单角色的权限。

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击角色名称。

   默认情况下，“角色管理”页显示用户管理数据库中的所有角色。 如果角色列表很大，请使用页面顶部的查找区域来搜索特定的角色名称。

1. 选择要查看其权限的角色，然后单击“权限”选项卡。
1. 要更改这些权限，请单击“查找权限”，选中要添加到角色的权限对应的复选框，单击“确定”，然后单击“保存”。
1. 要删除权限，请选择该权限，单击“删除”，然后单击“保存”。

### AEM forms权限 {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM：** 添加、删除和修改服务的端点

**Admin Console登录：** 查看管理控制台

**证书修改：** 修改信任存储区中任何证书的信任设置

**证书读取：** 读取信任存储区中的任何证书

**证书写入：** 将证书添加到信任存储区

**组件添加：** 在系统中安装新组件

**组件删除：** 删除系统中的任何组件

**组件读取：** 读取系统中的任何组件

**Contentspace管理员：** Contentspace（已弃用）管理员的权限

**Contentspace控制台登录：** Contentspace（已弃用）控制台登录的权限

**核心设置控制：** 在管理控制台中管理“核心系统设置”页面上的设置

**CREATE_VERSION_PERM：** 创建新版本的服务

**凭据修改：** 修改信任存储区中的任何签名凭据

**凭据读取：** 读取信任存储区中的任何签名凭据

**凭据写入：** 将签名凭据添加到信任存储区

**CRL修改：** 修改信任存储区中的任意CRL（证书吊销列表）

**CRL读取：** 读取信任存储区中的任意CRL

**CRL写入：** 将CRL添加到信任存储区

**委派：** 在资源上设置ACL

**DELETE版本PERM：** 删除服务的版本

**文档上传：** 在AEM表单中上传文档

**域控制：** 创建、删除或修改任何用户管理域的设置，包括其身份验证和目录提供程序

**事件类型编辑：** 编辑事件类型

**身份模拟控制：** 在用户管理器中模拟身份

**调用_PERM：** 对服务调用所有操作

**LCDS数据模型控制：** 读取和部署数据服务中的数据模型

**License Manager更新：** 更新许可证信息

**MODIFY_CONFIG_PERM：** 修改服务的配置

**搜索词** 修改服务的版本

**PDFGAdminPermission：** PDFG管理员

**PDFGUserPermission：** PDFG用户

**PERM_DCTM_ADMIN：** Documentum Connector管理员

**PERM_FILENET_ADMIN：** FileNet连接器管理员

**PERM_FORMS_ADMIN：** Forms管理员

**PERM_IBMCM_ADMIN：** IBM CM Connector管理员

**PERM_OUTPUT_ADMIN：** 输出管理员

**PERM_APPLICATION_EXTENSIONS_WEB_READER：** 使用Acrobat Reader DC扩展Web应用程序

**PERM_SP_管理员：** 管理SharePoint Connector设置

**PERM_WORKSPACE管理员：** 管理工作区设置

**PERM_WORKSPACE_USER：** 登录到Workspace最终用户应用程序

**主体控制：** 管理任何域的用户和组，并管理任何域中所有用户和组的角色分配

**处理记录读取/删除：** 列出和检索工作流审核实例

**PROCESS_OWNER_PERM：** 查看趋势数据并对从流程创建的服务执行管理操作

**读取：** 读取资源的内容

**读取_PERM：** 读取或查看服务

**续订断言：** 在用户管理中续订断言

**存储库委派：** 在资源上设置ACL

**存储库读取：** 读取资源的内容

**存储库遍历：** 在列表资源请求中包含资源或读取资源的元数据

**存储库写入：** 编写存储库元数据和内容

**Rights Management更改策略所有者：** 更改策略所有者

**最终用户控制台登录Rights Management：** 登录到Rights Management最终用户UI

**Rights Management管理配置：** 管理服务器配置

**Rights Management管理受邀用户和本地用户：** 管理受邀用户和本地用户

**Rights Management管理策略集：** 管理任何策略集中的所有策略和文档

**Rights Management策略集添加协调器：** 添加、删除和更改策略集协调器的权限

**Rights Management策略集创建策略：** 为策略集创建新策略

**Rights Management策略集删除策略：** 从策略集中删除策略

**Rights Management策略集编辑策略：** 编辑策略集中的策略

**Rights Management策略集管理文档发布者：** 创建策略集时，可以为用户分配文档发布者的角色。 文档发布者是使用策略保护文档的用户。

**Rights Management策略集删除协调器：** 从策略集中删除策略集协调器

**Rights Management策略集撤销文档：** 撤销对策略集中文档的访问权限

**Rights Management策略集交换机策略：** 切换文档的策略

**Rights Management策略集取消撤销文档：** 取消撤销文档

**Rights Management策略集查看事件：** 查看策略集内任何策略或文档的策略和文档事件

**Rights Management查看服务器事件：** 搜索并查看所有审核事件

**角色控制：** 在用户管理中创建、删除和修改角色

**服务激活：** 启动任何服务，使其可用于调用

**服务添加：** 将新服务部署到服务注册表。 这包括添加新进程和进程变体

**服务停用：** 停止系统中的任何服务

**服务删除：** 删除系统中的任何服务，包括进程和进程变体

**服务调用：** 在运行时调用服务注册表中的任何服务

**服务修改：** 修改系统中任何服务的配置属性。 这包括在IDE中锁定和解锁服务，以及添加或删除服务的端点

**服务读取：** 读取系统中的所有服务。 这包括所有进程和进程变体

**SERVICE_AGENT_PERM：** 查看从流程创建的服务的数据，并与流程实例交互

**SERVICE_MANAGER_PERM：** 对从进程创建的服务执行负载平衡和其他管理操作

**START_STOP_PERM：** 启动或停止服务

**主管_PERM：** 查看从流程创建的服务的流程实例数据

**遍历：** 在列表资源请求中包含资源或读取资源的元数据

**写入：** 编写存储库元数据和内容

**在Workbench中打开文件**

要在Workbench中查看“资源”视图的内容并打开文件进行查看，用户需要以下权限：

* 存储库读取
* 存储库遍历
* 服务调用
* 服务读取

## 从角色中删除用户或组 {#remove-a-user-or-group-from-a-role}

使用“角色管理”页可以从特定角色中删除用户和组。 如果用户或组继承了角色分配，则无法在用户或组级别移除角色。 从继承树中删除用户或组，或从父项中删除角色。

1. 在管理控制台中，单击设置>用户管理>角色管理，然后单击角色名称。

   默认情况下，“角色管理”页显示用户管理数据库中的所有角色。 如果角色列表很大，请使用页面顶部的查找区域来搜索特定的角色名称。

1. 在角色列表中，单击要更新的角色的名称，然后单击角色用户选项卡。 将显示与角色关联的用户和组的列表。
1. 选中要从角色中删除的用户和组的复选框，然后单击取消分配。
1. 单击“保存”，然后单击“确定”。
