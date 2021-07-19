---
title: Dynamic Media 6.5中的Adobe Experience Manager存储库重组
description: 了解如何进行必要的更改，以便迁移到适用于Dynamic Media的Experience Manager6.5中的新存储库结构。
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
feature: 升级
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 4%

---

# Dynamic Media 6.5中的Adobe Experience Manager存储库重组 {#dynamic-media-repository-restructuring-in-aem}

如父级[Adobe Experience Manager 6.5](/help/sites-deploying/repository-restructuring.md)中的存储库重组页面中所述，升级到Experience Manager6.5的客户应使用此页面评估与影响Dynamic Media的存储库更改相关的工作量。 某些更改在Experience Manager6.5升级过程中需要工作，而其他更改可能会推迟到将来的升级。

**未来升级前**

* [自定义自适应视频编码配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media(DMS7)云配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media（DM混合）Cloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTubeCloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [杂项](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 未来升级前 {#prior-to-upgrade}

### 自定义自适应视频编码配置  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>您可以运行以下迁移脚本以迁移到新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience ManagerUI中编辑配置，并将更改保存到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media(DMS7)云配置 {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>客户可以在此位置运行迁移脚本：<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>重新启动Dynamic Media OSGi包。</li>
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
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>您可以运行以下迁移脚本，以便与最新模型保持一致：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media -YouTubeCloud Service配置  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>1.取消发布YouTube<br /> 2中的所有视频。 使用新的TouchUI（从<code>/conf</code>）创建YouTube配置，包括从旧位置<br /> 3复制所有通道。 将所有视频发布回YouTube。</p> <p>此工作流会生成新的YouTube URL。 如果在创建触屏UI YouTube配置之前未取消发布，则在“属性”下方会列出多个YouTube URL，因为如果有机会，重新创建的渠道会再次发布。 此功能意味着您在“属性”下列出了无用的URL。</p> </td>
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
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
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
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>客户可以运行以下迁移脚本。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>
