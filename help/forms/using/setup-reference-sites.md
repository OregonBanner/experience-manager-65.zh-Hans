---
title: 设置和配置We.Finance和Employee自助服务参考站点
seo-title: 设置和配置We.Finance和Employee自助服务参考站点
description: AEM Forms参考站点展示了如何使用AEM Forms在组织中实施端到端工作流。
seo-description: AEM Forms参考站点展示了如何使用AEM Forms在组织中实施端到端工作流。
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 设置和配置We.Finance和Employee自助服务参考站点{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

AEM Forms提供参考站点实施，以演示AEM Forms如何帮助金融服务行业和政府组织将复杂的交易转变为随时随地通过任何设备实现的简单而引人入胜的数字体验。

We.Finance参考站点利用真实案例与现有和潜在客户进行互动，从初次接触开始，以个性化和经济有效的方式管理通信和交易。

通过参考站点，您可以浏览和展示AEM Forms的以下主要功能。

* 简化了引人入胜的响应式自适应表单和交互式通信的创作体验。
* 交互通信，创建可适应设备设置和布局的交互式、个性化和响应式客户通信。
* 通过数据集成连接到不同的数据源，通过表单数据模型预填和提交表单数据。
* 使业务流程和工作流实现自动化的表单工作流程。
* 高级用户数据管理和处理功能。
* 与Adobe Sign集成，安全地签署和提交自适应表单。
* 与Adobe目标集成，提供有针对性的推荐并执行A/B测试，从而最大化表单的投资回报。
* 与Adobe Analytics集成，衡量表单或活动的性能并做出明智的决策。
* 增强的表单填写体验。

参考站点提供可重复使用的资产，您可以将这些资产用作模板来创建您自己的资产。

* 与Adobe Sign集成，安全地签署和提交自适应表单。

* 与Adobe Sign集成，安全地签署和提交自适应表单。

## 设置参考站点的先决条件和步骤 {#prerequisites-and-steps-to-set-up-reference-sites}

在设置参考站点之前，请确保您具有以下各项：

* **AEM Essentials** AEM QuickStart、AEM Forms加载项包和参考站点包。 有关 [附加和参考站点包详细信息](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) ，请参阅AEM Forms版本。

* **SMTP服务**&#x200B;可以使用任何SMTP服务。

* **Adobe Sign开发人员帐户和Adobe Sign API应用程序** 。要使用数字签名功能，需要Adobe Sign开发人员帐户。 请参 [阅Adobe Sign](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)。

* 要与AEM Forms集成的Microsoft Dynamics 365的正在运行实例。 要运行引用站点，请将示例数据导入Microsoft Dynamics实例以预填充引用站点中使用的交互式通信。
* 带有Forms Add-on包的AEM的正在运行实例。 有关详细信息，请参 [阅安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

按照建议的顺序执行以下步骤以设置和配置引用站点。

<table>
 <tbody>
  <tr>
   <th><strong>步骤</strong></th>
   <th><strong>配置</strong></th>
   <th><strong>注释</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">安装和配置AEM表单</a></td>
   <td>创作和发布</td>
   <td>安装和配置AEM Forms作者实例和发布实例。</td>
  </tr>
  <tr>
   <td><a href="#ssl">配置SSL</a></td>
   <td>创作和发布<br /> </td>
   <td>启用HTTP over SSL，与Adobe Sign进行安全通信。</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">配置Day CQ Link Externalizer配置</a></p> </td>
   <td>创作和发布<br /> </td>
   <td><p>参考站点使用案例会为不同的事务发送电子邮件。 此设置是通过电子邮件投放新闻稿时必需的。 它确保URL和图像指向发布实例。 </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">配置Day CQ Mail服务</a></td>
   <td>创作和发布</td>
   <td>电子邮件通信必需。</td>
  </tr>
  <tr>
   <td><a href="#xss">覆盖默认的XSS配置</a></td>
   <td>发布</td>
   <td>用于覆盖受xss安全性阻止的$、{和}字符。</td>
  </tr>
  <tr>
   <td><a href="#aemds">配置AEM DS设置</a></td>
   <td>作者</td>
   <td>配置AEM DS，以便在发布实例上提交表单，并在创作实例上处理工作流。</td>
  </tr>
  <tr>
   <td><a href="#refsite">部署参考站点包</a></td>
   <td>作者</td>
   <td>在AEM Forms作者实例上部署引用站点包。</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">将示例数据导入Microsoft Dynamics</a></td>
   <td>创作和发布</td>
   <td>导入信用卡申请、住房抵押申请和住房保险申请演练的样本数据</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">为Microsoft Dynamics配置OAuth云服务</a></td>
   <td>创作和发布</td>
   <td>在AEM Forms中配置OAuth云服务，以启用AEM Forms与Microsoft Dynamics之间的通信。 </td>
  </tr>
  <tr>
   <td><a href="#scheduler">配置Adobe Sign调度程序</a></td>
   <td>创作和发布<br /> </td>
   <td>更改调度程序的配置，每两分钟检查一次状态。</td>
  </tr>
  <tr>
   <td><a href="#sign-service">配置参考站点Adobe Sign云服务</a></td>
   <td>创作和发布<br /> </td>
   <td>引用站点包附带的配置，需要使用有效凭据重新配置。</td>
  </tr>
  <tr>
   <td><a href="#anonymous">为匿名用户配置Forms Common Configuration Service</a></td>
   <td>发布</td>
   <td>该配置允许匿名用户提交、签署和文档记录生成。</td>
  </tr>
  <tr>
   <td><a href="#fdm">修改表单数据模型的Rest Service Swagger文件</a></td>
   <td>创作和发布<br /> </td>
   <td>为您的环境修改服务。</td>
  </tr>
 </tbody>
</table>

## 安装和配置AEM表单 {#installandconfigureaemform}

按照在OSGi上安装和配置AEM Forms [中所述安装和部署AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

>[!NOTE]
>
>如果不同计算机上有多个发布实例或作者实例和发布实例，请配置复制和反向复制代理。

## 配置SSL {#ssl}

需要SSL配置才能与Adobe Sign服务器通信。 有关详细步骤，请参 [阅启用HTTP Over SSL](/help/sites-administering/ssl-by-default.md)。

>[!CAUTION]
>
>请勿对文件夹配置强制使用SSL `/etc/map` 功能。

## 配置Day CQ Link Externalizer配置 {#externalizer}

在AEM中， **Externalizer** 是一项OSGI服务，允许您以编程方式转换资源路径(例如，/path/to/my/page)通过预配置的DNS为路径添加前缀，使其成为外部和绝对URL(例如，https://www.mycompany.com/path/to/my/page)。 请参 [阅将URL外置](/help/sites-developing/externalizer.md)。

>[!CAUTION]
>
>如果您使用SSL的自签名证书，请勿外置为HTTPS URL。
>
>此外，对于本地服务器，请使用localhost而不是其主机名。

对创作实例和发布实例执行以下步骤：

1. 转到位于https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr的OSGi配置。
1. 查找并点按 **Day CQ Link Externalizer配置** 。
将打开Day CQ Link Externalizer对话框，用于编辑配置。
1. 在Day CQ Link Externalizer对话框的域字段中：

   * 在创作实例上，指定可从外部系统访问的发布URL。 例如，主机名或发布Web服务器。
   * 在发布实例上，指定作者URL和发布URL。

1. 在作者实例和发布实例上，确保在“域”字段中指定本地服务器URL。
1. 点按&#x200B;**保存**。等待一段时间，以便所有服务重新启动。

## 配置Day CQ Mail服务 {#cqmail}

参考站点实施要求示例用户在填写和提交表单时向其发送电子邮件。 通过配置Day CQ Mail服务，您可以提供SMTP服务详细信息，以向客户发送自动电子邮件。 See [Configuring Email Notifications](/help/sites-administering/notification.md).

执行以下步骤以在发布实例上配置邮件服务：

1. 转到位于https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr的OSGi配置。
1. 查找并点 **按Day CQ Mail Service** ，打开它进行配置。
1. 提供SMTP服务器主机名和端口值。
1. Tap **Save.**

>[!NOTE]
>
>您可以使用企业SMTP服务或Gmail等公共服务。 有关配置SMTP服务的信息，请参阅SMTP服务文档。

## 覆盖默认的XSS配置 {#xss}

We.Finance参考站点的电子邮件模板包含电子邮件中的个性化链接。 这些链接具有占位符 `${placeholder}`。 在发送电子邮件之前，这些占位符会被实际值替换。 AEM的默认XSS保护配置不允许HTML内容中的URL中出现大括号(**{ }**)。 但是，您可以对发布实例执行以下步骤来覆盖默认配置：

1. 复制 `/libs/cq/xssprotection/config.xml` 到 `/apps/cq/xssprotection/config.xml`。
1. 打开 `/apps/cq/xssprotection/config.xml`.
1. 在该部 `common-regexps` 分中，按如 `onsiteURL` 下方式修改条目并保存文件。

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>大括号(**{ }**)作为HTML内容中的URL中可接受的字符包含在内。

配置SMTP服务器后，尝试使用Sarah Rose人物填写表单并将其另存为草稿。 另存为草稿时，您可以选择通过电子邮件接收草稿。 点击“发 **送电子邮件** ”按钮时，如果您收到一封电子邮件，其中包含指向应用程序草稿的链接，则您的电子邮件配置将成功。 确保使用Sarah的凭据登录以查看草稿。

## 配置AEM DS设置 {#aemds}

在参考站点用例中，电子邮件通信的发布实例需要AEM DS服务设置。 有关在发布实例上配置AEM DS服务设置的详细步骤，请参 [阅配置AEM DS设置](../../forms/using/configuring-the-processing-server-url-.md)。

对于AEM Forms引用站点，在AEM DS设置服务中，指定发布服务器的URL而不是处理服务器的URL。

>[!CAUTION]
>
>如果要为AEM `/lc` Forms OSGi配置处理服务器URL，请勿将其放入该URL中。

## 部署参考站点包 {#refsite}

使用包共享安装参考站点包。

* [AEM Forms FSI参考站点包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-FSI-REF-SITE)
* [AEM Forms Gov参考站点包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-GOV-REF-SITE)

要进一步了解如何使用包和包共享，请参阅 [如何使用包](/help/sites-administering/package-manager.md)。

安装包并启动作者实例和发布实例后，请在浏览器中访问以下URL:

* `https://'[server]:[port]'/wegov`
* `https://'[server]:[port]'/wefinance`

如果安装成功，您可以访问和We.Finance参考站点登陆页。

## （可选）将示例数据导入Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

家庭抵押申请和汽车保险申请参考站点被配置为使用来自Microsoft Dynamics的记录。 引用站点包会安装自定义实体和示例记录，您可以将它们导入Microsoft Dynamics以运行引用站点。 执行以下步骤以迁移和设置示例数据：

要导入自动保险申请的自定义实体，请执行以下操作：

1. 从您 **的AEM作者实例中下载WeFinanceAutoInsurance_1_0.zip**`https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` 解决方案包。
1. 在Microsoft Dynamics实例中，转到“设置”>“解 **决方案”** ，然后单击“ **导入”**。 选择并导入包。

要导入自动保险申请的自定义实体，请执行以下操作：

1. 从下 **载AEMFormsFSIRefsite_1_0.zip** 包 `https://[author]:'port'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`。 选择并导入包。

1. 在Microsoft Dynamics实例中，转到“设置”>“解 **决方案”** ，然后单击“ **导入”**。 选择并导入包。

要导入客户和保险单记录，请执行以下操作：

1. 从AEM作 **者实例的以下位置下载We.Finance Customers.csv、We.Finance Auto Insurance Renewals.csv****和家庭抵押** :

   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. 在Microsoft Dynamics实例中，执行以下操作：

   * 转到“ **Sales** > **We.Finance Customers** ”，然后单击“ **Import**”。

   * 转到“ **Sales** > **We.Finance Auto Insurance** ”，然后单击“ **Import**”。

   * 转到“ **Sales** > **We.Finance Home Mortgage”(销售> We.Finance住房抵押** )，然后单 **击“Import**”。

## 为Microsoft Dynamics配置OAuth云服务 {#configure-oauth-cloud-service-for-microsoft-dynamics}

在AEM Forms中配置OAuth云服务，以启用AEM Forms与Microsoft Dynamics之间的通信。 执行以下步骤以在AEM作者和发布实例上配置OAuth云服务：

1. 在AEM作者实例中，转到工 **具** > **Cloud Services** > **Data Sources** > **** globalChick。 点按 **刷新Dynamics集成图标** ，然后点按属性。
1. 转到Microsoft Azure Active Directory帐户。 将复制的云服务配置URL添加到注册应 **用程序的“回复URL** ”设置中。 保存配置。
1. 在“身份验证设置”选项卡中， **为Microsoft Dynamics实例指定服务根**、客户端Id **、**&#x200B;客户端机密 **和****** 资源URL。 单 **击重定向到** Microsoft Dynamics登录页面的“连接到OAuth”。
1. 提供登录凭据。 登录后，您将被重定向到AEM Forms云服务配置页面。 单击 **保存并关闭**。 将保存云服务配置。
1. 转到“表 **单** ”>“数 **据集成** ” **>**“We.Finance”。 选择自动保险（动态），然后单击编辑。 Microsoft Dynamics实体列在“数据源”选项卡下。 等到从Microsoft Dynamics获取所有实体并列在数据源选项卡下。
1. 选择AutoInsuranceRenewal **实体** ，然后单 **击“测试模型对象”**。 在输入请求部分，将客户ID的值指定为“900001”，然后单击“测 **试”**。 “输出”部分显示从Microsoft Dynamics获取的客户ID 900001的记录。
1. 在输入请求部分，将客户ID的值指定为“900001”，然后单击“测 **试”**。 “输出”部分显示从Microsoft Dynamics获取的客户ID 900001的记录。
1. 对发布实例重复步骤1-6。

## 配置Adobe Sign调度程序 {#scheduler}

对作者实例和发布实例执行以下操作：

1. 转到AEM Web配置控制台(位于 `https://'[server]:[port]'system/console/configMgr`)。
1. 查找并点 **[!UICONTROL 按Adobe Sign配置服务]** ，以打开它进行配置。
1. 将状 **[!UICONTROL 态更新调度程序表达式配]** 置为0 0/2 * * * ? ****。

   >[!NOTE]
   >
   >上述调度程序配置每两分钟检查一次Adobe Sign服务的状态。

1. 点按&#x200B;**[!UICONTROL 保存]**。

## 配置参考站点Adobe Sign云服务 {#sign-service}

对作者实例和发布实例执行以下操作：

1. 转到“ **工具** ”>“ **云服务** ” **>“** Adobe Sign”>“全 **局签名**”。 选择 **AEM Forms Reference Site Sign** ，然后点按属性。

   >[!CAUTION]
   >
   >确保将 `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html` URL添加到Adobe Sign API应用程序OAuth配置的重定向URL列表。

1. 指定Adobe Sign应用程序OAuth配置的客户端ID和机密。
1. （可选）选择“ **[!UICONTROL 为附件启用Adobe Sign]** ”选项，然后点 **[!UICONTROL 按“连接到Adobe Sign”]**。 它会将附加到自适应表单的文件附加到发送以供签名的相应Adobe Sign文档。
1. 点 **[!UICONTROL 按连接到Adobe Sign]** ，然后使用Adobe Sign凭据登录。

## 配置Forms Common Configuration Service {#anonymous}

对发布实例执行以下操作以允许匿名用户访问：

1. 转到AEM Web配置控制台(位于 `https://'[server]:[port]'/system/console/configMgr`)。
1. 查找并点按 **[!UICONTROL 表单常用配置服务]** ，打开它进行配置。
1. 为“所有 **[!UICONTROL 用户]** ”配置 **[!UICONTROL “允许”字段]**。
1. 点按&#x200B;**[!UICONTROL 保存]**。

## 修改表单数据模型的Rest服务 {#fdm}

对作者实例和发布实例执行以下操作：

1. 请访问CRXDE `https://'[server]:[port]'/crx/de/index.jsp`。
1. 导航至 **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile** ，然后打开swagger文件。
1. 根据您的环境更新主机和端口设置。
1. 保存设置。
1. (仅&#x200B;**限作者实例**)转到“工具 **”** >“云 **服务”** >“源”>“全 ********&#x200B;局数据”>“Cloud Services”。 选择 **并点按属性****。点按身份验证设置**，然后将“身份验证类型”设 ************&#x200B;置设置为“基本身份验证”。 指定 `admin`/ `admin`作为访问服务的用户名／密码。 点按 **保存并关闭**。

## 与Marketing Cloud集成 {#integrate-with-marketing-cloud}

您可以将AEM Forms与Adobe Analytics和Adobe目标集成。 Adobe Analytics可以帮助您生成报告并分析自适应表单的性能，而Adobe目标则可以帮助您提供个性化体验并对自适应表单执行A/B测试。

执行以下操作以在AEM Forms中配置Adobe Analytics和Adobe目标。

### 配置Adobe Analytics {#configureanalytics}

AEM Forms与Adobe Analytics集成，使您能够监视和分析客户与表单和文档的交互方式。 它可以帮助您识别和修复问题区域并采取行动提高转化率。

要在参考站点中体验此功能，请按照配置分析和报告中的说明配 [置您的Analytics帐户](../../forms/using/configure-analytics-forms-documents.md)。

要生成报告，种子数据会与引用站点绑定。 在使用种子数据之前，请执行以下操作：

1. 确保We.Finance分析配置在AEM Cloud服务中可用。 您可以通过以下任一方式查找云服务：

   * 导航到 **[!UICONTROL 工具>云服务>旧版云服务]** ，或浏览到https://&lt;host>:&lt;port>/libs/cq/core/content/tools/cloudservices.html。
   * 在云服 **[!UICONTROL 务页面]** ，在 **[!UICONTROL Adobe Analytics部分下，单击]**`Show Configurations`。 您可以看到We.Finance的可用配置。 单击以打开配置。 在配置页面中，单击 **[!UICONTROL 编辑]**。 提供有效的公司、用户名、共享机密（密码）和数据中心，然后单击“ **[!UICONTROL 连接到分析”]**。 连接成功对话框后，单击配 **[!UICONTROL 置对话框]** 上的确定。 根据配置分析和报告中所述的分析配置 [下配置框架](../../forms/using/configure-analytics-forms-documents.md)。

1. 导航到https://&lt;*host*>:&lt;*port*>/system/console/configMgr并执行以下操作：

   * 在Web控制 **[!UICONTROL 台配置页面中]** ，查找并单击 **[!UICONTROL AEM表单分析配置]**。

   * 在“AEM Forms Analytics配置 **** ”对话框的“SiteCatalyst框架”字段中，选择we-finance(we-finance)或we-gov(we-gov)。
   * 单击 **[!UICONTROL 保存]** ，然后让页面刷新。

1. 导航到位于https://&lt;host>:&lt;port>/aem/forms的表单管理器，然后执行以下操作：

   * 打开We.Finance文件夹，然后选择要查看其报告的表单。
   * 单击操作工具栏中的启用分析。 为表单启用分析后，单击分析报告。 您可以看到生成的空白报告。 生成空白报告后，您必须提供随refsite包一起提供的种子数据，以生成分析报告以用于演示目的。
   参考站点为分析报告提供信用卡、家庭抵押和儿童支持用例的种子数据。

### 配置目标 {#configure-target}

参考站点展示AEM Forms与Adobe目标的集成，允许您在自适应文档中包含有针对性的个性化内容。 它还支持为自适应表单创建A/B测试。

要体验引用站点中的集成，请执行以下操作以在AEM中配置目标:

1. 开始使用jvm参数的作者快速 `-Dabtesting.enabled=true` 启动以在服务器上启用A/B测试。

   >[!NOTE]
   >
   >如果AEM实例在JBoss上运行（从Turnkey安装以服务形式启动），请在文件中的 `-Dabtesting.enabled=true` 以下条目中添加 `jboss\bin\standalone.conf.bat` 参数：
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. 访问 `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html`.

1. 在 **[!UICONTROL Adobe目标部分]** ，单击显 **[!UICONTROL 示配置]**。 您可以看到We.Finance目标配置。 单击以打开配置。 在配置页面中，单击 **[!UICONTROL 编辑]**。 此时将 **[!UICONTROL 打开配置的“编辑组件]** ”对话框。

1. 指定与您的目标帐户关联的客户代码、电子邮件和密码。 选择API类型作为 **[!UICONTROL REST]**。
1. Click **[!UICONTROL Connect to Adobe target]**. 成功配置目标帐户后，单击“确 **[!UICONTROL 定”]**。 您可以看到打包的配置有一个目标框架。

1. 转到 `https://<hostname>:<port>/system/console/configMgr`.

1. 单击“ **[!UICONTROL AEM表单目标配置”]**。
1. 选择目标框架。
1. 在“ **[!UICONTROL 目标URL]** ”字段中，指定AEM表单的URL。 For example: `https://<hostname>:<port>/`.

1. 单击&#x200B;**[!UICONTROL 保存]**。

信用卡应用程序和家庭按揭贷款应用程序使用案例演示了如何执行A/B测试并展示报告以用于演示目的。 有关演练，请参 [阅We.Finance参考站点演练](../../forms/using/finance-reference-site-walkthrough.md)。

## Next step {#next-step}

现在，您已准备好浏览参考站点。 有关参考站点工作流和步骤的详细信息，请参阅：

* [We.Finance参考站点演练](../../forms/using/finance-reference-site-walkthrough.md)
* [员工自助服务参考站点演练](../../forms/using/employee-self-service-reference-site.md)

