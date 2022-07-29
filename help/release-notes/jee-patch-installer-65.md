---
title: AEM Forms JEE补丁安装程序
description: AEM Forms JEE补丁安装程序
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: d28d78e426f1e89caa8bd28b067765d40b95cb8a
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 29%

---

# AEM Forms JEE补丁安装程序 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[联系支持人员](https://www.adobe.com/cn/account/sign-in.supportportal.html) 以获取更多信息或获取修补程序。

## 关于修补程序安装程序 {#about-the-patch-installer}

AEM 6.5 Forms JEE修补程序安装程序包含AEM 6.5 Forms JEE的所有组件在发布此修补程序之前的所有已修复问题。 查看最新  [Service Pack发行说明](release-notes.md) 以获取已修复问题的完整列表。

## 安装修补程序的先决条件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## 安装和配置修补程序 {#installing-and-configuring-the-patch}

1. 备份&lt;*AEM_forms_root*>/deploy文件夹。 如果您决定卸载快速修补程序，则必须执行此操作。
1. 停止应用程序服务器。
1. 将补丁安装程序存档文件提取到硬盘驱动器。
1. 在根据您所使用的操作系统命名的目录中：

   * **Windows**
导航到安装介质上的相应目录或硬盘上复制安装程序的文件夹，然后双击aemforms65_cfp_install.exe文件。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
导航到相应的目录，然后从命令提示符下键入 
`./aem65_cfp_install.bin`。

      * (Linux) `Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 在“Choose Install Folder（选择安装文件夹）”屏幕上，验证显示的默认位置对于您的现有安装是否正确，或单击 **[!UICONTROL 浏览]** 要选择安装AEM表单的替代文件夹，请单击 **[!UICONTROL 下一个]**.
1. 阅读“Quick Fix Patch Summary”信息，然后单击 **[!UICONTROL Next]**。
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。

1. 在单击“完成”之前，请取消选择“开始配置管理器”选项。 在使用 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe**，导航到 *&lt;aemforms_install_dir>\configurationManager\bin* 目录和更新 `ConfigurationManager.lax` 和 `ConfigurationManager_IPv6.lax` 具有以下重命名操作的文件：

   * `axis.jar` 到 `axis-1.4.1.1.jar`
   * `serializer-2.7.1.jar` 到 `serializer-2.7.2.jar`
   * `xalan-2.7.1.jar` 到 `xalan-2.7.2.jar`
   * `xercesImpl-2.9.1.jar` 到 `xercesImpl-2.12.0.jar`
   * `xml-apis-2.7.1.jar` 到 `xml-apis-2.7.2.jar`

1. 默认情况下，“开始配置管理器”(Start Configuration Manager)复选框处于选中状态。 单击 **[!UICONTROL Done]** 以运行配置管理器。

1. 要稍后运行配置管理器，请先取消选择 Start Configuration Manager 选项，然后再单击 Done。您稍后可以使用 `[AEM_forms_root]/configurationManager/bin` 目录访问Advertising Cloud的帮助。

1. 根据您的应用程序服务器，选择以下文档之一，然后按照 *配置和部署AEM表单* 中。

   * [安装和部署AEM forms for JBoss](http://www.adobe.com/go/learn_aemforms_installJBoss_65_cn)
   * [安装和部署AEM for WebSphere表单](http://www.adobe.com/go/learn_aemforms_installWebSphere_65_cn)

1. （仅限JBoss）安装修补程序并配置服务器后，删除JBoss应用程序服务器的tmp和工作目录。

>**注意：** 启动之前 **配置管理器**、下载和替换 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 文件。

## 部署后配置 {#post-deployment-configurations}

### SAML配置 {#saml-configurations}

如果您配置了SAML身份验证，并且遇到了大型IDP元数据的问题，请在安装修补程序后执行以下操作：

1. 在应用程序服务器中设置以下系统属性：\
   `um.saml.enable.large.xml=true`
1. 重新启动服务器。
1. 按照SAML设置中的所述，删除现有SAML身份验证提供程序，并再次为现有域添加它们。

## 受影响的模块 {#impacted-modules}

* 文档服务
* 文档安全
* Foundation JEE

[联系支持人员](https://www.adobe.com/account/sign-in.supportportal.html)
