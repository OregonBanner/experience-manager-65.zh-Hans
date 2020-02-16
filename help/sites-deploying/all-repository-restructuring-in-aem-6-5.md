---
title: AEM 6.5中的常见存储库重组
seo-title: AEM 6.5中的常见存储库重组
description: 了解如何进行必要的更改以迁移到AEM 6.5中的新存储库结构，这是AEM所有区域通用的。
seo-description: 了解如何进行必要的更改以迁移到AEM 6.5中的新存储库结构，这是AEM所有区域通用的。
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5中的常见存储库重组 {#common-repository-restructuring-in-aem}

如AEM 6.5页面中的父存储库重组中所述，升级到AEM 6.5的客户应使用此页来评估与存储库更改相关的工作成果，这些更改可能会影响所有解决方案。 [](/help/sites-deploying/repository-restructuring.md) 某些更改需要在AEM 6.5升级过程中进行工作，而其他更改可能会延迟到将来升级。

**升级6.5版**

* [工作流实例](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [工作流模型](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [工作流启动器](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [工作流脚本](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**在将来升级之前**

* [ContextHub 配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [经典云服务设计](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [经典仪表板设计](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [经典报表设计](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [默认设计](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Adobe DTM javaScript端点](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Adobe DTM Web-Hook端点](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [收件箱任务](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [多站点管理器Blueprint配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM Projects Dashboard小工具配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [复制通知电子邮件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [标记](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [翻译云服务](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [翻译语言](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [翻译规则](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [翻译构件客户端库](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [树状激活Web控制台](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [供应商翻译连接器云服务](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [工作流通知电子邮件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 升级6.5版 {#with-upgrade}

### 工作流模型 {#workflow-models}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的工作流模型迁移到/conf/global/workflow/models。</p>
    <ol>
     <li>将修改后的工作流模型部署到本地AEM 6.4开发实例中，以便它们存在于“上一个”位置。</li>
     <li>在AEM &gt;工具&gt;工作流&gt;模型中，使用AEM的工作流模型编辑器编辑工作流模型。</li>
     <li>迁移修改的AEM提供的工作流模型时
      <ol>
       <li>在工作流模型编辑器打开的情况下，修改浏览器的地址URL，并将路径段/libs/settings/workflow/models替换为/etc/workflow/models。
        <ul>
         <li>例如，更改：http://localhost:4502/editor.html <em>/libs/settings/workflow/models<strong>/dam/update_asset.html</strong>to</em> http://localhost:4502/editor.html <em>/etc/workflow/models<strong></strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>在工作流模型编辑器中启用编辑模式，该模式会将工作流模型定义复制到/conf/global/workflow/models。</li>
     <li>点按“同步”按钮，将更改同步到/var/workflow/models下的“运行时工作流模型”。</li>
     <li>导出工作流模型(/conf/global/workflow/models/&lt;workflow-model&gt;)和运行时工作流模型(/var/workflow/models/&lt;workflow-model&gt;)并集成到AEM项目中。
      <ol>
       <li>例如，导出：
        <ul>
         <li><code>/config/settings/workflow/models/dam/my_workflow_model</code> 和 </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>工作流模型解析按以下顺序进行：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>因此，如果要保留AEM提供的工作流模型，则必须将它们的任何自定义项移动到/conf/global/settings/workflow/models中，否则将被/libs/settings/workflow/models中AEM提供的工作流模型定义所取代。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流实例 {#workflow-instances}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>无需执行任何操作即可与新位置对齐。</p> <p>历史工作流实例可以安全地继续驻留在上一位置，而新的工作流实例将在新位置创建。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>代码中指向“上一位 <code>
     custom
    </code> 置”的任何显式路径引用也应考虑“新位置”。 建议重新构建此代码以使用AEM Workflow API。</td>
  </tr>
 </tbody>
</table>

### 工作流启动器 {#workflow-launchers}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的工作流启动器迁移到 <code>/conf/global/workflow/launcher/config</code>。</p>
    <ol>
     <li>将任何新的或修改的工作流启动器配置从上一个位置复制到新位置(<code>/conf/global</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>工作流启动器的分辨率按以下顺序进行：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>因此，在“上一位置”中保留的AEM提供的工作流启动器的任何自定义都必须移到“新位置”(如果要保留这些自定义，否则将被中的AEM提供的工作流启动器定义取代<code>/conf/global/settings/workflow/launcher</code><code>/libs/settings/workflow/launcher</code>。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流脚本 {#workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的工作流脚本迁移到新位置，并更新引用的工作流模型以反映新位置。</p>
    <ol>
     <li>将任何新的或修改的工作流脚本从上一个位置复制到新位置。<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> 应在单片机中维护。</li>
      </ul> </li>
     <li>更新对工作流模型中先前位置的工作流脚本的任何引用，以指向新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>AEM 6.4 SP1在发布时允许将此重组推迟到6.5 <code>
      upgrade
     </code>。</p> <p>如果在发布AEM 6.4 SP1之前升级到AEM 6.4，则此重组应作为升级项目的一部分执行。 如果不这样做，编辑和保存引用上一个位置中的脚本的工作流步骤将从工作流步骤中完全删除工作流脚本引用，并且只有新位置中的工作流脚本将在脚本选择下拉列表中可用。</p> </td>
  </tr>
 </tbody>
</table>

## 在将来升级之前 {#prior-to-upgrade}

### ContextHub 配置 {#contexthub-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的ContextHub配置迁移到新位置，并且必须更新引用的AEM站点页面以反映新位置。</p>
    <ol>
     <li>将任何新的或修改的ContextHub配置从先前位置复制到新位置。</li>
     <li>将适用的AEM配置与AEM内容层次关联。
      <ol>
       <li><strong>通过AEM站点&gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置实现AEM站点页面层次</strong>。</li>
      </ol> </li>
     <li>将迁移的任何旧版ContextHub配置与上述AEM内容层次结构取消关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典云服务设计 {#classic-cloud-services-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>适用于在SCM中管理的、在运行时不通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一位置”复制到“新位置”(<code>/apps</code>)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为客 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">户端库</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新对上一个位置的引 <span class="code"><code>
        cq
       </code>用：       属 <code>
        designPath
       </code></span> 性。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. proxy servlet。</li>
    </ol> <p>适用于未在SCM中管理的任何设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作的设计移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典仪表板设计 {#classic-dashboards-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>适用于在SCM中管理的、在运行时不通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一位置”复制到“新位置”(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为客 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">户端库</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新对上一位置的引用： <code>
       cq
      </code>     属 <code>
       designPath
      </code> 性。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. proxy servlet。</li>
    </ol> <p>适用于未在SCM中管理的任何设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作的设计移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典报表设计 {#classic-reports-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>适用于在SCM中管理的、在运行时不通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一位置”复制到“新位置”(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为客 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">户端库</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新对上一位置的引用： <code>
       cq
      </code>     属 <code>
       designPath
      </code> 性。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. proxy servlet。</li>
    </ol> <p>适用于未在SCM中管理的任何设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作的设计移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 默认设计 {#default-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>适用于在SCM中管理的、在运行时不通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一位置”复制到“新位置”(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为客 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">户端库</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新对上一位置的引用： <code>
       cq
      </code>     属 <code>
       designPath
      </code> 性。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. proxy servlet。</li>
    </ol> <p>适用于未在SCM中管理的任何设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作的设计移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### Adobe DTM javaScript端点 {#adobe-dtm-javascript-endpoint}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>无需执行任何操作。</p> <p>公共先前位置充当专用新位置的代理端点。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### Adobe DTM Web-Hook端点 {#adobe-dtm-web-hook-endpoint}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>无需执行任何操作。</p> <p>公共先前位置充当专用新位置的代理端点。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 收件箱任务 {#inbox-tasks}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td>根据需 <strong>要，使用收件箱清除维护任务</strong> ，从先前位置删除旧任务。</td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>将任务迁移到新位置无需执行任何操作。</p>
    <ul>
     <li>“上一位置”中的任务仍可用并可正常工作。</li>
     <li>新任务将在新位置中创建。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 多站点管理器Blueprint配置 {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong><em></em>上一位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td>
    <ol>
     <li>将自定义配置从复 <code>/etc/blueprints</code> 制到 <code>/apps/msm</code>。</li>
     <li>删除 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### AEM Projects Dashboard小工具配置 {#aem-projects-dashboard-gadget-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的AEM Projects控制面板小工具配置迁移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>将任何新的或修改的AEM Projects控制面板小工具配置从先前位置复制到新位置(<code>/apps</code>)。
      <ol>
       <li>请勿复制未修改的AEM Projects Dashboard小工具配置，因为新位置(<code>/libs</code>)中现在存在这些配置。</li>
      </ol> </li>
     <li>更新引用“上一位置”的任何AEM项目模板，以指向相应的新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>如果应用了AEM 6.4兼容性包，则需要在删除兼容性包时执行存储库对齐活动。</td>
  </tr>
 </tbody>
</table>

### 复制通知电子邮件模板 {#replication-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的复制通知电子邮件模板迁移到新位置(<code>/apps</code>)</p>
    <ol>
     <li>将任何新的或修改的复制通知电子邮件模板从先前的位置复制到新位置(<code>/apps</code>)。</li>
     <li>从以前的位置删除所有迁移的复制通知电子邮件模板。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>唯一支持的新复制通知电子邮件模板是支持新区域设置。</p> <p>复制通知电子邮件模板解析按以下顺序进行：</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 标记 {#tags}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将所有标记迁移到 <code>/content/cq:tags</code>。</p>
    <ol>
     <li>将所有标记从上一个位置复制到新位置。</li>
     <li>从上一位置删除所有标记。</li>
     <li>通过AEM Web Console，在 <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> for AEM中重新启动Day Computle 5 Tagging OSGi bundle，以识别新位置包含内容并应使用。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>重新启动Day Commule标记OSGi捆绑只在“上一个位置”为空时将“新位置”注册为标记根。</p> <p>针对利用AEM的TagManager API进行标记解析的所有功能，迁移到新位置后，对上一位置的引用将继续工作。</p> <p>任何明确引用该路径的自定 <code>/etc/tags</code> 义代码都必须更新为 <span class="code">/content/ <code>
       cq
      </code><code>
       :tags
      </code></span>，或者最好重写以利用TagManager Java API，并伴以此迁移。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译云服务 {#translation-cloud-services}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>任何新的翻译云服务都必须迁移到新位置(<code>/apps</code>或 <code>/conf/global</code><code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>将先前位置中的现有配置迁移到新位置。
      <ul>
       <li>通过AEM创作UI在“工具”&gt;“云服务”&gt;“翻译云服务”中手 <strong>动重新创建新的翻译云服务配置</strong>。<br /> 或者 </li>
       <li>将任何新的Translation cloud服务配置从“上一位置”复制到“新位置”(<code>/apps</code>或 <code>/conf/global</code> ) <code>/conf/&lt;tenant&gt;</code>中。</li>
      </ul> </li>
     <li>将适用的AEM配置与AEM内容层次关联。
      <ol>
       <li>通过 <strong>AEM Sites &gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置实现AEM Sites页面层次</strong>。</li>
       <li>通过AEM体验片段&gt;体 <strong>验片段&gt;属性&gt;云服务选项卡&gt;云配置获得的AEM体验片段层次结构</strong>。</li>
       <li>通过AEM体验片段&gt;文件夹&gt;属 <strong>性&gt;云服务选项卡&gt;云配置获得的AEM体验片段文件夹层次结构</strong>。<br /> </li>
       <li>通过 <strong>AEM资产&gt;文件夹&gt;文件夹属性&gt;云服务选项卡&gt;配置获得AEM资产文件夹层次结构</strong>。</li>
       <li>通过 <strong>AEM项目&gt;项目&gt;项目属性&gt;高级选项卡&gt;云配置创建AEM项目</strong>。</li>
      </ol> </li>
     <li>取消与上述AEM内容层次结构中迁移的任何旧版翻译云服务的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>Translation Cloud services的解决顺序如下：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>迁移的翻译云服务必须与AEM 6.4兼容。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译语言 {#translation-languages}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>任何新的或修改的翻译语言定义都需要将所有翻译语言定义迁移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>如果对翻译语言定义进行了任何添加或修改，则将所有翻译语言定义从先前位置复制到新位置(<code>/apps</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>翻译语言路径解析按以下顺序进行：</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>此分辨率不支持合并叠加，这意味着已解析的路径必须包含所有支持的语言，并且不会从更高分辨率继承支持的语言。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译规则 {#translation-rules}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>修改后的翻译规则XML文件必须迁移到新位<code>/apps</code>置(或 <code>/conf/global</code>)。</p> <p>1.将修改后的翻译规则XML文件从先前的位置复制到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>复制转换规则XML的解析顺序如下：</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 翻译构件客户端库 {#translation-widget-client-library}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>适用于在SCM中管理的、在运行时不通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一位置”复制到“新位置”(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为客 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">户端库</a><code>allowProxy = true</code>。</li>
     <li>在以下位置更新对上一位置的引用： <code>
       cq
      </code>     属 <code>
       designPath
      </code> 性。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. proxy servlet。</li>
    </ol> <p>适用于未在SCM中管理的任何设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作的设计移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 树状激活Web控制台 {#tree-activation-web-console}

| **上一位置** | `/etc/replication/treeactivation` |
|---|---|
| **新位置** | `/libs/replication/treeactivation` |
| **重组指导** | 无需执行任何操作。 |
| **注释** | 树激活Web控制台现在可通过“工具”>“部 **署”>“复制”>“激活树”使用**。 |

### 供应商翻译连接器云服务 {#vendor-translation-connector-cloud-services}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的供应商翻译连接器云服务迁移到新位<code>/apps</code>置( <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>将“上一位置”中的现有配置迁移到“新位置”。
      <ul>
       <li>通过 <strong>AEM创作UI，在“工具”&gt;“云服务”&gt;“翻译云服务”中手动创建新的供应商翻译连接器云服务配置</strong>。<br /> 或者 </li>
       <li>将任何新的供应商翻译连接器云服务配置从先前位置复制到新位<code>/apps</code>置( <code>/conf/global </code>或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>将适用的AEM配置与AEM内容层次关联。
      <ol>
       <li>通过 <strong>AEM Sites &gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置实现AEM Sites页面层次</strong>。</li>
       <li>通过AEM体验片段&gt;体 <strong>验片段&gt;属性&gt;云服务选项卡&gt;云配置获得的AEM体验片段层次结构</strong>。</li>
       <li>通过AEM体验片段&gt;文件夹&gt;属 <strong>性&gt;云服务选项卡&gt;云配置获得的AEM体验片段文件夹层次结构</strong>。</li>
       <li>通过 <strong>AEM资产&gt;文件夹&gt;文件夹属性&gt;云服务选项卡&gt;配置获得AEM资产文件夹层次结构</strong>。</li>
       <li>通过 <strong>AEM项目&gt;项目&gt;项目属性&gt;高级选项卡&gt;云配置创建AEM项目</strong>。</li>
      </ol> </li>
     <li>取消与上述AEM内容层次结构中迁移的任何旧版翻译云服务的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>Translation Cloud services的解决顺序如下：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流通知电子邮件模板 {#workflow-notification-email-templates}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>任何修改的工作流通知电子邮件模板都必须迁移到新位置(<code>/conf/global</code>)。</p>
    <ol>
     <li>将任何修改后的工作流通知电子邮件模板从上一个位置复制到新位置。</li>
     <li>从上一个位置删除迁移的工作流通知电子邮件模板。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>工作流通知电子邮件模板解析按以下顺序进行：</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流包 {#workflow-packages}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>应将先前位置中的现有工作流包迁移到新位置。</p>
    <ol>
     <li>删除之前位置中未被其他内容引用且不需要的任何工作流包。</li>
     <li>在以前的位置中移动任何未被其他内容引用但在新位置中需要的工作流包。</li>
     <li>保留之前位置中其他内容引用的任何工作流包。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>通过经典UI Miscadmin控制台创建的工作流包会保留在上一个位置，而所有其他包则会保留到新位置。</p> <p>存储在以前或以下位置的工作流包可以通过经典UI Miscadmin控制台进行管理。</p> </td>
  </tr>
 </tbody>
</table>

