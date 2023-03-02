---
title: 在JBoss® Linux®环境中安装AEM Forms JEE 6.5.15.0 Service Pack时出现问题
description: AEM Forms JEE 6.5.15.0 Service Pack未在JBoss® Linux®环境中正确安装，任何修补程序更改都不会应用到应用程序服务器。 将“RUP_BOM.xml”文件添加到XML目录。
source-git-commit: 76a3a87408ceb13023737379c20fb44ce5fb180a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---


# 在JBoss®环境中安装AEM Forms 6.5.15.0 JEE Service Pack时出现问题 {#aem-forms-installation-issue-environment}

## 带有 OS 剪贴板 {#issue}

JBoss® Linux®环境中未正确安装AEM Forms JEE 6.5.15.0 Service Pack。 In `PatchInstallerProcessing[1-9*].log` 记录日志条目， `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`，将会被记录。 此条目表示AEM Forms JEE 6.5.15.0 Service Pack的安装不成功。

## 应用到 {#applies-to}

此解决方案适用于：
* JBoss® Linux®环境

>[!NOTE]
>
> 在执行以下步骤之前，请确保至少在应用程序服务器上安装过一次AEM Forms JEE 6.5.15.0 Service Pack： [将RUP_BOM.xml文件添加到XML目录](#solution-solution).

## 解决方案 {#solution}

要修复安装问题，请添加AEM Forms JEE 6.5.15.0 Service Pack `RUP_BOM.xml` 文件到XML目录：
1. 导航到从中提取修补程序的文件夹 `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. 导航到 `/CDROM_Installers/Linux/Disk1/InstData` 位置并找到 `Resource1.zip` 文件。
1. 复制 `Resource1.zip` 解压缩解压缩文件夹外部某个不同位置的文件 `Resource1.zip` 文件。
1. 导航到 `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` 并复制 `RUP_BOM.xml` 文件。
1. 将RUP_BOM.xml文件粘贴到 `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. 重新安装 [AEM Forms JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).