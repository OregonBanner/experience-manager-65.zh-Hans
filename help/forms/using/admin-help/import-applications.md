---
title: 导入和管理应用程序
seo-title: Import and manage applications
description: 了解如何导入和管理应用程序。
seo-description: Learn how to import and manage applications.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 导入和管理应用程序{#import-and-manage-applications}

在AEM Forms中， *应用程序* 是一个容器，用于存储实施AEM forms解决方案所需的资源。 例如，表单设计、表单片段、图像、进程、DDX文件、表单指南、HTML页和SWF文件。 在项目的开发阶段，Workbench用户可以直接从Workbench的“应用程序”视图中部署应用程序。 部署后，这些应用程序将显示在管理控制台的“应用程序管理”页面上的“应用程序”选项卡中。

当应用程序完成并准备好部署到生产服务器时，Workbench用户将该应用程序打包到 *AEM forms应用程序文件* (.lca)。 然后，管理员使用“应用程序管理”页上的“应用程序”选项卡，使用管理控制台导入和部署应用程序文件。

您还可以使用“应用程序管理”页上的“存档”选项卡，导入使用Workbench 8.x创建的LCA。

>[!NOTE]
>
>存在一个已知问题，即未来版本的LCA文件不一定向后兼容。 虽然可以从未来版本的AEM Forms（例如，预览版本）查看和导入LCA文件，但这样做不受支持，并且可能会导致异常行为。

使用“应用程序”标签导入和管理在Workbench中创建的应用程序。 应用程序管理员还可以导出应用程序的运行时配置。 导出运行时配置无需在启动已部署的应用程序之前在生产环境中手动重新配置设置。 运行时配置文件包含：

* 服务配置设置
* 池配置设置
* 端点配置设置
* 安全性配置文件

## 导入应用程序或存档 {#import-an-application-or-archive}

1. 在管理控制台中，单击服务>应用程序和服务>应用程序管理。
1. 单击导入。
1. 单击“浏览”并选择要导入的.lca文件，然后单击“预览”。 “预览应用程序”页显示有关应用程序的信息。
1. （可选）要查看应用程序中包含的资产列表，请单击查看资产。
1. （可选）要将资源部署到运行时，请选择在导入完成后将资源部署到运行时。 如果不选择此选项，您可以稍后部署资产。
1. 单击导入。该应用程序将显示在“应用程序”选项卡上。
1. 使用管理员凭据登录CRX存储库。
1. 导航到content/dam/lcapplications

   >[!NOTE]
   >
   >导入的应用程序显示在lcpapplications节点中。

1. 单击其中一个导入的应用程序。

   右侧的属性选项卡显示选定CRX节点的属性。

   此 **syncState** 属性指示AEM Forms服务器和CRX存储库之间数据同步的状态。 导入过程一旦开始，此状态即设置为0（零）。 此状态表示数据当前未同步。 当数据同步时，状态将设置为1。

## 部署应用程序 {#deploy-an-application}

您可以部署已导入的应用程序，也可以部署从Workbench导入的Workbench用户。

1. 在管理控制台中，单击服务>应用程序和服务>应用程序管理。
1. 选中要部署的应用程序旁边的复选框，然后单击部署。
1. 在出现的确认对话框中单击“确定”。

## 取消部署应用程序 {#undeploy-an-application}

您可以从运行时取消部署应用程序。

1. 在管理控制台中，单击服务>应用程序和服务>应用程序管理。
1. 选中要取消部署的应用程序旁边的复选框，然后单击取消部署。
1. 在出现的确认对话框中单击“确定”。

## 从服务器中删除应用程序 {#remove-an-application-from-the-server}

先取消部署应用程序，然后再将其从服务器中删除。

1. 在管理控制台中，单击服务>应用程序和服务>应用程序管理。
1. 选中要删除的应用程序旁边的复选框，然后单击删除。
1. 在出现的确认对话框中单击“确定”。

## 导入应用程序的运行时配置 {#import-an-application-s-runtime-configuration}

如果应用程序管理员为应用程序导出运行时配置，则可以将其导入已部署的应用程序。 您可以使用管理控制台或通过脚本式LCA部署导入它。

1. 在管理控制台中，单击服务>应用程序和服务>应用程序管理。
1. 单击应用程序的名称。
1. 单击“导入运行时配置”。
1. 单击“浏览”并选择包含运行时配置的XML文件。
1. 单击导入。

## 导出应用程序的运行时配置 {#export-an-application-s-runtime-configuration}

您可以导出已部署应用程序的运行时配置信息。

1. 在管理控制台中，单击服务>应用程序和服务>应用程序管理。
1. 单击应用程序的名称。
1. 单击“导出运行时配置”并保存生成的配置文件(XML)。

## AEM表单应用程序的脚本部署 {#scripted-deployment-of-aem-forms-applications}

您还可以使用脚本部署工具来部署应用程序文件，包括指定以下设置的settings.xml文件：

* 服务配置设置
* 池配置设置
* 端点配置设置
* 安全性配置文件

通过脚本部署，无需在启动已部署的应用程序之前手动重新配置生产环境中的设置。

1. 在命令提示符下，导航到 *[aem-forms根]*/sdk/misc/Foundation/ArchiveManagement。
1. 有关更多详细说明，请查看ReadMe.txt文件。
1. 按照readme.txt文件中的说明，手动修改scriptedDeploy.bat和sample-files/sample.xml文件。
1. 运行scriptedDeploy.bat文件。 此操作使用覆盖设置部署AEM表单存档文件。
