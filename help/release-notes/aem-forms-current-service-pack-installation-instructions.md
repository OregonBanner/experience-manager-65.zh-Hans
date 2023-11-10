---
title: 适用于AEM Forms的AEM Forms修补程序安装说明
description: 适用于OSGi和JEE环境的AEM Forms Service Pack安装说明
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 41ef1b05e4082bb50b93ff6511542ed56a77497c
workflow-type: tm+mt
source-wordcount: '1771'
ht-degree: 9%

---

# AEM 6.5 Forms Service Pack安装说明 {#aem-form-patch-installation-instructions}

## 发行版信息

| 产品 | Adobe Experience Manager 6.5 Forms |
|---|---|
| 版本 | 6.5.18.0 |
| 类型 | Service Pack版本 |
| 日期 | 2023 年 31 月 8 日 |
| 下载 URL | [最新AEM Forms版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>查看最新信息 [AEM Service Pack发行说明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html) 以获取已修复问题的完整列表。

## Experience Manager Forms 6.5中包含的内容

Adobe Experience Manager (AEM) Forms service pack包含新增和升级的功能，例如客户请求的关键增强功能、性能、稳定性和安全性改进。 AEM Forms会定期发布Service Pack，以提供最新功能和改进功能。 根据您的栈栈，选择以下路径之一下载并在您的环境中安装Service Pack：

* [在JEE环境的AEM表单上下载并安装Service Pack](#download-and-install-for-jee-service-pack)
* [在OSGi环境上的AEM表单上下载并安装Service Pack](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe每六个Service Pack发布一个完整安装程序。 AEM 6.5 Forms Service Pack 18 (6.5.18.0)是最新的JEE完整安装程序。 完整安装程序支持新平台，而常规Service Pack安装程序包括新增功能、错误修复和常规改进。 如果您要在JEE环境中执行全新安装或计划使用最新软件来安装AEM 6.5 Forms on JEE，Adobe建议使用于2023年8月31日发布的AEM 6.5.18.0 Forms on JEE完整安装程序，而不是于2019年4月8日发布的AEM 6.5 Forms安装程序或于2022年3月3日发布的AEM 6.5.12 Forms安装程序。 使用完整安装程序后，安装最新的Service Pack。
> 
> * 中提供的AEM Forms功能，例如自适应Forms [AEM 6.5快速入门](https://experienceleague.corp.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)仅供探索及评估之用。 对于生产使用，获得AEM Forms的有效许可证至关重要。




## 在JEE环境的AEM表单上下载并安装Service Pack {#download-and-install-for-jee-service-pack}

![JEE安装](/help/forms/using/assets/jeeinstallation.png)

+++1. 备份现有环境：

1. 备份 [CRX存储库、数据库模式和GDS（全局文档存储）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. 备份&lt;*AEM_forms_root*>/部署文件夹。

>[!NOTE]
>
> 在运行AEM Service Pack安装程序之前，请确保您对AEM安装目录具有写访问权限。

+++

+++2.下载所需软件：

* [AEM Forms on JEE Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [片段Servlet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. 在JEE Service Pack上安装AEM Forms：

1. 停止应用程序服务器。
1. 提取 **AEM Forms on JEE Service Pack安装程序存档** 到您的硬盘：

   * **Windows**
导航到安装介质上的相应目录，或硬盘上您在其中复制了安装程序的文件夹，然后双击 `aemforms65_cfp_install.exe` 文件。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
导航到相应的目录，然后从shell和键入 `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 在 **选择安装文件夹** 屏幕，验证显示的默认位置对于您的现有安装是否正确，或者单击 **[!UICONTROL 浏览]** 选择安装AEM表单的备用文件夹，然后单击 **[!UICONTROL 下一个]**.
1. 阅读Service Pack摘要信息，然后单击 **[!UICONTROL 下一个]**.
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。
1. **[仅适用于Windows]：** 执行以下步骤之一：

   * 取消选择 **启动Configuration Manager** 选项，然后再单击 **[!UICONTROL 完成]**. 运行 **配置管理器** 通过使用 **ConfigurationManager.bat** 文件位置 `[aem-forms root]\configurationManager\bin`.

   * 或者取消选择 **启动Configuration Manager** 选项，然后再单击 **[!UICONTROL 完成]**. 运行之前 **配置管理器** 使用 **Configurationmanager.exe** 或 **ConfigurationManager_IPv6.exe**，导航到 *`<AEMForms_Install_Dir>\configurationManager\bin`* 目录和替换 [配置管理器.lax](/help/assets/ConfigurationManager.lax) 和 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 文件。

     >[!NOTE]
     >
     >* 更新或替换 **ConfigurationManager.bat** 文件可帮助您避免手动更新.lax文件。

1. **[仅适用于基于Unix的]：** 此 **启动Configuration Manager** 复选框默认处于选中状态。 单击 **[!UICONTROL 完成]** 立即运行配置管理器或运行 **配置管理器** 稍后，取消选择 **启动Configuration Manager** 选项，然后再单击 **[!UICONTROL 完成]**. 您可以开始 **配置管理器** 稍后使用中的相应脚本 `[AEM_forms_root]/configurationManager/bin` 目录。

1. 根据您的应用程序服务器，选择以下文档之一，然后按照 *配置和部署AEM表单* 部分。

   * [安装和部署AEM forms for JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安装和部署AEM forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [安装和部署AEM Forms for WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [安装和部署AEM forms for JBoss®聚类](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [安装和部署AEM forms for WebSphere®群集](https://helpx.adobe.com/content/dam/help/cn/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [安装和部署AEM Forms for WebLogic群集](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> 在JEE Service Pack上安装AEM Forms后，您需要从删除Forms附加组件包 `crx-repository\install` 文件夹，然后再重新启动appserver。 从下载最新的Forms附加组件包 [软件分发门户](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

+++4. 安装servlet片段(AEM Service Pack 6.5.14.0或更低版本)

>[!NOTE]
>
> * 如果您要从 **AEM Service Pack 6.5.15.0**，安装 **servlet片段** 非必填。 对于版本 **AEM Service Pack 6.5.14.0** 或更早版本，必须安装servlet片段。
> * 必须安装 **servlet片段** 用于所有应用程序服务器，运行在 **JBoss® EAP 7.4.0**.


要下载并安装servlet片段，请执行以下操作：

1. 如果您尚未下载片段，请从下载 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. 启动应用程序服务器，等待日志稳定并检查捆绑包状态。

1. 打开Web控制台包。 默认URL为 `http://[Server]:[Port]/system/console/bundles`.

1. 单击安装/更新。 选择下载的片段， `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. 单击 **安装** 或 **更新**. 等待应用程序服务器稳定

1. 停止应用程序服务器。

+++

+++5. 安装 AEM Service Pack

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，则Adobe建议重新启动。
1. 安装之前，请拍摄快照或进行全新备份 [!DNL Experience Manager] 实例。
1. 从以下位置下载Service Pack [Software Distribution](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 以上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).
1. 选择包，然后选择 **[!UICONTROL 安装]**.

**自动安装**

可以使用两种不同的方法来自动安装 [!DNL ExperienceManager] service pack。<!--       UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹（当服务器联机时）。
软件包会自动安装。

* 使用 [包管理器中的HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). 使用  `cmd=install&recursive=true` 以便安装嵌套包。

  >[!NOTE]
  >
  Experience ManagerService Pack不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

  **验证安装**

  要了解经认证可与本版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

   1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (spversion)` 下 [!UICONTROL 已安装的产品].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. 所有OSGi捆绑包包 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台(使用Web控制台： `/system/console/bundles`)。
   1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.14或更高版本(使用WebConsole： `/system/console/     bundles`)。

+++

+++6. 安装AEM Experience Manager Forms附加组件包

1. 确保您已安装 [!DNL Experience Manager] service pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 安装Forms附加组件包，如中所述 [安装AEM Forms附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 如果您在Experience Manager6.5 Forms中使用字母，请安装 [最新的AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## 在OSGi环境上的AEM表单上下载并安装Service Pack {#download-and-install-for-osgi-service-pack}

![OSGi安装步骤](/help/forms/using/assets/osgiinstallation.png)


+++1. 备份现有环境：

1. 备份 [CRX存储库和数据库架构](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
如果安装关系数据库的AEM Forms Service Pack，则必须备份DB_schema。

+++

+++2.下载所需软件：

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++3. 安装 AEM Service Pack

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，则Adobe建议重新启动。
1. 安装之前，请拍摄快照或进行全新备份 [!DNL Experience Manager] 实例。
1. 从以下位置下载Service Pack [Software Distribution](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 以上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).
1. 选择包，然后选择 **[!UICONTROL 安装]**.

**自动安装**

可以使用两种不同的方法来自动安装 [!DNL Experience Manager] service pack。<!--  UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹（当服务器联机时）。 软件包会自动安装。
* 使用 [包管理器中的HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

  >[!NOTE]
  >
  Experience ManagerService Pack不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

  **验证安装**

  要了解经认证可与本版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

   1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (spversion)` 下 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. 所有OSGi捆绑包包 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

      1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.14或更高版本(使用Web控制台： `/system/console/bundles`)。

+++

+++4. 安装AEM Experience Manager Forms附加组件包

1. 确保您已安装 [!DNL Experience Manager] service pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 安装Forms附加组件包，如中所述 [安装AEM Forms附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 如果您在Experience Manager6.5 Forms中使用字母，请安装 [最新的AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## 疑难解答

* 如果 **包管理器UI上的对话框** 会在安装Service Pack期间退出，等待错误日志稳定下来后再访问部署。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题发生在Safari浏览器中，但可能会间歇性地发生在任何浏览器中。

* 安装完成后，检查监视器日志(error.log)中是否有任何活动。 等待几分钟，直到日志中没有活动。 重新启动AEM实例。

* 万一你得到 **服务不可用错误** 安装AEM Forms 6.5.15.0或更高版本的Service Pack后， [安装servlet片段和捆绑包](/help/forms/using/aem-service-pack-installation-solution.md) 以修复错误。
