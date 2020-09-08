---
title: 安装和配置数据捕获功能
seo-title: 安装和配置数据捕获功能
description: 安装和配置自适应表单、PDF forms和HTML5Forms。 配置Adobe Analytics和Adobe Target，以便根据自适应表单分析表单和目标用户的用户档案。
seo-description: 安装和配置自适应表单、PDF forms和HTML5Forms。 配置Adobe Analytics和Adobe Target，以便根据自适应表单分析表单和目标用户的用户档案。
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: cbc43991143397c8bc0080b7402bfdc664522ab8
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 1%

---


# 安装和配置数据捕获功能{#install-and-configure-data-capture-capabilities}

## 简介 {#introduction}

AEM Forms提供一组表单从最终用户处获取数据：自适应表单、HTML5Forms和PDF forms。 它还提供了各种工具，用于列表网页上所有可用表单、分析表单的使用情况以及根据用户的用户档案目标用户。 这些功能包含在AEM Forms附加软件包中。 加载项包部署在AEM的作者或发布实例上。

**自适应表单：** 这些表单根据设备的屏幕大小更改外观，具有吸引力并具有交互性。 适应性Forms也可以与Adobe Analytics、Adobe Sign和Adobe Target相集成。 它使您能够根据用户人口统计和其他功能向用户提供个性化的表单和面向流程的体验。 您还可以将自适应表单与Adobe Sign集成。

**PDF forms** 适合在PDF文档中进行像素级完美的打印和数字信息捕捉。 在数字化头像中，您可以使用Adobe Acrobat或Acrobat Reader填写这些表单。 您可以将这些表单托管在您的网站上，或使用表单门户在AEM站点上列表这些表单。 您还可以将这些表单作为附件发送给其他人。 这些表单最适合桌面环境。

**HTML5Forms** 是浏览器友好的PDF forms版本。 HTML5Forms适合不支持PDF插件的环境。 HTML5Forms支持在不支持基于XFA的PDF的移动设备和桌面浏览器上渲染基于XFA的表单。 这些表单最适合平板电脑和桌面环境。

