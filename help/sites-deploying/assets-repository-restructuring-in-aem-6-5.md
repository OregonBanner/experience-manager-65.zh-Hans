---
title: AEM 6.5中的资产存储库重组
seo-title: Assets Repository Restructuring in AEM 6.5
description: 了解如何进行必要的更改，以便迁移到AEM 6.5 for Assets中的新存储库结构。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 2%

---

# AEM 6.5中的资产存储库重组 {#assets-repository-restructuring-in-aem}

如父项中所述 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到AEM 6.5的客户应使用此页面来评估与影响AEM Assets解决方案的存储库更改相关的工作量。 某些更改需要在AEM 6.5升级过程中完成工作，而其他更改可能会推迟到将来进行升级。

**升级6.5版**

* [杂项](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**在将来升级之前**

* [资产/收集事件电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [经典资产共享设计](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [下载资产电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [DRM许可证示例](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [链接共享电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign工作流脚本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [视频转码配置](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [杂项](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 升级6.5版 {#with-upgrade}

### 杂项 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>如果有任何自定义代码依赖于此位置(即 代码明确依赖于此路径)，则必须更新代码以在升级前使用新位置；理想情况下，使用Java API来减少对JCR中任何特定路径的依赖关系。</p> <p>存放zip文件以供客户端下载的临时位置。 自从客户端请求下载资产后，便无需进行更新。 它将在新位置生成文件。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

## 在将来升级之前 {#prior-to-upgrade}

### 资产/收集事件电子邮件通知模板 {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>如果客户修改了电子邮件模板，请执行以下操作以便与新存储库结构保持一致：</p>
    <ol>
     <li>的 <code>/libs/settings/dam/notification</code> 电子邮件模板应从 <strong><code>/etc/notification/email/default</code></strong> to <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>因为目标位于<strong> <code>/apps</code></strong> 应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹： <strong><code>/etc/dam/notification/email/default</code></strong> 电子邮件模板之后。<br />
      <ol>
       <li>如果未对<strong> <code>/etc/notification/email/default</code></strong>，则由于原始电子邮件模板位于下，因此可以删除该文件夹 <strong><code>/libs/settings/notification/email/default</code></strong> 作为AEM 4安装的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 经典资产共享设计 {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>对于在SCM中管理且未在运行时通过设计对话框写入的任何设计，请执行以下操作以与最新型号保持一致：</p>
    <ol>
     <li>将设计从“上一位置”复制到 <code>/apps</code>.</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> with <code>allowProxy = true</code>.</li>
     <li>更新对 <code>cq:designPath</code> 属性通过 <strong>AEM &gt; DAM管理员&gt;资产共享页面&gt;页面属性&gt;高级选项卡&gt;设计字段</strong>.</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别。 这需要更新页面实施代码。</li>
     <li>更新Dispatcher规则，以允许通过 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>对于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时，请勿将可授权设计移出 <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 下载资产电子邮件通知模板 {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>如果电子邮件模板(<strong>下载资产</strong> 或 <strong>transitworkflowcompleted</strong>)进行了修改，然后按照以下过程与新结构保持一致：</p>
    <ol>
     <li>更新的电子邮件模板应从 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> to <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>因为目标位于<strong> <code>/apps</code></strong> 应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹： <code>/etc/dam/workflow/notification/email/downloadasset </code>电子邮件模板之后。<br />
      <ol>
       <li>如果未对<strong> <code>/etc</code></strong>，则由于原始电子邮件模板位于下，因此可以删除该文件夹 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> 作为AEM 6.4安装的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>While <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 在技术上支持查找(优先于通过常规Sling CAConfig查找的/apps，但优先于 <code>/etc</code>)可以将模板放置在 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. 但是，不建议这样做，因为没有运行时UI来促进电子邮件模板的编辑。</td>
  </tr>
 </tbody>
</table>

### DRM许可证示例 {#example-drm-licenses}

| **上一位置** | `/etc/dam/drm/licenses/` |
|---|---|
| **新位置** | `/libs/settings/dam/drm` |
| **重组指导** | 不适用 |
| **注释** | 不适用 |

### 链接共享电子邮件通知模板 {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>如果客户修改了电子邮件模板，则要与新的存储库结构保持一致：</p>
    <ol>
     <li>更新的电子邮件模板应从 <strong><code>/etc/dam/adhocassetshare</code></strong> to <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>因为目标位于<strong> <code>/apps</code></strong> 应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹： <strong><code>/etc/dam/adhocassetshare</code></strong> 电子邮件模板之后。<br />
      <ol>
       <li>如果未对<strong> <code>/etc</code></strong>，则由于原始电子邮件模板位于下，因此可以删除该文件夹 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> 作为AEM 6.4安装的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>While <code>/conf/global/settings/dam/adhocassetshare</code> 在技术上支持查找(优先于 <code>/apps</code> ，但在 <code>/etc</code>)，则模板可以放置在 <code>/conf/global/settings/dam/adhocassetshare</code>. 但是，不建议这样做，因为没有运行时UI来便于编辑电子邮件模板</td>
  </tr>
 </tbody>
</table>

### InDesign工作流脚本 {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>要与新的存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>从以下位置复制所有自定义或修改的脚本 <strong><code>/etc/dam/indesign/scripts</code></strong> to <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>只有作为AEM提供的未修改脚本复制新的或已修改的脚本，才能通过 <strong><code>/libs/settings</code></strong> 在AEM 6.5中</li>
      </ol> </li>
     <li>找到使用媒体提取流程WF步骤的所有工作流模型和
      <ol>
       <li>对于工作流步骤的每个实例，更新配置中的路径，以明确指向<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> 或 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 酌情。</li>
      </ol> </li>
     <li>删除<strong> <code>/etc/dam/indesign/scripts</code></strong> 完全。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>建议将自定义脚本存储在 <code>/apps</code>，因为这是应存储代码的位置。</td>
  </tr>
 </tbody>
</table>

### 视频转码配置 {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>需要剪切并粘贴项目级别的自定义项，这些自定义项位于对等项下 <code>/apps</code> 或 <code>/conf</code> 路径（如果适用）。</p> <p>要与AEM 6.4存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>从以下位置复制任何修改的视频配置 <code>/etc/dam/video</code> to <code>/apps/settings/dam/video</code></li>
     <li>删除 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 查看器预设配置 {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>对于开箱即用的查看器预设，该查看器预设将仅在新位置中可用。</p> <p>对于自定义查看器预设：</p>
    <ul>
     <li>您必须运行迁移脚本才能将节点从 <code>/etc</code> to <code>/conf</code>. 脚本位于 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>或者，您也可以编辑配置，这些配置将自动保存到新位置。</li>
    </ul> <p>请注意，您不必调整其copyURL/嵌入代码即可指向 <code>/conf</code>. 对 <code>/etc</code> 将被重新路由到 <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 杂项 {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>调整任何参照，以指向 <code>/libs</code> 使用 <code>/etc.clientlibs/</code> 允许代理前缀。</p> <p>最后，通过从中删除迁移的clientlib的文件夹来进行清理 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>
