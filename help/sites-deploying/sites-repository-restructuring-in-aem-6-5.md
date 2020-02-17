---
title: AEM 6.5中的站点存储库重组
seo-title: AEM 6.5中的站点存储库重组
description: 了解如何进行必要的更改以迁移到AEM 6.5 for Sites中的新存储库结构。
seo-description: 了解如何进行必要的更改以迁移到AEM 6.5 for Sites中的新存储库结构。
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5中的站点存储库重组 {#sites-repository-restructuring-in-aem}

如AEM 6.5页面中的父存储库重组中所述 [](/help/sites-deploying/repository-restructuring.md) ，升级到AEM 6.5的客户应使用此页面评估与影响AEM Sites Solution的存储库更改相关的工作成果。 某些更改需要在AEM 6.5升级过程中进行工作，而其他更改可能会延迟到将来升级。

**升级6.5版**

* [ContextHub 区段](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**在将来升级之前**

* [Adobe Analytics客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [经典Microsoft word到网页设计](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [移动设备模拟器配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [多站点管理器Blueprint配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [多站点管理器转出配置](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [页面事件通知电子邮件模板](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [页面基架](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [响应式网格更少](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [静态模板设计](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Adobe Search and Promote集成客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Adobe Target集成客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [WCM Foundation客户端库](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## 升级6.5版 {#with-upgrade}

### ContextHub 区段 {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>如果任何新的或修改的ContextHub区段都希望在源代码控件中编辑而不是在AEM中编辑，则必须将其迁移到新位置：</p>
    <ol>
     <li>将任何新的或修改过的ContextHub区段从先前位置复制到相应的新位置(/<code>apps</code>、 <code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>将之前位置中对ContextHub区段的引用更新到新位置(、、、)中已迁移的ContextHub区<code>/apps</code>段 <code>/conf/global</code>的引 <code>/conf/&lt;tenant&gt;</code>用。</li>
    </ol> <p>以下QueryBuilder查询将查找对ContextHub区段的所有引用，这些引用位于以前的位置。<br /> 可 <br /> 以通 <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> 过AEM QueryBuilder调试器UI <br /> 执行此操作 <a href="/help/sites-developing/querybuilder-api.md" target="_blank"></a>。 请注意，这是一个遍历查询，因此不要针对生产运行它，并确保根据需要调整遍历限制。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>ContextHub区段会在 <strong>AEM &gt;个性化&gt;受众中以只读方式保留到先前的位置</strong>。</p> <p>如果ContextHub区段要在AEM中进行编辑，则必须将其迁移到新位置(<code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。 在AEM中创建的任何新ContentHub区段将保留到新位置(<code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)。</p> <p>AEM站点页面属性仅允许选择上一位置(<code>/etc</code>)或单个新位置(<code>/apps</code><code>/conf/global</code> 或 <code>/conf/&lt;tenant&gt;</code>)，因此必须相应地迁移ContextHub区段。</p> <p>可以删除AEM引用站点中任何未使用的ContextHub区段，但不能将其迁移到新位置：</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>注意：如果ClientContext正在使用，建议转换为ContextHub。</p> </td>
  </tr>
 </tbody>
</table>

## 在将来升级之前 {#prior-to-upgrade}

### Adobe Analytics客户端库 {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
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
     <li>应更新对“上一位置”中路径的客户端库的任何引用，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的客户端库引用框架</a>。</li>
     <li>如果无法使用AEM的客户端库引用框架，则可以通过AEM的客户端库代理Servlet引用客户端库的绝对路径。
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
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访 <code>cq:ClientLIbraryFolder</code> 问每个节点并检查类别属性。</p>
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

### 经典Microsoft word到网页设计 {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>适用于在SCM中管理的、在运行时不通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一位置”复制到“新位置”(<code>/apps</code>)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为客 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">户端库</a><code>allowProxy = true</code>。</li>
     <li>更新对cq:designPath属性中“上一个位置”的引用。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过代理Servlet提供客 <code>/etc.clientlibs/</code> 户端库。</li>
    </ol> <p>对于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时：</p>
    <ul>
     <li>请勿将可创作的设计移出 <code>/etc</code>。</li>
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
   <td><strong>上一位置</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td>必须将任何新的移动设备模拟器配置迁移到新位置。
    <ol>
     <li>将任何新的移动设备模拟器配置从上一个位置复制到新位置(<code>/apps</code>、 <code>/conf/global</code>、 <code>/conf/&lt;tenant&gt;</code>)。</li>
     <li>对于依赖于这些移动设备模拟器配置的任何AEM站点页面，请更新页面的 <span class="code">节 <code>
        jcr
       </code><code>
        :content
       </code></span> 点： <br /> [ <span class="code">cq:Page]/jcr:content@cq:       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>对于依赖于这些移动设备模拟器配置的任何可编辑模板，请更新可编辑模板，指向 <span class="code"><code>
        cq
       </code>:       到 <code>
        deviceGroups
       </code></span> 新位置。</li>
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

### 多站点管理器Blueprint配置 {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/apps/msm</code> （客户Blueprint配置）</p> <p><code>/libs/msm</code> （Screens、Commerce的开箱即用Blueprint配置）</p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的多站点管理器Blueprint配置迁移到新位置(<code>/apps</code>)。</p>
    <ol>
     <li>将任何新的或修改的多站点管理器Blueprint配置从“上一个位置”复制到“新位置”(<code>/apps</code>)。</li>
     <li>从“上一位置”中删除所有迁移的多站点管理器Blueprint配置。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>所有AEM提供的多站点管理器Blueprint配置都位于中的新位置 <code>/libs</code>。</p> <p>内容不引用多站点管理器蓝色配置，因此没有要调整的内容引用。</p> </td>
  </tr>
 </tbody>
</table>

### 多站点管理器转出配置 {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须将任何新的或修改的多站点管理器转出配置迁移到新位置。</p>
    <ol>
     <li>将任何新的或修改的多站点管理器转出配置从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>将AEM页面上的任何引用更新到“上一个位置”中的多站点管理器转出配置，以指向“新位置”（或）中的<code>/libs</code> 对应 <code>/apps</code>位置。</li>
    </ol> <p>从上一个位置删除迁移的多站点管理器转出配置。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>未能从上一个位置删除迁移的多站点管理器转出配置会导致向AEM作者显示重复的转出选项。</td>
  </tr>
 </tbody>
</table>

### 页面事件通知电子邮件模板 {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
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
   <td><p>必须将任何新的或修改的页面事件通知电子邮件模板迁移到以下位置 <code>/apps</code>:</p>
    <ol>
     <li>将任何新的或修改的页面事件通知电子邮件模板从上一个位置复制到新位置(<code>/apps</code>)。</li>
     <li>从上一个位置删除所有迁移的页面事件通知电子邮件模板。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 页面基架 {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><span class="code">/libs/settings// <code>
       wcm
      </code>template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/ <code>
       wcm
      </code>template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td>在“上一位置”下创建的基架使用旧版基架框架，无法迁移到“新位置”。 要与新位置对齐，必须使用支持的Scaffolding框架重新开发任何旧版Scaffolding。</td>
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
   <td><strong>上一位置</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>必须更新对自定义LESS文件中“上一位置”的任何引用，才能从“新位置”导入。</p>
    <ul>
     <li>更新引用“上一位置”中引用grid_base.less的任何自定义LESS文件以引用新位置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>引用非现有文 <code>grid_base.less</code> 件会导致页面和模板编辑器的布局模式无效，并中断页面布局。</td>
  </tr>
 </tbody>
</table>

### 静态模板设计 {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>重组指导</strong></td>
   <td><p>适用于在SCM中管理的、在运行时不通过设计对话框写入的任何设计。</p>
    <ol>
     <li>将设计从“上一位置”复制到“新位置”(<code>/apps</code>)。</li>
     <li>将设计中的任何CSS、JavaScript和静态资源转换为客 <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">户端库</a><code>allowProxy = true</code>。</li>
     <li>通过 <code>cq:designPath</code> AEM &gt;站点&gt;自定义站点页面&gt;页面属性&gt;高级选项卡&gt;设计字段更新对属性中上一个位置的引用 <strong></strong>。</li>
     <li>更新引用“上一位置”的任何页面以使用新的“客户端库”类别（这需要更新页面实施代码）。</li>
     <li>更新AEM Dispatcher规则，以允许通过代理servlet提供客 <code>/etc.clientlibs/</code> 户端库。</li>
    </ol> <p>对于任何未在SCM中管理的设计，以及通过设计对话框修改的运行时：</p>
    <ul>
     <li>请勿将可创作的设计移出 <code>/etc</code>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>建议使用可编辑模板构建AEM站点和页面，这些模板使用结构内容和策略代替设计。</td>
  </tr>
 </tbody>
</table>

### Adobe Search and Promote集成客户端库 {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
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
     <li>应更新对“上一位置”中路径的客户端库的任何引用，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的客户端库引用框架</a>。</li>
     <li>如果无法使用AEM的客户端库引用框架，则可以通过AEM的客户端库代理servlet引用客户端库的绝对路径：</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访问每个cq:ClientLiaryFolder节点并检查类别属性：</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Adobe Target集成客户端库 {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
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
     <li>应更新对“上一位置”中路径的客户端库的任何引用，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的客户端库引用框架</a>。</li>
     <li>如果无法使用AEM的客户端库引用框架，则可以通过AEM的客户端库代理servlet引用客户端库的绝对路径：</li>
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
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访问每个cq:ClientLiaryFolder节点并检查类别属性：</p>
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
   <td><strong>上一位置</strong></td>
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
     <li>应更新对“上一位置”中路径的客户端库的任何引用，以使用 <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM的客户端库引用框架</a>。</li>
     <li>如果无法使用AEM的客户端库引用框架，则可以通过AEM的客户端库代理Servlet引用客户端库的绝对路径。</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td><p>从不支持编辑这些客户端库。</p> <p>要获取客户端库类别，请通过CRXDELite访 <code>cq:ClientLIbraryFolder</code> 问每个节点并检查类别属性：</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

