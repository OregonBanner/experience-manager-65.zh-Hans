---
title: AEM 6.5中的Dynamic media存储库重组
seo-title: AEM 6.5中的Dynamic media存储库重组
description: 了解如何进行必要的更改以迁移到AEM 6.5 for Dynamic Media中的新存储库结构。
seo-description: 了解如何进行必要的更改以迁移到AEM 6.5 for Dynamic Media中的新存储库结构。
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5中的Dynamic media存储库重组 {#dynamic-media-repository-restructuring-in-aem}

如AEM 6.5页面中的父存储库重组中所述 [](/help/sites-deploying/repository-restructuring.md) ，升级到AEM 6.5的客户应使用此页面评估与影响Dynamic Media Solution的存储库更改相关的工作成果。 某些更改需要在AEM 6.5升级过程中进行工作，而其他更改可能会延迟到将来升级。

**在将来升级之前**

* [自定义自适应视频编码配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media(DMS7)云配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media(DM Hybrid)云服务配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - youTube云服务配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [Misc](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 在将来升级之前 {#prior-to-upgrade}

### 自定义自适应视频编码配置 {#custom-adaptive-video-encoding-configurations}

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
   <td><p>您可以运行以下迁移脚本以迁移到新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在AEM UI中编辑配置，更改将保存到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media (DMS7) Cloud configuration {#dynamic-media-dms-cloud-configuration}

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
   <td><p>客户可以在以下位置运行迁移脚本：<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>重新启动Dynamic Media OSGi捆绑。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### Dynamic Media(DM Hybrid)云服务配置 {#cloudserviceconfiguration}

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
   <td><p>您可以运行以下迁移脚本以与最新型号保持一致：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - youTube云服务配置 {#youtubecloudserviceconfiguration}

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
   <td><p>1.从YouTube<br /> 2取消发布所有视频。 使用新的TouchUI（从）创建YouTube配置， <code>/conf</code>包括从旧位置<br /> 3复制所有渠道。 将所有视频发布回YouTube。</p> <p>此工作流会生成新的YouTube URL。 如果在创建新的TouchUI YouTube配置之前未取消发布，则在“属性”下将列出多个YouTube URL，因为如果有机会，重新创建的频道将再次发布。 这意味着您的URL将列在“属性”下。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### Misc {#misc}

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
   <td><p>客户可以运行以下迁移脚本。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在AEM UI中编辑配置，更改将保存到新位置。</p> </td>
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

