---
title: 禁用适用于JEE和OSGI的PDFG配置的UAC
description: 为PDFG配置禁用UAC的步骤
source-git-commit: f6dcb488c64dad2d65facc0e8e1d6685b7375a08
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# 无法在Windows Server上将Word或Excel文件转换为PDF {#unable-to-convert-word-excel-files-PDF}

## 带有 OS 剪贴板 {#issue}

当用户尝试在Microsoft Windows Server上将Word或Excel文件转换为PDF时，遇到以下错误：

*来自主转换器的错误消息：ALC-PDG-015-003-The系统无法打开输入文件。 请再次提交您的文件或与系统管理员联系。*


## 解决方案 {#solution}

执行以下步骤以解决问题：
1. 要访问系统配置实用程序，请转到 **[!UICONTROL 开始>运行]** 然后输入 **[!UICONTROL MSCONFIG]**.
1. 单击 **[!UICONTROL 工具]** 向下滚动并选择 **[!UICONTROL 更改UAC设置]**. 单击 **[!UICONTROL Launch]** 在新窗口中运行命令。
1. 将滑块调整到“从不通知”级别。 完成后，关闭命令窗口并关闭系统配置窗口。
1. 验证UAC的注册表设置是否设置为0（零）。 执行以下步骤以验证：

   1. Microsoft®建议在修改注册表之前先备份该注册表。 有关详细步骤，请参阅 [如何在Windows中备份和恢复注册表](https://support.microsoft.com/en-us/help/322756).
   1. 打开Microsoft® Windows Registry编辑器。 要打开注册表编辑器，请转到“开始”>“运行”，键入regedit，然后单击“确定”。
   1. 导航到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`。确保将EnableLUA的值设置为0（零）。
   1. 确保的值 **EnableLUA** 设置为0（零）。 如果值不为0，请将值更改为0。 关闭注册表编辑器。

1. 重新启动计算机。

## 适用于 {#appliesto}

此解决方案适用于以下情况：
* AEM Forms on JEE Server
* AEM Forms on OSGi Server