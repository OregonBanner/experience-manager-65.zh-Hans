---
title: AEM FormsJEE修补程序安装程序
description: 'null'
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: c1af919d4c0fd984249e1a7009274c63b8ce9adb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---


# AEM FormsJEE修补程序安装程序 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[有关详细信息](https://www.adobe.com/account/sign-in.supportportal.html) ，请与支持部门联系或获取修补程序。

## 关于修补程序安装程序 {#about-the-patch-installer}

AEM 6.5FormsJEE修补程序安装程序包含AEM 6.5FormsJEE所有组件在发布此修补程序之前可用的所有已修复问题。 有关已修复 [问题的完整列表](sp-release-notes.md) ，请参阅最新的Service Pack发行说明。

## 安装修补程序的先决条件 {#prerequisites-to-installing-the-patch}

* AEM 6.5Forms

## 安装和配置修补程序 {#installing-and-configuring-the-patch}

1. 备份&lt;AEM_*forms_root*>/deploy文件夹。 如果您决定卸载快速修复，则此操作是必需的。
1. 停止应用程序服务器。
1. 将修补程序安装程序存档文件解压到硬盘。
1. 在根据您所使用的操作系统命名的目录中：

   * **Windows**&#x200B;导航到硬盘上复制安装程序的安装介质或文件夹上的相应目录，然后多次单击aemforms65_cfp_install.exe文件。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**&#x200B;导航到相应的目录，然后从命令提示符中键入 
`./aem65_cfp_install.bin`。

      * (Linux) `Linux/Disk1/InstData/NoVM`

   这将启动一个安装向导，指导您完成安装。

1. 在“简介”面板上，单击“ **[!UICONTROL 下一步]**”。
1. 在“选择安装文件夹”屏幕上，验证显示的默认位置是否适用于您的现有安装，或单击“浏 **[!UICONTROL 览]** ”选择安装AEM表单的备用文件夹，然后单击“下 **[!UICONTROL 一步”]**。
1. 阅读“快速修复修补程序摘要”信息，然后单击“ **[!UICONTROL 下一步]**”。
1. 阅读“预安装摘要”信息，然后单击“ **[!UICONTROL 安装]**”。
1. 安装完成后，单击“下 **[!UICONTROL 一步]** ”，将快速修复更新应用到您已安装的文件。

1. 单击“完成”之前，请取消选择“开始配置管理器”选项。 在使用ConfigurationManager.exe或 **ConfigurationManager** _IPv.exe运行ConfigurationManager之前 **，请导航至************ &lt;AORMS_Install_>目录并将Axis.jar更新至\configurationManager\bin轴-1.4.1.1.1，在以下文件中：

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. 默认情况下，开始配置管理器复选框处于选中状态。 单击 **[!UICONTROL 完成]** ，以运行Configuration Manager。

1. 要稍后运行Configuration Manager，请在单击“完成”之前取消选择“开始配置管理器”选项。 您以后可以使用目录中的相应脚本开始Configuration `[AEM_forms_root]/configurationManager/bin` Manager。

1. 根据您的应用程序服务器，选择以下文档之一，然后按照配置和部署AEM表 *单部分中的说明* 。

   * [为JBoss安装和部署AEM表单](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安装和配置AEM forms for WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. （仅限JBoss）安装修补程序并配置服务器后，删除JBoss应用程序服务器的tmp和工作目录。

## 部署后配置 {#post-deployment-configurations}

### SAML配置 {#saml-configurations}

如果您已配置SAML身份验证，并且遇到大型IDP元数据的问题，请在安装修补程序后执行以下操作：

1. 在应用程序服务器中设置以下系统属性：\
   `um.saml.enable.large.xml=true`
1. 重新启动服务器。
1. 如SAML设置中所述，删除现有SAML身份验证提供者，然后再次为现有域添加它们。

## 受影响的模块 {#impacted-modules}

* 文档服务
* 文档安全
* Foundation JEE

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
