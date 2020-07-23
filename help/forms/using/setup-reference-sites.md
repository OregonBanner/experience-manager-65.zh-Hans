---
title: 设置和配置We.Finance和Employee自助参考站点
seo-title: 设置和配置We.Finance和Employee自助参考站点
description: AEM Forms参考站点展示了如何使用AEM Forms在组织中实现端对端工作流。
seo-description: AEM Forms参考站点展示了如何使用AEM Forms在组织中实现端对端工作流。
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: 371ecbdaad97b7111353f40d1ddfb686e99d46c5
workflow-type: tm+mt
source-wordcount: '2878'
ht-degree: 1%

---


# 设置和配置We.Finance和Employee自助参考站点{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

AEM Forms提供参考站点实施，以展示AEM Forms如何帮助金融服务行业和政府组织随时随地在任何设备上将复杂的交易转化为简单、引人入胜的数字体验。

We.Finance参考站点利用真实案例与现有和潜在客户进行互动，从初次接触开始，以个性化和经济有效的方式管理通信和交易。

通过参考站点，您可以探索和展示AEM Forms的以下主要功能。

* 引人入胜的响应式自适应表单和交互式通信的简化创作体验。
* 交互式通信，创建可适应设备设置和布局的交互式、个性化和响应式客户通信。
* 整合数据以连接到不同的数据源，通过表单数据模型预填和提交表单数据。
* 可自动处理业务流程和工作流的表单工作流程。
* 高级用户数据管理和处理功能。
* 与Adobe Sign集成，安全地签署和提交自适应表单。
* 与Adobe Target集成，提供有针对性的建议并执行A/B测试，从表单中最大化ROI。
* 与AdobeAnalytics集成，衡量表单或活动的表现并做出明智的决策。
* 增强的表单填写体验。

参考站点提供可重复使用的资产，您可以将这些资产用作模板来创建自己的资产。

* 与Adobe Sign集成，安全地签署和提交自适应表单。

* 与Adobe Sign集成，安全地签署和提交自适应表单。

## 设置参考站点的先决条件和步骤 {#prerequisites-and-steps-to-set-up-reference-sites}

在设置参考站点之前，请确保您具有以下各项：

