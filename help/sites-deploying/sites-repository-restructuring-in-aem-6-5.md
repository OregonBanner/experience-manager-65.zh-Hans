---
title: AEM 6.5中的Sites存储库重构
description: 了解如何进行必要的更改，以迁移到AEM 6.5 for Sites中的新存储库结构。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: b4531792-06dd-4545-9dbb-57224be20dc7
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 1%

---

# AEM 6.5中的Sites存储库重构 {#sites-repository-restructuring-in-aem}

如父项中所述 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到AEM 6.5的客户应使用此页面评估与影响AEM Sites解决方案的存储库更改相关的工作量。 在AEM 6.5升级过程中，有些更改需要您尽心尽力，而其他更改则可能会推迟到将来升级时再进行。

**6.5版升级**

* [ContextHub 区段](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**在将来升级之前**

* [Adobe Analytics客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [经典Microsoft Word到网页设计](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [移动设备模拟器配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [多站点管理器蓝图配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [多站点管理器转出配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [页面事件通知电子邮件模板](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [页面基架](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [响应式网格更少](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [静态模板设计](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Adobe Target集成客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## 6.5版升级 {#with-upgrade}

### ContextHub 区段 {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code><br /> </p> <p><code>/conf/settings/settings/wcm/segments</code><br /> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>如果打算在源代码管理中编辑任何新的或修改的ContextHub区段，而不是在AEM中编辑它们，则必须将它们迁移到新位置：</p>
    <ol>
     <li>将任何新区段或修改的ContextHub区段从上一个位置复制到适当的新位置(/<code>apps</code>， <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>将之前位置对ContextHub区段的引用更新为新位置中已迁移的ContextHub区段(<code>/apps</code>， <code>/conf/global</code>， <code>/conf/&lt;tenant&gt;</code>)。</li>
    </ol> <p>以下QueryBuilder查询将查找对ContextHub区段的所有引用，并位于以前的位置。<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> 可以通过以下方式执行： <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM QueryBuilder调试器UI</a>. 请注意，这是一个遍历查询，因此不要对生产运行它，并确保根据需要调整遍历限制。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>保留到之前位置的ContextHub区段在中显示为只读 <strong>AEM &gt;个性化&gt;受众</strong>.</p> <p>如果要在AEM中编辑ContextHub区段，则必须将其迁移到新位置(<code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。 在AEM中创建的任何新ContentHub区段都会保留到新位置(<code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p> <p>AEM Sites页面属性仅允许使用上一个位置(<code>/etc</code>)或单个新位置(<code>/apps</code>， <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)，因此必须相应地迁移ContextHub区段。</p> <p>可以从AEM引用站点中删除任何未使用的ContextHub区段，并且不会将其迁移到新位置：</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segment/geometrixx-outdoors</li>
    </ul> <p>注意：如果ClientContext正在使用，建议转换为ContextHub。</p> </td>
  </tr>
 </tbody>
</table>

## 在将来升级之前 {#prior-to-upgrade}

### Adobe Analytics客户端库 {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>这些客户端库的任何自定义使用都应按类别而不是路径引用客户端库：</p>
    <ol>
     <li>应更新以前位置按路径对客户端库的任何引用，以便使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM客户端库引用框架</a>.</li>
     <li>如果无法使用AEM客户端库引用框架，可以通过AEM客户端库代理servlet引用客户端库的绝对路径。
      <ul>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li>
      </ul> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请访问每个类别 <code>cq:ClientLIbraryFolder</code> 节点通过CRXDELite并检查categories属性。</p>
    <ul>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 经典Microsoft Word到网页设计 {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>用于任何在SCM中管理，且未在运行时通过“设计”对话框写入的设计。</p>
    <ol>
     <li>将设计从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>将设计中的所有CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对cq：designPath属性中“上一位置”的引用。</li>
     <li>更新任何引用了先前位置的页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则以允许通过提供客户端库 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>对于未在SCM中管理并通过设计对话框修改运行时的任何设计：</p>
    <ul>
     <li>请勿将可创作设计移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 移动设备模拟器配置 {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td>必须将任何新的移动设备模拟器配置迁移到新位置。
    <ol>
     <li>将任何新的移动设备模拟器配置从上一个位置复制到新位置(<code>/apps</code>， <code>/conf/global</code>， <code>/conf/&lt;tenant&gt;</code>)。</li>
     <li>对于依赖于这些Mobile Device Emulator配置的任何AEM Sites页面，请更新页面的 <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> 节点： <br /> <span class="code">[cq：Page]/jcr：content@cq：
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>对于依赖这些移动设备模拟器配置的任何可编辑模板，请更新可编辑模板，并指向 <span class="code">
       <code>
        cq
       </code>：
       <code>
        deviceGroups
       </code></span> 到新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>移动设备模拟器配置分辨率按以下顺序进行：</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li><code>/conf/global/settings/mobile</code></li>
     <li><code>/apps/settings/mobile</code></li>
     <li><code>/libs/settings/mobile</code></li>
     <li><code>/etc/mobile</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 多站点管理器蓝图配置 {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/msm</code> （客户Blueprint配置）</p> <p><code>/libs/msm</code> （用于屏幕、商务的现成Blueprint配置）</p> </td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>任何新的或修改的多站点管理器Blueprint配置必须迁移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>将任何新的或修改过的多站点管理器Blueprint配置从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>从上一个位置删除所有迁移的多站点管理器Blueprint配置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>所有AEM提供的多站点管理器Blueprint配置都存在于中的新位置 <code>/libs</code>.</p> <p>内容未引用多站点管理器蓝色配置，因此没有要调整的内容引用。</p> </td>
  </tr>
 </tbody>
</table>

### 多站点管理器转出配置 {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>任何新的或修改的多站点管理器转出配置必须迁移到新位置。</p>
    <ol>
     <li>将任何新的或修改过的多站点管理器转出配置从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>将AEM页面上的任何引用更新到上一位置的多站点管理器转出配置，以指向新位置中的对应项(<code>/libs</code> 或 <code>/apps</code>)。</li>
    </ol> <p>从上一个位置删除已迁移的多站点管理器转出配置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>未能从“上一位置”删除迁移的多站点管理器转出配置，会导致向AEM作者显示重复的转出选项。</td>
  </tr>
 </tbody>
</table>

### 页面事件通知电子邮件模板 {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>唯一支持的新页面事件通知电子邮件模板是支持新区域设置。</p> <p>页面事件电子邮件模板解析的顺序如下：</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>任何新的或修改过的页面事件通知电子邮件模板必须迁移到下的新位置 <code>/apps</code>：</p>
    <ol>
     <li>将任何新的或修改过的页面事件通知电子邮件模板从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>从上一个位置删除任何迁移的页面事件通知电子邮件模板。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 页面基架 {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td>在“先前位置”下创建的基架使用旧版基架框架，无法迁移到新位置。 要与新位置保持一致，必须使用支持的基架框架重新开发任何旧式基架。</td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 响应式网格更少 {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>必须更新自定义LESS文件中对“先前位置”的任何引用，才能从“新位置”导入。</p>
    <ul>
     <li>在“上一位置”更新任何引用grid_base.less的自定义LESS文件以引用新位置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>引用不存在的项目 <code>grid_base.less</code> 文件导致页面和模板编辑器的布局模式无法正常工作，并中断页面布局。</td>
  </tr>
 </tbody>
</table>

### 静态模板设计 {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>用于任何在SCM中管理，且未在运行时通过“设计”对话框写入的设计。</p>
    <ol>
     <li>将设计从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>将设计中的所有CSS、JavaScript和静态资源转换为 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a> 替换为 <code>allowProxy = true</code>.</li>
     <li>更新对中先前位置的引用 <code>cq:designPath</code> 属性路径 <strong>AEM &gt;站点&gt;自定义站点页面&gt;页面属性&gt;高级选项卡&gt;设计字段</strong>.</li>
     <li>更新任何引用了先前位置的页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则以允许通过为客户端库提供服务 <code>/etc.clientlibs/</code> 代理servlet。</li>
    </ol> <p>对于未在SCM中管理并通过设计对话框修改运行时的任何设计：</p>
    <ul>
     <li>请勿将可创作设计移出 <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>推荐的方法是使用可编辑模板构建AEM Sites和页面，这些模板使用结构内容和策略来代替设计。</td>
  </tr>
 </tbody>
</table>

<!-- Search&Promote is end of life as of September 1, 2022 ### Adobe Search and Promote Integration Client Libraries {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Previous location</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>New location(s)</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Restructuring guidance</strong></td>
   <td><p>Any custom use of these Client Libraries should reference the Client Library by category, and not by path.</p>
    <ol>
     <li>Any references to the Client Library by path at the Previous Location should be updated to use <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM's Client Library referencing framework</a>.</li>
     <li>If AEM's Client Library referencing framework cannot be used, the absolute path of the Client Libraries can be referenced via AEM's Client Library Proxy servlet:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td><p>Editing of these Client Libraries was never supported.</p> <p>To obtain the Client Library categories, visit each cq:ClientLIbraryFolder node via CRXDELite and inspect the categories property:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table> -->

### Adobe Target集成客户端库 {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>这些客户端库的任何自定义使用都应按类别而不是路径引用客户端库。</p>
    <ol>
     <li>应更新以前位置按路径对客户端库的任何引用，以便使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM客户端库引用框架</a>.</li>
     <li>如果无法使用AEM客户端库引用框架，可以通过AEM客户端库代理servlet引用客户端库的绝对路径：</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访问每个cq：ClientLIbraryFolder节点，并检查类别属性：</p>
    <ul>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### WCM Foundation客户端库 {#wcm-foundation-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>重组指南</strong></td>
   <td><p>这些客户端库的任何自定义使用都应按类别而不是路径引用客户端库。</p>
    <ol>
     <li>应更新以前位置按路径对客户端库的任何引用，以便使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM客户端库引用框架</a>.</li>
     <li>如果无法使用AEM客户端库引用框架，可以通过AEM客户端库代理servlet引用客户端库的绝对路径。</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请访问每个类别 <code>cq:ClientLIbraryFolder</code> 节点通过CRXDELite并检查categories属性：</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
