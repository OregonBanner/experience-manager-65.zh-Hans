---
title: 设置和配置We.Gov和We.Finance引用站点
description: 安装、配置和自定义AEM Forms演示包。
contentOwner: anujkapo
docset: aem65
exl-id: 1fee474e-7da5-4ab2-881a-34b8e055aa29
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '4603'
ht-degree: 3%

---

# 设置和配置We.Gov和We.Finance引用站点 {#set-up-and-configure-we-gov-reference-site}

## 演示包详细信息 {#demo-package-details}

### 安装先决条件 {#installation-prerequisites}

此包是为创建 **AEM Forms 6.4 OSGI创作**&#x200B;已经过测试，因此以下平台版本支持该扩展：

| AEM版本 | AEM Forms包版本 | 状态 |
|---|---|---|
| 6.4 | 5.0.86 | **支持** |
| 6.5 | 6.0.80 | **支持** |
| 6.5.3 | 6.0.122 | **支持** |

此包包含支持以下平台版本的云配置：

| 云提供商 | 服务版本 | 状态 |
|---|---|---|
| Adobe Sign | v5 API | **支持** |
| Microsoft® Dynamics 365 | 1710 (9.1.0.3020) | **支持** |
| Adobe Analytics | v1.4 Rest API | **支持** |
**软件包安装注意事项：**

* 在干净的服务器上安装该包，无需安装其他演示包或早期演示包版本。
* 在OSGI服务器上安装包，该服务器以创作模式运行。

### 此包包含什么内容 {#what-does-this-package-include}

此 [AEM Forms We.Gov演示包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/we-gov-forms.pkg.all-2.0.2.zip) (**we-gov-forms.pkg.all-&lt;version>.zip**)作为包提供，其中包括多个其他子包和服务。 该软件包包含以下模块：

* **we-gov-forms.pkg.all-&lt;version>.zip** - *完成演示包*

   * **we-gov-forms.ui.apps-&lt;version>.zip** *— 包含所有组件、客户端库、示例用户、工作流模型等。*

      * **we-gov-forms.core-&lt;version>.jar** - *包含所有OSGI服务、自定义工作流步骤实施等。*

      * **we-gov-forms.derby&lt;version>.jar** - *包含所有OSGI服务、数据库架构等。*

      * **core.wcm.components.all-2.0.4.zip** - *示例WCM组件的集合*

      * **grid-aem.ui.apps-1.0-SNAPSHOT.zip** - *站点页面列控件的AEM Sites网格布局包*

   * **we-gov-forms.ui.content-&lt;version>.zip** - *包含所有内容、页面、图像、表单、交互式通信资源等。*

   * **we-gov-forms.ui.ananalytics-&lt;version>.zip** - *包含要存储在存储库中的所有We.Gov Forms Analytics数据。*

   * **we-gov-forms.config.public-&lt;version>.zip** - *包含所有默认配置节点，包括占位符云配置以帮助避免表单数据模型和服务绑定问题。*

此包中包含的资源包括：

* 包含可编辑模板的AEM网页
* AEM Forms自适应Forms
* AEM Forms交互式通信（打印和Web Channel）
* AEM Forms XDP记录文档
* AEM Forms MS® Dynamics Forms数据模型
* Adobe Sign集成
* AEM工作流模型
* AEM Assets示例图像
* 示例（内存中）Apache Derby数据库
* Apache Derby数据源（用于表单数据模型）

## 演示包安装 {#demo-package-installation}

本部分包含有关安装演示软件包的信息。

### 来自Software Distribution {#from-software-distribution}

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 过滤器]** 部分：
   1. 选择 **[!UICONTROL Forms]** 从 **[!UICONTROL 解决方案]** 下拉列表。
   2. 选择包的版本和类型。 您也可以使用 **[!UICONTROL 搜索下载]** 用于筛选结果的选项。
1. 点按 **we-gov-forms.pkg.all-&lt;version>.zip** 包名称，选择 **[!UICONTROL 接受EULA条款]**，然后点击 **[!UICONTROL 下载]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择包并单击 **[!UICONTROL 安装]**.

   ![我们管理表单包](assets/wegov_forms_package.jpg)

1. 允许安装过程完成。
1. 导航到 *https://&lt;aemserver>：&lt;port>/content/we-gov/home.html？wcmmode=disable* 以确保安装成功。

### 从本地ZIP文件 {#from-a-local-zip-file}

1. 下载并找到 **we-gov-forms.pkg.all-&lt;version>.zip** 文件。
1. 导航到 *https://&lt;aemserver>：&lt;port>/crx/packmgr/index.jsp*.
1. 选择“上传包”选项。

   ![上传包选项](assets/upload_package.jpg)

