---
title: AEM 6.5中的常见存储库重组
seo-title: AEM 6.5中的常见存储库重组
description: 了解如何进行必要的更改，以便迁移到AEM 6.5中新的存储库结构，该结构对于AEM的所有区域都是通用的。
seo-description: 了解如何进行必要的更改，以便迁移到AEM 6.5中新的存储库结构，该结构对于AEM的所有区域都是通用的。
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2724'
ht-degree: 2%

---

# AEM 6.5 {#common-repository-restructuring-in-aem}中的常见存储库重组

如AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的父[存储库重组页面中所述，升级到AEM 6.5的客户应使用此页面评估与存储库更改相关的工作量，这些工作量可能会影响所有解决方案。 某些更改需要在AEM 6.5升级过程中完成工作，而其他更改可能会推迟到将来进行升级。

**升级6.5版**

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
* [AdobeDTM Web-Hook端点](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [收件箱任务](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [多站点管理器Blueprint配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM项目功能板小工具配置](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [复制通知电子邮件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [标记](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [翻译云服务](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [翻译语言](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [翻译规则](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [翻译小组件客户端库](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [树状激活Web控制台](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [供应商翻译连接器Cloud Services](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [工作流通知电子邮件模板](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 使用6.5升级{#with-upgrade}

### ContextHub 配置 {#contexthub-6.5}

从AEM 6.4开始，没有默认的ContextHub配置。 因此，在站点的根级别上，应设置`cq:contextHubPathproperty`以指示应使用的配置。

1. 导航到站点的根。
1. 打开根页面的页面属性，然后选择个性化选项卡。
1. 在Contexthub路径字段中，输入您自己的ContextHub配置路径。

此外，在ContextHub配置中，`sling:resourceType`需要更新为相对值，而非绝对值。

1. 在CRX DE Lite中打开ContextHub配置节点的属性，例如`/apps/settings/cloudsettings/legacy/contexthub`
1. 将`sling:resourceType`从`/libs/granite/contexthub/cloudsettings/components/baseconfiguration`更改为`granite/contexthub/cloudsettings/components/baseconfiguration`

例如， ContextHub配置的`sling:resourceType`必须是相对配置，而不是绝对配置。

### 工作流模型 {#workflow-models}

<table style="table-layout:auto">
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
     <li>将修改的工作流模型部署到本地AEM 6.5开发实例中，以便它们存在于“上一个”位置。</li>
     <li>使用AEM工作流模型编辑器(位于AEM &gt;工具&gt;工作流&gt;模型)编辑工作流模型。</li>
     <li>迁移修改的AEM提供的工作流模型时
      <ol>
       <li>打开工作流模型编辑器后，修改浏览器的地址URL，并将路径段/libs/settings/workflow/models替换为/etc/workflow/models。
        <ul>
         <li>例如，更改：<em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em>至<em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>在工作流模型编辑器中启用编辑模式，该模式会将工作流模型定义复制到/conf/global/workflow/models。</li>
     <li>点按同步按钮，将更改同步到/var/workflow/models下的运行时工作流模型。</li>
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
   <td><p>工作流模型解析按以下顺序发生：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>因此，如果要保留“上一位置”中保留的AEM提供的工作流模型的任何自定义，则必须将其移至/conf/global/settings/workflow/models中，否则将被/libs/settings/workflow/models中AEM提供的工作流模型定义所取代。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流实例 {#workflow-instances}

<table style="table-layout:auto">
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
   <td><p>无需执行任何操作即可与新位置保持一致。</p> <p>历史工作流实例可以安全地继续驻留在先前位置，并且将在新位置中创建新的工作流实例。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>中的任何显式路径引用
    “上一位置”的<code>
     custom
    </code>代码也应考虑“新位置”。 建议对此代码进行重构以使用AEM工作流API。</td>
  </tr>
 </tbody>
</table>

### 工作流启动器 {#workflow-launchers}

<table style="table-layout:auto">
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
   <td><p>必须将任何新的或修改的工作流启动器迁移到<code>/conf/global/workflow/launcher/config</code>。</p>
    <ol>
     <li>将任何新的或修改的工作流启动器配置从“上一位置”复制到“新位置”(<code>/conf/global</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>工作流启动器解析按以下顺序发生：</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>因此，在“上一位置”中保留的AEM提供工作流启动器的任何自定义项都必须移到“新位置”(<code>/conf/global/settings/workflow/launcher</code>)中才能保留，否则将被<code>/libs/settings/workflow/launcher</code>中AEM提供的工作流启动器定义所取代。</p> </td>
  </tr>
 </tbody>
</table>

### 工作流脚本{#workflow-scripts}

<table style="table-layout:auto">
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
   <td><p>任何新的或修改的工作流脚本都必须迁移到新位置，并且引用的工作流模型已更新以反映新位置。</p>
    <ol>
     <li>将任何新的或修改的工作流脚本从上一位置复制到新位置。<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> 应在SCM中维护。</li>
      </ul> </li>
     <li>在工作流模型中的先前位置更新对工作流脚本的任何引用，以指向新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>AEM 6.4 SP1在发布时，会使其延迟至6.5
     <code>
      upgrade
     </code>。</p> <p>如果在AEM 6.4 SP1发布之前升级到AEM 6.4，则应在升级项目中执行此重组。 如果不这样做，编辑和保存在“上一位置”中引用脚本的工作流步骤将完全从工作流步骤中删除工作流脚本引用，并且脚本选择下拉列表中将只提供位于新位置的工作流脚本。</p> </td>
  </tr>
 </tbody>
</table>

## 在将来升级之前{#prior-to-upgrade}

### ContextHub 配置 {#contexthub-configurations}

<table style="table-layout:auto">
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
   <td><p>必须将任何新的或修改的ContextHub配置迁移到新位置，并且必须更新引用的AEM Sites页面以反映新位置。</p>
    <ol>
     <li>将任何新的或已修改的ContextHub配置从上一个位置复制到新位置。</li>
     <li>将适用的AEM配置与AEM内容层次结构关联。
      <ol>
       <li><strong>AEM Sites页面层级通过AEM Sites &gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置</strong>。</li>
      </ol> </li>
     <li>取消与上述AEM内容层级中任何迁移的旧版ContextHub配置的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典Cloud Services设计{#classic-cloud-services-designs}

<table style="table-layout:auto">
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
   <td><p>适用于在SCM中管理且不在运行时通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从上一位置复制到新位置(<code>/apps</code>)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a>。</li>
     <li>更新对<span class="code">中先前位置的引用
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span>属性。</li>
     <li>更新引用上一位置的任何页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>适用于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作设计移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典功能板设计{#classic-dashboards-designs}

<table style="table-layout:auto">
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
   <td><p>适用于在SCM中管理且不在运行时通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从上一位置复制到新位置(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a>。</li>
     <li>更新对
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>属性。</li>
     <li>更新引用上一位置的任何页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>适用于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作设计移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 经典报表设计{#classic-reports-designs}

<table style="table-layout:auto">
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
   <td><p>适用于在SCM中管理且不在运行时通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从上一位置复制到新位置(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a>。</li>
     <li>更新对
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>属性。</li>
     <li>更新引用上一位置的任何页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>适用于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作设计移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 默认设计{#default-designs}

<table style="table-layout:auto">
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
   <td><p>适用于在SCM中管理且不在运行时通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从上一位置复制到新位置(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a>。</li>
     <li>更新对
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>属性。</li>
     <li>更新引用上一位置的任何页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>适用于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作设计移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### AdobeDTM JavaScript端点{#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
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
   <td><p>无需执行任何操作。</p> <p>公共先前位置用作专用新位置的代理端点。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### AdobeDTM Web-Hook端点{#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
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
   <td><p>无需执行任何操作。</p> <p>公共先前位置用作专用新位置的代理端点。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 收件箱任务{#inbox-tasks}

<table style="table-layout:auto">
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
   <td>使用<strong>收件箱清除维护任务</strong>可根据需要从先前位置删除旧任务。</td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>将任务迁移到新位置无需执行任何操作。</p>
    <ul>
     <li>“上一位置”中存在的任务可继续使用并正常运行。</li>
     <li>新任务将在新位置中创建。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 多站点管理器Blueprint配置{#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
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
     <li>将自定义配置从<code>/etc/blueprints</code>复制到<code>/apps/msm</code>。</li>
     <li>删除 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### AEM项目功能板小工具配置{#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
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
   <td><p>必须将任何新的或修改的AEM项目功能板小工具配置迁移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>将任何新的或已修改的AEM项目功能板小工具配置从先前的位置复制到新位置(<code>/apps</code>)。
      <ol>
       <li>请勿复制未修改的AEM项目功能板小工具配置，因为这些配置现在存在于新位置(<code>/libs</code>)中。</li>
      </ol> </li>
     <li>更新任何引用“上一个位置”的AEM项目模板，以指向相应的新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>如果应用了AEM 6.4兼容包，则需要在删除兼容包时执行存储库对齐活动。</td>
  </tr>
 </tbody>
</table>

### 复制通知电子邮件模板{#replication-notification-e-mail-template}

<table style="table-layout:auto">
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
   <td><p>任何新的或修改的复制通知电子邮件模板都必须迁移到新位置(<code>/apps</code>)</p>
    <ol>
     <li>将任何新的或修改的复制通知电子邮件模板从先前的位置复制到新位置(<code>/apps</code>)。</li>
     <li>从先前的位置删除所有迁移的复制通知电子邮件模板。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>唯一支持的新复制通知电子邮件模板是支持新区域设置。</p> <p>复制通知电子邮件模板的解决顺序如下：</p>
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
   <td><strong>上一位置</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将所有标记迁移到<code>/content/cq:tags</code>。</p>
    <ol>
     <li>将所有标记从上一位置复制到新位置。</li>
     <li>从上一位置删除所有标记。</li>
     <li>通过AEM Web控制台，在<em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em>中重新启动Day Commule 5标记OSGi包，以便AEM识别新位置包含内容且应使用。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>重新启动日公报标记OSGi包将仅在“上一位置”为空时将“新位置”注册为标记根。</p> <p>在迁移到新位置后，对“上一位置”的引用将继续有效，因为所有功能都可利用AEM TagManager API进行标记解析。</p> <p>任何显式引用路径<code>/etc/tags</code>的自定义代码必须更新为<span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>，或者最好进行重写以结合此迁移来利用TagManager Java API。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译云服务 {#translation-cloud-services}

<table style="table-layout:auto">
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
   <td><p>任何新的翻译Cloud Services都必须迁移到新位置（<code>/apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。</p>
    <ol>
     <li>将先前位置的现有配置迁移到新位置。
      <ul>
       <li>通过位于<strong>工具&gt;Cloud Services&gt;翻译Cloud Services</strong>的AEM创作UI，手动重新创建新的翻译Cloud Services配置。<br /> 或者 </li>
       <li>将任何新的翻译Cloud Services配置从“上一位置”复制到“新位置”（<code>/apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。</li>
      </ul> </li>
     <li>将适用的AEM配置与AEM内容层次结构关联。
      <ol>
       <li>通过<strong>AEM Sites &gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置</strong>来AEM Sites页面层次。</li>
       <li>通过<strong>AEM体验片段&gt;体验片段&gt;属性&gt;Cloud Services选项卡&gt;云配置</strong>实现的AEM体验片段层次结构。</li>
       <li>通过<strong>AEM体验片段&gt;文件夹&gt;属性&gt;Cloud Services选项卡&gt;云配置</strong>的AEM体验片段文件夹层次结构。<br /> </li>
       <li>通过<strong>AEM Assets &gt;文件夹&gt;文件夹属性&gt;Cloud Services选项卡&gt;配置</strong>来AEM Assets文件夹层次结构。</li>
       <li>通过<strong>AEM项目&gt;项目&gt;项目属性&gt;高级选项卡&gt;云配置</strong>进行AEM项目。</li>
      </ol> </li>
     <li>取消与上述AEM内容层次结构中任何迁移的旧版翻译Cloud Services的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>翻译Cloud Services解析按以下顺序进行：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>迁移的翻译Cloud Services必须与AEM 6.4兼容。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译语言{#translation-languages}

<table style="table-layout:auto">
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
     <li>如果对“翻译语言”定义进行了任何添加或修改，则将所有“翻译语言”定义从上一个位置复制到新位置(<code>/apps</code>)。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>翻译语言路径解析按以下顺序进行：</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>此分辨率不支持合并叠加，这意味着解析的路径必须包含所有受支持的语言，并且不会从更高级分辨率继承受支持的语言。</p> </td>
  </tr>
 </tbody>
</table>

### 翻译规则{#translation-rules}

<table style="table-layout:auto">
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
   <td><p>必须将修改的翻译规则XML文件迁移到新位置（<code>/apps</code>或<code>/conf/global</code>）。</p> <p>1.将修改的翻译规则XML文件从先前的位置复制到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>复制转换规则XML解析按以下顺序发生：</p>
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

### 翻译小组件客户端库{#translation-widget-client-library}

<table style="table-layout:auto">
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
   <td><p>适用于在SCM中管理且不在运行时通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从上一位置复制到新位置(/apps)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a>。</li>
     <li>更新对
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>属性。</li>
     <li>更新引用上一位置的任何页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过/etc.clientlibs/.. 代理servlet。</li>
    </ol> <p>适用于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时。</p>
    <ul>
     <li>请勿将可创作设计移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

### 树激活Web控制台{#tree-activation-web-console}

| **上一位置** | `/etc/replication/treeactivation` |
|---|---|
| **新位置** | `/libs/replication/treeactivation` |
| **重组指导** | 无需执行任何操作。 |
| **注释** | 树激活Web控制台现在可通过&#x200B;**工具>部署>复制>激活树**&#x200B;获得。 |

{style=&quot;table-layout:auto&quot;}

### 供应商翻译连接器Cloud Services{#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
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
   <td><p>任何新的供应商翻译连接器Cloud Services都必须迁移到新位置（<code>/apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。</p>
    <ol>
     <li>将“上一位置”中的现有配置迁移到“新位置”。
      <ul>
       <li>通过<strong>AEM创作UI(位于工具&gt;Cloud Services&gt;翻译Cloud Services</strong>)手动创建新的供应商翻译连接器Cloud Services配置。<br /> 或者 </li>
       <li>将任何新的供应商翻译连接器Cloud Services配置从先前位置复制到新位置（<code>/apps</code>、<code>/conf/global </code>或<code>/conf/&lt;tenant&gt;</code>）。</li>
      </ul> </li>
     <li>将适用的AEM配置与AEM内容层次结构关联。
      <ol>
       <li>通过<strong>AEM Sites &gt;页面&gt;页面属性&gt;高级选项卡&gt;云配置</strong>来AEM Sites页面层次。</li>
       <li>通过<strong>AEM体验片段&gt;体验片段&gt;属性&gt;Cloud Services选项卡&gt;云配置</strong>实现的AEM体验片段层次结构。</li>
       <li>通过<strong>AEM体验片段&gt;文件夹&gt;属性&gt;Cloud Services选项卡&gt;云配置</strong>实现AEM体验片段文件夹层次结构。</li>
       <li>通过<strong>AEM Assets &gt;文件夹&gt;文件夹属性&gt;Cloud Services选项卡&gt;配置</strong>来AEM Assets文件夹层次结构。</li>
       <li>通过<strong>AEM项目&gt;项目&gt;项目属性&gt;高级选项卡&gt;云配置</strong>进行AEM项目。</li>
      </ol> </li>
     <li>取消与上述AEM内容层次结构中任何迁移的旧版翻译Cloud Services的关联。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>翻译Cloud Services解析按以下顺序进行：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流通知电子邮件模板{#workflow-notification-email-templates}

<table style="table-layout:auto">
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
     <li>将之前位置中任何修改的工作流通知电子邮件模板复制到新位置。</li>
     <li>从上一个位置删除迁移的工作流通知电子邮件模板。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>工作流通知电子邮件模板解析按以下顺序发生：</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 工作流包{#workflow-packages}

<table style="table-layout:auto">
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
   <td><p>应将之前位置中的现有工作流包迁移到新位置。</p>
    <ol>
     <li>删除之前位置中其他内容未引用且不需要的任何工作流包。</li>
     <li>在以前的位置移动任何未被其他内容引用但在新位置中需要的工作流包。</li>
     <li>保留先前位置中其他内容引用的任何工作流包。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>通过经典UI Miscadmin控制台创建的工作流包将保留在先前的位置，而所有其他工作流包则保留到新位置。</p> <p>可以通过经典UI Miscadmin控制台管理存储在以前或以下位置中的工作流包。</p> </td>
  </tr>
 </tbody>
</table>
