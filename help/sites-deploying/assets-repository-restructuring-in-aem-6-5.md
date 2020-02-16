---
title: AEM 6.5中的资产存储库重组
seo-title: AEM 6.5中的资产存储库重组
description: 了解如何进行必要的更改，以便迁移到AEM 6.5 for Assets中的新存储库结构。
seo-description: 了解如何进行必要的更改，以便迁移到AEM 6.5 for Assets中的新存储库结构。
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5中的资产存储库重组 {#assets-repository-restructuring-in-aem}

如AEM 6.5页面中的父存储库重组中所述 [](/help/sites-deploying/repository-restructuring.md) ，升级到AEM 6.5的客户应使用此页面评估与影响AEM资产解决方案的存储库更改相关的工作成果。 某些更改需要在AEM 6.5升级过程中进行工作，而其他更改可能会延迟到将来升级。

**升级6.5版**

* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**在将来升级之前**

* [资产／收藏集活动电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [经典资源共享设计](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [下载资产电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [DRM许可证示例](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [链接共享电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign工作流脚本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [视频转码配置](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 升级6.5版 {#with-upgrade}

### Misc {#misc}

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
   <td><p>如果任何自定义代码都依赖于此位置(即 代码显式依赖于此路径)，则必须更新代码才能在升级之前使用新位置；理想情况下，使用Java API来减少对JCR中任何特定路径的依赖性。</p> <p>保存zip文件以供客户端下载的临时位置。 由于客户端请求下载资产，因此无需进行更新。 它将在新位置生成文件。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

## 在将来升级之前 {#prior-to-upgrade}

### 资产／收藏集活动电子邮件通知模板 {#asset-collection-event-e-mail-notification-template}

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
   <td><p>如果客户修改了电子邮件模板，请执行以下操作以便与新的存储库结构保持一致：</p>
    <ol>
     <li>应 <code>/libs/settings/dam/notification</code> 将电子邮件模板从复制 <strong><code>/etc/notification/email/default</code></strong> 到 <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>因为目标位于<strong> SCM <code>/apps</code></strong> 中，所以应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹：在 <strong><code>/etc/dam/notification/email/default</code></strong> 其中的电子邮件模板被移动之后。<br />
      <ol>
       <li>如果未对下方的电子邮件模板进行任何更新<strong> ，则可以删除该文件夹，因为AEM 4安装中的原始电子邮件模板 <code>/etc/notification/email/default</code></strong><strong><code>/libs/settings/notification/email/default</code></strong> 位于下方。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 经典资源共享设计 {#classic-asset-share-designs}

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
   <td><p>对于在SCM中管理且未在运行时通过设计对话框写入的任何设计，请执行下列操作以与最新型号保持一致：</p>
    <ol>
     <li>将设计从“上一位置”复制到“新位置”下的“新位置” <code>/apps</code>。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为客 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">户端库</a><code>allowProxy = true</code>。</li>
     <li>通过 <code>cq:designPath</code> AEM &gt; DAM管理员&gt;资产共享页面&gt;页面属性&gt;高级选项卡&gt;设计字段更新对属性中上一个位置的引用 <strong></strong>。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别。 这需要更新页面实施代码。</li>
     <li>更新Dispatcher规则，以允许通过代理Servlet提供客 <code>/etc.clientlibs/</code> 户端库。</li>
    </ol> <p>对于未在SCM中管理的设计，以及通过设计对话框修改运行时的设计，请勿将可创作设计移出 <code>/etc</code>。</p> </td>
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
   <td><p>如果电子邮件模板(<strong>下载资产</strong><strong>或过渡工</strong>作流已完成)已修改，则请按照以下过程对齐新结构：</p>
    <ol>
     <li>更新的电子邮件模板应从复制到 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong><strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>因为目标位于<strong> SCM <code>/apps</code></strong> 中，所以应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹：在 <code>/etc/dam/workflow/notification/email/downloadasset </code>其中的电子邮件模板被移动之后。<br />
      <ol>
       <li>如果未对下方的电子邮件模板进行任何更新<strong> ，则可以删除该文件夹，因为AEM 6.4安装中的 <code>/etc</code></strong><strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> “原始电子邮件模板”位于下方。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>虽然 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 在技术上支持查找(优先于/apps之前通过常规的Sling CAConfig查找，但之后 <code>/etc</code>)，模板可以放入 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>。 但是，不建议这样做，因为没有运行时UI来便于编辑电子邮件模板。</td>
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
     <li>更新的电子邮件模板应从复制到 <strong><code>/etc/dam/adhocassetshare</code></strong><strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>因为目标位于<strong> SCM <code>/apps</code></strong> 中，所以应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹：在 <strong><code>/etc/dam/adhocassetshare</code></strong> 其中的电子邮件模板被移动之后。<br />
      <ol>
       <li>如果未对下方的电子邮件模板进行任何更新<strong> ，则可以删除该文件夹，因为AEM 6.4安装中的 <code>/etc</code></strong><strong><code>/libs/settings/dam/adhocassetshare</code></strong> “原始电子邮件模板”位于下方。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>虽然 <code>/conf/global/settings/dam/adhocassetshare</code> 在技术上支持查找(它优先于通常的Sling CAConfig查找，但 <code>/apps</code> 在之后 <code>/etc</code>)，但可以放置模板 <code>/conf/global/settings/dam/adhocassetshare</code>。 但是，不建议这样做，因为没有运行时UI来便于编辑电子邮件模板</td>
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
   <td><p>要与新存储库结构对齐，请执行以下操作：</p>
    <ol>
     <li>将所有自定义或修改的脚本从复制 <strong><code>/etc/dam/indesign/scripts</code></strong> 到 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>在AEM 6.5中，只有将新脚本或修改的脚本复制为AEM提供的未修改的脚 <strong><code>/libs/settings</code></strong> 本才能通过</li>
      </ol> </li>
     <li>找到所有使用媒体提取流程WF步骤的工作流模型，并
      <ol>
       <li>对于工作流步骤的每个实例，更新配置中的路径，以便明确指向位于相应脚本下<strong><code>/apps/settings/dam/indesign/scripts</code></strong> 或 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 视需要指向。</li>
      </ol> </li>
     <li>完全删<strong><code>/etc/dam/indesign/scripts</code></strong> 除。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>建议在下面存储自定义脚 <code>/apps</code>本，因为这是应存储代码的位置。</td>
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
   <td><p>项目级别自定义需要根据相应的对等或路径进 <code>/apps</code> 行剪 <code>/conf</code> 切和粘贴。</p> <p>要与AEM 6.4存储库结构对齐，请执行以下操作：</p>
    <ol>
     <li>将任何修改后的视频配置从复制 <code>/etc/dam/video</code> 到 <code>/apps/settings/dam/video</code></li>
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
   <td><p>对于开箱即用的查看器预设，它仅在新位置中可用。</p> <p>对于“自定义查看器预设”:</p>
    <ul>
     <li>您必须运行迁移脚本才能将节点从移动 <code>/etc</code> 到 <code>/conf</code>。 该脚本位于https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json <em>上</em></li>
     <li>或者，您也可以编辑配置，这些配置将自动保存到新位置。</li>
    </ul> <p>请注意，您不必调整其copyURL/embed代码即可指向 <code>/conf</code>。 现有的请求 <code>/etc</code> 将重新路由到中的正确内容 <code>/conf</code>。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### Misc {#misc2}

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
   <td><p>使用“允许代理前缀”调整任何引 <code>/libs</code> 用以指向 <code>/etc.clientlibs/</code> 新资源。</p> <p>最后，通过从 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

