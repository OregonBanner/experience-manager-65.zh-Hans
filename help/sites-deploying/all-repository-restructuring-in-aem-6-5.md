---
title: AEM 6.5中的常见存储库重组
seo-title: Common Repository Restructuring in AEM 6.5
description: 了解如何进行必要的更改，以便迁移到AEM 6.5中适用于AEM所有区域的新存储库结构。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 that are common for all areas of AEM.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
source-git-commit: 3f64bd7f5b4eb43aeefb9277a94e10ef1f0df59c
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 2%

---

# AEM 6.5中的常见存储库重组 {#common-repository-restructuring-in-aem}

如父项中所述 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到AEM 6.5的客户应使用此页面评估与存储库更改关联的工作量，这些更改可能会影响所有解决方案。 在AEM 6.5升级过程中，有些更改需要您投入精力，而有些则可能会推迟到将来升级。

**6.5版升级**

* [ContextHub 配置](#contexthub-6.5)
* [工作流实例](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [工作流模型](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [工作流启动器](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [工作流脚本](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**在将来升级之前**

* [ContextHub 配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [经典Cloud Services设计](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [经典功能板设计](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [经典报表设计](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [默认设计](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [AdobeDTM JavaScript端点](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [AdobeDTM Web挂接端点](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [收件箱任务](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [多站点管理器Blueprint配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM项目功能板小工具配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [复制通知电子邮件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [标记](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [翻译云服务](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [翻译语言](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [翻译规则](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [翻译构件客户端库](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [树激活Web控制台](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [供应商翻译连接器Cloud Services](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [工作流通知电子邮件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 6.5版升级 {#with-upgrade}

### ContextHub 配置 {#contexthub-6.5}

从AEM 6.4开始，没有默认的ContextHub配置。 因此，在站点的根级别上 `cq:contextHubPathproperty` 应设置为指示应使用的配置。

1. 导航到站点的根目录。
1. 打开根页面的页面属性，然后选择个性化选项卡。
1. 在Contexthub路径字段中，输入您自己的ContextHub配置路径。

此外，在ContextHub配置中， `sling:resourceType` 需要更新为相对路径而不是绝对路径。

1. 在CRX DE Lite中打开ContextHub配置节点的属性，例如 `/apps/settings/cloudsettings/legacy/contexthub`
1. 更改 `sling:resourceType` 起始日期 `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` 到 `granite/contexthub/cloudsettings/components/baseconfiguration`

即 `sling:resourceType` ContextHub配置的项必须是相对项而不是绝对项。

### 工作流模型 {#workflow-models}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新的或修改过的工作流模型必须迁移到/conf/global/workflow/models。</p>
    <ol>
     <li>将修改过的工作流模型部署到本地AEM 6.5开发实例中，以便它们存在于“上一个”位置。</li>
     <li>在“AEM”&gt;“工具”&gt;“工作流”&gt;“模型”中使用“AEM工作流模型编辑器”编辑工作流模型。</li>
     <li>迁移修改的AEM提供的工作流模型时
      <ol>
       <li>打开工作流模型编辑器后，修改浏览器的地址URL，并将路径段/libs/settings/workflow/models替换为/etc/workflow/models。
        <ul>
         <li>例如，更改： <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/model</strong>/dam/update_asset.html</em> 到 <em>http://localhost:4502/editor.html<strong>/etc/workflow/model</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>在工作流模型编辑器中启用编辑模式，该模式会将工作流模型定义复制到/conf/global/workflow/models。</li>
     <li>点按“同步”按钮，将更改同步到/var/workflow/models下的“运行时工作流模型”。</li>
     <li>导出两个工作流模型(/conf/global/workflow/models/&lt;workflow-model&gt;)和运行时工作流模型(/var/workflow/models/&lt;workflow-model&gt;)并集成到AEM项目中。
      <ol>
       <li>例如，导出：
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code> 和 </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>工作流模型解析的顺序如下：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>因此，如果要保留AEM提供的工作流模型的任何自定义项，则必须将其移至/conf/global/settings/workflow/models ，否则它们将被替换为/libs/settings/workflow/models中AEM提供的工作流模型定义。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流实例 {#workflow-instances}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>无需执行任何操作即可与新位置对齐。</p> <p>历史工作流实例可以安全地继续驻留在前一位置，而新工作流实例将创建在新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>中的任何显式路径引用
    <code>
     custom
    </code> “上一位置”的代码还应考虑“新位置”。 建议重构此代码以使用AEM Workflow API。</td>
  </tr>
 </tbody>
</table>

### 工作流启动器 {#workflow-launchers}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新的或修改过的工作流启动器都必须迁移到 <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>将任何新的或修改过的工作流启动器配置从上一个位置复制到新位置(<code>/conf/global</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>工作流启动器解析的顺序如下：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>因此，必须将AEM提供的工作流启动器保留在上一个位置的任何自定义项移至新位置(<code>/conf/global/settings/workflow/launcher</code> 如果要保留它们，则它们将由AEM提供的工作流启动器定义取代。 <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### 工作流脚本 {#workflow-scripts}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新的或修改过的工作流脚本必须迁移到新位置，并且引用工作流模型必须更新以反映新位置。</p>
    <ol>
     <li>将任何新的或修改过的工作流脚本从以前的位置复制到新位置。<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> 应在SCM中维护。</li>
      </ul> </li>
     <li>更新对工作流模型中先前位置处的工作流脚本的任何引用，以指向新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>AEM 6.4 SP1在发布后规定，此重组可以推迟到6.5
     <code>
      upgrade
     </code>.</p> <p>如果在发布AEM 6.4 SP1之前升级到AEM 6.4，则此重构应作为升级项目的一部分执行。 如果不这样做，则编辑和保存引用先前位置中的脚本的工作流步骤将会从工作流步骤中完全删除工作流脚本引用，并且只有新位置中的工作流脚本才会在脚本选择下拉菜单中可用。</p> </td>
  </tr>
 </tbody>
</table>

## 在将来升级之前 {#prior-to-upgrade}

### ContextHub 配置 {#contexthub-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新的或修改过的ContextHub配置都必须迁移到新位置，并且必须更新引用的AEM Sites页面以反映新位置。</p>
    <ol>
     <li>将任何新的或修改过的ContextHub配置从上一个位置复制到新位置。</li>
     <li>将适用的AEM配置与AEM内容层次结构关联。
      <ol>
       <li><strong>通过AEM Sites &gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置，查看AEM Sites页面层次结构</strong>.</li>
      </ol> </li>
     <li>取消任何已迁移的旧版ContextHub配置与上述AEM内容层次结构的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典Cloud Services设计 {#classic-cloud-services-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>用于任何在SCM中管理，且未在运行时通过“设计”对话框写入的设计。</p>
    <ol>
     <li>将设计从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对中先前位置的引用 <span class="code">
       <code>
        cq
       </code>：
       <code>
        designPath
       </code></span> 属性。</li>
     <li>更新任何引用以前位置的页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则以允许通过/etc.clientlibs/提供客户端库。 代理servlet。</li>
    </ol> <p>用于未在SCM中管理的任何设计，并通过“设计”对话框修改运行时设置。</p>
    <ul>
     <li>请勿将可创作设计移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典功能板设计 {#classic-dashboards-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>用于任何在SCM中管理，且未在运行时通过“设计”对话框写入的设计。</p>
    <ol>
     <li>将设计从上一个位置复制到新位置(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对中先前位置的引用
      <code>
       cq
      </code>：
      <code>
       designPath
      </code> 属性。</li>
     <li>更新任何引用以前位置的页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则以允许通过/etc.clientlibs/提供客户端库。 代理servlet。</li>
    </ol> <p>用于未在SCM中管理的任何设计，并通过“设计”对话框修改运行时设置。</p>
    <ul>
     <li>请勿将可创作设计移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典报表设计 {#classic-reports-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>用于任何在SCM中管理，且未在运行时通过“设计”对话框写入的设计。</p>
    <ol>
     <li>将设计从上一个位置复制到新位置(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对中先前位置的引用
      <code>
       cq
      </code>：
      <code>
       designPath
      </code> 属性。</li>
     <li>更新任何引用以前位置的页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则以允许通过/etc.clientlibs/提供客户端库。 代理servlet。</li>
    </ol> <p>用于未在SCM中管理的任何设计，并通过“设计”对话框修改运行时设置。</p>
    <ul>
     <li>请勿将可创作设计移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 默认设计 {#default-designs}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>用于任何在SCM中管理，且未在运行时通过“设计”对话框写入的设计。</p>
    <ol>
     <li>将设计从上一个位置复制到新位置(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对中先前位置的引用
      <code>
       cq
      </code>：
      <code>
       designPath
      </code> 属性。</li>
     <li>更新任何引用以前位置的页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则以允许通过/etc.clientlibs/提供客户端库。 代理servlet。</li>
    </ol> <p>用于未在SCM中管理的任何设计，并通过“设计”对话框修改运行时设置。</p>
    <ul>
     <li>请勿将可创作设计移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### AdobeDTM JavaScript端点 {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>无需执行任何操作。</p> <p>以前的公共位置用作专用新位置的代理端点。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### AdobeDTM Web挂接端点 {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>无需执行任何操作。</p> <p>以前的公共位置用作专用新位置的代理端点。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 收件箱任务 {#inbox-tasks}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td>使用 <strong>收件箱清除维护任务</strong> 以根据需要从上一个位置删除旧任务。</td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>无需执行任何操作即可将任务迁移到新位置。</p>
    <ul>
     <li>“上一位置”中的任务继续可用并正常工作。</li>
     <li>新任务是在新位置创建的。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 多站点管理器Blueprint配置 {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong><em></em>上一个位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td>
    <ol>
     <li>从以下位置复制自定义配置 <code>/etc/blueprints</code> 到 <code>/apps/msm</code>.</li>
     <li>移除 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### AEM项目功能板小工具配置 {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新的或修改过的AEM项目功能板小工具配置必须迁移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>将任何新的或修改过的AEM项目功能板小工具配置从上一个位置复制到新位置(<code>/apps</code>)。
      <ol>
       <li>请勿复制未修改的AEM项目功能板小工具配置，因为这些配置现在位于新位置(<code>/libs</code>)。</li>
      </ol> </li>
     <li>更新任何引用了先前位置的AEM Projects模板，以指向适当的新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>如果应用了AEM 6.4兼容包，则必须在删除兼容包时执行存储库对齐活动。</td>
  </tr>
 </tbody>
</table>

### 复制通知电子邮件模板 {#replication-notification-e-mail-template}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新的或修改过的复制通知电子邮件模板必须迁移到新位置(<code>/apps</code>)</p>
    <ol>
     <li>将任何新的或修改过的复制通知电子邮件模板从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>从上一个位置删除任何已迁移的复制通知电子邮件模板。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>唯一支持的新复制通知电子邮件模板是支持新区域设置。</p> <p>复制通知电子邮件模板解析的顺序如下：</p>
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

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>必须将所有标记迁移到 <code>/content/cq:tags</code>.</p>
    <ol>
     <li>将所有标记从上一个位置复制到新位置。</li>
     <li>从上一个位置删除所有标记。</li>
     <li>通过AEM Web Console，重新启动Day Communique 5 Tagging OSGi捆绑包，网址为 <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> ，以便AEM识别新位置，该位置包含内容，应当使用。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>重新启动Day Communique Tagging OSGi捆绑包后，只有当Previous Location为空时，才会将新位置注册为标记根。</p> <p>对于所有利用AEM TagManager API进行标记解析的功能，在迁移到新位置后，对之前位置的引用将继续有效。</p> <p>任何显式引用路径的自定义代码 <code>/etc/tags</code> 必须更新到 <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>，或者最好进行重写以结合此迁移使用TagManager Java API。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译云服务 {#translation-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新翻译Cloud Services都必须迁移到新位置(<code>/apps</code>， <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>将之前位置中的现有配置迁移到新位置。
      <ul>
       <li>通过AEM创作UI手动重新创建新的翻译Cloud Services配置，网址为 <strong>“工具”&gt;“Cloud Services”&gt;“翻译Cloud Services”</strong>.<br /> 或者 </li>
       <li>将任何新的翻译Cloud Services配置从上一个位置复制到新位置(<code>/apps</code>， <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>将适用的AEM配置与AEM内容层次结构关联。
      <ol>
       <li>AEM Sites页面层级，通过 <strong>AEM Sites &gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置</strong>.</li>
       <li>通过以下方式的AEM体验片段层次结构 <strong>AEM体验片段&gt;体验片段&gt;属性&gt;Cloud Services选项卡&gt;云配置</strong>.</li>
       <li>通过以下方式的AEM体验片段文件夹层次结构 <strong>AEM Experience Fragments &gt;文件夹&gt;属性&gt;Cloud Services选项卡&gt;云配置</strong>.<br /> </li>
       <li>AEM Assets文件夹层次结构，通过 <strong>AEM Assets &gt;文件夹&gt;文件夹属性&gt;Cloud Services选项卡&gt;配置</strong>.</li>
       <li>AEM项目，通过 <strong>AEM项目&gt;项目&gt;项目属性&gt;高级选项卡&gt;云配置</strong>.</li>
      </ol> </li>
     <li>取消任何已迁移旧版翻译Cloud ServicesAEM与上述内容层级的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>翻译Cloud Services解析的顺序如下：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>已迁移的翻译Cloud Services必须与AEM 6.4兼容。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译语言 {#translation-languages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新的或修改的翻译语言定义都需要将所有翻译语言定义迁移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>如果对翻译语言定义进行了任何添加或修改，则将所有翻译语言定义从上一个位置复制到新位置(<code>/apps</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>翻译语言路径解析的顺序如下：</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>此分辨率不支持合并叠加，这意味着解析的路径必须包含所有支持的语言，并且不会从更高分辨率继承支持的语言。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译规则 {#translation-rules}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>必须将修改后的翻译规则XML文件迁移到新位置(<code>/apps</code>，或 <code>/conf/global</code>)。</p> <p>1.将修改后的“翻译规则”XML文件从上一个位置复制到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>复制翻译规则XML解析的顺序如下：</p>
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

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>用于任何在SCM中管理，且未在运行时通过“设计”对话框写入的设计。</p>
    <ol>
     <li>将设计从上一个位置复制到新位置(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对中先前位置的引用
      <code>
       cq
      </code>：
      <code>
       designPath
      </code> 属性。</li>
     <li>更新任何引用以前位置的页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则以允许通过/etc.clientlibs/提供客户端库。 代理servlet。</li>
    </ol> <p>用于未在SCM中管理的任何设计，并通过“设计”对话框修改运行时设置。</p>
    <ul>
     <li>请勿将可创作设计移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 树激活Web控制台 {#tree-activation-web-console}

| **上一个位置** | `/etc/replication/treeactivation` |
|---|---|
| **新位置** | `/libs/replication/treeactivation` |
| **重构指南** | 无需执行任何操作。 |
| **注释** | 树激活Web控制台现在可通过以下方式使用 **工具>部署>复制>激活树**. |

{style="table-layout:auto"}

### 供应商翻译连接器Cloud Services {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何新的供应商翻译连接器Cloud Services必须迁移到新位置(<code>/apps</code>， <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p>
    <ol>
     <li>将以前位置中的现有配置迁移到新位置。
      <ul>
       <li>通过，手动创建新的供应商翻译连接器Cloud Services配置 <strong>位于“工具”&gt;“Cloud Services”&gt;“翻译Cloud Services”中的AEM创作UI</strong>.<br /> 或者 </li>
       <li>将任何新的供应商翻译连接器Cloud Services配置从上一个位置复制到新位置(<code>/apps</code>， <code>/conf/global </code>或 <code>/conf/&lt;tenant&gt;</code>)。</li>
      </ul> </li>
     <li>将适用的AEM配置与AEM内容层次结构关联。
      <ol>
       <li>AEM Sites页面层级，通过 <strong>AEM Sites &gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置</strong>.</li>
       <li>通过以下方式的AEM体验片段层次结构 <strong>AEM体验片段&gt;体验片段&gt;属性&gt;Cloud Services选项卡&gt;云配置</strong>.</li>
       <li>通过以下方式的AEM体验片段文件夹层次结构 <strong>AEM Experience Fragments &gt;文件夹&gt;属性&gt;Cloud Services选项卡&gt;云配置</strong>.</li>
       <li>AEM Assets文件夹层次结构，通过 <strong>AEM Assets &gt;文件夹&gt;文件夹属性&gt;Cloud Services选项卡&gt;配置</strong>.</li>
       <li>AEM项目，通过 <strong>AEM项目&gt;项目&gt;项目属性&gt;高级选项卡&gt;云配置</strong>.</li>
      </ol> </li>
     <li>取消任何已迁移旧版翻译Cloud ServicesAEM与上述内容层级的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>翻译Cloud Services解析的顺序如下：</p>
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

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>任何修改过的工作流通知电子邮件模板必须迁移到新位置(<code>/conf/global</code>)。</p>
    <ol>
     <li>将任何修改过的工作流通知电子邮件模板从上一个位置复制到新位置。</li>
     <li>从上一个位置删除已迁移的工作流通知电子邮件模板。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>工作流通知电子邮件模板解析的顺序如下：</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流包 {#workflow-packages}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>应将以前位置中的现有Workflow包迁移到新位置。</p>
    <ol>
     <li>删除先前位置中未被其他内容引用且在其他情况下不需要的任何工作流包。</li>
     <li>将任何未由其他内容引用、但在新位置有其他要求的工作流包移动到以前的位置。</li>
     <li>将其他内容引用的任何工作流包保留在上一个位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>通过经典UI Miscadmin控制台创建的工作流包将保留在以前的位置，而所有其他工作流包将保留在新位置。</p> <p>通过经典UI Miscadmin控制台，可以管理存储在以前或以下位置的工作流包。</p> </td>
  </tr>
 </tbody>
</table>