* **AEM Essentials** AEM QuickStart、AEM Forms加载项包和参考站点包。 有关 [附加和参考](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 站点包的详细信息，请参阅AEM Forms版本。

* **SMTP服务**&#x200B;可使用任何SMTP服务。

* **Adobe Sign开发人员帐户和Adobe Sign API应用程序要使用数字签名功能** ，需要Adobe Sign开发人员帐户。 请参 [阅Adobe Sign](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)。

* 要与AEM Forms集成的Microsoft Dynamics 365正在运行的实例。 要运行引用站点，可将示例数据导入Microsoft Dynamics实例，以预填引用站点中使用的交互式通信。
* AEM的正在运行的实例（带有Forms加载项包）。 有关详细信息，请参 [阅安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

按照建议的顺序执行以下步骤来设置和配置引用站点。

<table>
 <tbody>
  <tr>
   <th><strong>步骤</strong></th>
   <th><strong>配置</strong></th>
   <th><strong>注释</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">安装和配置AEM Forms</a></td>
   <td>创作和发布</td>
   <td>安装和配置AEM Forms作者和发布实例。</td>
  </tr>
  <tr>
   <td><a href="#ssl">配置SSL</a></td>
   <td>Author and Publish<br /> </td>
   <td>启用HTTP over SSL，与Adobe Sign进行安全通信。</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">配置Day CQ链接外部器配置</a></p> </td>
   <td>Author and Publish<br /> </td>
   <td><p>参考站点使用案例针对不同的交易发送电子邮件。 此设置是通过电子邮件投放新闻稿时必需的。 它确保URL和图像指向发布实例。 </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">配置Day CQ邮件服务</a></td>
   <td>创作和发布</td>
   <td>电子邮件通信必需。</td>
  </tr>
  <tr>
   <td><a href="#xss">覆盖默认XSS配置</a></td>
   <td>发布</td>
   <td>用于覆盖受xss安全性阻止的$、{和}字符。</td>
  </tr>
  <tr>
   <td><a href="#aemds">配置AEM DS设置</a></td>
   <td>作者</td>
   <td>在发布实例上配置AEM DS以提交表单，并在创作实例上处理工作流。</td>
  </tr>
  <tr>
   <td><a href="#refsite">部署参考站点包</a></td>
   <td>作者</td>
   <td>在AEM Forms作者实例上部署引用站点包。</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">将示例数据导入Microsoft Dynamics</a></td>
   <td>创作和发布</td>
   <td>导入信用卡申请、住房抵押申请和住房保险申请的示例数据演练</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">为Microsoft Dynamics配置OAuth云服务</a></td>
   <td>创作和发布</td>
   <td>在AEM Forms中配置OAuth云服务，以启用AEM Forms与Microsoft Dynamics之间的通信。 </td>
  </tr>
  <tr>
   <td><a href="#scheduler">配置Adobe Sign调度程序</a></td>
   <td>Author and Publish<br /> </td>
   <td>更改调度程序配置，每两分钟检查一次状态。</td>
  </tr>
  <tr>
   <td><a href="#sign-service">配置参考站点Adobe SignCloud Service</a></td>
   <td>Author and Publish<br /> </td>
   <td>引用站点包附带的配置，需要使用有效凭据进行重新配置。</td>
  </tr>
  <tr>
   <td><a href="#anonymous">为匿名用户配置Forms Common Configuration Service</a></td>
   <td>发布</td>
   <td>该配置允许匿名用户提交、签署和文档记录生成。</td>
  </tr>
  <tr>
   <td><a href="#fdm">修改表单数据模型的Rest Service Swagger文件</a></td>
   <td>Author and Publish<br /> </td>
   <td>修改环境的服务。</td>
  </tr>
 </tbody>
</table>

## 安装和配置AEM Forms {#installandconfigureaemform}

按照在OSGi上安装和配置 [AEM Forms中的说明安装和部署AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

>[!NOTE]
>
>如果不同计算机上有多个发布实例或作者实例和发布实例，请配置复制和反向复制代理。

## 配置SSL {#ssl}

需要SSL配置才能与Adobe Sign服务器通信。 有关详细步骤，请 [参阅启用HTTP over SSL](/help/sites-administering/ssl-by-default.md)。

>[!CAUTION]
>
>请勿对文件夹配置强制 `/etc/map` SSL。

## 配置Day CQ链接外部器配置 {#externalizer}

在AEM中， **Externalizer** 是一个OSGI服务，它允许您以编程方式转换资源路径(例如， /path/to/my/page)通过预配置DNS来预装路径，从而将其导入外部和绝对URL(例如，https://www.mycompany.com/path/to/my/page)。 请参 [阅将URL外置](/help/sites-developing/externalizer.md)。

>[!CAUTION]
>
>如果使用SSL的自签名证书，请勿外置为HTTPS URL。
>
>此外，对于本地服务器，请使用localhost而不是其主机名。

对创作和发布实例执行以下步骤：

1. 转到位于https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr的OSGi配置。
1. 查找并点 **按Day CQ Link Externalizer配置** 。
将打开“Day CQ Link Externalizer”对话框，用于编辑配置。
1. 在Day CQ Link Externalizer对话框中的域字段中：

   * 在创作实例上，指定可从外部系统访问的发布URL。 例如，主机名或发布Web服务器。
   * 在发布实例上，指定作者URL和发布URL。

1. 在作者实例和发布实例上，确保在“域”字段中指定本地服务器URL。
1. 点按&#x200B;**保存**。等待一段时间，以便所有服务重新启动。

## 配置Day CQ邮件服务 {#cqmail}

参考站点实施要求在填写和提交表单时向示例用户发送电子邮件。 通过配置Day CQ邮件服务，您可以提供SMTP服务详细信息，以向客户发送自动电子邮件。 See [Configuring Email Notifications](/help/sites-administering/notification.md).

执行以下步骤以在发布实例上配置邮件服务：

1. 转到位于https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr的OSGi配置。
1. 查找并点 **按Day CQ邮件服务** ，打开它进行配置。
1. 提供SMTP服务器主机名和端口值。
1. Tap **Save.**

>[!NOTE]
>
>您可以使用企业SMTP服务或Gmail等公共服务。 有关配置SMTP服务的信息，请参阅SMTP服务文档。

## 覆盖默认XSS配置 {#xss}

We.Finance参考站点的电子邮件模板包含电子邮件中的个性化链接。 这些链接具有占位符 `${placeholder}`。 在发送电子邮件之前，这些占位符会被实际值替换。 AEM的默认XSS保护配置不允许HTML内容&#x200B;**中** URL中的大括号({ })。 但是，您可以对发布实例执行以下步骤来覆盖默认配置：

1. 复制 `/libs/cq/xssprotection/config.xml` 到 `/apps/cq/xssprotection/config.xml`。
1. 打开 `/apps/cq/xssprotection/config.xml`.
1. 在部分 `common-regexps` 中，按如 `onsiteURL` 下方式修改条目并保存文件。

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>大括号(**{ }**)在HTML内容的URL中包含为可接受的字符。

配置SMTP服务器后，尝试使用Sarah Rose人物填写表单并将其另存为草稿。 另存为草稿时，您可以选择通过电子邮件接收草稿。 点击“发 **送电子邮件** ”按钮时，如果您收到一封包含指向应用程序草稿的链接的电子邮件，则您的电子邮件配置将成功。 确保使用Sarah的凭据登录以查看草稿。

## 配置AEM DS设置 {#aemds}

在参考站点用例中，电子邮件通信的发布实例需要AEM DS服务设置。 有关在发布实例上配置AEM DS服务设置的详细步骤，请参 [阅配置AEM DS设置](../../forms/using/configuring-the-processing-server-url-.md)。

对于AEM Forms引用站点，在AEM DS设置服务中，指定发布服务器的URL而不是处理服务器的URL。

>[!CAUTION]
>
>如果要为 `/lc` AEM FormsOSGi配置处理服务器URL，请勿将其放入。

## 部署参考站点包 {#refsite}

使用“软件分发”安装参 [考站点包](https://docs.adobe.com/content/help/en/experience-cloud/software-distribution/home.html)。

* [AEM FormsFSI参考站点包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2FAEM-FORMS-6.5-FSI-REF-SITE)
* [AEM Forms政府参考站点包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2FAEM-FORMS-6.5-GOV-REF-SITE)

要进一步了解如何使用包，请参 [阅如何使用包](/help/sites-administering/package-manager.md)。

安装包并启动创作和发布实例后，请在浏览器中访问以下URL:

* `https://'[server]:[port]'/wegov`
* `https://'[server]:[port]'/wefinance`

如果安装成功，您可以访问和We.Finance参考站点登陆页。

## （可选）将示例数据导入Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

家庭抵押申请和汽车保险申请参考站点被配置为使用来自Microsoft Dynamics的记录。 引用站点包会安装自定义实体和示例记录，您可以将它们导入Microsoft Dynamics以运行引用站点。 请执行以下步骤来迁移和设置示例数据：

要导入汽车保险应用程序的自定义实体，请执行以下操作：

1. 从您的 **AEM作者实例上下载WeFinanceAutoInsurance_1_0** .zip `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` 解决方案包。
1. 在Microsoft Dynamics实例中，转到“设置”>“ **解决方案”** ，然后单击“ **导入**”。 选择并导入包。

要导入汽车保险应用程序的自定义实体，请执行以下操作：

1. 从下 **载AEMFormsFSIRefsite_1_0.zip** 包 `https://[author]:'port'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`。 选择并导入包。

1. 在Microsoft Dynamics实例中，转到“设置”>“ **解决方案”** ，然后单击“ **导入**”。 选择并导入包。

要导入客户和保险单记录，请执行以下操作：

1. 从AEM **作者实例的以下位置下载We.Finance** Customers.csv、We.Finance Auto Insurance Renewals **.** csv和家庭抵押数据文件：

   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. 在Microsoft Dynamics实例中，执行以下操作：

   * 转至“销 **售** ”> **“We.Finance客户** ”，然 **后单击**“导入”。

   * 转至“销 **售** ”> **“We.Finance汽车保险”** ，然后单 **击“导入**”。

   * 转至“销 **售** ”> **“We.Finance Home Mortgage”** ，然后单 **击“Import**”。

## 为Microsoft Dynamics配置OAuth云服务 {#configure-oauth-cloud-service-for-microsoft-dynamics}

在AEM Forms中配置OAuth云服务，以启用AEM Forms与Microsoft Dynamics之间的通信。 执行以下步骤以在AEM作者和发布实例上配置OAuthCloud Service:

1. 在AEM作者实例中，转 **到工具** > **Cloud Service** > **数据源** > **全**&#x200B;局。 点按 **Refsite Dynamics Integration图标** ，然后点按属性。
1. 转到Microsoft Azure Active Directory帐户。 将复制的云服务配置URL添加到已注 **册应用程** 序的回复URL设置中。 保存配置。
1. 在“身份验证设置”选 **项卡中**，为 **您的Microsoft** Dynamics实例指 **定服务根、**&#x200B;客户端Id、 **客户端机密和** 资源URL。 单击 **“连接到** OAuth”，它将重定向到Microsoft Dynamics登录页。
1. 提供登录凭据。 登录后，您将被重定向到“AEM Forms云服务配置”页。 单击&#x200B;**保存并关闭**。云服务配置已保存。
1. 转至 **表单** >数 **据集成** > **We.Finance**。 选择自动保险（动态），然后单击编辑。 Microsoft Dynamics实体列在“数据源”选项卡下。 请等待，直到从Microsoft Dynamics获取所有实体并列在数据源选项卡下。
1. 选择AutoInsuranceRenewal **实体** ，然后单 **击“测试模型对象”**。 在输入请求部分，将客户ID的值指定为“900001”，然后单击“ **测试**”。 “输出”部分显示从Microsoft Dynamics为客户ID 900001获取的记录。
1. 在输入请求部分，将客户ID的值指定为“900001”，然后单击“ **测试**”。 “输出”部分显示从Microsoft Dynamics为客户ID 900001获取的记录。
1. 对发布实例重复步骤1-6。

## 配置Adobe Sign调度程序 {#scheduler}

对创作和发布实例执行以下操作：

1. 转到AEM Web配置控制台(位 `https://'[server]:[port]'system/console/configMgr`置)。
1. 查找并点 **[!UICONTROL 按Adobe Sign Configuration Service]** ，打开它进行配置。
1. 将状 **[!UICONTROL 态更新调度程序表达式]** 配置为0 0/2 * * ? ****。

   >[!NOTE]
   >
   >上述调度程序配置每两分钟检查一次Adobe Sign服务的状态。

1. 点按&#x200B;**[!UICONTROL 保存]**。

## 配置参考站点Adobe Sign云服务 {#sign-service}

对创作和发布实例执行以下操作：

1. 转至“工 **具** ”> **Cloud Service** > **“Adobe** Sign” **>**“全局”。 选择 **AEM Forms引用站点签名** ，然后点按属性。

   >[!CAUTION]
   >
   >确保将该 `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html` URL添加到Adobe Sign API应用程序OAuth配置的重定向URL列表。

1. 指定Adobe Sign应用程序OAuth配置的客户端ID和机密。
1. （可选）选择“ **[!UICONTROL 启用Adobe Sign for attachments ando]** ”选项，然 **[!UICONTROL 后点按Connect to Adobe Sign]**。 它会将附加到自适应表单的文件附加到发送以供签名的相应Adobe Sign文档。
1. 点 **[!UICONTROL 按Connect至Adobe Sign]** ，然后使用您的Adobe Sign凭据登录。

## 配置表单通用配置服务 {#anonymous}

在发布实例上执行以下操作以允许匿名用户访问：

1. 转到AEM Web配置控制台(位 `https://'[server]:[port]'/system/console/configMgr`置)。
1. 查找并点 **[!UICONTROL 按表单通用配置服务]** ，以打开它进行配置。
1. 为“所有 **[!UICONTROL 用户]** ”配置 **[!UICONTROL “允许”字段]**。
1. 点按&#x200B;**[!UICONTROL 保存]**。

## 修改表单数据模型的余料服务 {#fdm}

对创作和发布实例执行以下操作：

1. 请访问CRXDE `https://'[server]:[port]'/crx/de/index.jsp`。
1. 导航到 **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile** ，然后打开swagger文件。
1. 根据您的环境更新主机和端口设置。
1. 保存设置。
1. (仅&#x200B;**限作者实例**)转到 **工具** > **Cloud Service** > **Sources******> Global Data 。 选择 **roi-rest** 并点按属 **性**。点按身份验 **证设置** ，将身份验证类型 **设置为基本******&#x200B;身份验证。 指 `admin`定/ `admin`作为用户名／口令访问服务。 点按 **保存并关闭**。

## 与Marketing Cloud集成 {#integrate-with-marketing-cloud}

您可以将AEM Forms与AdobeAnalytics和Adobe Target集成。 AdobeAnalytics可以帮助您生成报告并分析自适应表单的性能，而Adobe Target则可以帮助您提供个性化体验并对自适应表单执行A/B测试。

执行以下操作以在AEM Forms中配置AdobeAnalytics和Adobe Target。

### 配置AdobeAnalytics {#configureanalytics}

AEM Forms与AdobeAnalytics的集成使您能够监控和分析客户如何与您的表单和文档互动。 它有助于您识别和修复问题区域并采取行动增加转化率。

要在参考站点中体验此功能，请按照配置分析和报告中的 [说明配置Analytics帐户](../../forms/using/configure-analytics-forms-documents.md)。

要生成报告，种子数据会与引用站点绑定。 在使用种子数据之前，请执行以下操作：

1. 确保We.Finance分析配置在AEM cloud services中可用。 您可以通过以下方式之一查找云服务：

   * 导航到“ **[!UICONTROL 工具”>“Cloud Service]** ”>“旧Cloud Service”或浏览到https://&lt;host>:&lt;port>/libs/cq/core/content/tools/cloudservices.html。
   * 在Cloud Service **[!UICONTROL 页面中]** ，在Adobe **[!UICONTROL Analytics部]** 分下 `Show Configurations`，单击。 您可以看到We.Finance的可用配置。 单击以打开配置。 在配置页面中，单击 **[!UICONTROL 编辑]**。 提供有效公司、用户名、共享机密（密码）和数据中心，然后单击“连 **[!UICONTROL 接到Analytics”]**。 连接成功对话框后，单击 **[!UICONTROL 配置]** 对话框中的确定。 在Analytics配置下配置框架，如配置Analytics [和报告中所述](../../forms/using/configure-analytics-forms-documents.md)。

1. 导航到https://&lt;*host*>:&lt;*port*>/system/console/configMgr并执行以下操作：

   * 在“Web控 **[!UICONTROL 制台配置]** ”页中，找到并单 **[!UICONTROL 击AEM FormsAnalytics配置]**。

   * 在“AEM Forms **[!UICONTROL Analytics配置]** ”对话框的“SiteCatalyst框架”字段中，选择we-finance(we-finance)或we-gov(we-gov)。
   * 单击 **[!UICONTROL 保存]** ，然后让页面刷新。

1. 导航到位于https://&lt;host>:&lt;port>/aem/forms的表单管理器，然后执行以下操作：

   * 打开We.Finance文件夹，选择要查看其报表的表单。
   * 单击“操作”工具栏中的“启用Analytics”。 为表单启用分析后，单击Analytics报告。 您可以看到生成的空白报告。 生成空白报告后，您必须提供refsite包附带的种子数据，以生成分析报告以用于演示。

   参考站点为分析报告提供信用卡、家庭抵押和儿童支持使用案例的种子数据。

### 配置目标 {#configure-target}

参考站点展示AEM Forms与Adobe Target的集成，允许您在自适应文档中包含有针对性的个性化内容。 它还支持为自适应表单创建A/B测试。

要体验引用站点中的集成，请执行以下操作以在AEM中配置目标:

1. 将作者快速启动与jvm参数开始 `-Dabtesting.enabled=true` ，以在服务器上启用A/B测试。

   >[!NOTE]
   >
   >如果AEM实例在JBoss上运行，而JBoss是从Turnkey安装中作为服务启动的，请在文 `-Dabtesting.enabled=true` 件的以下条目中添加 `jboss\bin\standalone.conf.bat` 参数：
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. 访问 `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html`.

1. 在Adobe Target **[!UICONTROL 部分]** ，单击显 **[!UICONTROL 示配置]**。 您可以看到可用的We.Finance目标配置。 单击以打开配置。 在配置页面中，单击 **[!UICONTROL 编辑]**。 此时 **[!UICONTROL 将打开配]** 置的编辑组件对话框。

1. 指定与您的目标帐户关联的客户代码、电子邮件和密码。 选择API类型 **[!UICONTROL 为REST]**。
1. Click **[!UICONTROL Connect to Adobe target]**. 成功配置目标帐户后，单击“ **[!UICONTROL 确定]**”。 您可以看到打包配置有一个目标框架。

1. 转到 `https://<hostname>:<port>/system/console/configMgr`.

1. 单击 **[!UICONTROL AEM Forms目标配置]**。
1. 选择目标框架。
1. 在目标 **[!UICONTROL URL]** 字段中，指定AEM Forms的URL。 For example: `https://<hostname>:<port>/`.

1. 单击&#x200B;**[!UICONTROL 保存]**。

信用卡应用程序和家庭抵押应用程序使用案例演示了如何执行A/B测试并展示报告以用于演示目的。 有关演练，请参 [阅We.Finance参考站点演练](../../forms/using/finance-reference-site-walkthrough.md)。

## Next step {#next-step}

现在，您已准备好浏览参考站点。 有关参考站点工作流程和步骤的详细信息，请参阅：

* [We.Finance参考站点演练](../../forms/using/finance-reference-site-walkthrough.md)
* [员工自助参考站点演练](../../forms/using/employee-self-service-reference-site.md)

