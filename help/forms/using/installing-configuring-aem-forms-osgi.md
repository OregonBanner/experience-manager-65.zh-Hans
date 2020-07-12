---
title: 安装和配置数据捕获功能
seo-title: 安装和配置数据捕获功能
description: 安装和配置自适应表单、PDF forms和HTML5表单。 配置AdobeAnalytics和Adobe Target的自适应表单，以根据其用户档案分析表单和目标用户的使用情况。
seo-description: 安装和配置自适应表单、PDF forms和HTML5表单。 配置AdobeAnalytics和Adobe Target的自适应表单，以根据其用户档案分析表单和目标用户的使用情况。
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: a18a018181a779b9f48ef3e39c26410a1bc4919b
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 1%

---


# 安装和配置数据捕获功能{#install-and-configure-data-capture-capabilities}

## 简介 {#introduction}

AEM Forms提供一组表单以从最终用户获取数据： 自适应表单、HTML5表单和PDF forms。 它还提供了各种工具，用于列表网页上所有可用表单、分析表单的使用情况以及根据用户的用户档案目标用户。 这些功能包含在AEM Forms附加包中。 加载项包部署在AEM的作者或发布实例上。

**自适应表单：** 这些表单根据设备的屏幕大小更改外观，具有吸引力并具有交互性。 自适应表单还可以与AdobeAnalytics、Adobe Sign和Adobe Target集成。 它使您能够根据用户人口统计和其他功能向用户提供个性化的表单和面向流程的体验。 您还可以将自适应表单与Adobe Sign集成。

**PDF forms** 适合在PDF文档中进行像素级完美的打印和数字信息捕捉。 在数字化头像中，您可以使用Adobe Acrobat或Acrobat Reader填写这些表单。 您可以将这些表单托管在您的网站上，或使用表单门户在AEM站点上列表这些表单。 您还可以将这些表单作为附件发送给其他人。 这些表单最适合桌面环境。

**HTML5 Forms** 是浏览器友好型PDF forms。 HTML5 Forms适用于不支持PDF插件的环境。 HTML5 Forms支持在移动设备和桌面浏览器上呈现基于XFA的表单，而不支持基于XFA的PDF。 这些表单最适合平板电脑和桌面环境。

