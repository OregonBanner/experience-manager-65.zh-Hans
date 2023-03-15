---
title: 最佳实践
seo-title: Best Practices
description: 查找由Adobe工程和咨询团队编译的最佳实践，帮助管理员启动并运行。
seo-description: Find best practices compiled by Adobe engineering and consulting teams to help administrators get up and running.
uuid: 862d4fcf-ca61-4228-9344-b95a49b59b32
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f6468a0-7721-454f-9334-c449968b8fe7
exl-id: 576d87c8-cc96-45a0-b3cf-defb440babbb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 18%

---

# 最佳实践{#best-practices}

最佳实践描述如何以尽可能高效和最有效的方式开发、管理或使用AEM。 这些主题涵盖 AEM 中的多个区域，此外还将不断增加新的主题。

目前已经有针对以下区域的最佳实践文档：

* [Assets](#assets)
* [Sites](#sites)

有关创作、部署和维护或开发的最佳实践，请参阅以下内容之一：

* [创作最佳实践](/help/sites-authoring/best-practices.md)
* [开发最佳实践](/help/sites-developing/best-practices.md)
* [部署最佳实践](/help/sites-deploying/best-practices.md)

以下各表中介绍了具体的文档并提供了相应链接。

## Assets {#assets}

以下主题介绍了有关资产的最佳实践，包括Dynamic Media功能和Dynamic Media Classic集成：

<table>
 <tbody>
  <tr>
   <td>Assets周围不同区域的最佳实践，用于增强系统在负载下的稳定性和性能</td>
   <td><a href="/help/assets/best-practices-for-assets.md">用于资产的最佳实践</a></td>
   <td>包含指向Assets各个不同领域的最佳实践指南的链接。 查看这些模板后，您将拥有构建和管理企业资产管理系统的知识和工具。</td>
  </tr>
  <tr>
   <td>如何组织内容（文件夹层次结构）</td>
   <td><a href="/help/assets/organize-assets.md">文件管理最佳实践</a></td>
   <td>许多处理配置文件是基于文件夹的，因为视频、元数据、图像处理始终应用于文件夹。 此最佳实践文档介绍了如何定义和设置文件夹层次结构，因为层次结构对如何处理内容有显着影响。 </td>
  </tr>
  <tr>
   <td>Scene7与AEM集成</td>
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">将Scene7与AEM集成的最佳实践</a></td>
   <td><p>描述何时启用轮询导入程序、如何测试您的集成，以及何时使用内容浏览器而不是直接上传到Assets。</p> </td>
  </tr>
  <tr>
   <td>图像预设选项</td>
   <td>了解 <a href="/help/assets/managing-image-presets.md#understanding-image-presets">图像预设</a> 和 <a href="/help/assets/managing-image-presets.md#image-preset-options">图像预设最佳实践</a></td>
   <td>作为的文档的一部分， <a href="/help/assets/managing-image-presets.md">管理图像预设</a>，以下主题介绍了什么是图像预设以及有关选择图像预设选项的最佳实践。</td>
  </tr>
  <tr>
   <td>Dynamic Media与Scene7的直接集成</td>
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Scene7/AEM集成与Dynamic Media</a></td>
   <td>描述何时最好使用Dynamic Media解决方案、何时将S7与AEM集成或者何时同时使用这两个解决方案。</td>
  </tr>
 </tbody>
</table>

## Sites {#sites}

在管理和创作网站内容方面具有一些最佳实践，如下所述：

<table>
 <tbody>
  <tr>
   <td>GDPR合规性</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR合规性</a></td>
   <td>欧盟有关数据隐私权的《通用数据保护条例》自2018年5月起生效。 AEM Sites符合GDPR。 本页将指导客户完成在AEM Sites中处理GDPR请求的过程。 它描述了私有数据的存储位置，以及如何手动或使用代码删除私有数据。</td>
  </tr>
  <tr>
   <td>为您的实例定义默认UI。</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">为实例配置默认UI</a></p> </td>
   <td>AEM具有两个UI：触屏优化和经典。 本节详细介绍如何为实例定义默认UI。</td>
  </tr>
  <tr>
   <td>多站点管理</td>
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM 最佳实践</a></td>
   <td>使用MSM自动化内容部署的最佳实践。 </td>
  </tr>
  <tr>
   <td>翻译内容</td>
   <td><a href="/help/sites-administering/tc-bp.md">翻译最佳实践</a></td>
   <td>规划和实施多语言站点的最佳实践。</td>
  </tr>
  <tr>
   <td>用户管理</td>
   <td><a href="/help/sites-administering/security.md#best-practices">权限和权限最佳实践</a></td>
   <td>描述使用权限和权限时的最佳实践 </td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">工作流最佳实践 — 配置</a></td>
   <td>通过工作流，您可以自动化Adobe Experience Manager (AEM)活动，并且可以表示在AEM环境中发生的大量处理，因此强烈建议仔细规划和配置工作流实施。</td>
  </tr>
 </tbody>
</table>
