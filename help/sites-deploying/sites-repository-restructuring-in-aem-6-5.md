---
title: AEM 6.5中的Sites Repository Restructing
seo-title: AEM 6.5中的Sites Repository Restructing
description: 了解如何进行必要的更改以迁移到适用于站点的AEM 6.5中的新存储库结构。
seo-description: 了解如何进行必要的更改以迁移到适用于站点的AEM 6.5中的新存储库结构。
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 1%

---


# AEM 6.5 {#sites-repository-restructuring-in-aem}中的站点存储库重组

如AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的父级[存储库重组页所述，升级到AEM 6.5的客户应使用此页评估与影响AEM Sites解决方案的存储库更改相关的工作。 某些更改需要在AEM 6.5升级过程中进行工作，而其他更改可能会延迟到将来的升级。

**通过6.5升级**

* [ContextHub 区段](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**在将来升级之前**

* [Adobe Analytics Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [经典Microsoft Word到网页设计](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [移动设备模拟器配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [多站点管理器Blueprint配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [多站点管理器转出配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [页面事件通知电子邮件模板](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [页面基架](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [响应式网格更少](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [静态模板设计](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Adobe搜索和提升集成客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Adobe Target Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## 使用6.5升级{#with-upgrade}

### ContextHub 区段 {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>如果任何新的或修改的ContextHub区段要在源代码控件中进行编辑而不是在AEM中进行编辑，则必须将其迁移到新位置：</p>
    <ol>
     <li>将任何新的或修改过的ContextHub区段从上一个位置复制到相应的新位置（/<code>apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）</li>
     <li>将之前位置中对ContextHub区段的引用更新到新位置(<code>/apps</code>、<code>/conf/global</code>、<code>/conf/&lt;tenant&gt;</code>)中迁移的ContextHub区段。</li>
    </ol> <p>以下QueryBuilder查询将查找对“上一个位置”中ContextHub区段的所有引用。<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> 可通过AEM QueryBuilder调 <a href="/help/sites-developing/querybuilder-api.md" target="_blank">试器UI执行此操作</a>。请注意，这是一个遍历查询，因此不要针对生产运行它，并确保根据需要调整遍历限制。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>ContextHub区段会在<strong>AEM &gt;个性化&gt;受众</strong>中以只读方式保留到之前的位置。</p> <p>如果要在AEM中编辑ContextHub区段，则必须将它们迁移到新位置（<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。 在AEM中创建的任何新ContentHub区段会保留到新位置（<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>）。</p> <p>AEM Sites页面属性只允许选择上一位置(<code>/etc</code>)或单个新位置（<code>/apps</code>、<code>/conf/global</code>或<code>/conf/&lt;tenant&gt;</code>），因此必须相应地迁移ContextHub区段。</p> <p>可以删除AEM引用站点中任何未使用的ContextHub区段，但不能将其迁移到新位置：</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>注意：如果正在使用ClientContext，建议转换为ContextHub。</p> </td>
  </tr>
 </tbody>
</table>

## 未来升级前{#prior-to-upgrade}

### Adobe Analytics客户端库{#adobe-analytics-client-libraries}

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
   <td><strong>重组指导</strong></td>
   <td><p>对这些客户端库的任何自定义使用都应按类别引用客户端库，而不应按路径引用：</p>
    <ol>
     <li>应更新Previous Location（上一个位置）上按路径对客户端库的任何引用，以使用<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">引用framework</a>的AEM客户端库。</li>
     <li>如果无法使用AEM客户端库引用框架，则可以通过AEM客户端库代理servlet引用客户端库的绝对路径。
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
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访问每个<code>cq:ClientLIbraryFolder</code>节点并检查类别属性。</p>
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

### 经典Microsoft Word到网页设计{#classic-microsoft-word-to-web-page-designs}

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
   <td><strong>重组指导</strong></td>
   <td><p>适用于以SCM管理且不在运行时通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一个位置”复制到“新位置”(<code>/apps</code>)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a>。</li>
     <li>在cq:designPath属性中更新对“上一个位置”的引用。</li>
     <li>更新引用上一个位置的任何页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过<code>/etc.clientlibs/</code>代理servlet提供客户端库。</li>
    </ol> <p>对于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时：</p>
    <ul>
     <li>请勿将可创作设计移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 移动设备模拟器配置{#mobile-device-emulator-configurations}

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
   <td><strong>重组指导</strong></td>
   <td>任何新的移动设备模拟器配置都必须迁移到新位置。
    <ol>
     <li>将任何新的移动设备模拟器配置从上一个位置复制到新位置(<code>/apps</code>、<code>/conf/global</code>、<code>/conf/&lt;tenant&gt;</code>)。</li>
     <li>对于依赖于这些移动设备模拟器配置的任何AEM Sites页面，请更新该页面的<span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span>节点：<br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>对于任何依赖这些移动设备模拟器配置的可编辑模板，请更新可编辑模板，并指向<span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span>到新位置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>移动设备模拟器配置的分辨率按以下顺序进行：</p>
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

### 多站点管理器Blueprint配置{#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/msm</code> （客户Blueprint配置）</p> <p><code>/libs/msm</code> （Screens、Commerce的现成Blueprint配置）</p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的多站点管理器Blueprint配置迁移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>将任何新的或已修改的多站点管理器Blueprint配置从“上一个位置”复制到“新位置”(<code>/apps</code>)。</li>
     <li>从“上一个位置”中删除任何迁移的多站点管理器Blueprint配置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>所有AEM提供的多站点管理器Blueprint配置都存在于<code>/libs</code>中的新位置中。</p> <p>内容不引用多站点管理器蓝色配置，因此没有要调整的内容引用。</p> </td>
  </tr>
 </tbody>
</table>

### 多站点管理器转出配置{#multi-site-manager-rollout-configurations}

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
   <td><strong>重组指导</strong></td>
   <td><p>任何新的或修改的多站点管理器转出配置都必须迁移到新位置。</p>
    <ol>
     <li>将任何新的或已修改的多站点管理器转出配置从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>将AEM页面上的任何引用更新到“上一个位置”中的多站点管理器转出配置，以指向“新位置”（<code>/libs</code>或<code>/apps</code>）中的对应位置。</li>
    </ol> <p>从上一个位置删除迁移的多站点管理器转出配置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>未能从“上一个位置”中删除迁移的多站点管理器转出配置，结果将显示重复转出选项给AEM作者。</td>
  </tr>
 </tbody>
</table>

### 页面事件通知电子邮件模板{#page-event-notification-e-mail-template}

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
   <td><strong>重组指导</strong></td>
   <td><p>唯一支持的新页面事件通知电子邮件模板是支持新区域设置。</p> <p>页面事件电子邮件模板解析按以下顺序进行：</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>必须将任何新的或修改的页面事件通知电子邮件模板迁移到<code>/apps</code>下的新位置：</p>
    <ol>
     <li>将任何新的或修改的页面事件通知电子邮件模板从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>从上一个位置删除任何迁移的页面事件通知电子邮件模板。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 页面基架{#page-scaffolding}

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
      </code>/template types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td>在“上一位置”下创建的基架使用旧版Scaffolding框架，无法迁移到新位置。 要与新位置对齐，必须使用支持的Scaffolding框架重新开发任何旧版Scaffolding。</td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>

### 响应式网格LESS {#responsive-grid-less}

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
   <td><strong>重组指导</strong></td>
   <td><p>必须更新对自定义LESS文件中的“上一位置”的任何引用，以从“新位置”中导入。</p>
    <ul>
     <li>更新在“上一位置”中引用grid_base.less的任何引用自定义LESS文件以引用新位置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>引用非现有<code>grid_base.less</code>文件会导致页面和模板编辑器的布局模式无法工作，并导致页面布局中断。</td>
  </tr>
 </tbody>
</table>

### 静态模板设计{#static-template-designs}

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
   <td><strong>重组指导</strong></td>
   <td><p>适用于以SCM管理且不在运行时通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一个位置”复制到“新位置”(<code>/apps</code>)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为具有<code>allowProxy = true</code>的<a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">客户端库</a>。</li>
     <li>通过<strong>AEM &gt;站点&gt;自定义站点页&gt;页面属性&gt;高级选项卡&gt;设计字段</strong>更新对<code>cq:designPath</code>属性中的上一个位置的引用。</li>
     <li>更新引用上一个位置的任何页面以使用新的客户端库类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过<code>/etc.clientlibs/</code>代理servlet提供客户端库。</li>
    </ol> <p>对于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时：</p>
    <ul>
     <li>请勿将可创作设计移出<code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>建议的方法是使用可编辑模板（使用结构内容和策略代替设计）来构建AEM Sites和页面。</td>
  </tr>
 </tbody>
</table>

### Adobe搜索和提升集成客户端库{#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>对这些客户端库的任何自定义使用都应按类别引用客户端库，而不应按路径引用。</p>
    <ol>
     <li>应更新Previous Location（上一个位置）上按路径对客户端库的任何引用，以使用<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">引用framework</a>的AEM客户端库。</li>
     <li>如果无法使用AEM Client Library引用框架，则可以通过AEM Client Library Proxy servlet引用客户端库的绝对路径：</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访问每个cq:ClientLIbraryFolder节点并检查类别属性：</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Adobe Target Integration Client Libraries {#adobe-target-integration-client-libraries}

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
   <td><strong>重组指导</strong></td>
   <td><p>对这些客户端库的任何自定义使用都应按类别引用客户端库，而不应按路径引用。</p>
    <ol>
     <li>应更新Previous Location（上一个位置）上按路径对客户端库的任何引用，以使用<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">引用framework</a>的AEM客户端库。</li>
     <li>如果无法使用AEM Client Library引用框架，则可以通过AEM Client Library Proxy servlet引用客户端库的绝对路径：</li>
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
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访问每个cq:ClientLIbraryFolder节点并检查类别属性：</p>
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

### WCM Foundation客户端库{#wcm-foundation-client-libraries}

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
   <td><strong>重组指导</strong></td>
   <td><p>对这些客户端库的任何自定义使用都应按类别引用客户端库，而不应按路径引用。</p>
    <ol>
     <li>应更新Previous Location（上一个位置）上按路径对客户端库的任何引用，以使用<a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">引用framework</a>的AEM客户端库。</li>
     <li>如果无法使用AEM客户端库引用框架，则可以通过AEM客户端库代理servlet引用客户端库的绝对路径。</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访问每个<code>cq:ClientLIbraryFolder</code>节点并检查类别属性：</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

