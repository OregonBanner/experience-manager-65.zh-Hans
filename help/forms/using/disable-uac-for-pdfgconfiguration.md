---
title: 禁用适用于JEE和OSGI的PDFG配置的UAC
description: 为PDFG配置禁用UAC的步骤
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# 无法在Windows Server上将Word或Excel文件转换为PDF {#unable-to-convert-word-excel-files-PDF}

## 带有 OS 剪贴板 {#issue}

当用户尝试在Microsoft Windows Server上将Word或Excel文件转换为PDF时，遇到以下错误：

*来自主转换器的错误消息： ALC-PDG-015-003 — 系统无法打开输入文件。 请再次提交文件或联系系统管理员。*


## 解决方案 {#solution}

执行以下步骤来解决问题：
1. 要访问系统配置实用程序，请转到 **[!UICONTROL “开始”>“运行”]** 然后输入 **[!UICONTROL MSCONFIG]**.
1. 单击 **[!UICONTROL 工具]** 制表符，向下滚动并选择 **[!UICONTROL 更改UAC设置]**. 单击 **[!UICONTROL Launch]** 在新窗口中运行命令。
1. 将滑块调整为从不通知级别。 完成后，关闭命令窗口并关闭“System Configuration（系统配置）”窗口。
1. 验证UAC的注册表设置是否设置为0（零）。 执行以下步骤进行验证：

   1. Microsoft®建议在修改注册表之前对其进行备份。 有关详细步骤，请参阅 [如何在Windows中备份和还原注册表](https://support.microsoft.com/en-us/help/322756).
   1. 打开Microsoft® Windows注册表编辑器。 要打开注册表编辑器，请转到“开始”>“运行”，键入regedit ，然后单击“确定”。
   1. 导航到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。确保EnableLUA的值设置为0 （零）。
   1. 确保值 **EnableLUA** 设置为0（零）。 如果值不为0，则将值更改为0。 关闭注册表编辑器。

1. 重新启动计算机。

## 应用于 {#appliesto}

此解决方案适用于以下内容：
* JEE服务器上的AEM Forms
* OSGi服务器上的AEM Forms
