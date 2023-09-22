---
title: AEM 6.5中的Assets存储库重构
description: 了解如何进行必要的更改，以迁移到Adobe Experience Manager (AEM) 6.5 for Assets中的新存储库结构。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 2%

---

# AEM 6.5中的Assets存储库重构 {#assets-repository-restructuring-in-aem}

如父项中所述 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到Adobe Experience Manager (AEM) 6.5的客户应使用此页面评估与影响AEM Assets解决方案的存储库更改相关的工作量。 在AEM 6.5升级过程中，有些更改需要您尽心尽力，而其他更改则可能会推迟到将来升级时再进行。

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
   <td><strong>重组指南</strong></td>
   <td><p>如果有任何自定义代码依赖于此位置（即，代码明确依赖于此路径），则必须更新代码以使用新位置，然后再升级。 理想情况下，当可用时使用Java™ API以减少对JCR中任何特定路径的依赖性。</p> <p>用于保存供客户端下载的zip文件的临时位置。 客户端请求下载资产后，无需更新。 它会在新位置生成文件。</p> </td>
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
   <td><strong>重组指南</strong></td>
   <td><p>如果客户修改了电子邮件模板，请执行以下操作以与新的存储库结构保持一致：</p>
    <ol>
     <li>此 <code>/libs/settings/dam/notification</code> 电子邮件模板应复制自 <strong><code>/etc/notification/email/default</code></strong> 到 <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>因为目标位于<strong> <code>/apps</code></strong>，此更改应保留在SCM中。</li>
      </ol> </li>
     <li>删除文件夹： <strong><code>/etc/dam/notification/email/default</code></strong> 移动其中的电子邮件模板之后。<br />
      <ol>
       <li>如果未对下的电子邮件模板进行更新<strong> <code>/etc/notification/email/default</code></strong>，可删除该文件夹，因为下存在原始电子邮件模板 <strong><code>/libs/settings/notification/email/default</code></strong> 作为AEM 4安装的一部分。</li>
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
   <td><strong>重组指南</strong></td>
   <td><p>对于在SCM中管理，且未在运行时通过“设计”对话框写入的任何设计，请执行以下操作以对齐最新模型：</p>
    <ol>
     <li>将设计从上一个位置复制到下的新位置 <code>/apps</code>.</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对中先前位置的引用 <code>cq:designPath</code> 通过以下方式获得资产 <strong>AEM &gt; DAM管理员&gt;资产共享页面&gt;页面属性&gt;高级选项卡&gt;设计字段</strong>.</li>
     <li>要使用新的“客户端库”类别，请更新任何引用先前位置的页面。 这需要更新页面实施代码。</li>
     <li>更新Dispatcher规则，以便您可以允许通过提供客户端库 <code>/etc.clientlibs/</code> 代理servlet。</li>
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
   <td><strong>重组指南</strong></td>
   <td><p>如果电子邮件模板(<strong>downloadasset</strong> 或 <strong>transientworkflowcompleted</strong>)，然后执行以下过程以调整新结构：</p>
    <ol>
     <li>应从以下位置复制更新的电子邮件模板 <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> 到 <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>因为目标位于<strong> <code>/apps</code></strong>，此更改应保留在SCM中。</li>
      </ol> </li>
     <li>删除文件夹： <code>/etc/dam/workflow/notification/email/downloadasset </code>移动其中的电子邮件模板之后。<br />
      <ol>
       <li>如果未对下的电子邮件模板进行更新<strong> <code>/etc</code></strong>，可删除该文件夹，因为下存在原始电子邮件模板 <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> 作为AEM 6.4安装的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>同时 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> 从技术上讲，支持查找(通过常用的Sling CAConfig查找在/apps之前优先，但在之后 <code>/etc</code>)模板可以放置在 <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. 但是，不建议这样做，因为没有运行时UI来简化电子邮件模板的编辑。</td>
  </tr>
 </tbody>
</table>

### 示例DRM许可证 {#example-drm-licenses}

| **上一个位置** | `/etc/dam/drm/licenses/` |
|---|---|
| **新位置** | `/libs/settings/dam/drm` |
| **重组指南** | 不适用 |
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
   <td><strong>重组指南</strong></td>
   <td><p>如果客户修改了电子邮件模板，则要与新的存储库结构保持一致：</p>
    <ol>
     <li>应从以下位置复制更新的电子邮件模板 <strong><code>/etc/dam/adhocassetshare</code></strong> 到 <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>因为目标位于<strong><code>/apps</code></strong>，此更改应保留在SCM中。</li>
      </ol> </li>
     <li>删除文件夹： <strong><code>/etc/dam/adhocassetshare</code></strong> 移动其中的电子邮件模板之后。<br />
      <ol>
       <li>如果未对下的电子邮件模板进行更新<strong> <code>/etc</code></strong>，可删除该文件夹，因为下存在原始电子邮件模板 <strong><code>/libs/settings/dam/adhocassetshare</code></strong> 作为AEM 6.4安装的一部分。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>同时 <code>/conf/global/settings/dam/adhocassetshare</code> 技术上支持查找(它优先于 <code>/apps</code> 通过Sling CAConfig查找，但之后 <code>/etc</code>)，模板可以放置在 <code>/conf/global/settings/dam/adhocassetshare</code>. 但是，不建议这样做，因为没有运行时UI来简化电子邮件模板的编辑</td>
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
   <td><strong>重组指南</strong></td>
   <td><p>要与新的存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>复制所有自定义脚本或修改的脚本 <strong><code>/etc/dam/indesign/scripts</code></strong> 到 <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>只有复制新脚本或修改后的脚本才能作为由AEM提供的未修改脚本使用，其方式为 <strong><code>/libs/settings</code></strong> 在AEM 6.5中</li>
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
   <td><strong>重组指南</strong></td>
   <td><p>项目级别的自定义项必须剪切并粘贴到等效项下 <code>/apps</code> 或 <code>/conf</code> 路径（如果适用）。</p> <p>要与AEM 6.4存储库结构保持一致，请执行以下操作：</p>
    <ol>
     <li>从复制任何已修改的视频配置 <code>/etc/dam/video</code> 到 <code>/apps/settings/dam/video</code></li>
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
   <td><strong>重组指南</strong></td>
   <td><p>对于现成的查看器预设，它仅在新位置可用。</p> <p>对于自定义查看器预设：</p>
    <ul>
     <li>运行迁移脚本，以便您能够将节点从 <code>/etc</code> 到 <code>/conf</code>. 脚本位于 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>或者，您也可以编辑配置，并将它们自动保存到新位置。</li>
    </ul> <p>您不必调整其copyURL/嵌入代码以指向 <code>/conf</code>. 对的现有请求 <code>/etc</code> 被重新路由到正确的内容，从 <code>/conf</code>.</p> </td>
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
   <td><strong>重组指南</strong></td>
   <td><p>调整任何引用以指向下的新资源 <code>/libs</code> 使用 <code>/etc.clientlibs/</code> 允许代理前缀。</p> <p>最后，通过从删除已迁移的clientlibs的文件夹进行清理 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>
