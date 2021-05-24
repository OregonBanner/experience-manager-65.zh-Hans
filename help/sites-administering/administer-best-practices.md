---
title: 最佳实践
seo-title: 最佳实践
description: 查找由Adobe工程和咨询团队编译的最佳实践，以帮助管理员快速启动并运行。
seo-description: 查找由Adobe工程和咨询团队编译的最佳实践，以帮助管理员快速启动并运行。
uuid: 862d4fcf-ca61-4228-9344-b95a49b59b32
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f6468a0-7721-454f-9334-c449968b8fe7
exl-id: 576d87c8-cc96-45a0-b3cf-defb440babbb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 13%

---

# 最佳实践{#best-practices}

最佳实践介绍如何以最有效、最有效的方式开发、管理或使用AEM。 这些主题涵盖 AEM 中的多个区域，此外还将不断增加新的主题。

目前已经有针对以下区域的最佳实践文档：

* [资产](#assets)
* [站点](#sites)

有关创作、部署和维护或开发的最佳实践，请参阅以下内容之一：

* [创作最佳实践](/help/sites-authoring/best-practices.md)
* [开发最佳实践](/help/sites-developing/best-practices.md)
* [部署最佳实践](/help/sites-deploying/best-practices.md)

以下各表中介绍了具体的文档并提供了相应链接。

## 资产 {#assets}

以下主题介绍了有关资产(包括Dynamic Media功能和Dynamic Media Classic集成)的最佳实践：

<table>
 <tbody>
  <tr>
   <td>围绕Assets的不同领域的最佳实践，以增强负载下的系统稳定性和性能</td>
   <td><a href="/help/assets/best-practices-for-assets.md">用于资产的最佳实践</a></td>
   <td>包括指向资产不同区域最佳实践指南的链接。 在审核了这些信息后，您将拥有构建和管理企业资产管理系统的知识和工具。</td>
  </tr>
  <tr>
   <td>如何组织内容（文件夹层次结构）</td>
   <td><a href="/help/assets/organize-assets.md">文件管理最佳实践</a></td>
   <td>大多数处理配置文件都基于文件夹，因为视频、元数据和图像处理始终应用于文件夹。 此最佳实践文档介绍了如何定义和设置文件夹层次结构，因为该层次结构对内容的处理方式有重大影响。 </td>
  </tr>
  <tr>
   <td>集成Scene7和AEM</td>
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">将Scene7与AEM集成的最佳实践</a></td>
   <td><p>介绍何时打开轮询导入器、如何测试集成，以及何时使用内容浏览器，何时直接上传到资产。</p> </td>
  </tr>
  <tr>
   <td>图像预设选项</td>
   <td>了解<a href="/help/assets/managing-image-presets.md#understanding-image-presets">图像预设</a>和<a href="/help/assets/managing-image-presets.md#image-preset-options">图像预设最佳实践</a></td>
   <td>在<a href="/help/assets/managing-image-presets.md">管理图像预设</a>的文档中，以下主题介绍了图像预设的含义以及有关选择图像预设选项的最佳实践。</td>
  </tr>
  <tr>
   <td>Dynamic Media与Scene7的直接集成</td>
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Scene7/AEM集成与Dynamic Media</a></td>
   <td>描述何时最好使用Dynamic Media解决方案，何时将S7与AEM集成，或何时同时使用这两者。</td>
  </tr>
 </tbody>
</table>

## 站点 {#sites}

在管理和创作网站内容方面具有一些最佳实践，如下所述：

<table>
 <tbody>
  <tr>
   <td>GDPR合规</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR合规</a></td>
   <td>欧盟的《数据隐私权通用数据保护条例》已于2018年5月正式生效。 AEM Sites符合GDPR。 本页面将指导客户完成在AEM Sites中处理GDPR请求的过程。 它描述了存储的专用数据的位置，以及如何手动或使用代码删除这些数据。</td>
  </tr>
  <tr>
   <td>为实例定义默认UI。</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">为实例配置默认UI</a></p> </td>
   <td>AEM有两个UI:触控优化和经典。 本节详细介绍如何为实例定义默认UI。</td>
  </tr>
  <tr>
   <td>多站点管理</td>
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM最佳实践</a></td>
   <td>使用MSM自动部署内容的最佳实践。 </td>
  </tr>
  <tr>
   <td>翻译内容</td>
   <td><a href="/help/sites-administering/tc-bp.md">翻译最佳实践</a></td>
   <td>规划和实施多语言站点的最佳实践。</td>
  </tr>
  <tr>
   <td>用户管理</td>
   <td><a href="/help/sites-administering/security.md#best-practices">权限和权限最佳实践</a></td>
   <td>介绍使用权限和权限时的最佳实践 </td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">工作流最佳实践 — 配置</a></td>
   <td>工作流使您能够自动执行Adobe Experience Manager(AEM)活动，并且可以代表AEM环境中发生的大量处理，因此强烈建议仔细规划和配置工作流实施。</td>
  </tr>
 </tbody>
</table>