1. 使用文件浏览器导航到下载的ZIP文件并将其选中。
1. 单击“打开”以上传。
1. 上传后，选择“安装”选项以安装包。

   ![安装WeGov Forms包](assets/wegov_forms_package-1.jpg)

1. 允许安装过程完成。
1. 导航到 *https://&lt;aemserver>：&lt;port>/content/we-gov/home.html？wcmmode=disable* 以确保安装成功。

### 安装新包版本 {#installing-new-package-versions}

要安装新的软件包版本，请按照4.1和4.2中定义的步骤操作。可以在已安装其他旧软件包时安装较新的软件包版本，但建议先卸载旧软件包版本。 为此，请执行以下步骤。

1. 导航到 *https://&lt;aemserver>：&lt;port>/crx/packmgr/index.jsp*
1. 查找较旧的 **we-gov-forms.pkg.all-&lt;version>.zip** 文件。
1. 选择“更多”选项。
1. 从下拉列表中选择“卸载”选项。

   ![卸载WeGov包](assets/uninstall_wegov_forms_package.jpg)

1. 确认后，再次选择“卸载”，并允许卸载过程完成。

## 演示包配置 {#demo-package-configuration}

本节包含有关演示包在演示之前部署后配置的详细信息和说明。

### 虚构的用户配置 {#fictional-user-configuration}

1. 导航到 *https://&lt;aemserver>：&lt;port>/libs/granite/security/content/groupadmin.html*
1. 以管理员身份登录以执行以下任务。
1. 向下滚动到页面末尾以加载所有用户组。
1. 搜索&quot;**工作流**“。
1. 选择&quot;**workflow-users**&#x200B;组并单击“属性”。
1. 导航到“成员”选项卡。
1. 键入 **wegov** 在“选择用户或组”字段中。
1. 从下拉菜单中选择»**We.Gov Forms用户**“。

   ![编辑工作流用户的组设置](assets/edit_group_settings.jpg)

1. 单击菜单栏中的“保存并关闭”。
1. 通过搜索“”重复步骤2至7 **分析**&quot;，选择&quot;**Analytics管理员**”组，并添加“**We.Gov Forms用户**”组作为成员。
1. 通过搜索“”重复步骤2至7 **forms用户**&quot;，选择&quot;**forms-power-users**”组，并添加“**We.Gov Forms用户**”组作为成员。
1. 通过搜索“”重复步骤2至7 **forms-users**&quot;，选择&quot;**forms-users**”组，这次添加的是“**We.Gov用户**”组作为成员。

### 电子邮件服务器配置 {#email-server-configuration}

1. 查看设置文档 [配置电子邮件通知](/help/sites-administering/notification.md)
1. 以管理员身份登录以执行此任务。
1. 导航到 *https://&lt;aemserver>：&lt;port>/system/console/configMgr*
1. 找到并单击 **Day CQ邮件服务** 要配置的服务。

   ![配置Day CQ邮件服务](assets/day_cq_mail_service.jpg)

1. 将服务配置为连接到您选择的SMTP服务器：

   1. **SMTP服务器主机名**：例如， (smtp.gmail.com)
   1. **服务器端口**：例如，(465)适用于使用SSL的gmail
   1. **SMTP用户：** 演示@ &lt;companyname> .com
   1. **“发件人”地址**： aemformsdemo@adobe.com

   ![配置SMTP](assets/configure_smtp.jpg)

1. 单击“保存”以保存配置。

### （可选）AEM SSL配置 {#aemsslconfig}

此部分包含有关在AEM实例上配置SSL以便能够配置Adobe Sign云配置的详细信息。

**引用:**

1. [默认SSL](/help/sites-administering/ssl-by-default.md)

**注释:**

1. 导航到https://&lt;aemserver>：&lt;port>/aem/inbox ，您可以在此处完成上述参考文档链接中说明的过程。
1. 此 `we-gov-forms.pkg.all-[version].zip` 该包中包含示例SSL密钥和证书，可通过解压 `we-gov-forms.pkg.all-[version].zip/ssl` 文件夹是包的一部分。

1. SSL证书和密钥详细信息：

   1. 颁发给“CN=localhost”
   1. 10年有效期
   1. “password”的密码值
1. 私钥是 *localhostprivate.der*.
1. 证书是 *localhost.crt*.
1. 单击“下一个”。
1. HTTPS主机名应设置为 *localhost*.
1. 端口应设置为系统已公开的端口。