AEM Forms是一个功能强大的企业级平台，数据捕获(自适应表单、PDF forms和HTML5Forms)只是AEM Forms的一项功能。 有关功能的完整列表，请参 [阅AEM Forms简介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓扑 {#deployment-topology}

AEM Forms加载项包是部署到AEM上的应用程序。 您至少需要一个AEM作者实例和AEM发布实例才能运行AEM Forms数据捕获功能。 建议使用以下拓扑运行AEM FormsAEM Forms数据捕获功能。 有关拓扑的详细信息，请参 [阅AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md)。

![推荐拓扑](assets/recommended-topology.png)

## 系统要求 {#system-requirements}

在开始安装和配置AEM Forms的数据捕获功能之前，请确保：

* 硬件和软件基础架构已到位。 有关受支持硬件和软件的详细列表，请参 [阅技术要求](/help/sites-deploying/technical-requirements.md)。

* AEM实例的安装路径不包含空格。
* AEM实例已启动且正在运行。 对于Windows用户，请在提升模式下安装AEM实例。 在AEM术语中，“实例”是在创作或发布模式下在服务器上运行的AEM的副本。 您至少需要两个AEM [实例（一个作者实例和一个发布实例）](/help/sites-deploying/deploy.md) ，才能运行AEM Forms数据捕获功能：

   * **作者**:用于创建、上传和编辑内容以及管理网站的AEM实例。 内容准备就绪后，即会复制到发布实例。
   * **发布**:通过Internet或内部网络向公众提供已发布内容的AEM实例。

* 满足内存要求。 AEM Forms附加包要求：

   * 15 GB临时空间，用于基于Microsoft Windows的安装。
   * 6 GB临时空间用于基于UNIX的安装。

* 为作者实例和发布实例设置复制和反向复制。 For details, see [Replication](/help/sites-deploying/replication.md).
* 对于基于UNIX的系统：

   * 从安装介质安装以下32位包：

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>伊比库</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 如果服务器上已安装OpenSSL，请将其升级到最新版本。
>* 创建分别指向libcurl、libcrypto.so和libssl.so库最新版本的symlinks。

>



* 从安装介质安装以下64位包：

   * 伊比库

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

AEM Forms加载项包是部署到AEM上的应用程序。 该软件包包含AEM Forms数据捕获和其他功能。 请执行以下步骤来安装加载项包：

1. 开放 [软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID才能登录软件分发。
1. 点按 **[!UICONTROL 标题]** 菜单中提供的Adobe Experience Manager。
1. 在过滤器 **[!UICONTROL 部分]** :
   1. 从“ **[!UICONTROL 解决方]** 案 **[!UICONTROL ”下拉]** 列表中选择Forms。
   2. 选择包的版本和类型。 您还可以使用“搜 **[!UICONTROL 索下载]** ”选项筛选结果。
1. 点按适用于您的操作系统的包名称，选择“ **[!UICONTROL 接受EULA条款]**”，然后点 **[!UICONTROL 按下载]**。
1. 打开 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然后单 **[!UICONTROL 击“上传包]** ”以上传包。
1. Select the package and click **[!UICONTROL Install]**.

   您还可以通过AEM Forms版本文章中列出的直接链接下载 [该包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 。
1. 安装包后，系统会提示您重新启动AEM实例。 **请勿立即重新启动服务器。** 在停止AEM Forms服务器之前，请等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止显示在文 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 件中并且日志是稳定的。
1. 对所有“作者”和“发布”实例重复步骤1-7。

### （仅限Windows）Visual Studio可再发行组件的自动安装 {#automatic-installation-visual-studio-redistributables}

如果以提升模式安装AEM实例，则在安装AEM Forms加载项包时会自动安装缺少的Visual Studio可再发行组件。

要评估Visual Studio可再发行组件是否自动安装，请打 `error.log` 开目录中可用的 `/crx-repository/logs/` 文件。 日志包含以下消息：

`Redist <service name> already installed on system, will not attempt re-installation`

如果可再发行组件无法安装，日志中将包含以下消息：

`Current user does not have elevated privileges, aborting installation of redist <service name>`

要解决此问题，请重新启动AEM服务器，在提升模式下安装AEM，然后安装AEM Forms加载项包。

如果权限检查失败，日志将包含以下消息：

`Privilege escalation check failed with error: <error message>`

## 安装后配置 {#post-installation-configurations}

AEM Forms有一些强制性和可选配置。 必需配置包括配置BouncyCastle库和序列化代理。 可选配置包括配置调度程序、Forms门户、Adobe Sign、Adobe Analytics和Adobe Target。

### 强制安装后配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle库  {#configure-rsa-and-bouncycastle-libraries}

对所有“作者”和“发布”实例执行以下步骤以引导委派库：

1. 停止基础AEM实例。
1. Open the `[AEM installation directory]\crx-quickstart\conf\sling.properties` file for editing.

   如果您曾 `[AEM installation directory]\crx-quickstart\bin\start.bat` 经开始AEM，请编辑位于的sling.properties `[AEM_root]\crx-quickstart\`。

1. 将以下属性添加到sling.properties文件：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. 保存并关闭文件，并开始AEM实例。
1. 对所有“作者”和“发布”实例重复步骤1-4。

#### 配置序列化代理 {#configure-the-serialization-agent}

对所有“作者”和“发布”实例执行以下步骤，将包添加到该允许列表:

1. 在浏览器窗口中打开AEM Configuration Manager。 默认URL为 `https://'[server]:[port]'/system/console/configMgr`。
1. 搜索 **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** 并打开配置。
1. 将sun. **util.calendar包添加** 到“ **** ”字段。 单击&#x200B;**保存**。
1. 对所有“作者”和“发布”实例重复步骤1-3。

### 可选安装后配置 {#optional-post-installation-configurations}

#### 配置调度程序 {#configure-dispatcher}

调度程序是Adobe Experience Manager的缓存和／或负载平衡工具，可与企业级Web服务器结合使用。 如果您使 [用Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，请为AEM Forms执行以下配置：

1. 为AEM Forms配置访问：

   打开调度程序。any文件进行编辑。 导航到筛选器部分，然后将以下筛选器添加到筛选器部分：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存并关闭文件。 有关过滤器的详细信息，请参 [阅Dispatcher文档](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 配置推荐人筛选器服务：

   以管理员身份登录到Apache Felix配置管理器。 配置管理器的默认URL为 `https://[server]:[port_number]/system/console/configMgr`。 在“配 **置** ”菜单中，选 **择“Apache Sling推荐人过滤器** ”选项。 在“允许主机”字段中，输入调度程序的主机名以允许它作为推荐人，然后单击“保 **存”**。 条目的格式为https://[server]:[port]。

#### 配置缓存 {#configure-cache}

缓存是一种缩短数据访问时间、减少延迟和提高输入／输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于缩短渲染自适应表单所需的时间。

* 在使用自适应表单缓存时， [使用AEM](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) Dispatcher缓存自适应表单的客户端库（CSS和JavaScript）。
* 在开发自定义组件时，在用于开发的服务器上禁用自适应表单缓存。

请执行以下步骤以配置自适应表单缓存：

1. 转到AEM Web控制台配置管理器[(位]于[https://&#39;]server:port&#39;/system/console/configMgr)。
1. 单击 **自适应表单和交互式通信Web渠道配置** ，以编辑其配置值。 在“编辑配置值”对话框中，在“Number of Adaptive Bidow”(自适应Forms)字段中指定AEM Forms服务器实例可缓存的最 **大表单或文档** 。 默认值为 100。单击&#x200B;**保存**。

   >[!NOTE]
   >
   >要禁用缓存，请将“Number of Adaptive Genative”(自适应Forms)字段中的值设 **置为0**。 在禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

#### 为表单数据模型配置SSL通信 {#configure-ssl-communcation-for-form-data-model}

可以为表单数据模型启用SSL通信。 要为表单数据模型启用SSL通信，请在启动任何AEM Forms实例之前，向所有实例的Java信任存储添加证书。 您可以运行以下命令来添加证书：&quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### 配置Adobe Sign {#configure-adobe-sign}

Adobe Sign为自适应表单启用电子签名工作流。 电子签名可改善处理法律、销售、工资、人力资源管理等文档的工作流。

在典型的Adobe Sign和自适应表单场景中，用户填写自适应表单 **以申请服务**。 例如，信用卡申请和公民福利表。 当用户填写、提交和签署应用程序表单时，该表单将发送给服务提供商以执行进一步操作。 服务提供商审阅应用程序，并使用Adobe Sign标记已批准的应用程序。 要启用类似的电子签名工作流，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms结合， [将Adobe Sign与AEM Forms结合](/help/forms/using/adobe-sign-integration-adaptive-forms.md)。

#### 配置Adobe Analytics {#configure-adobe-analytics}

AEM Forms与Adobe Analytics集成，使您能够捕获和跟踪已发布表单和文档的绩效指标。 分析这些指标的目的是根据使表单或文档更可用所需的更改数据做出明智决策。

要将Adobe Analytics与AEM Forms结合使用，请参 [阅配置分析和报告](/help/forms/using/configure-analytics-forms-documents.md)。

#### 整合Adobe Target {#integrate-adobe-target}

如果您的客户提供的体验不吸引人，他们可能会放弃表单。 虽然这令客户感到沮丧，但也可以增加组织的支持量和成本。 识别和提供正确的客户体验是至关重要的，也具有挑战性，可以增加转化率。 AEM表单是解决此问题的关键。

AEM forms与Adobe Marketing Cloud解决方案Adobe Target集成，跨多个数字渠道提供个性化、引人入胜的客户体验。 要使用Adobe Target测试自适应表单，请将 [Adobe Target与AEM Forms整合](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

## 后续步骤 {#next-steps}

您已配置环境以使用AEM Forms数据捕获功能。 现在，使用该功能的后续步骤是：

* [创建您的第一个自适应表单](/help/forms/using/create-your-first-adaptive-form.md)
* [创建您的第一个PDF表单](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5简介Forms](/help/forms/using/introduction.md)

