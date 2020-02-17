---
title: AEM 6.5中的存储库重组
seo-title: AEM 6.5中的存储库重组
description: 了解AEM 6.5中的存储库重组
seo-description: 了解AEM 6.5中的存储库重组
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# AEM 6.5中的存储库重组 {#repository-restructuring-in-aem}

## 简介 {#introduction}

在AEM 6.5之前，客户代码部署在JCR的不可预测区域，这些区域可能会在升级时发生更改。 因此，在正式的AEM版本（主要版本、功能包、服务包或修补程序）中，覆盖自定义代码、配置或内容很常见。 此外，客户更改有时会覆盖AEM产品代码或内容，破坏产品功能。

这些冲突并不总是可以自动解决的，需要花费大量处理时间来标记，需要人为干预来解决，解决问题的方法并不总是明确的。 通过清晰定义AEM产品代码和客户代码的层次结构，可以避免这些冲突。

为此，从AEM 6.5开始并在将来的版本中继续，内容将从存储库中的其他文件夹进行重组，并遵循以下高级规则，指导内容在哪些位置上转移： `/etc`

* AEM产品代码将始终放 `/libs`置在中，且不得被自定义代码覆盖
* 应将自定义代码放 `/apps`置在 `/content`、和 `/conf`

本文分为三个部分，分别表示已移出的内容类型 `/etc`:

1. 配置
1. 客户端库
1. 杂项

每个部分包括：

* 包含调整后的位置和其他上下文的表。 在不久的将来，预计这些表将格式化为更平整的结构，以提高可读性。
* 允许自定义代码成功扩展驻留在以下位置的AEM应用程序代码的可扩展性策略 `/libs`。

## 向后兼容性 {#backwards-compatibility}

在大多数情况下，升级到AEM 6.5后，将保持与旧位置的向后兼容性。这是通过保留旧位置并受产品代码尊重以及添加新位置来实现的。 在大多数情况下，条件逻辑用于检查旧文件夹是否存在以及从那里读取内容而不是从新位置读取内容。

在6.5升级后，建议客户按照自己的时间线删除旧位置，以便使用新位置中的内容。 下表包含符合每个位置新内容结构的说明。

>[!NOTE]
>
>就地升级实例除了新位置之外，还将包括旧内容位置。 新的开发人员安装将仅包括新位置。

## 如何阅读表 {#how-to-read-the-tables}

每个部分中的表包括：

* 与此内容相关的AEM解决方案（站点、资产、表单等）
* 旧（6.4及更早版本）位置
* 新的6.5位置
* 与新内容结构对齐的说明。 例如，在6.5升级后的几周或几个月内，可能需要执行脚本或手动移动文件
* AEM用来为从先前版本升级到AEM 6.5的客户保持旧内容位置向后兼容性的方法

## 配置 {#configuration}

本节中的内容位置通常指位于、或下的文 `/settings` 件夹下 `/libs`的 `/apps`内容 `/conf`。

### 可扩展性策略 {#extensibility-strategy}

一般而言，但除少数例外情况外，本节中的内容可以使用Apache Sling的上下文感知配置功 [ 能进行扩展](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) 。

简而言之，上下文感知配置允许存储库某个部分的内容被存储库其他部分的内容多次覆盖。 例如，中的内 `/libs` 容可以由中的内容覆盖 `/apps`，然后可以由中的内容覆盖 `/conf`。 此外，全局文件夹下的内 `/conf` 容可由特定的“租户”或“站点”(例如， `/conf/we-retail/settings`)。

通常，上下文感知配置用作扩展功能配置的策略，但有时其他内容类型会使用它。

下表还包含一列名为“配置类型”，用于说明可覆盖配置的程度。 以下是这些配置类型的更多详细信息：

**不感知上下文**

* 资源恰好位于上下文感知型文件夹结构(如 `/libs/settings`)中，但始终通过绝对路径引用，因此上下文感知不起作用。
* 资源可能随处可用。 例如，资产DRM许可证可能位于 `/content/my-customer/licenses/creative-commons.html`
* 示例:

   * 工作流脚本-> `/apps/settings/workflow/scripts/noop.ecma`
   * 资产DRM许可证-> `/apps/settings/dam/drm/my-license`

