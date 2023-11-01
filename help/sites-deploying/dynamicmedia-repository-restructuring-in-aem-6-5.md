---
title: Adobe Experience Manager 6.5中的Dynamic Media存储库重构
description: 了解如何在Experience Manager6.5中做出必要的更改，以迁移到新的Dynamic Media存储库结构。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 4%

---

# Adobe Experience Manager 6.5中的Dynamic Media存储库重构 {#dynamic-media-repository-restructuring-in-aem}

如父项中所述 [Adobe Experience Manager 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到Experience Manager6.5的客户应使用此页面评估与影响Dynamic Media的存储库更改相关的工作量。 在Experience Manager6.5升级过程中，有些更改需要您尽心尽力，而有些则可能会推迟到将来升级。

**在将来升级之前**

* [自定义自适应视频编码配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media (DMS7)云配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media（DM混合）Cloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTubeCloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [杂项](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 在将来升级之前 {#prior-to-upgrade}

### 自定义自适应视频编码配置  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>您可以运行以下迁移脚本以迁移到新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience ManagerUI中编辑配置，并将更改保存到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media (DMS7)云配置 {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>客户可以在以下位置运行迁移脚本：<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>重新启动Dynamic Media OSGi捆绑包。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### Dynamic Media（DM混合）Cloud Service配置 {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>您可以运行下面的迁移脚本以与最新模型保持一致：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - YouTubeCloud Service配置  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>1.从YouTube取消发布所有视频<br /> 2. 使用新的TouchUI创建YouTube配置(从 <code>/conf</code>)，包括从旧位置复制所有渠道<br /> 3. 将所有视频发布回YouTube。</p> <p>此工作流可生成新的YouTube URL。 如果您在创建TouchUI YouTube配置之前没有取消发布，则您将在属性下列出多个YouTube URL，因为如果有机会，重新创建的渠道会再次发布。 此功能意味着您的“属性”下列出了无用的URL。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 杂项 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>客户可以运行以下迁移脚本。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience ManagerUI中编辑配置，并将更改保存到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>客户可以运行以下迁移脚本。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>
