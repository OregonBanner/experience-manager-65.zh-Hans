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
feature: 升级
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 2%

---

# AEM 6.5 {#assets-repository-restructuring-in-aem}中的资产存储库重组

如AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的父[存储库重组页面中所述，升级到AEM 6.5的客户应使用此页面评估与影响AEM Assets解决方案的存储库更改相关的工作量。 某些更改需要在AEM 6.5升级过程中完成工作，而其他更改可能会推迟到将来进行升级。

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

## 使用6.5升级{#with-upgrade}

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

## 在将来升级之前{#prior-to-upgrade}

### 资产/收集事件电子邮件通知模板{#asset-collection-event-e-mail-notification-template}

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
     <li><code>/libs/settings/dam/notification</code>电子邮件模板应从<strong><code>/etc/notification/email/default</code></strong>复制到<strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>由于目标位于<strong> <code>/apps</code></strong>中，因此应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹：<strong><code>/etc/dam/notification/email/default</code></strong>。<br />
      <ol>
       <li>如果未对<strong> <code>/etc/notification/email/default</code></strong>下的电子邮件模板进行任何更新，则可以删除文件夹，因为作为AEM 4安装的一部分，原始电子邮件模板位于<strong><code>/libs/settings/notification/email/default</code></strong>下。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 经典资产共享设计{#classic-asset-share-designs}

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
     <li>将设计从“上一位置”复制到<code>/apps</code>下的“新位置”。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a>。</li>
     <li>通过<strong>AEM &gt; DAM管理员&gt;资产共享页面&gt;页面属性&gt;高级选项卡&gt;设计字段</strong>更新对<code>cq:designPath</code>属性中上一位置的引用。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别。 这需要更新页面实施代码。</li>
     <li>更新Dispatcher规则，以允许通过<code>/etc.clientlibs/</code>代理Servlet提供客户端库。</li>
    </ol> <p>对于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时，请勿将可授权设计移出<code>/etc</code>。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 下载资产电子邮件通知模板{#download-asset-e-mail-notification-template}

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
   <td><p>如果电子邮件模板（<strong>downloadasset</strong>或<strong>transientworkflowcompleted</strong>）已修改，请按照以下步骤与新结构保持一致：</p>
    <ol>
     <li>更新的电子邮件模板应从<strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong>复制到<strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>由于目标位于<strong> <code>/apps</code></strong>中，因此应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹：<code>/etc/dam/workflow/notification/email/downloadasset </code>在电子邮件模板中移动后。<br />
      <ol>
       <li>如果未对<strong> <code>/etc</code></strong>下的电子邮件模板进行任何更新，则可以删除该文件夹，因为作为AEM 6.4安装的一部分，原始电子邮件模板位于<strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong>下。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>虽然在技术上支持<code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>进行查找（优先于/apps通过常规的Sling CAConfig查找，但在<code>/etc</code>之后），模板可以放置在<code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>中。 但是，不建议这样做，因为没有运行时UI来促进电子邮件模板的编辑。</td>
  </tr>
 </tbody>
</table>

### DRM许可证示例{#example-drm-licenses}

| **上一位置** | `/etc/dam/drm/licenses/` |
|---|---|
| **新位置** | `/libs/settings/dam/drm` |
| **重组指导** | 不适用 |
| **注释** | 不适用 |

### 链接共享电子邮件通知模板{#link-share-e-mail-notification-template}

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
     <li>更新的电子邮件模板应从<strong><code>/etc/dam/adhocassetshare</code></strong>复制到<strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>由于目标位于<strong> <code>/apps</code></strong>中，因此应在SCM中保留此更改。</li>
      </ol> </li>
     <li>删除文件夹：<strong><code>/etc/dam/adhocassetshare</code></strong>。<br />
      <ol>
       <li>如果未对<strong> <code>/etc</code></strong>下的电子邮件模板进行任何更新，则可以删除文件夹，因为作为AEM 6.4安装的一部分，原始电子邮件模板位于<strong><code>/libs/settings/dam/adhocassetshare</code></strong>下。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>虽然在技术上支持<code>/conf/global/settings/dam/adhocassetshare</code>进行查找（它优先于通过常规的Sling CAConfig查找在<code>/apps</code>之前，但在<code>/etc</code>之后），但模板可以放置在<code>/conf/global/settings/dam/adhocassetshare</code>中。 但是，不建议这样做，因为没有运行时UI来便于编辑电子邮件模板</td>
  </tr>
 </tbody>
</table>

### InDesign工作流脚本{#indesign-workflow-scripts}

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
     <li>将所有自定义或修改的脚本从<strong><code>/etc/dam/indesign/scripts</code></strong>复制到<strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>只有在AEM 6.5中的<strong><code>/libs/settings</code></strong>中提供了由AEM提供的未修改脚本，才能将新脚本或已修改的脚本作为未修改脚本复制</li>
      </ol> </li>
     <li>找到使用媒体提取流程WF步骤的所有工作流模型和
      <ol>
       <li>对于工作流步骤的每个实例，更新配置中的路径，以根据需要明确指向<strong> <code>/apps/settings/dam/indesign/scripts</code></strong>或<strong><code>/libs/settings/dam/indesign/scripts</code></strong>下的正确脚本。</li>
      </ol> </li>
     <li>完全删除<strong> <code>/etc/dam/indesign/scripts</code></strong>。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>建议将自定义脚本存储在<code>/apps</code>下，因为这是应存储代码的位置。</td>
  </tr>
 </tbody>
</table>

### 视频转码配置{#video-transcoding-configurations}

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
   <td><p>需要在相应的<code>/apps</code>或<code>/conf</code>路径下剪切并粘贴项目级别的自定义设置。</p> <p>要与AEM 6.4存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>将任何已修改的视频配置从<code>/etc/dam/video</code>复制到 <code>/apps/settings/dam/video</code></li>
     <li>删除 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 查看器预设配置{#viewer-preset-configurations}

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
     <li>您必须运行迁移脚本才能将节点从<code>/etc</code>移动到<code>/conf</code>。 脚本位于<em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>或者，您也可以编辑配置，这些配置将自动保存到新位置。</li>
    </ul> <p>请注意，您不必调整其copyURL/embed代码即可指向<code>/conf</code>。 对<code>/etc</code>的现有请求将被重新路由到<code>/conf</code>中的正确内容。</p> </td>
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
   <td><p>使用<code>/etc.clientlibs/</code>允许代理前缀调整任何引用以指向<code>/libs</code>下的新资源。</p> <p>最后，通过从中删除迁移的clientlib的文件夹来进行清理 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>