**仅全局**

* 仅具有全局配置的功能
* 作为参考点，请在此示例中优先使用以下设置： `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* AEM仅支持全局配置，不支持租户化配置
* AEM将始终开始首先在/conf/global级别查找配置

* 示例:

   * 工作流启动器 -> `/libs/settings/workflow/launcher`
   * 工作流模型 -> `/conf/global/settings/workflow/models`

**租户感知**

* 对于租户感知型配置，请参阅此示例以了解配置路径的优先级：&lt; `/libs/settings``/apps/settings` &lt; `/conf/global``/conf/we-retail`，其中we-retail是租户名称。 租户感知配置还支持子租户。

* AEM支持已授权的配置。 它尊重层 `cq:conf` 次结构上的属性
* 示例:

   * 可编辑的模板 -> `/conf/we-retail/settings/wcm/templates`
   * 云配置-> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>解决方案</strong></td>
   <td><strong>上一位置</strong><br /> </td>
   <td><strong>新位置</strong></td>
   <td><strong>上下文感知配置类型</strong><br /> </td>
   <td><strong>向后兼容性方法</strong></td>
   <td><strong>与最新型号一致的要求</strong></td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>租户感知</td>
   <td><p>旧版云服务。</p> <p>坚持就地升级。 列出和读取这些代码的代码仍在AEM中作为备用。</p> </td>
   <td>延迟内容迁移实用程序可通过表单迁移UI触发，以便自动转换为新路径。<br /> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>租户感知</td>
   <td><p>旧版云服务。</p> <p>在就地升级设置上保留。 列出和读取这些代码的代码仍在AEM中作为备用。</p> </td>
   <td>延迟内容迁移实用程序可通过表单迁移UI触发，以便自动转换为新路径。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>租户感知</td>
   <td>旧版内容结构比新的OOTB结构优先级更高。</td>
   <td>项目级别自定义需要剪切并粘贴到相应的对等 <code>/apps</code> 或路 <code>/conf</code> 径中（如果适用）。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>租户感知</td>
   <td>旧版内容结构比新的OOTB结构优先级更高。</td>
   <td>项目级别自定义需要剪切并粘贴到相应的对等 <code>/apps</code> 或路 <code>/conf</code> 径中（如果适用）。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>不感知上下文</td>
   <td>旧版内容结构比新的OOTB结构优先级更高。</td>
   <td>项目级别自定义需要剪切并粘贴到相应的对等 <code>/apps</code> 或路 <code>/conf</code> 径中（如果适用）。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>租户感知</td>
   <td>旧版内容结构比新的OOTB结构优先级更高。</td>
   <td><p>项目级别自定义需要剪切并粘贴到相应的等 <code>/apps</code> 效或 <code>/conf</code> 路径下。</p> <p>运行自定义的资产摄取工作流时，对/etc中旧位置的引用仍会存在于媒体提取过程配置中。 除了将脚本从/etc移出到对等的/apps和/conf路径外，自定义媒体提取进程参数还需要从绝对路径更改为相对路径，以适应更改。</p> <p>有关详细信息，请参 <a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">阅此页</a>。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>租户感知</td>
   <td>旧版内容结构优先级高于新的，即装即用。</td>
   <td>项目级别自定义需要剪切并粘贴到相应的对等 <code>/apps</code> 或路 <code>/conf</code> 径中（如果适用）。</td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>租户感知</td>
   <td>旧版内容结构优先级高于新的，即装即用。</td>
   <td>项目级别自定义需要剪切并粘贴到相应的对等 <code>/apps</code> 或路 <code>/conf</code> 径中（如果适用）。</td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Assets</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>不感知上下文</td>
   <td><p>消费服务会了解旧位置。</p> <p>考虑从旧位置进行的配置</p> </td>
   <td><br /> 将自定义内容从移 <code>/etc/design</code> 动到 <code>/apps/settings/wcm/design</code> 新存储库结构中，以便与其对齐。 将来，请考虑将您的站点升级为使用可编辑的模板功能，该功能将取代设计模式的需求，进而取代此内容。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>不感知</td>
   <td>旧位置下的组件将继续 <code>/etc/scaffolding</code> 运行，但已弃用。</td>
   <td>Adobe建议您在新位置下使用新的scaffold组件。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>/libs/msm，用于开箱即用的屏幕和商务蓝图配置</p> <p> </p> </td>
   <td>不感知上下文</td>
   <td><p>消费服务会了解旧位置。</p> <p>将考虑从旧位置进行的配置。</p> </td>
   <td>需要将配置复制到新位置。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>租户感知</td>
   <td>该功能利用配置管理器，并且仍支持旧位置作为备用。</td>
   <td>
    <ol>
     <li>将配置从重新定 <code>/etc</code> 位到 <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>然后，按如下方式更新内容中的引用：</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>不适用</td>
   <td><p>消费服务会了解旧位置。</p> <p>如果在旧版位置检测到配置，则将使用它们。</p> </td>
   <td>要与新模型对齐，需要在新位置创建配置，而且必须删除下面的 <code>/etc</code> 旧配置。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>租户感知</td>
   <td><p>旧位置的区段：</p>
    <ul>
     <li>在受众控制台中保持只读模式。</li>
     <li>仍加载到页面上(如果在页面属性&gt;个性化&gt;区段路 <strong>径中选择了给定路径</strong>)。</li>
     <li>可用于内容定位。</li>
    </ul> </td>
   <td>您可以使用区 <a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">段迁移工具</a> ，迁移到新位置。</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>不适用</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>代码可感知旧模板的位置。 将继续引用现有模板并从中读／写 <code>/etc</code>。</p> <p><br /> 对于电子邮件模板，如果客户已通过在 <strong>AEM Communities电子邮件回复配置中配置模板根路径来将其自定义模板置于其他路径</strong><strong></strong> ，则该模板将保持不变。</p> </td>
   <td><p>迁移 <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">实用程序</a> ，可以与最新的AEM Communities模板模型保持一致。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>徽章规则：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>徽章图像：</strong></p> <p>将旧位置的现成图像移 <code>/etc/community/badging/images</code> 至 <code>/libs/community/badging/images </code> </p> <p> </p> <p>自定义图像将移至 <code>/content/community/badging/images</code>。</p> <p> </p> </td>
   <td>租户感知</td>
   <td><p>该代码识别旧的徽章路径。</p> <p><br /> 它将首先检查旧路径是否存在<br /> 。 如果它们不存在，则它们将使用新路径。</p> </td>
   <td><p>需要手动迁移才能与最新型号保持一致。 请按照以下步骤操作，以实现此目标：</p>
    <ol>
     <li>使用“工具”下的配置浏览器创建站点上下文存储段 <strong>。</strong></li>
     <li>转到站点根目录</li>
     <li>将属性 <code>cq:conf</code> 设置为存储所有配置的存储段路径。 也可以通过站点编辑向导- <strong>设置云配置输入</strong>，然后保存更改来设置</li>
     <li>将相关标记规则和评分规则从上一 <code>etc/community/*</code> 步创建的站点上下文存储段移至</li>
     <li>调整站 <code>badgingRules</code> 点根 <code>scoringRules</code> 上的和属性，使其具有对新规则位置的相对引用。 例如，如果设 <code>cq:conf</code> 置为 <code>/conf/we-retail</code>，则规则现在移 <code>badgingRules</code> 到此新存储段时 <code>community/badging/rules</code> ，其值将为</li>
     <li>同样，调整标记规则节点中对评分规则的引用以具有相对路径。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>租户感知</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>该代码识别旧的徽章路径。</p> <p><br /> 它将首先检查旧路径是否存在<br /> 。 如果它们不存在，则它们将使用新路径。</p> </td>
   <td><p>需要手动迁移步骤才能与最新型号保持一致。</p> <p>上述徽章规则中的步骤相同。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>不感知上下文</td>
   <td><p>这些配置不向后兼容。 有关如何迁移到新位置的步骤，请参阅“与最新型号对齐的要求”列。<br /> </p> <br /> </td>
   <td><p>需要手动迁移才能与最新型号保持一致。 您可以使用Granite配置管理器将配置移到下的新路径 <code>/apps/settings</code>。</p> <p>因此，您需要在节点上将 <code>mergeList</code> 属性设置为true, <code>/libs/settings/community/subscriptions</code> 然后添加子 <code>nt:unstructured</code> 节点。<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>不感知上下文</td>
   <td>这些配置不向后兼容。 有关如何迁移到新位置的步骤，请参阅“与最新型号对齐的要求”列。</td>
   <td><p>需要手动迁移才能与最新型号保持一致。 您可以使用Granite配置管理器将配置移到下的新路径 <code>/apps/settings</code>。</p> <p>因此，您需要在节点上将 <code>mergeList</code> 属性设置为true, <code>/libs/settings/community/subscriptions</code> 然后添加子 <code>nt:unstructured</code> 节点。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>全局</td>
   <td>这些配置向后兼容。 如果检测到旧路径，则将使用它们。 否则，新路径优先。</td>
   <td><p>“延迟内容迁移任务”以下列形式可用 <code>CQ64CommunitiesConfigsCleanupTask</code>:</p> <p>有关详细信息，请参阅 <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">延迟迁移文档</a>。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>不适用</td>
   <td>这些配置向后兼容。 如果检测到旧路径，则将使用它们。 否则，新路径优先。</td>
   <td><p>“延迟内容迁移任务”以下列形式可用 <code>CQ64CommunitiesConfigsCleanupTask</code>:</p> <p>必须手动将关注词从移动 <code>/etc/watchwords</code> 到 <code>/conf/global/settings/community/watchwords</code>。</p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>全局</td>
   <td><p>如果存在，且或中不存在配置，则使用旧 <code>/libs</code> 位置 <code>/conf</code>。</p> <p>编辑OOTB工作流模型时，必须在下面创建上下文感知型叠加， <code>/conf</code> 以允许它们可以修改。</p> <p>包导出需要在或中包含模 <code>/libs</code> 型， <code>/conf</code> 并在 <code>/var/workflow/models.</code></p> </td>
   <td><p>新创建的模型将创建在该位 <code>/conf/global/settings</code> 置。</p> <p>在中或要 <code>/etc</code> 求您 <code>/libs</code> 在中显式创建覆盖，然 <code>/conf/global/settings</code> 后才能进行编辑。 必须选择“编辑”按钮，这将导致创建覆盖并允 <code>/conf</code> 许进行编辑。</p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>全局</td>
   <td>如果存在，并且位置中不存在配置<br /> ，则使用旧 <code>/libs</code> 版位 <code>/conf</code> 置。 这样，自定义启动器就会被保留。</td>
   <td><p>新创建或编辑的启动器配置位于该 <code>/conf</code> 位置。</p> <p>所有启动器应从旧位置移 <code>/etc</code> 至<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>全局</td>
   <td>如果存在，且位置中不存在配置<br /> ，则使用旧 <code>/libs</code> 版位 <code>/conf</code> 置。 这样，将保留自定义工作流模型。</td>
   <td><p>所有工作流模型应从旧版位置移 <code>/etc</code> 到旧版 <code>/conf/global/settings/workflow/models</code>。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>不感知上下文</td>
   <td><p>为了向后兼容，将使用旧版位置（如果有）。</p> <p>以前，现成模板必须通过在中编辑来覆盖 <code>/etc</code>。 现在，覆盖应存储在中 <code>/conf/global</code>。</p> </td>
   <td>有关详细信息，请参阅工作流文档。<br /> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>租户感知</td>
   <td>旧版云服务。 将在就地升级设置上保留。 列出并阅读它们的代码仍在产品中作为备用。</td>
   <td><p>要将云配置移至以下任 <code>/conf</code>一位置，您可以：</p>
    <ul>
     <li>使用新的触控UI创建配置<br /> ，或<br /> </li>
     <li>将配置从复 <code>/etc/cloudservices/translation</code> 制到相应的新位置</li>
    </ul> <p>完成此操作后，配置需要通过用户界面中的“站点” <strong>&gt;“属性</strong> ”与“站点”关联。</p> <p><em>注意：翻译连接器必须与AEM 6.5兼容，才能正常工作。</em></p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>租户感知</td>
   <td>旧版云服务。 将在就地升级设置上保留。 列出并阅读它们的代码仍在产品中作为备用。</td>
   <td><p>要将云配置移至以下任 <code>/conf</code>一位置，您可以：</p>
    <ul>
     <li>使用新的触控UI或<br /> </li>
     <li>将旧配置从 <code>/etc/cloudservices/translation</code> 其各自的新位置复制</li>
    </ul> <p>完成此操作后，配置需要通过用户界面中的“站点” <strong>&gt;“属性</strong> ”与“站点”关联。</p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>租户感知</td>
   <td><p>升级实例 <code>/etc</code> 时，当前条目仍保留在原位。</p> <p>升级后访问云设置UI将复制现有云设置到新存储库结构，同时保留现有内容以实现向后兼容性。</p> </td>
   <td><p>内容模型相同，只有位置已更改以与上下文感知型配置保持一致。</p> <p>涵盖 <a href="/help/sites-deploying/lazy-content-migration.md">这些云设置的延迟迁移任务</a> ，将执行以下操作：</p>
    <ul>
     <li>将现有云设置复制到 <code>/etc/cloudsettings</code> <code>/conf/global/settings/cloudsettings</code></li>
     <li>删除 <code>/etc/cloudsettings</code></li>
    </ul> <p>但是，在升级之后和运行延迟迁移任务之前，需要手动执行以下步骤：</p>
    <ul>
     <li>所有指向的引 <code>/etc/cloudsettings/*</code> 用都需要更新以指向 <code>/conf/global</code></li>
    </ul> <p>警告：</p>
    <ul>
     <li>需 <code>/etc/cloudsettings</code> 要保留容器</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>仅全局</td>
   <td><p>Dynamic Media的云配置- Scene7(<code>dynamicmedia_scene7</code> 运行模式)设置将保留在同一位置。 该过程按原样运行。 如果您需要调整云配置值，则有两个选项可用于执行此操作：</p>
    <ol>
     <li>通过旧云配置UI更新现有配置。</li>
     <li>通过新的触屏UI创建新的云配置。 这比旧的高优先级。</li>
    </ol> </td>
   <td><p>为了与最新模型对齐，您需要运行位于以下位置的脚本：</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>仅全局</td>
   <td><p>OOTB查看器预设将仅在新位置可用，而自定义查看器预设将一直在下方，直 <code>/etc</code> 到发生修改。</p> <p>修改后，它将通过延迟迁移保存在新位置。 嵌入图像服务器在收到请求后将查看旧路径和新路径。 因此，无需更改其嵌入代码或URL。</p> </td>
   <td><p>现成查看器预设仅在新位置中可用。 对于自定义查看器预设，您需要在以下位置运行迁移脚本：</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>与向后兼容性情况类似，您不必调整copyURL/embed代码以指向 <code>/conf</code>。 要发送的现有请 <code>/etc</code> 求将在内部重新路由到正确的内容 <code>/conf</code>。</p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>仅全局</td>
   <td>下面的宏 <code>/etc</code> 仍然有效。 如果对其进行修改，则修改后的节点将通过延迟迁移任务移 <code>/conf</code> 动到下的新位置。</td>
   <td><p>您需要在以下位置运行迁移脚本：</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>不适用</td>
   <td><p>现成视频配置文件将被删除，而无需更新资产文件夹属性以链接到配置文件。</p> <p>编码过程在新旧位置之间有内置的转换。 它将转换旧路径以查看新的配置文件路径。</p> </td>
   <td>无需更改。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>仅全局</td>
   <td><p>在您修改自定义视频配置文件之前，该自定义视频配置文件将保持原样。</p> <p>然后，它将通过延迟迁移任务移到新位置。 这与编码查找时的现成视频预设类似。 编码过程具有内置路径转换器，用于首先查看旧位置，然后查看视频配置文件的新位置。</p> </td>
   <td><p>为了与最新的模型对齐，您可以在以下位置运行迁移脚本：</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>仅全局</td>
   <td><p>Dynamic Media混合设置（运行模式）的<code>dynamicmedia</code> 云配置将保留在同一位置。 该过程按原样运行。 如果需要调整配置值，可以通过两种方式进行调整。</p>
    <ol>
     <li>通过旧云配置UI更新现有配置。</li>
     <li>通过新的触控UI创建新的云配置。 这比旧的高优先级。</li>
    </ol> </td>
   <td><p>您需要运行迁移脚本才能与最新型号保持一致。 您可以在以下位置找到脚本：<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>仅全局</td>
   <td><p>DM-Youtube设置的云配置将保留在同一位置。 该过程按原样运行。 如果您需要调整云配置值，可以通过两种方式执行此操作：</p>
    <ol>
     <li>通过旧的云配置UI更新现有配置。</li>
     <li>通过新触控UI创建新的云配置。 这比旧的高优先级。</li>
    </ol> </td>
   <td><p>您可以运行迁移脚本以与最新型号保持一致。 脚本可在以下位置找到：<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>仅全局</td>
   <td>无需执行任何操作。</td>
   <td><p>您可以运行迁移脚本以与最新模式对齐。 脚本可在以下位置找到：<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>仅全局</td>
   <td>中的模 <code>/etc/notification/email/default/</code> 板优先于中的模板 <code>/libs/settings/notification-templates</code>。</td>
   <td>为了与最新的模型对齐，您可以在下面创建新模板并 <code>/apps/settings/notification-templates</code> 在此处执行新修改。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>不适用</td>
   <td><p>消费服务会了解旧位置。</p> <p>如果在旧版位置检测到配置，则将使用它们。</p> </td>
   <td>要与新模型对齐，需要在新位置创建配置，而且必须删除下面的 <code>/etc</code> 旧配置。</td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>不感知上下文</td>
   <td>注意，自定义语言需要添加到列表中。<br /> </td>
   <td>使用其他语言（如果有）叠加和更新新列表。 或者，将旧列表复制到 <code>/apps</code> 位置也会有效。</td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>仅全局</td>
   <td>将在就地升级设置上保留。 用于列出和阅读产品中仍然存在的代码。</td>
   <td>要保留更改，请将XML文件从复 <code>/etc</code> 制到 <code>/libs</code> 或 <code>/conf</code>。 或者，<strong> 从 </strong>中删除文件 <code>/etc</code>。</td>
  </tr>
 </tbody>
</table>

## 客户端库 {#client-side-libraries}

[客户端库是在浏览器中处理的javascript和CSS代码](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) 。

### 可扩展性策略 {#extensibility-strategy-1}

AEM提供了一个可扩展性框架，可附加多个JavaScript文件。 将附加具有相同“类别”属性的任何文件，允许自定义代码扩展位于下方的AEM代码 `/libs`。

<table>
 <tbody>
  <tr>
   <td><strong>解决方案</strong></td>
   <td><strong>上一位置</strong><br /> </td>
   <td><strong>新位置</strong></td>
   <td><strong>向后兼容性方法</strong></td>
   <td><strong>与最新型号一致的要求</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>将保留在通过就地升级升级升级的实例上的旧版clientlib。</p> <p>新clientlib与“<strong><code>replaces</code></strong>”属性具有相同的类别名称，以避免合并旧的和新的clientlib。</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>将保留在通过就地升级升级的实例上的旧版clientlib。</p> <p>新clientlib与“<strong><code>replaces</code></strong>”属性具有相同的类别名称，以避免合并旧的和新的clientlib。</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>旧版clientlibs。 将在通过就地升级升级的实例上保留。 新clientlib与“<strong><code>replaces</code></strong>”属性具有相同的类别名称，以避免合并旧的和新的clientlib。</td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>这不再作为AEM 6.5开箱即用包的一部分。</td>
   <td><p>自适应表单中的现成主题。</p> <p>将在就地升级设置上保留。</p> </td>
   <td>这是部分由用户生成的内容。 这将作为引用内容包提供，并且名称 <code>aem-forms-reference-themes</code> 为。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>旧版clientlibs。 将在通过就地升级升级的实例上保留。 新clientlib与“<strong><code>replaces</code></strong>”属性具有相同的类别名称，以避免合并旧的和新的clientlib。</td>
   <td>无需执行任何操作。<p> </p> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>不直接使用的旧版Analytics和Target客户端库。 </td>
   <td>使用清除过滤器清理升级后的内容。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>旧版clientlib有不同的客户端类别名称。</td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>这些是旧版clientlib。 它们将保留在就地升级设置上。 新clientlib与“<code>replaces</code>”属性具有相同的类别名称，以避免合并旧的和新的clientlib。</td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>这些是旧版clientlib。 将在就地升级设置上保留。</p> <p>新的clientlib具有相同的类别名称。</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>这些是旧版clientlib。 将在就地升级设置上保留。</p> <p>新的clientlib具有相同的类别名称。</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>这些是旧版clientlib。 将在就地升级设置上保留。</p> <p>新客户端具有相同的类别名称</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>这些是旧版clientlib。 将在就地升级设置上保留。</p> <p>新的clientlib具有相同的类别名称。</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>新的clientlib具有相同的类别名称。</td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>旧版clientlibs。 将在就地升级设置上保留。 新clientlib的类别名称与“<strong>replaces</strong>”属性相同，可避免合并旧的和新的clientlib。</td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>在就地升级时，旧版文件(/etc/clientlibs/wcm/..._)将保留且不会自动删除，因此对旧版/etc/clientlibs/wcm/foundation/grid/grid_base.less文件的引用将继续保持静态。</p> <p><em>请注意，这是一种异常情况，即此LESS文件通过LESS @import语句被绝对路径引用，而NOT则被clientlib类别引用。</em></p> <p>如果引用“grid_base.less”的客户LESS指向非现有文件，则“可编辑模板布局”模式将断开，并且不会显示使用该模板进行的任何调整(即， 所有组件将为页面的全宽)。</p> </td>
   <td>更新自定义代码中的任何引用（即在引用已移动grid_base.less文件的任何LESS文件中）以指向新位置，并删除旧位置。</td>
  </tr>
 </tbody>
</table>

这些是前几部分没有涉及的其他重组。

### 可扩展性策略 {#extensibility-strategy-2}

查看每个表行，了解任何支持的可扩展性模型。 本节中的内容通常不会扩展。

## 杂项 {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>解决方案</strong></td>
   <td><strong>上一位置</strong><br /> </td>
   <td><strong>新位置</strong></td>
   <td><strong>向后兼容性方法</strong></td>
   <td><strong>与最新型号一致的要求</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>旧版AEM Forms Portal OOTB模板。 在就地升级设置后，这些模板将保留在/etc中。</p> <p>在模板列表中，单词<em> “deprecated</em>”（已弃用）将添加到模板标题中，以使它们与较新的模板区分开来。</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>旧版对应管理注释文件。 不是直接消费的。 升级后将使用清除过滤器清除。</td>
   <td>旧版位置使用清理过滤器清理升级后的内容。</td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>标签管理器API支持旧版和新位置。 当JCR标签管理器工厂OSGi组件启动时，它会检测它是在升级实例还是旧实例上运行，并使用相应的位置。<br /> </td>
   <td><p>为了与新模型正确对齐：</p>
    <ol>
     <li>通过使用<code>/etc/tags</code><code>/content/cq:tags</code> <code>tagID.</code></li>
     <li>登录到CRXDE Lite</li>
     <li>将标记从移 <code>/etc/tags</code> 动到 <code>/content/cq:tags</code></li>
     <li>重新启动OSGi组件 <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>用于处理飞行中工作流程<br /> 的传统位置。 新的工作流使用 <code>/var.</code></td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>现有工作流模型在升级后，引用旧版位置中的工作流脚本的 <code>/etc/workflow/scripts</code> 步骤将继续指向这些脚本并正确执行。</p> <p>请注意用于创作工作流步骤的AEM UI’（流程、拆分等）不再列出用于工 <code>/etc/workflow/scripts</code> 作流脚本的下拉列表中的脚本。</p> </td>
   <td><p>如果未在AEM中编辑关联的工作流进程步骤，则利用这些脚本的工作流将继续按预期工作。</p> <p>但是，要实现完全向后兼容性（包括编辑步骤时），需要客户在升级后手动执行以下操作：</p>
    <ul>
     <li>必须将脚本从移动到 <code>/etc/workflow/scripts</code> <code>/apps/workflow/scripts.</code></li>
     <li>必须<strong> 更新对工 </strong>作流模型步骤中的任何引用，以引用新位 <code>/etc/workflow/scripts</code><code>/apps/workflow/scripts</code> 置。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>ClassicUI实用程序页面在升级时保持不变。</td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>用于保存为AEM资产下载操作调用生成的zip文件的临时位置。</p> <p>无需更新，因为当客户端请求下载资产时，它将在新位置生成文件。</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>旧内容将保持原位，并在升级后可用。</p> <p>提供了延迟迁移任务以迁移到新位置。</p> </td>
   <td><p>迁移通过“延迟迁移”任务执行： <code>CQ64CommerceMigrationTask.</code></p> <p>它执行以下步骤：</p>
    <ul>
     <li>调整从旧位置到指向新位置的参照</li>
     <li>将内容从旧位置移到新位置</li>
     <li><p>删除旧位置，最终激活整个系统中新位置的使用</p> </li>
    </ul> <p>任务所涵盖的位置有：</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>对于较大的目录，建议通过将以下Java系统属性传递给AEM来单独运行商务迁移任务：</p>
    <ul>
     <li>属性名称: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>属性值: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>迁移后，AEM需要重新启动。</p> </td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>旧内容将保持原位，并在升级后可用。</p> <p>提供了延迟迁移任务以迁移到新位置。</p> </td>
   <td>请参阅上面的说明 <code>/etc/commerce/products</code>。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>旧内容将保持原位，并在升级后可用。</p> <p>提供了延迟迁移任务以迁移到新位置。</p> </td>
   <td>请参阅上面的说明 <code>/etc/commerce/products</code>。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>无需执行任何操作。</td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>旧内容将保持原位，并在升级后可用。</p> <p>提供了延迟迁移任务以迁移到新位置。</p> </td>
   <td>请参阅上面的说明 <code>/etc/commerce/products</code>。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>旧内容将保持原位，并在升级后可用。</p> <p>提供了延迟迁移任务以迁移到新位置。</p> </td>
   <td>请参阅上面的说明 <code>/etc/commerce/products</code>。</td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>新任务创建于 <code>/var/taskmanagement</code></p> <p>旧位置中的现有任务仍将显示在AEM收件箱中。</p> </td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>通过AEM包管理器创建的AEM包仍存储在 <code>/etc/workflow/packages.</code></p> <p>通过AEM Sites和工作流创建的其他包将继续存储在<code>/var/workflow/packages.</code></p> <p>在和中找到的 <code>/etc/workflow/packages</code> 包仍 <code>/var/workflow/packages</code> 可以通过AEM的包管理器进行编辑。 </p> </td>
   <td><p>无需执行任何操作。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>新的工作流实例将自动创 <code>/var</code> 建。</td>
   <td>无需执行任何操作。</td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>搜索和提升源内容的新位置。</p> <p>旧URL继续工作，请求由ServletFilter转发到新位置。</p> </td>
   <td><br /> 无需执行任何操作。 <br /> </td>
  </tr>
  <tr>
   <td>所有</td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>DTM Web-Hooks的新位置。</p> <p>旧URL继续工作，请求由ServletFilter转发到新位置。</p> </td>
   <td><br /> 无需执行任何操作。 <br /> </td>
  </tr>
 </tbody>
</table>

