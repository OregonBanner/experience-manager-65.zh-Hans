---
title: 适用于AEM Form Service Pack的修补程序
description: 提供了有关如何下载和安装AEM Forms Service Pack修补程序的信息
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Adobe Experience Manager修补程序{#aem-form-hotfix}

安装最新版本 [AEM Service Pack](/help/release-notes/release-notes.md) 推荐的版本包括安全性、性能、稳定性，以及自Adobe Experience Manager 6.5正式发布以来发布的关键客户修复和增强功能。

## 自适应Forms的修补程序 {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日期</strong></td>
    <td><strong>修补程序名称</strong></td>
    <td><strong>修复</strong></td>
   </tr>
   <tr>
    <td>2023 年 11 月 20 日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">适用于Linux的AEM Service Pack 6.5.18.0的修补程序</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">适用于Windows的AEM Service Pack 6.5.18.0的修补程序</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">适用于Mac操作系统的AEM Service Pack 6.5.18.0的修补程序</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在自适应表单的指南容器中设置重定向URL后，内联签名将停止工作。 (FORMS-10493)</li>
    <li>无法为本地化的自适应Forms发布记录文档(DoR)模板。 (FORMS-10535)</li>
    <li>在编辑模式下无法打开包含大型内嵌图像的交互式通信。 (FORMS-10578)</li>
    </ul>
    </td>    
    </tr>
    <tbody>
     </table>

## 下载和安装修补程序 {#download-install-hotfix}

执行以下步骤以下载并安装修补程序：

1. 下载 [修补程序](#hotfix-for-adaptive-forms) 从SD链接。
1. 解压缩修补程序存档文件，以便获取Experience Manager包(.zip)和捆绑包(.jar)文件。
1. 通过包管理器上传并安装包(.zip)。
1. 打开配置管理器包 `https://server:host/system/console/bundles`，上传并安装捆绑包(.jar)。
