---
title: AEM Forms AEM Forms补丁安装说明
description: AEM Forms Service Pack安装OSGi和JEE环境的说明
source-git-commit: b52e050ffbda8c38a5ba53d1c72218c21a64d0b9
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 7%

---


# AEM 6.5 Forms Service Pack安装说明 {#aem-form-patch-installation-instructions}

## 发行版信息

| 产品 | Adobe Experience Manager 6.5Forms |
|---|---|
| 版本 | 6.5.15.0 |
| 类型 | Service Pack版本 |
| 日期 | 2022 年 12 月 01 日 |

## Experience Manager Forms 6.5.15.0中包含的内容

Adobe Experience Manager(AEM)Forms service pack包含新增和升级的功能，例如客户请求的关键增强功能、性能、稳定性和安全性改进。 AEM Forms会定期发布Service Pack，以提供最新功能和改进。 根据您的堆栈，选择以下路径之一以在您的环境中下载并安装Service Pack:

* [在JEE环境上的AEM Forms上下载并安装Service Pack](#download-and-install-for-jee-service-pack)
* [在OSGi环境中的AEM Forms上下载并安装Service Pack](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe在每第6个Service Pack后发布一个完整安装程序。 JEE上的AEM 6.5 Forms Service Pack 12(6.5.12.0)是最后一个完整安装程序。 完整安装程序支持新平台，而常规Service Packack安装程序仅包含错误修复和常规改进。 如果您正在执行全新安装或计划，以在JEE环境中为AEM 6.5 Forms使用最新软件，则Adobe建议在2022年3月03日发布的JEEfull安装程序上使用AEM 6.5.12.0 Forms，而不是2019年4月08日发布的AEM 6.5 Forms安装程序。 使用完整安装程序后，安装最新的Service Pack。

## 在JEE环境上的AEM Forms上下载并安装Service Pack {#download-and-install-for-jee-service-pack}

![](assets/aem-forms-on-jee.png)


+++1. 备份现有环境：

1. 备份 [CRX存储库、数据库模式和GDS（全局文档存储）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. 备份&lt;*AEM_forms_root*>/deploy文件夹。 如果您决定卸载Service Pack，则需要此插件。

+++

+++2.下载所需的软件：


* AEM Forms on JEE 6.5.15.0 Service Pack
* AEM 6.5.15.0 服务包
* Forms 附加组件包
* 包
* 片段

+++

+++3. 在JEE Service Pack上安装AEM Forms:

1. 停止应用程序服务器。
1. 提取 **AEM Forms on JEE 6.5.15.0 Service Pack安装程序存档** 到硬盘：

   * **Windows**
导航到安装介质上的相应目录或硬盘上复制安装程序的文件夹，然后双击 
`aemforms65_cfp_install.exe` 文件。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
导航到相应的目录，并从外壳和类型导航到 
`./aem65_cfp_install.bin`。

      * (Linux) `Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 在 **选择安装文件夹** 屏幕，验证显示的默认位置对于您的现有安装是否正确，或单击 **[!UICONTROL 浏览]** 要选择安装AEM表单的替代文件夹，请单击 **[!UICONTROL 下一个]**.
1. 阅读“Sevice Pack（服务包）”摘要信息，然后单击 **[!UICONTROL 下一个]**.
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。
1. **[仅适用于Windows]:** 执行以下步骤之一：

   * 取消选择 **启动配置管理器** 选项 **[!UICONTROL 完成]**. 运行 **配置管理器** 使用 **ConfigurationManager.bat** 位于 `[aem-forms root]\configurationManager\bin`.

   * 或取消选择 **启动配置管理器** 选项 **[!UICONTROL 完成]**. 运行前 **配置管理器** 使用 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe**，导航到 *`<AEMForms_Install_Dir>\configurationManager\bin`* 目录和替换 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 和 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 文件。

      >[!NOTE]
      >
      > 使用 **ConfigurationManager.bat** 文件可帮助您避免手动更新.lax文件的名称。

1. **[仅适用于基于Unix的]:** 的 **启动配置管理器** 复选框。 单击 **[!UICONTROL 完成]** 立即运行配置管理器或运行 **配置管理器** 稍后，取消选择 **启动配置管理器** 选项 **[!UICONTROL 完成]**. 您可以开始 **配置管理器** 稍后在 `[AEM_forms_root]/configurationManager/bin` 目录访问Advertising Cloud的帮助。

1. 根据您的应用程序服务器，选择以下文档之一，然后按照 *配置和部署AEM表单* 中。

   * [安装和部署AEM forms for JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安装和部署AEM for WebSphere表单](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [安装和部署AEM Forms for WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)

+++

+++4. 安装Servlet片段

必须安装 **servlet片段** 对于除运行在JBoss EAP 7.4.0上的应用程序服务器以外的所有应用程序服务器。要下载并安装Servlet片段，请执行以下操作：

1. 如果尚未下载片段，请从下载 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

1. 启动应用程序服务器，等待日志稳定并检查包状态。

1. 打开Web控制台包。 默认URL为 `http://[Server]:[Port]/system/console/bundles`.

1. 单击“安装/更新”。 选择下载的片段org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar。 单击安装或更新。 等待应用程序服务器稳定

1. 停止应用程序服务器。

+++

+++5. 安装 AEM Service Pack

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 Adobe建议，如果实例的当前正常运行时间较高，则重新启动。
1. 在安装之前，请拍摄快照或对 [!DNL Experience Manager] 实例。
1. 从下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).
1. 选择包，然后选择 **[!UICONTROL 安装]**.
1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**自动安装**

可以使用两种不同的方法自动安装 [!DNL ExperienceManager] 6.5.15.0。<!--       UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹。
包会自动安装。

* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用     `cmd=install&recursive=true` 以便安装嵌套包。

   >[!NOTE]
   >
   >Experience Manager6.5.15.0不支持Bootstrap安装。 <!-- UPDATE FOR EACHNEW RELEASE -->

**验证安装**

要了解经认证可与此版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience      Manager (6.5.15.0)` 在 [!UICONTROL 已安装的产品].<!-- UPDATE FOR EACH NEW RELEASE -->
1. 所有OSGi包都 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** (使用Web控制台： `/system/console/bundles`)。
1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.13或更高版本(使用WebConsole: `/system/console/     bundles`)。

+++

+++6. 安装AEM Experience Manager Forms附加组件包

1. 确保您已安装 [!DNL Experience Manager] 服务包。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 按照 [安装AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. 如果您在Experience Manager6.5 Forms中使用字母，请安装 [最新的AEMFDCompatibility包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++


<!-- 1. (JBoss only) After installing the patch and configuring the server, delete  tmp  and work directories of JBoss application server.

>[!IMPORTANT]
>
>Before installing [AEM 6.5.15.0 service pack](#install-the-aem-service-pack-install-aem-service-pack), for all the AEM Forms on JEE environments using any application servers other than JBoss EAP 7.4.0: 
> * Install  the [org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) servlet fragment and wait for the application server to stabilize.
>* If you install the latest [AEM service pack (6.5.15.0)](#install-the-aem-service-pack-install-aem-service-pack), prior to the fragment servlet `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` on JEE environment, the CRX/bundle and the start page show service unavailable errors, [click here](/help/forms/using/aem-service-pack-installation-solution.md) to know the troubleshooting steps. 

### !-->


## 在OSGi环境中的AEM Forms上下载并安装Service Pack {#download-and-install-for-osgi-service-pack}

![](assets/aem-forms-on-osgi.png)


+++1. 备份现有环境：

1. 备份 [CRX存储库和数据库架构](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
> 如果为关系数据库安装AEM Forms Service Pack，则必须备份DB_schema。

+++

+++2.下载所需的软件：

* [AEM 6.5.15.0 服务包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)
* [Forms 附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)

+++

+++3. 安装 AEM Service Pack

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 Adobe建议，如果实例的当前正常运行时间较高，则重新启动。
1. 在安装之前，请拍摄快照或对 [!DNL Experience Manager] 实例。
1. 从下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).
1. 选择包，然后选择 **[!UICONTROL 安装]**.
1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**自动安装**

可以使用两种不同的方法自动安装 [!DNL Experience Manager] 6.5.15.0。<!--       UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹。 包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用     `cmd=install&recursive=true` 以便安装嵌套包。

   >[!NOTE]
   >
   >Experience Manager6.5.15.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与此版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience      Manager (6.5.15.0)` 在 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi包都 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

   1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.13或更高版本(使用Web控制台： `/system/console/bundles`)。

+++

+++4. 安装AEM Experience Manager Forms附加组件包

1. 确保您已安装 [!DNL Experience Manager] 服务包。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 按照 [安装AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package-install-aem-forms-add-on-package).
1. 如果您在Experience Manager6.5 Forms中使用字母，请安装 [最新的AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## 疑难解答

* 如果 **包管理器UI中的对话框** 在安装Service Pack期间退出，等待错误日志稳定后再访问部署。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常，此问题会在Safari浏览器中发生，但可能会间歇性地在任何浏览器上发生。

* 安装完成后，检查任何活动的监视器日志(error.log)。 等待几分钟，直到日志中没有活动。 重新启动AEM实例。

* 如果您遇到 **服务不可用错误** 安装最新的AEM Forms 6.5.15.0 service pack后， [单击此处](/help/forms/using/aem-service-pack-installation-solution.md) 以查看疑难解答步骤。