AEM Forms是一个功能强大的企业级平台，数据捕获(自适应表单、PDF forms和HTML5表单)只是AEM Forms的一项功能。 有关功能的完整列表，请参 [阅AEM Forms简介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓扑 {#deployment-topology}

AEM Forms加载项包是部署到AEM上的应用程序。 运行AEM Author数据捕获功能至少需要一个AEM Publish和AEM Forms实例。 建议使用以下拓扑运行AEM FormsAEM Forms数据捕获功能。 有关拓扑的详细信息，请参 [阅AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md)。

![推荐拓扑](assets/recommended-topology.png)

## 系统要求 {#system-requirements}

在开始安装和配置AEM Forms的数据捕获功能之前，请确保：

* 硬件和软件基础架构已到位。 有关受支持硬件和软件的详细列表，请参 [阅技术要求](/help/sites-deploying/technical-requirements.md)。

* AEM实例的安装路径不包含空格。
* AEM实例已启动并正在运行。 在AEM术语中，“实例”是在创作或发布模式下在服务器上运行的AEM的副本。 您至少需要两个 [AEM实例（一个作者实例和一个发布实例）](/help/sites-deploying/deploy.md) ，才能运行AEM Forms数据捕获功能：

   * **作者**: 用于创建、上传和编辑内容以及管理网站的AEM实例。 内容准备就绪后，即会复制到发布实例。
   * **发布**: 通过Internet或内部网络向公众提供已发布内容的AEM实例。

* 满足内存要求。 AEM Forms加载项包需要：

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

1. 开放 [软件分发](https://experience.adobe.com/downloads)。 您需要Adobe ID登录软件分发。
1. 点按 **[!UICONTROL 标题]** 菜单中可用的Adobe Experience Manager。
1. 在过滤器 **[!UICONTROL 部分]** :
   1. 从“ **[!UICONTROL 解决方]** 案 **[!UICONTROL ”下]** 拉列表中选择“表单”。
   2. 选择包的版本和类型。 您还可以使用“搜 **[!UICONTROL 索下载]** ”选项筛选结果。
1. 点按适用于您的操作系统的包名称，选择“ **[!UICONTROL 接受EULA条款]**”，然后点 **[!UICONTROL 按下载]**。
1. 打开 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然后单 **[!UICONTROL 击“上传包]** ”以上传包。
1. Select the package and click **[!UICONTROL Install]**.

   您还可以通过AEM Forms版本文章中列出的直接链接下载 [该包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 。
1. 安装包后，系统会提示您重新启动AEM实例。 **请勿立即重新启动服务器。** 在停止AEM Forms服务器之前，请等到文件中出现ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息， `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 并且日志是稳定的。
1. 对所有“作者”和“发布”实例重复步骤1-7。

## 安装后配置 {#post-installation-configurations}

AEM Forms有一些必选和可选配置。 必需配置包括配置BouncyCastle库和序列化代理。 可选配置包括配置调度程序、Forms Portal、Adobe Sign、AdobeAnalytics和Adobe Target。

### 强制安装后配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle库  {#configure-rsa-and-bouncycastle-libraries}

对所有“作者”和“发布”实例执行以下步骤以引导委派库：

1. 停止基础AEM实例。
1. Open the `[AEM installation directory]\crx-quickstart\conf\sling.properties` file for editing.

   如果您曾 `[AEM installation directory]\crx-quickstart\bin\start.bat` 经开始过AEM，请编辑位于的sling.properties `[AEM_root]\crx-quickstart\`。

1. 将以下属性添加到sling.properties文件：

   ```
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

#### 配置Dispatcher {#configure-dispatcher}

Dispatcher是AEM的缓存和负载平衡工具。 AEMDispatcher还有助于保护AEM服务器免受攻击。 您可以结合使用Dispatcher与企业级Web服务器，提高AEM实例的安全性。 如果您使 [用Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，则对AEM Forms执行以下配置：

1. 为AEM Forms配置访问权限：

   打开调度程序。any文件进行编辑。 导航到筛选器部分，然后将以下筛选器添加到筛选器部分：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存并关闭文件。 有关过滤器的详细信息，请参阅 [Dispatcher文档](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 配置推荐人筛选器服务：

   以管理员身份登录到Apache Felix配置管理器。 配置管理器的默认URL为 `https://[server]:[port_number]/system/console/configMgr`。 在“配 **置** ”菜单中，选 **择“Apache Sling推荐人过滤器** ”选项。 在“允许主机”字段中，输入调度程序的主机名以允许它作为推荐人，然后单击“保 **存”**。 条目的格式为https://[server]:[port]。

#### 配置缓存 {#configure-cache}

缓存是一种缩短数据访问时间、减少延迟和提高输入／输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于缩短渲染自适应表单所需的时间。

* 在使用自适应表单缓存时，请 [使用AEMDispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) 来缓存自适应表单的客户端库（CSS和JavaScript）。
* 在开发自定义组件时，在用于开发的服务器上禁用自适应表单缓存。

请执行以下步骤以配置自适应表单缓存：

1. 转到位于https://&#39;[server]:[port]&#39;/system/console/configMgr的AEM Web控制台配置管理器。
1. 单击 **自适应表单和交互式通信Web渠道配置** ，以编辑其配置值。 在“编辑配置值”对话框中，在“自适应表单数”字段中指定AEM Forms服务器实例可以缓存的最 **大表单数或文档** 。 默认值为 100。单击&#x200B;**保存**。

   >[!NOTE]
   >
   >要禁用缓存，请将“自适应表单数”字段中的值设置 **为0**。 在禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

#### 为表单数据模型配置SSL通信 {#configure-ssl-communcation-for-form-data-model}

可以为表单数据模型启用SSL通信。 要为表单AEM Forms模型启用SSL通信，请在启动任何实例之前，向所有实例的Java信任存储添加证书。 您可以运行以下命令来添加证书： &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### 配置Adobe Sign {#configure-adobe-sign}

Adobe Sign支持自适应表单的电子签名工作流。 电子签名可改善处理法律、销售、工资、人力资源管理等文档的工作流。

在典型的Adobe Sign和自适应表单场景中，用户填写自适应表单 **以申请服务**。 例如，信用卡申请和公民福利表。 当用户填写、提交和签署应用程序表单时，该表单将发送给服务提供商以执行进一步操作。 服务提供商审阅应用程序，并使用Adobe Sign标记已批准的应用程序。 要启用类似的电子签名工作流，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms结合使 [用，请将Adobe Sign与AEM Forms结合使用](/help/forms/using/adobe-sign-integration-adaptive-forms.md)。

#### 配置AdobeAnalytics {#configure-adobe-analytics}

AEM Forms与AdobeAnalytics集成，使您能够捕获和跟踪已发布表单和文档的性能指标。 分析这些指标的目的是根据使表单或文档更可用所需的更改数据做出明智决策。

要将AdobeAnalytics与AEM Forms结合使用，请参 [阅配置分析和报告](/help/forms/using/configure-analytics-forms-documents.md)。

#### 集成Adobe Target {#integrate-adobe-target}

如果您的客户提供的体验不吸引人，他们可能会放弃表单。 虽然这令客户感到沮丧，但也可以增加组织的支持量和成本。 识别和提供正确的客户体验是至关重要的，也具有挑战性，可以增加转化率。 AEM表单是解决此问题的关键。

AEM表单与Adobe Target(一种Adobe Marketing Cloud解决方案)集成，跨多个数字渠道提供个性化、引人入胜的客户体验。 要使用Adobe Target测试自适应表单，请将 [Adobe Target与AEM Forms集成](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

## 后续步骤 {#next-steps}

您已配置环境以使用AEM Forms数据捕获功能。 现在，使用该功能的后续步骤是：

* [创建您的第一个自适应表单](/help/forms/using/create-your-first-adaptive-form.md)
* [创建您的第一个PDF表单](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5表单简介](/help/forms/using/introduction.md)

