---
title: AEM 6.5中的Assets存储库重组
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

# AEM 6.5中的Assets存储库重组 {#assets-repository-restructuring-in-aem}

如父项中所述 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到AEM 6.5的客户应使用此页面评估与影响AEM Assets解决方案的存储库更改相关的工作量。 在AEM 6.5升级过程中，有些更改需要您投入精力，而有些则可能会推迟到将来升级。

**6.5版升级**

* [杂项](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**在将来升级之前**

* [资产/收藏集事件电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [经典资产共享设计](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [下载资源电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [示例DRM许可证](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [链接共享电子邮件通知模板](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign工作流脚本](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [视频转码配置](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [杂项](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 6.5版升级 {#with-upgrade}

### 杂项 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>如果有任何自定义代码依赖于此位置(即 代码明确依赖于此路径)，然后必须在升级之前更新代码以使用新位置；理想情况下，使用Java API在可用时减少对JCR中任何特定路径的依赖性。</p> <p>保存zip文件以供客户端下载的临时位置。 客户端请求下载资产后，无需更新。 它将在新位置生成文件。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

## 在将来升级之前 {#prior-to-upgrade}

### 资产/收藏集事件电子邮件通知模板 {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>如果客户修改了电子邮件模板，请执行以下操作以与新的存储库结构保持一致：</p>
    <ol>
     <li>此 <code>/libs/settings/dam/notification</code> 电子邮件模板复制自 <strong><code>/etc/notification/email/default</code></strong> 到 <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>因为目标位于<strong> <code>/apps</code></strong> 此更改应保留在SCM中。</li>
      </ol> </li>
     <li>删除文件夹： <strong><code>/etc/dam/notification/email/default</code></strong> 中的电子邮件模板移动之后。<br />
      <ol>
       <li>如果未对下的电子邮件模板进行更新<strong> <code>/etc/notification/email/default</code></strong>，可删除该文件夹，因为下方存在原始电子邮件模板 <strong><code>/libs/settings/notification/email/default</code></strong> 作为AEM 4安装的一部分。</li>
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
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>对于在SCM中管理并且未在运行时通过“设计”对话框写入的任何设计，请执行以下操作以与最新模型对齐：</p>
    <ol>
     <li>将设计从“上一位置”复制到“下的新位置” <code>/apps</code>.</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对中先前位置的引用 <code>cq:designPath</code> 属性路径 <strong>AEM &gt; DAM管理员&gt;资产共享页面&gt;页面属性&gt;高级选项卡&gt;设计字段</strong>.</li>
     <li>更新任何引用以前位置的页面以使用新的客户端库类别。 这需要更新页面实施代码。</li>
     <li>更新Dispatcher规则以允许通过提供客户端库 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>对于未在SCM中管理并通过设计对话框修改运行时的任何设计，请勿将可创作设计移出 <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 下载资源电子邮件通知模板 {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>如果电子邮件模板(<strong>downloadasset</strong> 或 <strong>transientworkflowcompleted</strong>)，然后按照以下步骤操作以调整新结构：</p>
    <ol>
     <li>更新后的电子邮件模板应复制自 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> 到 <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>因为目标位于<strong> <code>/apps</code></strong> 此更改应保留在SCM中。</li>
      </ol> </li>
     <li>删除文件夹： <code>/etc/dam/workflow/notification/email/downloadasset </code>中的电子邮件模板移动之后。<br />
      <ol>
       <li>如果未对下的电子邮件模板进行更新<strong> <code>/etc</code></strong>，可删除该文件夹，因为下存在原始电子邮件模板 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> 作为AEM 6.4安装的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>While <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 从技术上讲，支持查找(通过常规Sling CAConfig查找优先于/apps，但优先于 <code>/etc</code>)模板可以放在 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. 但是，不建议这样做，因为没有运行时UI来简化电子邮件模板的编辑。</td>
  </tr>
 </tbody>
</table>

### 示例DRM许可证 {#example-drm-licenses}

| **上一个位置** | `/etc/dam/drm/licenses/` |
|---|---|
| **新位置** | `/libs/settings/dam/drm` |
| **重构指南** | 不适用 |
| **注释** | 不适用 |

### 链接共享电子邮件通知模板 {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>如果客户修改了电子邮件模板，则要与新的存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>更新后的电子邮件模板应复制自 <strong><code>/etc/dam/adhocassetshare</code></strong> 到 <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>因为目标位于<strong> <code>/apps</code></strong> 此更改应保留在SCM中。</li>
      </ol> </li>
     <li>删除文件夹： <strong><code>/etc/dam/adhocassetshare</code></strong> 中的电子邮件模板移动之后。<br />
      <ol>
       <li>如果未对下的电子邮件模板进行更新<strong> <code>/etc</code></strong>，可删除该文件夹，因为下方存在原始电子邮件模板 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> 作为AEM 6.4安装的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>While <code>/conf/global/settings/dam/adhocassetshare</code> 技术上支持查找(优先于 <code>/apps</code> 通过常规Sling CAConfig查找，但之后 <code>/etc</code>)，模板可以放在 <code>/conf/global/settings/dam/adhocassetshare</code>. 但是，不建议这样做，因为没有运行时UI可简化电子邮件模板的编辑</td>
  </tr>
 </tbody>
</table>

### InDesign工作流脚本 {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>要与新的存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>从以下位置复制所有自定义脚本或修改的脚本 <strong><code>/etc/dam/indesign/scripts</code></strong> 到 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>只有复制新脚本或修改的脚本才能使用，因为AEM提供的未修改的脚本将可通过以下方式使用 <strong><code>/libs/settings</code></strong> 在AEM 6.5中</li>
      </ol> </li>
     <li>找到所有使用媒体提取流程WF步骤的工作流模型并
      <ol>
       <li>对于工作流步骤的每个实例，更新config中的路径以明确指向下的正确脚本<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> 或 <strong><code>/libs/settings/dam/indesign/scripts</code></strong> 视情况而定。</li>
      </ol> </li>
     <li>移除<strong> <code>/etc/dam/indesign/scripts</code></strong> 全部。</li>
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
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>需要剪切并粘贴在等效项下的项目级别自定义项 <code>/apps</code> 或 <code>/conf</code> 路径（如果适用）。</p> <p>要与AEM 6.4存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>从复制任何修改的视频配置 <code>/etc/dam/video</code> 到 <code>/apps/settings/dam/video</code></li>
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
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>对于开箱即用的查看器预设，它仅在新位置可用。</p> <p>对于自定义查看器预设：</p>
    <ul>
     <li>您必须运行迁移脚本才能将节点从 <code>/etc</code> 到 <code>/conf</code>. 脚本位于 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>或者，您可以编辑配置，它们将自动保存到新位置。</li>
    </ul> <p>请注意，您不必调整其copyURL/嵌入代码以指向 <code>/conf</code>. 对的现有请求 <code>/etc</code> 将被重新路由到以下位置的正确内容： <code>/conf</code>.</p> </td>
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
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>调整任何引用以指向下的新资源 <code>/libs</code> 使用 <code>/etc.clientlibs/</code> 允许代理前缀。</p> <p>最后，通过从删除已迁移的clientlibs的文件夹进行清理 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>