### （可选）Adobe Sign云配置 {#adobe-sign-cloud-configuration}

此部分包含有关Adobe Sign云配置的详细信息和说明。

**引用:**

1. [将Adobe Sign与AEM Forms集成](adobe-sign-integration-adaptive-forms.md)

#### 云配置 {#cloud-configuration}

1. 查看先决条件。 请参阅 [AEM SSL配置](../../forms/using/forms-install-configure-gov-reference-site.md#aemsslconfig) 用于所需的SSL配置。
1. 导航至：

   *https://&lt;aemserver>：&lt;port>/libs/adobesign/cloudservices/adobesign.html/conf/we-gov*

   >[!NOTE]
   >
   >用于访问AEM服务器的URL应与Adobe Sign OAuth重定向URI中配置的URL匹配，以避免配置问题(例如， *https://&lt;aemserver>：&lt;port>/mnt/overlay/adobesign/cloudservices/adobesign/properties.html*)

1. 选择“We.gov Adobe Sign”配置。
1. 单击“属性”。
1. 导航到“设置”选项卡。
1. 输入oAuth URL，例如： [https://secure.na1.echosign.com/public/oauth](https://secure.na1.echosign.com/public/oauth)
1. 提供配置的Adobe Sign实例中配置的客户端ID和客户端密钥。
1. 单击“连接到Adobe Sign”。
1. 成功连接后，单击“保存并关闭”以完成集成。

### （可选）MS® Dynamics云配置 {#ms-dynamics-cloud-configuration}

此部分包含有关MS® Dynamics云配置的详细信息和说明。

**引用:**

1. [Microsoft](/help/forms/using/ms-dynamics-odata-configuration.md)
1. [配置Microsoft® Dynamics for AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/using-ms-dynamics-with-aem-forms.html)

#### MS® Dynamics OData云服务 {#ms-dynamics-odata-cloud-service}

1. 导航至：

   https://&lt;aemserver>：&lt;port>/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html/conf/we-gov

   1. 确保您正在使用MS® Dynamics应用程序注册中配置的同一重定向URL访问服务器。

1. 选择“Microsoft® Dynamics ODataCloud Service”配置。
1. 单击“属性”。

   ![Microsoft ODataCloud Service的属性](assets/properties_odata_cloud_service.jpg)

1. 导航到“Authentication Settings（身份验证设置）”选项卡。
1. 输入以下详细信息：

   1. **服务根：** 例如， `https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/`
   1. **身份验证类型：** OAuth 2.0
   1. **身份验证设置** (请参阅 [MS® Dynamics云配置设置](../../forms/using/forms-install-configure-gov-reference-site.md#dynamicsconfig) 以收集此信息)：

      1. 客户端ID — 也称为应用程序ID
      1. 客户端密钥
      1. OAuth URL — 例如 [https://login.microsoftonline.com/common/oauth2/authorize](https://login.microsoftonline.com/common/oauth2/authorize)
      1. 刷新令牌URL — 例如， [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. 访问令牌URL — 例如， [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. 授权范围 —  **openid**
      1. 身份验证标头 —  **授权持有者**
      1. 资源 — 例如， `https://msdynamicsserver.api.crm3.dynamics.com`

   1. 单击“连接到OAuth”。

1. 成功验证后，单击“保存并关闭”以完成集成。

#### MS® Dynamics云配置设置 {#dynamicsconfig}

包括此部分中详述的步骤，以帮助您从MS® Dynamics Cloud实例中查找客户端ID、客户端密钥和详细信息。

1. 导航到 [https://portal.azure.com/](https://portal.azure.com/) 和登录。
1. 从左侧菜单中选择“所有服务”。
1. 搜索或导航到“应用程序注册”。
1. 创建或选择现有的应用程序注册。
1. 复制 **应用程序Id** 将用作OAuth **客户端ID** AEM云配置中的
1. 单击“设置”或“清单”以配置 **回复URL。**

   1. 在配置OData服务时，此URL必须与用于访问AEM服务器的URL匹配。

1. 在“设置”视图中，单击“密钥”以查看新密钥(在AEM中用作客户端密钥)。

   1. 请确保保留密钥的副本，因为以后将无法在Azure或AEM中查看它。

1. 要找到资源URL/服务根URL，请导航到MS® Dynamics实例仪表板。
1. 在顶部导航栏中，单击“Sales”或您自己的实例类型和“Select Settings”。
1. 单击右下角附近的“自定义项”和“开发人员资源”。
1. 在此可以找到服务根URL：例如，

   *`https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/`

1. 有关刷新和访问令牌URL的详细信息，请参阅此处：

   *[https://learn.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app](https://learn.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app)*

#### 测试Forms数据模型(Dynamics) {#testing-the-form-data-model}

云配置完成后，您可能需要测试表单数据模型。

1. 导航至

   *https://&lt;aemserver>：&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. 选择“We.gov Microsoft® Dynamics CRM FDM”并选择“属性”。

   ![Dynamics CRM FDM的属性](assets/properties_dynamics_crm.jpg)

1. 导航到“更新源”选项卡。
1. 确保将“上下文感知配置”设置为“/conf/we-gov”，并且配置的数据源为“ms-dynamics-odata-cloud-service”。

   ![配置的数据源](assets/configured_data_source.jpg)

1. 编辑表单数据模型。

1. 测试服务，确保它们成功连接到配置的数据源。

   >[!NOTE]
   >
   测试服务后，单击 **取消** 以确保非自愿更改不会传播到表单数据模型。

   >[!NOTE]
   >
   据报告，需要重新启动AEM Server才能将数据源成功绑定到FDM。

#### 测试Forms数据模型(Derby) {#test-fdm-derby}

云配置完成后，您可能需要测试表单数据模型。

1. 导航到 *https://&lt;aemserver>：&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. 选择 **We.gov注册FDM** 并选择 **属性**.

   ![Dynamics CRM FDM的属性](assets/aftia-enrollment-fdm.jpg)

1. 导航至 **更新源** 选项卡。

1. 确保 **上下文感知配置** 设置为 `/conf/we-gov` 并且配置的数据源是 **We.Gov Derby DS**.

   ![Dynamics CRM FDM的属性](assets/aftia-update-data-source.jpg)

1. 选择&#x200B;**保存并关闭**。

1. [测试服务](work-with-form-data-model.md#test-data-model-objects-and-services) 以确保它们成功连接到配置的数据源

   * 要测试连接，请选择 **HOMEMORTGAGEACCOUNT** 然后给它一个获取服务。 测试服务，系统管理员可以查看正在检索的数据。

### Adobe Analytics配置（可选） {#adobe-analytics-configuration}

此部分包含有关Adobe Analytics Cloud配置的详细信息和说明。

**引用:**

* [与 Adobe Analytics 集成](../../sites-administering/adobeanalytics.md)

* [连接到Adobe Analytics并创建框架](../../sites-administering/adobeanalytics-connect.md)

* [查看页面分析数据](../../sites-authoring/pa-using.md)

* [配置分析和报表](configure-analytics-forms-documents.md)

* [查看和了解AEM Forms analytics报表](view-understand-aem-forms-analytics-reports.md)

### Adobe Analytics Cloud服务配置 {#adobe-analytics-cloud-service-configuration}

此包预配置为连接到Adobe Analytics。 提供以下步骤以允许更新此配置。

1. 导航到 *https://&lt;aemserver>：&lt;port>/libs/cq/core/content/tools/cloudservices.html*
1. 找到Adobe Analytics部分，然后选择“显示配置”链接。
1. 选择“We.Gov Adobe Analytics（Analytics配置）”配置。

   ![Analytics云服务配置](assets/analytics_config.jpg)

1. 单击“编辑”按钮以更新Adobe Analytics配置（您必须提供共享密钥）。 单击“连接到Analytics”进行连接，单击“确定”完成。

   ![We.Gov Adobe Analytics](assets/wegov_adobe_analytics.jpg)

1. 如果要更新框架配置，请在同一页面上单击“We.Gov Adobe Analytics Framework (Analytics Framework)”(请参阅 [启用AEM创作](../../forms/using/forms-install-configure-gov-reference-site.md#enableauthoring) 以启用创作)。

#### Adobe Analytics查找用户凭据 {#analytics-locating-user-credentials}

要查找帐户管理员必须执行以下任务的Adobe Analytics帐户的用户凭据，请执行以下操作：

1. 导航到Adobe Experience Cloud门户。
   * 使用管理员凭据登录
1. 在主功能板中选择Adobe Analytics图标。
   ![快速访问](assets/aftia-quick-access.jpg)
1. 导航到管理员选项卡，然后选择用户管理（旧版）项目
   ![报表](assets/aftia-reports.jpg)
1. 选择 **用户** 选项卡。
   ![用户管理](assets/aftia-user-management.jpg)
1. 从用户列表中选择所需的用户。
1. 滚动到页面底部，用户身份验证信息将显示在页面底部。
   ![管理访问权限](assets/aftia-admin-user-access.jpg)
1. 用户名和共享密钥信息显示在权限框的右侧。
1. 用户名在名称中带有冒号，冒号左侧的所有信息都是用户名，冒号右侧的所有信息都是公司名称。
   * 以下是示例： *用户名：公司名称*

#### 在Adobe Analytics中设置用户身份验证 {#setup-user-authentication}

管理员可以通过执行以下操作向用户提供AEM Analytics权限。

1. 导航到Adobe Admin Console。

1. 单击向Admin Console公开的Analytics实例。

   * 它位于管理页面的主页上。

1. 选择Analytics完全管理员访问权限。

1. 将用户添加到配置文件。

   ![Analytics完全管理员访问权限](assets/aftia-full-admin-access.jpg)

1. 将用户id映射到配置文件后，单击权限选项卡。

1. 确保所有权限都映射到配置文件。

   ![编辑权限](assets/aftia-admin-access-edit.jpg)

1. 一旦映射了权限之后用户登录功能可能需要几个小时。

### Adobe Analytics报表 {#adobe-analytics-reporting}

#### 查看Adobe Analytics站点报表 {#view-adobe-analytics-sites-reporting}

>[!NOTE]
>
AEM Forms Analytics数据在离线时或没有Adobe Analytics Cloud配置的情况下可用，如果 `we-gov-forms.ui.analytics-<version>.zip` 已安装包，但AEM Sites数据需要活动的cloud配置。

1. 导航到 *https://&lt;aemserver>：&lt;port>/sites.html/content*
1. 选择“AEM Forms We.Gov网站”以查看网站页面。
1. 选择一个网站页面（例如“主页”），然后选择“Analytics和Recommendations”。

   ![Analysis和Recommendations](assets/analytics_recommendations.jpg)

1. 在此页面上，您将看到从Adobe Analytics中获取的与AEM Sites页面相关的信息(注意：通过设计，这些信息会定期从Adobe Analytics中刷新，并且不会实时显示)。

   ![AEM Sites分析](assets/sites_analysis.jpg)

1. 返回页面查看页面（在步骤3中访问），您还可以通过更改显示设置以在“列表视图”中查看项目来查看页面查看信息。
1. 找到“View（查看）”下拉菜单，然后选择“List View（列表视图）”。

   ![列表视图](assets/list_view.jpg)

1. 从同一菜单中，选择“查看设置”，然后从“Analytics”部分中选择要显示的列。

   ![配置各列](assets/configure_columns.jpg)

1. 单击“更新”以使新列可用。

   ![新列的显示](assets/new_columns_display.jpg)

#### 查看Adobe Analytics Forms报表 {#view-adobe-analytics-forms-reporting}

>[!NOTE]
>
AEM Forms Analytics数据在离线时或没有Adobe Analytics Cloud配置的情况下可用，如果 `we-gov-forms.ui.analytics-<version>.zip` 已安装包，但AEM Sites数据需要活动的cloud配置。

1. 导航至

   *https://&lt;aemserver>：&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. 选择“健康权益注册应用程序”自适应表单，然后选择“Analytics报表”选项。

   ![Analytics报表](assets/analytics_report.jpg)

1. 等待页面加载并查看Analytics报表数据。

   ![查看Analytics报表数据](assets/analytics_report_data.jpg)

### Adobe自动Forms配置启用 {#automated-forms-enablement}

要使用AdobeForms安装和配置AEM Forms，转化工具用户必须满足以下条件。

1. 访问Adobe Developer。

1. 创建与AdobeForms转换服务集成的权限。

1. Adobe以创作方式运行的最新AEM 6.5 Service Pack。

阅读更多说明前，请查看以下内容：

* [配置自动化表单转换服务](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html)

#### 创建IMS配置第1部分 {#creating-ims-config}

要配置服务以便与表单转换工具正确通信，用户必须配置Identity Management System (IMS)服务以便能够注册Adobe I/O。

1. 导航到https://&lt;aemserver>：&lt;port> >单击左上方的Adobe Experience Manager >工具>安全> Adobe IMS配置。

1. 单击创建。

1. 执行下图中的操作。

   ![IMS技术帐户配置](assets/aftia-technical-account-configuration.jpg)

1. 确保下载证书。

1. 不要继续进行配置的其余部分 — 审查部分 [在Adobe I/O中创建集成](#create-integration-adobeio)

>[!NOTE]
>
在此部分中创建的证书将用于在Adobe I/O中创建集成服务。一旦用户在集成服务中创建了，用户就可以使用Adobe I/O中的该信息完成配置。

#### 在Adobe I/O中创建集成 {#create-integration-adobeio}

如果不联系系统管理员以创建集成，请确保您能够在Adobe域中创建集成。

1. 导航至 [Adobe I/O控制台](https://developer.adobe.com/console/).

1. 单击创建集成。

1. 选择访问API。

1. 确保您位于正确的组中（右上角的下拉列表）。

1. 在Experience Cloud部分中，选择Forms转换工具。

1. 单击“继续”。

1. 输入集成的名称和描述。

1. 使用2.1节中的公共密钥可将其置于密钥的集成中。

1. 为您的automated forms conversion选择配置文件。

   ![创建新集成](assets/aftia-create-new-integration.jpg)

#### 创建IMS配置第2部分 {#create-ims-config-part-next}

现在，您已创建集成，接下来让我们完成IMS配置的安装。

1. 在Adobe I/O中单击集成以显示连接详细信息。

1. 导航到AEM中的IMS配置（“工具”>“安全”>“IMS”）

1. 单击“IMS配置”屏幕上的下一步。

1. 输入授权服务器（屏幕快照中显示的值）。

1. 输入API密钥。

1. 输入客户端密码(必须单击在Adobe I/O中公开集成才能显示该密码)。

1. 单击Adobe I/O中的JWT选项卡以获取JWT有效负荷，并将其粘贴到IMS配置的有效负荷中。

   ![负载IMS配置](assets/aftia-payload-ims-config.jpg)

1. 创建后，单击IMS配置并选择运行状况检查，用户应会看到以下结果。

   ![运行状况确认](assets/aftia-health-confirmation.jpg)

#### 配置云配置（We.Gov AFC生产） {#configure-cloud-configuration}

IMS配置完成后，您可以继续查看AEM中的云配置。 如果配置不存在，请使用以下步骤在AEM中创建云配置：

1. 打开浏览器并导航到系统URL https://&lt;domain_name>：&lt;system_port>

1. 单击屏幕左上角的Adobe Experience Manager >工具>Cloud Service>自动Forms对话配置。

1. 选择要将配置放置到的配置文件夹。

1. 单击创建。

1. 在下面的屏幕快照中输入信息。

   ![AFC生产](assets/aftia-afc-production.jpg)

1. 为配置提供标题和名称。

1. 系统的服务URL设置为https://aemformsconversion.adobe.io/。

1. 模板URL */conf/we-gov/settings/wcm/templates/we-gov-flamingo-template*.

1. 主题URL： */content/dam/formsanddocuments-themes/adobe-gov-forms-themes/we-gov-theme*

1. 单击“下一个”。

1. 对于此配置，我们将两个复选框值留空。

   * 要详细了解这些选项，请参阅 [配置云服务](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service).

#### 配置云配置(We.Finance AFC Production) {#configure-cloud-configuration-wefinance}

IMS配置完成后，我们可以继续在AEM中创建云配置。

1. 打开浏览器并导航到系统URL https://&lt;domain_name>：&lt;system_port>

1. 单击屏幕左上角的Adobe Experience Manager >工具>Cloud Service>自动Forms对话配置。

1. 选择要将配置放置到的配置文件夹。

1. 单击创建。

1. 在下面的屏幕快照中输入信息。

   ![We.Finance AFC生产](assets/aftia-wefinance-afc-prod.jpg)

1. 为配置提供标题和名称。

1. 系统的服务URL设置为https://aemformsconversion.adobe.io/

1. 模板URL： */conf/we-finance/settings/wcm/templates/we-finance-adaptive-form*

1. 主题URL： */content/dam/formsanddocuments-themes/adobe-finance-forms-themes/we-finance-theme*

1. 单击“下一个”。

1. 对于此配置，我们将两个复选框值留空。

   * 要详细了解这些选项，请参阅 [配置云服务](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service).

#### 测试表单转换（We.Gov注册应用程序） {#test-forms-conversion}

设置配置后，用户可以通过上传PDF文档对其进行测试。

1. 导航到AEM系统https://&lt;domain_name>：&lt;system_port>

1. 单击Forms > Forms &amp; Documents > AEM Forms We.gov Forms > AFC。

1. 选择We.Gov注册申请PDF。

1. 单击 **启动自动转换** 在右上角。

1. 用户应该能够看到如下所示的选项。

   ![已转换的自适应表单](assets/aftia-converted-adaptive-form.jpg)

1. 选择按钮后，将为用户显示以下选项

   * 确保用户选择 *We.Gov AFC生产* 配置

   ![转换设置](assets/aftia-conversion-settings.jpg)

   ![高级转换设置](assets/aftia-conversion-settings-2.jpg)

1. 配置要使用的全部选项后，选择开始转换。

1. 转换过程开始时，用户应会看到以下屏幕：

   ![转换设置](assets/aftia-conversion-in-progress.jpg)

1. 转换完成后，用户将看到以下屏幕：

   ![已转换的自适应表单](assets/aftia-converted-adaptive-form-2.jpg)

   单击 **输出** 文件夹以查看生成的自适应表单。

#### 已知问题和说明 {#known-issues-notes}

automated forms conversion服务包含特定的 [最佳实践，已知的复杂模式](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/styles-and-pattern-considerations-and-best-practices.html)、和 [已知问题](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/known-issues.html). 在开始使用AEM FormsAutomated forms conversion服务之前，请查看这些内容。

1. 如果要在转换后将表单绑定到FDM，请在生成自适应表单时启用数据绑定来生成表单。

1. 确保模板文件夹启用了jcr：read for everyone权限，否则服务用户将无法从存储库中读取模板，并且转换将失败。

## 演示包自定义 {#demo-package-customizations}

本节包含有关自定义演示的说明。

### 模板自定义 {#templates-customization}

可在以下位置找到可编辑的模板：

*https://&lt;aemserver>：&lt;port>/libs/wcm/core/content/sites/templates.html/conf/we-gov*

这些模板包括AEM站点、自适应表单和交互式通信模板，这些模板是使用可以在以下位置找到的组件创建和组装的：

*https://&lt;aemserver>：&lt;port>/crx/de/index.jsp#/apps/we-gov/components*

#### 样式系统 {#customizetemplates}

此站点还具有客户端库，其中一个客户端库导入Bootstrap4 ( [https://getbootstrap.com/](https://getbootstrap.com/) )。 此客户端库位于

*https://&lt;aemserver>：&lt;port>/crx/de/index.jsp#/apps/we-gov/clientlibs/clientlib-base/css/bootstrap*

此包中包含的可编辑模板也预配置了模板/页面策略，这些策略使用Bootstrap4 CSS类进行分页、样式设置等。 并非所有类都已添加到模板策略中，但可以将Bootstrap4支持的任何类添加到策略中。 有关可用类的列表，请参阅入门页面：

[https://getbootstrap.com/docs/4.1/getting-started/introduction/](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

此包中包含的模板还支持样式系统：

[样式系统](../../sites-authoring/style-system.md)

#### 模板徽标 {#template-logos}

项目DAM资产还包含We.Gov徽标和图像。 这些资产位于：

*https://&lt;aemserver>：&lt;port>/assets.html/content/dam/we-gov*

在编辑页面和表单模板时，您可以选择通过编辑导航和页脚组件来更新品牌徽标。 这些组件提供了一个可用于更新徽标的可配置品牌和徽标对话框：

![模板徽标](assets/template_logos.jpg)

有关更多信息，请参阅编辑页面内容：

[编辑页面内容](../../sites-authoring/editing-content.md)

### 站点页面自定义 {#sites-pages-customization}

所有网站页面均可从以下位置访问： *https://&lt;aemserver>：&lt;port>/sites.html/content/we-gov*

这些站点页面还使用AEM Grid包来控制几个组件的布局。

#### 样式系统 {#style-system}

此包中包含的页面还支持样式系统：

[样式系统](../../sites-authoring/style-system.md)

您还可以看到 [模板自定义样式系统](../../forms/using/forms-install-configure-gov-reference-site.md#customizetemplates) 有关支持的样式的文档。

### 自适应表单自定义 {#adaptive-forms-customization}

所有自适应表单均可从以下位置获取：

*https://&lt;aemserver>：&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

可以自定义这些表单以适合某些用例。 某些字段和提交逻辑不应进行修改，以确保表单继续正常运行。 这包括：

**健康福利登记申请：**

* contact_id — 隐藏字段，用于在提交期间接收MS® Dynamics联系人ID
* 提交 — 需要自定义提交按钮逻辑才能支持回调。 记录了自定义设置，但在通过Forms数据模型向MS® Dynamics执行POST和GET操作时，需要大型脚本来提交表单。
* 根面板 — 初始化事件用于以尽可能少的侵入方式将MS® Dynamics按钮添加到AEM收件箱，因为所有AEM收件箱Granite UI组件都不可修改。

#### 自适应表单样式 {#adaptive-form-styling}

自适应表单也可以使用样式编辑器或主题编辑器设置样式：

* [自适应表单组件的内联样式](inline-style-adaptive-forms.md)
* [创建和使用主题](themes.md)

### 工作流自定义 {#workflow-customization}

注册自适应表单提交到OSGI工作流进行处理。 此工作流可在以下位置找到： *https://&lt;aemserver>：&lt;port>/conf/we-gov/settings/models/we-gov-process.html*.

由于存在某些限制，此工作流包含多个脚本和自定义OSGI工作流进程步骤。 这些工作流步骤是作为通用步骤创建的，尚未使用配置对话框创建。 目前，工作流步骤的配置依赖于进程参数。

所有工作流步骤Java™代码都包含在 **we-gov-forms.core-&lt;version>.jar** 捆绑。

## 演示注意事项和已知问题 {#demo-considerations-and-known-issues}

本节包含有关演示功能和设计决策的信息，在演示过程中可能需要特别考虑这些功能和决策。

### 演示注意事项 {#demo-considerations}

* 根据AGRS-159，确保注册自适应表单中使用的联系人姓名（名字、中间名和姓氏）是唯一的。
* 注册自适应表单会将Adobe Sign电子邮件发送到该表单的电子邮件字段中指定的电子邮件。 该电子邮件地址不能与用于配置Adobe Sign云配置的电子邮件相同。

### 已知问题 {#known-issues}

* (AGRS-120)站点导航组件当前不支持深度超过两级的嵌套子页面。
* (AGRS-159)当前MS® Dynamics FDM需要执行两项操作，即首先，将注册自适应表单数据POST到Dynamics，然后获取用户记录以检索联系人ID。 在其当前状态下，如果Dynamics中存在两个以上具有相同名称的用户，则获取联系人ID失败，这将不允许提交注册自适应表单。

## 配置辅助功能测试 {#configure-accessibility-testing}

### 启用辅助功能测试Chrome加载项 {#enable-chrome-add-on}

要执行辅助功能测试，请安装位于此处的Chrome插件 `https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en`. <!-- This URL is a 404. As such, fix and update this entire topic. We ought not to be writing about third-party software that we have no control over to avoid these 404s. Consider making this topic entirely generic and leaving it up to the user to choose their own Accessibility Testing add-on. -->

安装后，在Chrome浏览器中加载要测试的页面（注意：打开多个选项卡可能会影响分数，最好只打开一个选项卡）。 加载页面后， **右键单击** ，然后选择 **审核** 选项卡。 开发人员可以选择由“辅助功能”插件执行的审核类型。 选择所有所需选项后，用户可以单击“生成报告”按钮。 这将生成一个PDF文档，其中显示总体无障碍等级以及可用于提高总体无障碍等级的内容。

运行报表后，用户可以看到以下内容：

![辅助功能报告](assets/aftia-accessibility.jpg)

显示在用户面前的数字是他们已获得的总体无障碍评级。 此外，还提供了有关如何在分数后计算此值的说明。

如果用户希望导出此内容，可以单击屏幕右侧的三个按钮，然后从插件提供的其他选项中进行选择。

![辅助功能报告](assets/aftia-accessibility-report.jpg)

### 超海洋主题 {#ultramarine-theme}

由Adobe维护的公开的超海洋主题内建在
`we-gov-forms.pkg.all-<version>.zip` 可安装的ZIP文件。 使用CRX安装此包后。

AEM Forms在包管理器中，用户可以通过导航到 **Forms** > **主题** > **参考主题** > **超海洋无障碍**.

![超海洋主题](assets/aftia-ultramarine-theme.jpg)

## 配置选项 {#configuration-options}

用户可以配置各种工作流服务选项，其中包括：

1. Microsoft® Dynamics条目
1. Adobe Sign
1. AEM自定义通信管理
1. Adobe Analytics

要将它们配置为在工作流中启用，用户必须执行以下任务。

1. 导航到https://&#39;[服务器]：[端口]&#39;/system/console/configMgr.

1. 找到 *WeGov配置*.

1. 打开服务定义，并在工作流中调用选定的服务。

   >[!NOTE]
   >
   仅仅因为用户在Configuration Manager页面中启用了服务，用户仍需要设置服务配置才能与请求的外部服务通信。

   ![我们管理表单包](assets/aftia-configuration-options.jpg)

1. 完成后，单击保存以保存设置。

## 后续步骤 {#next-steps}

现在，您已准备好浏览We.Gov引用站点。 有关We.Gov引用站点工作流和步骤的更多信息，请参阅 [We.Gov引用站点演练](../../forms/using/forms-gov-reference-site-user-demo.md).
